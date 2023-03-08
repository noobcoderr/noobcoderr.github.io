## Git简单介绍
本篇不会介绍基本的git原理之类的，只记录在工作中的git使用经验。如果要学习git的基础与进阶，可以参考这个网站[git-tower](https://www.git-tower.com/learn/git/ebook/cn/command-line/basics/what-is-version-control#start)

本篇会简单介绍我在工作中都使用git做了哪些工作：   
- 基础使用。使用gitlab管理我们的源代码  

- 自动化。我们使用gitlab的CI进行自动代码检查、单元测试、代码打包  

- 多系统协作。我们使用gitlab的issue+webhook+钉钉作为简单的工单系统，支撑我们进行日常支撑工作  

### 1. 管理源码进行开发
以下都以gitlab为例，所有开发人员使用同一个仓库，基于不同的特性分支进行开发

我们的分支:
- master分支: 正式分支，也是打包分支

- develop分支: 开发分支，保持和master分支保持一致

- feature分支: 功能特性分支，不同的功能分别在对应的特性分支上进行开发测试。  

我们的开发流程:
- 建分支。建立特性/bug对应的issue，根据issue创建对应的分支(在web页面直接操作), 或者直接从develop分支迁出一个新的特性分支

- 开发。在特性分支上进行开发/测试，直到测试验收完毕，每次提交都会触发局部静态代码检查

- [合并前rebase并整理提交记录](http://jartto.wang/2018/12/11/git-rebase/)。分两步，先rebase develop保持特性分支为最新的develop代码，再rebase -i 变基commitid 整理特性分支的commit记录

- 合并前code-review。在gitlab网页界面创建merge-request，并指派其他开发进行review，直到所有人都无异议，此时会触发全局静态代码检查。

- 合并更新版本信息。研发主管将代码合并到develop分支后，在develop分支修改代码内的版本信息，再合并到master分支

- 打包发布。研发主管基于master分支进行打tag，此时会触发CI自动基于tag打包。

这样，我们的一次功能需求的开发就算完成了。目前整个流程还存在一些问题：
- 无法自动创建及更新CHANGELOG.md，即版本记录无法自动生成，跟我们的提交不规范有关系

- 没法自动触发CD，跟我们的服务架构有关系。


### 2.基于gitlab的CI进行自动化代码检查、打包
gitlab如何搭建CI，此处不做赘述，查看官方文档即可。[Runner部分教你如何搭建CI环境](https://docs.gitlab.com/runner/)，[CICD部分教你如何让CI运行起来](https://docs.gitlab.com/ee/ci/)

我们一共有4个任务: test，code_check_push，code_check_merge，feat_build，tag_build
- test。执行单元测试代码，每次push时触发

- code_check_push。执行局部静态代码检查，每次提交代码时触发，检查范围为提交的Py文件代码，且只检查Error级别的

- code_check_merge。执行全局静态代码检查，创建merge-request后触发，检查范围为工程内的主要python包，只检查error级别的

- feat_build。执行打包，每次push时触发，用于特性分支提测时配置

- tag_build。执行打包，只有提交创建tag时触发，用于正式环境的打包。


### 3.基于webhook和issue+钉钉的简易工单系统  

本系统涉及三个部分**gitlab服务**、**钉钉服务**、**简单的中转服务**   

**中转服务**  
 
为一个简单的http服务，用于接收gitlab内的issue相关变更的通知，并转发给钉钉机器人。

- 创建一个转发接口api，将该api设置到gitlab的webhook部分即可接收gitlab的通知

- 维护一个支持人员列表(转发钉钉时以对应手机号为准)，收到gitlab通知时转发到钉钉时艾特对应的支持人员进行处理

**gitlab服务**

- 建立一个公开的项目，用于接收issue，外部人员基于该项目的issue部分提交工单 

- 根据不同的业务类型，建立不同的工单模板，模板为markdown文件，需要放置于.gitlab/issue_templates/目录下，需要手动创建

- 在该项目的webhook部分添加上述中转服务的接收通知的api，后续所有issue的变更(建立、更新、关闭)都会通知到该api


**钉钉服务**

- 建立支持钉钉群，并添加webhook机器人，此机器人用于接收中转服务的通知

这样，一个简易的工单系统就建立起来了。外部人员建立issue反馈的时候，钉钉群内机器人就可以立马艾特对应支持人员进行处理，
处理完毕后在issue内同步结果信息，issue创建者会收到gitlab通知邮件



## git常用场景

记录我理解的以及我使用的业务中场景的处理办法，如果有错误的或者有差异的还请指正

**1、拉取远程项目的目标(如develop)分支**

`git clone 项目地址` 项目下来通常只包含master分支，这个时候又不想使用`git fetch all`拉取所有分支下来，而只想拉取指定的分支。 可以使用

`git checkout -b develop origin/develop `

这样就切换到想要的分支了，并且已经拉取到了对应分支的代码

**2、我需要为我的功能新建一个分支，并且同步到远程**

方法1：创建分支并直接关联远程分支 `git checkout -b new_branch origin/new_branch`   

方法2：先创建分支，先迁出新分支`git checkout -b new_branch`  再手动设置关联远程分支，手动设置远程分支也有两种方法 

- 第一种 `git branch --set-upstream-to=origin/new_branch  new_branch`
- 第二种 `git push --set-upstream origin new_branch(远程分支名)`


**3、我在自己的feature分支进行开发，但是develop分支产生了改动，我需要更新下来**   

先在本地的develop拉取最新的远程develop代码 `git pull origin develop`   

然后切回feature分支，直接针对develop分支进行rebase。`git rebase develop`

**4、master版本为10，但是我想回退到版本9**  

执行`git reset --hard 版本9的commit_id`   

前提是要提交未push到远程,否则本地再稍微修改生成一次新的提交`git push --force`  

但是如果目标是受保护的分支，那么--force不生效

**5、特性分支开发完毕后，删除掉该分支**  

先删除本地的分支 `git branch -D feat/xxxx`  

再删除远程的分支 `git push origin --delete feat/xxxx`  

**6、根据commit log生成changelog**  

conventional-changelog，需要使用npm安装

**7、git rebase之后，合并的提交其message不规范，需要重新修改message**

执行`git commit --amend`  


**8、本地代码以及改的面目全非，拉取远程最新代码覆盖本地，且不合并冲突**

先拉取远程所有代码 `git fetch --all`  

再重置版本 `git reset --hard origin/feature/当前分支`

**9、从某个tag分支上迁出新的分支进行开发**  

部分项目组可能未使用最新的tag进行研发，而是基于之前某个稳定版，此时添加紧急 特性时，需要从项目组使用的tag上迁出分支  

`git branch 新分支名 迁出tag版本 `  

例如：git branch feature/add-new-feat v1.3.4 则会从1.3.4版本迁出分支 

**10、在本地临时切换到某个提交**

执行`git checkout $commit_id` 。此时就可以切换到这次提交上，然后可以checkout回原分支，这么做可以定位某次提交是否出问题

**11、CICD脚本里的一些操作**

- 获取当前分支名。`git rev-parse --abbrev-ref HEAD`

- 获取当前分支最新的提交。`git rev-parse HEAD` 

- 获取最新版本的tag VERSION=`git describe --abbrev=0 --tags`

- git 取得两个 tag 之间的 commit，用于生成版本更新的changelog。`git log --pretty=oneline tagA...tagB > change.log`

- 获取倒数第二新的tag  

  - 先获取所有tag `git tag > tags.log` 
  
  - 获取所有tag数量 tags_num=`awk 'END {print NR}' tags.log` 
  
  - 计算倒数第二个tag的行数 num=$(($tags_num-1))  
  
  - 取倒数第二行tag内容 latest_tag=`sed -n $num'p' tags.log` 
  



## 参考
[Commit message 和 Change log 编写指南-阮一峰](https://www.nowcoder.com/ta/sql)  
[git-flow 的工作流程](https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow/)
[git clone --mirror和git clone --bare之间的区别是什么](https://www.imooc.com/wenda/detail/579025)  
[gogs迁移gitlab](https://www.cnblogs.com/zy0209/p/11265158.html)  
[手写git-hooks钩子](https://segmentfault.com/a/1190000040370691)  
[Git - 基于GitLab服务端、客户端钩子介绍](https://yanghongfei.github.io/2019/03/25/git-hooks/)  
[GitHub Actions 入门教程](https://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)  
[hugo使用github action自动部署到github pages](https://tomial.github.io/posts/hugo%E4%BD%BF%E7%94%A8github-action%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2%E5%8D%9A%E5%AE%A2%E5%88%B0github-pages/)
