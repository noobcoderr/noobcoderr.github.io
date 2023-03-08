# 工厂模式

一共有三种：简单工厂模式、工厂方法模式、抽象工厂模式

## 1、我理解的
工厂的行为就是按照指定的模具生成出对应的产品，我们对类进行实例化就相当于按指定的模具(类)生成(实例化)对应的产品(对象)。  

工厂是可以同时管理很多产品的生产的，所以工厂模式可能就是把一些类统一起来由工厂类(工厂方法？)集中管理。  

但是在实际编码中我们的业务类，大多互相不影响，不太需要统一(工厂)起来管理啊。

就算是我们的SDK，需要定义很多渠道类，但是也是只按需实例化对应的类即可啊。比如

```python
def login():
  channel_obj = None
	if channel_type == "weixin":
    channel_obj = WeixinChannel()
  else if channel_type == "qq":
    channel_obj = QQChannel()
  else if channel_type == "google":
    channel_obj = GoogleChannel()
  else if channel_type == "facebook":
    channel_obj = FaceBookChannel()
	if channel_obj != None:
    channel_obj.login_by_channel()

```

难道把这个if else的过程封装成一个函数,

```python
def get_channel_obj(channel_type):
    channel_obj = None
	if channel_type == "weixin":
    channel_obj = WeixinChannel()
  else if channel_type == "qq":
    channel_obj = QQChannel()
  else if channel_type == "google":
    channel_obj = GoogleChannel()
  else if channel_type == "facebook":
    channel_obj = FaceBookChannel()
  return channel_obj   
```

get_channel_obj函数就叫做工厂方法？或者把get_channel_obj放到一个类的静态方法，那么这个类就叫做工厂类？

```python
class ChannelFactory(object):
  @staticmethod
  def get_channel_obj(self, channel_type):
    channel_obj = None
    if channel_type == "weixin":
      channel_obj = WeixinChannel()
    else if channel_type == "qq":
      channel_obj = QQChannel()
    else if channel_type == "google":
      channel_obj = GoogleChannel()
    else if channel_type == "facebook":
      channel_obj = FaceBookChannel()
    return channel_obj  
  
ch_obj = ChannelFactory.get_channel_obj("weixin")
```

ChannelFactory就是工厂类？

> 还别说，这里其实就是简单工厂的逻辑，就是把这部分逻辑转移了下而已，可参考这篇文章[设计模式(Python)-简单工厂，工厂方法和抽象工厂模式](https://blog.csdn.net/huobanjishijian/article/details/79151351)

这里，将判断逻辑转移到了工厂类内部，使得主逻辑不需要关注判断逻辑，仅需要传入必要的参数即可获取对应的对象







## 2、百科内介绍的
### 简介
### 背景
### 实现思路
### 实现方式

## 3、自己思考总结结果
### 一句话总结
### 实现思路
### 目的
### 场景
### Python实现该模式
### Go实现该模式


## 4、参考

[设计模式(Python)-讲清了简单工厂](https://blog.csdn.net/huobanjishijian/article/details/79151351)

[实际开发中哪些场景需要用到工厂模式，小兔有点乖 讲清了简单工厂和工厂方法的区别](https://segmentfault.com/q/1010000005849224)

[简单工厂模式](https://design-patterns.readthedocs.io/zh_CN/latest/creational_patterns/simple_factory.html)