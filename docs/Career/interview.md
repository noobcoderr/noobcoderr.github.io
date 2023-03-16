# 面试
大学毕业时，其实参加的面试也不算多，但是也能稍微感受到一些套路，这里主要是想记录下，防止以后踩坑。
包含面试技巧，以及一些面试经验。

## 根据自身业务产生的一些面试点
每天多少订单量？怎么存储的？怎么保证订单号唯一，怎么保证订单号生成不混乱

200w, 接口QPS大约30

redis内存储

mongodb内存储

唯一靠的是使用redis内的INCR操作的原子性

不混乱靠的是

简历里写着参与了那么多项目，那么项目里面的疑难点是什么呢？有哪些关键技术？有什么闪光点？


2. 关键词：基本功，职业规划

所以，此时面试官会着重考察你的基本功，比如需求分析能力、数据分析能力、执行力、沟通能力等。这时候面试者也要尽量避免去扯一些诸如“战略”之类的东西，这样很容易把自己带沟里。

## 参考
[社招](https://github.com/aylei/interview)

[后端开发面试题](https://github.com/monklof/Back-End-Developer-Interview-Questions)

[面试-star法则](https://zhuanlan.zhihu.com/p/26558343)

[面试-star法则](http://www.jinwenhr.com/article/index.php?c=show&id=58)

[并性能高并发面试](https://www.cnblogs.com/heartstage/p/3415584.html)

[面试宝典](https://www.sohu.com/a/529243918_114819)