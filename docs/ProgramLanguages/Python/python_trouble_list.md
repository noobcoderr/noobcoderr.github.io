# Python踩坑指南
记录在开发Python服务中踩过的坑，都是血泪的教训

## 踩坑
### 1、临时变量切记不要覆盖已有变量, 因为Python是弱类型解释型语言，一个变量赋值各种类型都不会报错
如上下文内有user_id整型变量，在业务流程从上往下的过程中，user_id可能会被赋值为字符串、float、None，此时编译器都不会报错的，后面使用时如果
还是当做最初的整型来使用，可能会产生崩溃。

### 2、函数方法的返回要保持统一，且各个分支都要保证有返回
python方法返回给上层时，本质是返回了个元组回去，比如reture A, B，调用方收到的返回其实是(A,B), 调用方使用两个变量进行接收时是正常的，但是如果
只返回了一个A，即上层收到(A,)，那么编译器不会报错，但是具体运行到该部分时就会报错。

解决方案，使用pylint，R1710就是针对这种情况的报警
```markdown
R1710: Either all return statements in a function should return an expression, or none of them should. (inconsistent-return-statements)
```


## 总结：
### 1、Python作为解释型语言，具体错误都只会在运行时才能体现出来，所以我们一定要在我们的CI流程里加入pylint检查    
检查原则为：风格检查(`C\W级别`)可以按需检查， 但是错误`(E\F级别)`的检查是必要的，R级别的部分需要
- `C` - 惯例：违反了Python编程惯例`(PEP 8)`的代码。可用可不用，如果是新项目，则可以加上，从一开始就规范好代码，如果是老项目，则按需添加
- `W` - 警告：代码中存在的不影响代码运行的问题。可用可不用，如果是新项目，则可以加上，从一开始就规范好代码，如果是老项目，则按需添加
- `R` - 重构：写得比较糟糕需要重构的代码。  部分需要，如`R1710`
- `E` - 错误：代码中存在的影响代码运行的错误。 **强制检查**
- `F` - 致命错误：导致Pylint无法继续运行的错误。 **强制检查**

在CI流程中，我们使用`pylintrc`文件来配置具体的检查规则，对于上述的`C\W`，不做检查，`E\F`强制检查，`R`级别部分检查的配置示例为
```markdown
[MESSAGES CONTROL]
disable=C,W,R,no-self-argument

enable=R1710,inconsistent-return-statements
```
该部分检查可以放到`CI`的`push`部分，即仓库收到`push`就立马执行`pylint`，`pylint`完进行打分，如果分数低于`10`分，则通知到工作区进行整改


## 其他


业务设计内的数据库设计思考
1、要用什么数据库？Redis还是MongoDB
	Redis用于读取频率较高的场景，且只用于存储过期数据，即拿来当做缓存，而不是持久化存储
	Redis下位替代可选mongodb，

2、怎么根据业务设计表结构
	什么时候放一张表，什么时候放2张表？

本周
1、费曼学习法
2、python动态执行python代。已实现。

抽象类，单纯只用来被其他子类继承，而自身无法被实例化。
接口类，一样，只能用于继承，自身不能实例化

理解：经常看到很多基类，其下面有很多方法，但是每一个方法的实现逻辑都是空的，这个类是不是就是抽象类？
如果全部方法的实现都是空的，那么则是接口类， 类似于Go内的Interface，其类型下只定义方法名，没有实现，
如果有部分方法有实现，那么则是抽象类



变量第一次赋值后，有的类型就固定了，而有的则可以再接收其他类型的值
是因为
类型固定的为强类型语言，为编译型语言，其类型在编译阶段就已经确定了。如Golang、dart
类型可反复改变的为弱类型语言，为解释型语言，其类型只有在执行到那才能确认。如python、JavaScript


函数可以赋值给变量或作为参数传递给其他函数，这是函数式编程的典型特征。


想到一个idea和最后做出来结果中间不是简单的写代码就行了
还有着需求分析、设计、编码、测试
很多idea最后没有被实现的原因大概就是只想到了idea和最终结果
却没有去做好需求分析和设计。

所以我们需要加强分析能力和设计能力
分析能力是指从原始的简单需求内解析出真正的需求的能力
设计能力则是根据需求设计我们的服务的能力


之前一直比较疑惑，
gitlab、github都只是简单的代码仓库，为什么还可以执行cicd里面的一些脚本，
原来它也是需要一台工作终端去执行这些脚本命令的，比如gitlab里的runner，就相当于终端
github里则是




需求完成了方案设计之后进入编码阶段，编码阶段我们该注意什么情况呢？
1、函数的定义和引用
	每一个函数一定要做好入参的空值拦截判断
2、适度的try-catch
	保证网络请求、数据库io、数值计算判断等敏感操作时要加入try-catch，防止出现崩溃
3、做好边界值的测试



Python技术栈迁移复用能力？
我们日常开发使用Python，服务器工程使用的是Pypy，框架则是基于twisted的自研业务框架，那么在以后迁移的时候，有哪些和Python相关的能力是我们能复用的呢？
1、Python的设计模式，就算换了新框架，仍然可以复用，能帮助我们针对业务快速完成设计
	单例模式:常见于全局log对象
	观察者模式:

2、python处理高并发的能力
	我们的服务，目前可以承载多高的并发？没测试过，要怎么测试？

3、Python线上问题定位能力，主要是线上内存异常(溢出、持续增高)、CPU异常(突刺、持续增高)分析解决能力



twisted？
tasklet?

gvent
	greenlet类似于goroutine？底层将异步并发影藏，让人感受到的是同步的？
	stackless

go线上异常定位、内存泄漏、垃圾回收

关于协程，可以参考greenlet,stackless,gevent,eventlet等的实现。

async
yield

Stackless Python greenlet和gevent

gevent将greenlet库与 libev事件循环库结合在一起，并提供了Python绑定。一些有趣的Python库，例如 locust（HTTP负载测试框架）和gunicorn（Web服务器框架）都建立在gevent之上。

真正原生的并发支持，独立于生成器协程，使用具有特点功能的sync/await语法，异步上下文管理和sys（以及其他功能）中的标准库支持。这些特性在PEP 492在Python 3.5.x中的实现。


SDK进程启动
pypy tyframework/server.pyc conf_sdk.tyredis.me:6337:0:http-tysdk-yqddz-9998-00110



twisted
	RuntimeError: Request.finish called on a request after its connection was lost; use Request.notifyFinish to keep track of this.


彻底弄明白partial()
	https://zhuanlan.zhihu.com/p/47124891

python的类方法、静态方法、实例方法，什么时候用什么？
classmethod
staticmethod

