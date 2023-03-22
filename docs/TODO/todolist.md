TODOLIST 每周清理一次

近期
	python线上服务内存涨的比较快，应该是存在内存泄漏的情况，梳理一下python垃圾回收机制、频率，以及可能出现内存泄漏的情况
		1、线上服务内存监控
		估计是协程超时？
	python服务器和三方服务器交互时，协程直接假死了，未收到回复，因为是事件驱动机制，底层为异步，所以该协程的后续流程都被卡住，直到很久之后才因为
	触发协程本身的超时，才完成后续的流程，起码过去几十分钟了，这里要梳理一下
		1、是不是三方提前断开了TCP链接导致的协程被一直挂起，这里要梳理一下TCP四次挥手的过程，并用tcpdump抓包确认(curl -v排查)，
		2、python事件循环和协程的工作原理


3、垃圾回收算法是怎么设计的
	https://developer.aliyun.com/article/777750?source=5176.11533457&userCode=e4nptrfl
4、支持将本地文章一键发布到主流博客平台，剪贴板图片一键上传至图床（新浪、GitHub、图壳、腾讯云、阿里云、又拍云、七牛云）
	github.com/onblog/BlogHelper ​​​
7、二维码原理
	hellogithub2014.github.io/2019/08/05/qr-code-theory/
8、《etcd源码剖析》
	https://csunny.gitbook.io/etcd/?continueFlag=4a11cbdbee93355d0fd25f5c24abbff5

10、从源码中学习（阅读源码，初学者的有效成长方式）
	boholder.github.io/blogs/learn-from-source-code/
11、《学习费曼学习法》
	liujingyu.github.io/feynman/2020/03/17/learn-Feynman.html

12、再起一个文件夹，记录业务中遇到的一些问题
	[1、线上跳转几千万页导致mongodb产生慢查询，以及影响线上业务的问题](https://avohk9xvwg.feishu.cn/docx/doxcnGiUJsxx5nZJ6KJzQEQJtrg)
	2、线上mongo订单库数量过大产生的分表问题，该怎么分
	3、python类变量中使用未加载的函数值导致崩溃，服务启动过程是怎么样的

13、软件版本号规范与命名原则
	https://www.jianshu.com/p/75374e299ef8
	http://www.ttlsa.com/linux/alpha-beta-rc/
	
账号支付服务安全加固  https://avohk9xvwg.feishu.cn/docx/FBwXd1OuSofWW0xuMHZcLKN0nxe
mongo数据大于2亿问题  https://blog.csdn.net/miyatang/article/details/55509419
MongoDB的一些性能监控指标介绍  https://blog.csdn.net/jjwen/article/details/79977336

todo
Go 学习路线（2022）
	https://xie.infoq.cn/article/f24aafeede34ecb2855c83c14
Nginx配置文件详解	
	https://www.cnblogs.com/54chensongxia/p/12938929.html
Python Gevent
	https://www.jianshu.com/p/73ccb425a710
	https://www.jianshu.com/p/ccf3bd34340f
	https://blog.csdn.net/wangjianno2/article/details/51708658
高并发基础、思路以及普遍的处理方式
	https://juejin.cn/post/6928707578549665799
python requests 连接池
	http://www.gonglin91.com/python-requests-pool-connections/
	https://blog.csdn.net/shengruxiahua2571/article/details/105323719
	https://lockshell.com/2019/12/04/python-requests-http-connection-pool/
	https://segmentfault.com/a/1190000040016102
python字典和列表转换
	https://blog.csdn.net/loner_fang/article/details/80940600
基于gitlab issue为导向的分支管理
	https://blog.csdn.net/u011423145/article/details/107860812
用户系统设计与实现
	http://gglinux.com/2017/03/31/user/
	https://www.zhihu.com/question/30362871
	http://cwaiting.com/2020/09/18/%E7%94%A8%E6%88%B7%E8%B4%A6%E5%8F%B7%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1/
从0到1搭建域名邮件服务器
	https://segmentfault.com/a/1190000040727863
每日一问
	https://github.com/zerolab-fe/one-question-per-day/issues
设计模式
	推荐 https://zhuanlan.zhihu.com/p/58093669
	https://refactoringguru.cn/design-patterns/strategy/python/example
	https://refactoringguru.cn/design-patterns/strategy
	https://bugstack.cn/md/develop/design-pattern/2020-07-05-%E9%87%8D%E5%AD%A6%20Java%20%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E3%80%8A%E5%AE%9E%E6%88%98%E7%AD%96%E7%95%A5%E6%A8%A1%E5%BC%8F%E3%80%8B.html
	https://design-patterns.readthedocs.io/zh_CN/latest/behavioral_patterns/behavioral.html
python书籍
	chrome-extension://cdonnmffkdaoajfknoeeecmchibpmkmg/assets/pdf/web/viewer.html?file=https%3A%2F%2Fraw.githubusercontent.com%2Fsilenove%2Fpython_ebook%2Fmaster%2F%25E6%25B5%2581%25E7%2595%2585%25E7%259A%2584python.pdf
	https://python3-cookbook.readthedocs.io/zh_CN/latest/c01/p13_sort_list_of_dicts_by_key.html
vpn 木瓜云
	https://muguacloud.bar/auth/login
uml在线绘制
	https://plantuml.com/zh/
慕课
	https://coding.imooc.com/class/310.html
	https://coding.imooc.com/class/469.html
	https://coding.imooc.com/?c=be&sort=0&unlearn=0&page=1
k8s
	https://jimmysong.io/kubernetes-handbook/develop/minikube.html
	https://minikube.sigs.k8s.io/docs/start/
	https://k8s.easydoc.net/docs/dRiQjyTY/28366845/6GiNOzyZ/PCxg5EoS
	https://docker.easydoc.net/doc/81170005/cCewZWoN/N9VtYIIi
go-frame
	https://goframe.org/pages/viewpage.action?pageId=1115784
python网络库并发对比
	https://www.cnblogs.com/ydf0509/p/14655383.html
python logging
	https://juejin.cn/post/6844903692915703815
go 并发测试库
	https://github.com/rakyll/hey/blob/master/requester/requester.go
flutter写的开源记账软件(既可以参与开源，又可以学习flutter)
	https://github.com/feiyu-rs/lime

2022-07-03
Golangv1.13 版本的 runtime 源码分析
	https://github.com/LeoYang90/Golang-Internal-Notes

Mastering_Go 中文
	https://github.com/hantmac/Mastering_Go_ZH_CN

垃圾代码示例
	https://github.com/trekhleb/state-of-the-art-shitcode

后端思维之数据库性能优化方案
	https://developer.aliyun.com/article/945903?source=5176.11533457&userCode=e4nptrfl

Go语言轻松进阶
	http://tigerb.cn/go/#/kernal/?continueFlag=7a6ea4aef27f4b0cd02ff5391a95f3b9

appwrite
	https://github.com/appwrite/appwrite/blob/master/README-CN.md

maxiee blog
	https://www.maxieewong.com/Maxiee%20Weekly%20No.1%2020220617.html?continueFlag=7a6ea4aef27f4b0cd02ff5391a95f3b9

分布式系统下的认证与授权
	https://www.bmpi.dev/dev/authentication-and-authorization-in-a-distributed-system/
面向对象课程
	https://www.coursera.org/lecture/aoo

css框架
	https://www.tailwindcss.cn/
	https://headlessui.com/vue/listbox
k8s-minikube
	https://colobu.com/2022/06/02/setup-a-k8s-cluster-with-minikube/
	https://kubernetes.io/zh-cn/docs/tutorials/hello-minikube/

Alibaba/IOC-golang: 一款 Go 语言依赖注入框架
	https://ioc-golang.github.io/cn/
	关于IOC的讨论：https://www.v2ex.com/t/862639 ，29楼
毕业三年总结

房地产调控-天涯神贴
	https://github.com/shengcaishizhan/kkndme_tianya

可视化python
	https://pythontutor.com/render.html#mode=display

go-nsq
	https://github.com/nsqio/go-nsq

Python 协程 asyncio 极简入门与爬虫实战
	https://baijiahao.baidu.com/s?id=1714015900283907482&wfr=spider&for=pc
Python协程
	https://blog.csdn.net/d1240673769/article/details/121032458
	https://www.liaoxuefeng.com/wiki/1016959663602400/1017970488768640#0
tonardo：基于协程实现的老牌网络框架
	https://www.cnblogs.com/traditional/p/15942850.html
kratos开发文档
	https://go-kratos.dev/docs/intro/layout

在 k8s 中安装 jenkins 并配置实现 CI/CD
	https://segmentfault.com/a/1190000040469278
	https://www.jenkins.io/zh/blog/2018/09/14/kubernetes-and-secret-agents/
python官方文档-打包
	https://docs.python.org/zh-cn/3.9/library/zipapp.html
	https://docs.python.org/zh-cn/3/library/asyncio-task.html
go官方库文档
	https://books.studygolang.com/The-Golang-Standard-Library-by-Example/
python greenlet源码
	https://zhuanlan.zhihu.com/p/359595405
说说这篇「我为什么从python转向go
	https://www.jianshu.com/p/xiQzpL
python asyncio协程动态添加任务、协程池2
	https://blog.csdn.net/weixin_43968923/article/details/111397237

go协程和python协程的对比
	https://www.google.com/search?q=python+go%E5%8D%8F%E7%A8%8B%E5%AF%B9%E6%AF%94&oq=python+go%E5%8D%8F%E7%A8%8B%E5%AF%B9%E6%AF%94&aqs=chrome..69i57j0i546l2.6443j0j1&sourceid=chrome&ie=UTF-8

Sanic源码阅读：基于0.1.2
	https://zhuanlan.zhihu.com/p/32891129
探索Golang协程实现——从v1.0开始
	https://segmentfault.com/a/1190000038626134
	https://developpaper.com/the-principle-of-golang-concurrency/
谈谈并发编程中的协程
	https://studygolang.com/articles/2396
C 的 coroutine 库
	https://blog.codingnow.com/2012/07/c_coroutine.html
Golang 是单线程模型还是多线程模型？
	https://www.zhihu.com/question/268828178
30+张图讲解：Golang调度器GMP原理与调度全分析
	https://mp.weixin.qq.com/s/SEPP56sr16bep4C_S0TLgA
Python eggs - 简介
	https://zhuanlan.zhihu.com/p/25020501
这些并发模型你真的懂了吗？未必
	https://learnku.com/articles/32807
怎样理解阻塞非阻塞与同步异步的区别？
	https://www.zhihu.com/question/19732473
完整的Python异步IO之旅
	https://zhuanlan.zhihu.com/p/95685688
aiohttp
	https://github.com/aio-libs/aiohttp
you-get
	https://you-get.org/
Redis危险命令禁用keys、flushdb、flushall及解决方案
	https://blog.csdn.net/wfy2695766757/article/details/95751044
Redis——慢查询分析
	https://www.cnblogs.com/yangmingxianshen/p/8070594.html
rose-db
	https://github.com/flower-corp/rosedb/issues?q=slow

时间轮算法相关
	时间轮算法
		https://spongecaptain.cool/post/widget/timingwheel/
	那些惊艳的算法— 时间轮算法
		https://cloud.tencent.com/developer/article/1815722
	论文
		chrome-extension://cdonnmffkdaoajfknoeeecmchibpmkmg/assets/pdf/web/viewer.html?file=http%3A%2F%2Fwww.cs.columbia.edu%2F~nahum%2Fw6998%2Fpapers%2Fton97-timing-wheels.pdf

后端都要学习什么？
	https://www.zhihu.com/collection/460236281

平台中心8月份
	https://avohk9xvwg.feishu.cn/docx/doxcn7B3awBj5bg9UscvFy56l7c

危机感：

面试问题：
当你拿到offer的时候你就可以问他们项目的东西了，然后问问技术的领导有没有什么计划，会不会招更多的人，运营方面的有没有什么计划等等


http://tieba.baidu.com/p/7904223880?&share=9105&fr=sharewise&is_video=false&unique=568AF17FB3C3FC55B45010960D78DFEB&st=1656859361&client_type=1&client_version=12.25.1.0&sfc=copy&share_from=post&source=12_16_sharecard_a
一千万用户同时向一个账户转账，怎么设计。我回答说限流，然后用消息队列缓存请求，慢慢消费处理。
然后面试官问这样可能造成消息积压，怎么在消费者代码层面解决？没答上来


assuming that the caller of the routine blocks until the routine completes.
Both the average and worst case latency are of interest


广告平台一边对接广告主，就是想要投放广告的产品，比如化妆品，游戏等等
一边对接流量主，就是有流量的平台，比如微博，小红书等等
然后平台


thus it is comparable in complexity to standard priority queue implementations like heaps [7]，However, the constants appear to be better for Scheme 7


