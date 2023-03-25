# Go TODO

游戏的其他服务是可以用go比如匹配服务，商城服务，交易服务，聊天服务等。至于即时对战类服务已经有引擎自带都是c/cpp，，适合高并发

2、golang sdk的api设计，options和builder哪个更方便呢 

例如
NewClient(WithIp("1.2.3.4"),WithPort(80))
和
NewBuilder().Ip("1.2.3.4").Port(80).Build()
哪个更方便呢

go为什么要把业务模块放在internal模块下面：
	https://juejin.cn/post/6950094090969022472

# 参考
[在Go中是如何对epoll进行封装的](https://zhuanlan.zhihu.com/p/484458312)

评论区对epoll、reactor是否有回调、到底为同步阻塞还是同步非阻塞有分歧

[golang的位操作](https://learnku.com/go/t/23460/bit-operation-of-go)

[golang 服务平滑重启小结](https://www.cnblogs.com/wangiqngpei557/p/11704747.html)

[gnet: 一个轻量级且高性能的 Go 网络框架](https://strikefreedom.top/go-event-loop-networking-library-gnet)

[go知识图谱问题](https://segmentfault.com/a/1190000038922260)

https://github.com/nsqio/nsq

[golang面试题集合](https://github.com/lifei6671/interview-go)

[go-zero文档](https://go-zero.dev/cn/)

[go语言优秀项目整理](https://shockerli.net/post/go-awesome/#%E6%88%90%E5%93%81%E9%A1%B9%E7%9B%AE)

[the-way-to-go](https://github.com/unknwon/the-way-to-go_ZH_CN/blob/master/eBook/13.3.md)

[go-admin快速建站](https://github.com/go-admin-team/go-admin)

[go项目标准](https://github.com/golang-standards/project-layout/blob/master/README_zh.md)


[go导航](https://hao.studygolang.com/)

[go阅读清单](https://github.com/qichengzx/gopher-reading-list-zh_CN)

[微信SDK go版本](https://github.com/silenceper/wechat)

[golang服务部署到测试环境k8s](https://tuyoo.feishu.cn/docs/doccnE8eCLDmOuw5OosqnrQCrsf#IP8LFT)
