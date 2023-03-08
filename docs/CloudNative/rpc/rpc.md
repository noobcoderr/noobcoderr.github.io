《搞不清楚rpc和http的区别？》

记住一句话：RPC让你用别人家的东西就像自己家的一样
比如你在go服务定义了一个方法sayhello()，想让另外一个python服务能够调用，就只能走http请求，把该函数放在http请求处理函数里
但是如果使用rpc，你可以直接在python服务内调用x.sayhello()，就真的像是在本地的另外一个包的方法一样。


[IM开发基础知识补课(九)：想开发IM集群？先搞懂什么是RPC！](https://zhuanlan.zhihu.com/p/139203251)