## 背景

公司项目使用到的框架是基于异步IO模型reactor，所以想要系统性地学习一下IO模型
而且还有很多开源框架也是基于该模型的，如nginx、redis

IO模型: 同步阻塞、同步非阻塞、IO多路复用、信号驱动IO、异步IO
	100%弄明白5种IO模型  https://zhuanlan.zhihu.com/p/115912936
	io多路复用 复用的是什么  https://juejin.cn/post/6882984260672847879
		IO多路复用是一种同步IO模型，实现一个线程可以监视多个文件句柄；一旦某个文件句柄就绪，就能够通知应用程序进行相应的读写操作；没有文件句柄就绪时会阻塞应用程序，交出cpu。多路是指网络连接，复用指的是同一个线程

## Reactor的使用比较
redis也是使用的reactor模式
比较twisted和redis的reactor模型
nginx也是？

reactor模型常见
redis、nginx、netty、twisted
IO Event有哪些类型呢？读？写？连接？关闭？


requesthandler

github-reactor网络模型学习
1、经典论文翻译
2、自己使用语言实现最简单的例子，go、python
3、使用reactor网络模型的经典开源框架赏析
关键字：poll、epoll、select、阻塞、非阻塞、IO


reactor论文翻译，目前在github上没有搜到

golang实现的reactor
https://github.com/Allenxuxu/gev

python实现的reactor呢？
https://github.com/shafreeck/reactor.py
https://github.com/feiyu4581/network


如何学习异步 IO 运行时原理？
	所有的异步库都是调用的操作系统异步支持，Linux 是 epoll/select/io-uring, macos/bsd 是 kqueue ，Windows 是 iocp
	所以学习操作系统的异步支持入手比较好


一步一步使用异步IO实现一个http服务框架

如何使用reactor创建一个http服务？

    reactor.listenTCP(8000,factory)
    reactor.run()
从源码可以看出，上述实例本质上使用了事件驱动的方法 和 IO多路复用的机制来进行Socket的处理。
参考：https://zhuanlan.zhihu.com/p/50215687


我们服务一直会有内存持续上涨现象。
是不是因为使用twsited框架，每个请求，都需要创建一个协议实例？而这个实例在垃圾回收的时候，有问题？
或者是我们对connectionLost没有做合理的处理

回调是Twisted异步编程中的基础

## 参考

[必读-100%弄明白5种IO模型](https://zhuanlan.zhihu.com/p/115912936)

[必读-图解高性能网络结构：Reactor和Preactor](https://www.cnblogs.com/xiaolincoding/p/14706824.html)

[Reactor论文原文](chrome-extension://cdonnmffkdaoajfknoeeecmchibpmkmg/assets/pdf/web/viewer.html?file=http%3A%2F%2Fwww.dre.vanderbilt.edu%2F~schmidt%2FPDF%2Freactor-siemens.pdf)

[Reactor Pattern论文学习《An Object Behavioral Pattern for Concurrent Event Demultiplexing and Dispatching](https://zhuanlan.zhihu.com/p/464159297)

[深入理解Reactor模式,也是论文学习](https://www.s0nnet.com/archives/deep-understanding-of-reactor-design-patterns)

《并发模型csp和actor》
	https://jingwei.link/2018/07/08/actor-and-csp-model.html

[推荐-聊聊Linux 五种IO模型](https://www.jianshu.com/p/486b0965c296)

[彻底理解 IO 多路复用实现机制](https://juejin.cn/post/6882984260672847879)

[深入理解Reactor 网络编程模型](https://zhuanlan.zhihu.com/p/93612337)

[Redis中的Reactor 模型的工作机制](https://blog.csdn.net/qq_41688840/article/details/122182339)

[Redis 多线程网络模型全面揭秘](https://zhuanlan.zhihu.com/p/356059845)

[Reactor模式](https://dreamgoing.github.io/reactor.html)