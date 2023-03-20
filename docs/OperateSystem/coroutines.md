# 协程(coroutine)

## 前言
整理这篇文章的大纲为
1、介绍协程是什么，是什么背景下产生的，和进程、线程的区别和优缺点
2、介绍协程的实现原理，以及哪些项目使用到了协程
3、介绍Python的协程和Go的协程的使用，对比二者的实现，优缺点等等

梳理这篇文章的目的是
1、彻底搞清楚协程的产生背景
2、协程的实现原理
3、协程的优点和缺点
4、高级语言对协程的实现和使用

因为看完网上对协程的介绍后好像都有点似懂非懂的感觉，所以这里
梳理该篇文章的数据源直接看最初的论文，本篇参考以下论文
1、

最常见的关于协程的面试题
1、进程、线程、协程的简介和区别
2、


协作式程序(cooperation routine)



## python协程和go协程的对比
Python协程和Go协程的对比
我们常常使用多进程和多线程来干什么呢？
1、服务端请求处理，每到达一个请求，使用一个进程或者线程来处理
2、


定义
	前提：
		1、程序是一段可以被计算机运行的完整代码
		2、子程序是一个大型程序中的某部分代码，由一个或多个语句块组成。它负责完成某项特定任务，而且相较于其他代码，具备相对的独立性。
		一般会有输入参数并有返回值，提供对过程的封装和细节的隐藏
		3、函数、过程、面向对象里面的方法也是子程序
		4、子程序只能被动调用，只有等被调用了的子程序返回时，才能继续往下走
		程序由许多函数组成，函数在编译阶段被编译为独立的组件，在合适的位置被加载到内存中执行？
	定义：
		1、协程也是子程序，即可以是方法、过程、函数
		2、协程是协作式多任务的子程序
		3、协程可以主动让出执行权，而不仅仅是被动，通过yield
		4、允许执行被挂起与被恢复
		5、通过yield方式转移执行权的协程之间不是调用者与被调用者的关系，而是彼此对称、平等的
		6、子程序内部加入yield，就变成了生成器(协程)，而去掉yield，就变为了普通的子程序，即协程是特殊的子程序
		wiki：https://zh.m.wikipedia.org/zh/%E5%8D%8F%E7%A8%8B
		
		协程的思想是由程序自身指定中断点，在IO 操作时，程序可以自行中断，主动放弃CPU，此时调度另外的协程继续运行。 当IO 就绪后，再调度此程序从中断点继续向下执行。 Python 中的协程是基于生成器实现的，python2时，函数内加入yield，实现，python3时使用asynic/await实现，
		go则使用go func关键字实现，
		异步处理和事件回调处理，都被封装在了底层

		另外php内也使用yield实现生成器来实现协程。https://www.zhihu.com/question/26966414

适用场景
	IO密集型，web服务器，高并发
	客户端使用协程批量发送大量请求，压测等，如快速发送10w个请求。
	服务端使用协程来处理大量客户端请求，高并发，如快速处理10w个并发请求

使用方式
	定义一个协程
	运行一个协程
	获得一个协程的返回结果(x):协程不会返回结果?



实现原理

	python 异步io asyncio
	异步有什么问题？基于事件驱动，会产生callback hell，但是基本已经被框架和语言层面解决了
	解决GIL利用多核 = 多进程+多协程
	https://docs.python.org/zh-cn/3/library/asyncio-eventloop.html

	GO  MPG模型：https://developpaper.com/the-principle-of-golang-concurrency/
		https://mp.weixin.qq.com/s/SEPP56sr16bep4C_S0TLgA


区别
	python是使用异步IO+event_loop的协程实现的
	go


学习python的最好文档：官方库：https://docs.python.org/zh-cn/3.9/library/index.html
同样的go：https://books.studygolang.com/The-Golang-Standard-Library-by-Example/



背景
项目开发中使用到了Go和Python，二者都有协程的实现，这个文档尝试对二者协程进行对比，对比内容包括
1、基本使用的对比
2、性能的对比
3、底层实现的对比
对比
1、基本使用的对比
Go使用协程
Go使用关键字go来标识启动一个协程，示例如下
func main() {
   // 启动一个协程
   go func() {
      fmt.Println("i am a goroutine")
   }()
   //阻塞当前执行单元
   select {}
   return
}
1、示例内启动的协程已经不受main函数所在的执行单元管理了，是一个单独的协程，但是main函数直接退出，会导致新起的协程也直接退出。
2、新起的协程不会往main函数内返回任何东西，如果想要交互，只能通过channel了
3、新起的协程常备用来执行一些和主流程无关的行为，比如
给用户发送一条邮件
通知完游戏服发货之后，额外通知一下三方渠道已发货
华为谷歌等渠道订单消耗之后，需要调渠道接口确认消耗该订单

Python使用协程
Python3.5之后原生支持了协程，基于asyncio，使用方法是async/awit
# 1、定义协程
async def get_channel_user_info(url):
    """
    使用协程处理请求
    :return:
    """
    print("request start ", url)
    # 模拟请求三方服务的耗时操作
    await asyncio.sleep(1)
    print("request succ ", url)
    
def main():
    # 2、将协程加入事件循环中
    loop = asyncio.get_event_loop()
    tasks = [get_channel_user_info("baidu"), get_channel_user_info("bytedance"), get_channel_user_info("weixin")]
    loop.run_until_complete(asyncio.wait(tasks))
    loop.close()

if __name__ == '__main__':
    main()
和go相比，
1、Python启动一个协程也是直接使用关键字即可，定义函数前加async，则定义一个协程
2、go启动后会直接运行协程，而Python的则不行，需要将新定义的协程加入到事件循环内，启动事件循环才可以运行该协程
参考网络
chatgpt的对比总结
Python 协程和 Go 协程虽然都属于协作式多任务处理的范畴，但在具体实现上有一定的区别，主要包括以下几个方面：
1. 实现方式不同
Python 协程依赖于生成器和协程库（如 asyncio、gevent 等）来实现，而 Go 协程则由 Go 语言原生支持和实现。
2. 调度机制不同
Python 协程依赖于一个事件循环（Event Loop）来调度，并采用协作式的调度方式。而 Go 协程则由 Go 运行时系统自己管理和调度，采用 G-M-P 模型来实现并发。
3. 内存管理不同
Python 协程使用的是基于栈的内存管理方式，实现了用户态的线程切换，避免了系统线程切换带来的大量开销；而 Go 协程采用的则是开放式调度器（M:N 调度方式），实现了轻量级的协程切换和调度。
4. 异步编程方式不同
Python 协程采用的是 async、await 与回调函数的方式来实现异步编程；而 Go 则使用 channel 和 select 的方式来协调和通信。
总的来说，Python 协程与 Go 协程在实现方式和使用场景上有一定的差异，但都是高效实现并发处理的方式，适用于不同的应用场景。



python异步模型和go异步模型比较


## 参考文章
[当谈论协程时，我们在谈论什么](https://www.developers.pub/article/1125270),从底层实现说明    
[简单谈谈协程](https://juejin.cn/post/6961414532715511839), 谈到了stackless    
[图解｜揭开协程的神秘面纱](https://zhuanlan.zhihu.com/p/515916638), 图解的形式清晰明了    
[WIKI-协程](https://zh.wikipedia.org/zh-sg/%E5%8D%8F%E7%A8%8B)

