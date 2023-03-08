# 单例模式
## 我理解的
一个类(python)或者结构体(go)，在一个进程内，通过任意办法都只能获取一个唯一的实例化对象。  
这里的任意办法我想的是直接new函数或者直接实例化类的方式进行，都只能得到一个唯一的实例化对象

我们知道go是可以通过以下2种方法获取一个结构体的实例化对象的

```go
type Student struct {
	Id int
}

func main()  {
	stu := Student{Id:1}
	stu1 := new(Student)
}
```

而Python实例化一个类的方法就是

```python
class Student(object):
  def __init__(self):
    pass
  
stu = Student()
```

如何能够实现让用户调用以上三种方法都只返回唯一的实例化对象呢？




## 百科内介绍的
### 简介：  
1.单例对象的类必须保证只有一个实例存在。  
2.在某个服务器程序中，该服务器的配置信息存放在一个文件中，这些配置数据由一个单例对象统一读取，然后服务进程中的其他对象再通过这个单例对象获取这些配置信息。

```
关于第二点，参考我们内部框架，所有的配置都被读取到了内部的Context类的实例化对象中，Context类是个单例类。各种数据库配置、服务端口配置、数据库业务配置都被挂载到了其实例化对象下面供全局使用。
```

我们内部的这个context类是如何保证单例的呢？

```python
# file context.py
from DB inport config
class Context():
  def __init__(self):
    self.DBconfig = config

Context = Context() # 该步骤会在该模块被导入时执行，那么会被执行多次嘛？

# file biz.py
from context import Context
此时全局按照这种方式导入的，不是Context类，而是一个同一个已经实例化好的实例化对象，算不算另类的单例呢？(后续了解到其实是python最简单的一种实现单例的方式,而且改方案在多线程的情况下，会有问题，但是我们是单进程+多协程，所以没问题)
```

有一个疑问，当context.py模块被导入的时候，是会编译该文件内的代码的，那么

`Context = Context()`这行代码在后续的业务使用过程中被不断导入，会被执行多少次呢？

```
python在导入模块时，即import时究竟有哪些动作？在python中，导入并非只是把一个文本文件插入到另一个文件。导入其实是运行时的运算，程序第一次导入指定文件时，会执行以下三个步骤：
1、找到模块文件
2、编译成位码（即pyc文件）
3、执行模块的代码来创建其所定义的变量（你没看错，导入时代码是会执行的）
需要明确的事，模块导入只有在第一次导入时才会进行。此后，导入相同模块时，会跳过这三个步骤，而只提取内存中已经加载的模块对象。从技术上，Python把载入的模块储存在一个名为sys.modules的表中，并在第一次导入操作时，检查该表。如果不存在便会启动这三个过程。
————————————————
版权声明：本文为CSDN博主「python小工具」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_45144170/article/details/104907793
```

即main函数内第一次导入的时候，会执行一次，得到一个实例化对象，后续的所有导入，都会返回该对象。

### 实现单例模式的思路：  
1.一个类能返回对象一个引用（永远是同一个）和一个获得该实例的方法（必须是静态方法，通常使用getInstance这个名称） 

2.当我们调用这个方法时，如果类持有的引用不为空就返回这个引用，如果类保持的引用为空就创建该类的实例并将实例的引用赋予该类保持的引用  

3.同时我们还将该类的构造函数定义为私有方法，这样其他处的代码就无法通过调用该类的构造函数来实例化该类的对象，只有通过该类提供的静态方法来得到该类的唯一实例。  

关于第三点

```
其实在go中，将结构体的名词设置为小写开头，那么该结构体就无法被用户直接导入并实例化，而需要使用我们提供的专门的NewXXX()方法来获取该对象，那么在这一步就好控制了。
```





### 多线程情况下注意：  
如果当唯一实例尚未创建时，有两个线程同时调用创建方法，那么它们同时没有检测到唯一实例的存在，从而同时各自创建了一个实例，这样就有两个实例被构造出来，从而违反了单例模式中实例唯一的原则。 解决这个问题的办法是为指示类是否已经实例化的变量提供一个互斥锁

### 构建方式：  
懒汉方式。指全局的单例实例在第一次被使用时构建。  
Early Initialization: 饿汉方式。指全局的单例实例在类装载时构建。  



# 总结

一句话总结：  
单个进程生命周期内，一个类只能关联一个实例化对象

实现思路：  
修改默认的实例化方法(python __new__)或者让用户只能调用我们提供的获取实例化对象的方法(go 小写对象名)

目的:  
减少资源损耗、方便协调管理系统整体行为

场景：  
1、全局数据库连接client   
2、全局配置client

## Python单例模式

懒汉模式

```python
class Config(object):
    lock = threading.Lock

    def __new__(cls, *args, **kwargs):
        if not hasattr(Config, "_instance"):
            with Config.lock:
                if not hasattr(Config, "_instance"):
                    Config._instance = Config()
        return Config._instance


cfg = Config()
```



饿汉模式

```python
class Config(object):
    
    def __init__(self):
        pass


Config = Config() # 利用模块加载时执行
```



## GO单例模式

懒汉模式：用的时候再实例化

```go
var instance *Student
var once sync.Once

type Student struct {
}

func GetStudent() *Student {
	once.Do(func() {
		instance = &Student{}
	})
	return instance
}
```





饿汉模式：程序启动阶段就实例化

利用go的init函数，在程序初始化阶段自动执行

```go
var instance *Student

type Student struct {
}

func init() {
	instance = &Student{}
}
```







# 参考文档

[python中的单例模式实现,值得参考](https://blog.csdn.net/ManyPeng/article/details/92816138)

[菜鸟教程-单例模式，介绍部分写的很好](https://www.runoob.com/design-pattern/singleton-pattern.html)

[python单例，懒汉和饿汉的理解](https://www.jianshu.com/p/4d3c0319c12d)