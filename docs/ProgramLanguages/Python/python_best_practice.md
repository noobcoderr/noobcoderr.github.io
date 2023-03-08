# Python项目实践
尽管随着Python版本更迭，以及各种不同的发行版本发布更新，我们公司项目仍然继续保持相同的pypy60，也就是python2.7，虽然版本低，但是项目能跑，
能支撑业务我们基本就不会去更新到python3，所以重要的不是版本，而是规范化的维护服务工程，使其不乱，就算用老版本也可以不断创造价值。

本文是记录一下从事Python开发来的一些项目实践经验和规范。

## 项目管理
我们使用内部部署的Gitlab来管理存放公司内部的业务代码，所以以下很多内容可能都是以Gitlab为基础。梳理则是按照软件开发的生命周期进行的
- **项目结构**。即代码如何组织与管理，防止在不断的发展过程中，文件杂乱无章
- **模块和包管理**。同样是为了避免职责划分不规范，出现各种循环引用
- **代码格式化检查**。这样可以保证整个开发团队按照统一的风格进行开发，且防止出现错误代码上线到正式分支
- **配置管理**。提取出代码内基础的可变化的部分。
- **测试管理**。保障上线的代码质量。
- **代码分发与打包**。开发人员拿到代码后如何快速进行运行
- **服务部署与发布**。服务开发最后的步骤
- **线上服务维护**。当线上出现问题时，如何及时热更修复，防止频繁地重启服务，影响用户体验。

### 项目结构
首先我们需要一个规范的代码结构的目的是：

1. 让新接手的同事能快速了解代码架构，知道如何部署并启动服务，如何访问并测试服务。  

2. 让后续的维护者能很明确地知道，新增的功能需求代码文件应该放在什么目录模块之下。

3. 让维护者可以知道该项目的完整的研发生命流程，包含编码、测试、检查、测试环境部署、打包、正式环境部署、线上维护等等

你也不想招到新同事之后，啥文档也没有，然后让新同事逮着你问东问西吧，这样你不仅自己会觉得烦，而且新同事也会觉得这个团队不专业。

根据我们目前的服务项目组织结构和网上推荐的项目结构进行梳理后，我觉得一个规范的python项目工程目录应该为   
```markdown
ProjName                服务工程名
    src/                业务逻辑代码  
        login_package/  子包，用于存放同类型业务的处理代码
            login.py    具体业务模块
        utils/          工具包
        ......
        main.py         服务入口
    docs/           包含各种文档, api文档, 接入文档，使用文档等等
    tests/          包含各种单元测试文件
    configs/        存放各种配置，包含启动配置，业务里的静态配置，后续肯定还有动态配置，需要放在src里
    scripts/        包含各种脚本，启动脚本，打包脚本，pylint脚本，自动化测试脚本，makefile等
    logs/           用于存放项目日志
    Dockerfile      用于存放容器化的配置
    requirnement.txt   项目依赖 
    setup.py        项目安装、部署、打包的脚本
    README.md       包含项目的基础介绍，使用介绍
    CHANGELOG.md    包含项目的版本发布记录
    .gitlab-ci.yml  用于gitlab/git的自动CI流程配置
    .gitignore      不上传到git的文件，切记秘钥相关配置文件、日志类文件要筛除掉
```
这样的目录结构下，基本上我们整个开发生命过程中的所有节点都覆盖了，且有明确的存放位置
- 开发阶段。业务代码放src内部，生成的文档放docs下，配置的管理放configs下，启动脚本等放scripts内，然后日志放logs目录下，
- 打包分发阶段。项目依赖放requirements文件，并且setuo.py文件写明了打包情况
- 部署阶段。自动化CICD放.gitlab-ci.yml文件内，容器化部署操作放Dockerfile文件下

网络中搜集到的项目结构参考  
[Python 项目工程化最佳实践指南 - InfoQ 写作平台](https://xie.infoq.cn/article/0a599a0944a7eac39a96c5594)  
[Python目录结构](https://blog.csdn.net/qq_24224067/article/details/103187864)  
[结构化您的工程，Python最佳实践指南](https://pythonguidecn.readthedocs.io/zh/latest/writing/structure.html)  
[Python工程结构及模块最佳导入实践](https://www.cnblogs.com/harrymore/p/15989783.html)  
[stackoverflow关于项目工程的讨论](https://stackoverflow.com/questions/193161/what-is-the-best-project-structure-for-a-python-application)  


### 模块和包
通常单个python文件为模块，内部含__init__.py的文件夹则为包，一个包下可以包含很多模块，其结构大致为  
```markdown
包/   
    __init__.py     
    模块1.py      
    模块2.py      
    模块3.py
```
那么这部分我们todo

### 代码格式化与检查
todo
我们服务内目前没有进行代码格式化，因为是一堆陈年老代码，一个py文件几千行，只能对新增的py文件做单独的格式化


还是老问题，因为是老代码，所以有很多不规范的命名也不好进行修改，所以我们进行代码检查时，只进行错误级别的检查，即保证上线到线上的代码不包含错误


### 配置管理
我们的服务在启动过程中肯定有很多东西是不能写死在代码里的，而是需要通过配置进行获取，静态的比如redis和mongo的连接地址、实例情况等


### 测试管理
todo


### 代码分发与打包
todo

### 服务的部署与发布
todo


## 参考
[Python 项目工程化开发指南](https://pyloong.github.io/pythonic-project-guidelines/guidelines/project_management/project_structure/)



