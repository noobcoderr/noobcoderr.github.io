# Python跑数遇到的问题

## 背景
有个bug导致线上30w用户数据有缺失，需要在尽可能短的时间内完成手动更新，否则会影响用户体验，更新手段就是
调用一个HTTP接口。

## 分析
最开始的思路就是
直接读取用户列表，生成对应请求url，然后使用多协程gevent库进行执行，并发控制在200-300即可，使用自己的机器大概15分钟就可以跑完。


## 代码
```python
import time

import gevent
import requests


def update_user_info(req_url):
    try:
        rst = requests.get(req_url).json()
    except Exception as e:
        print(e)
        return False
    if rst.get("code", -1) == 0:
        print("succ ", req_url)
        return True
    else:
        return False


if __name__ == '__main__':
    uid_lst = [i for i in range(30000)]
    task_lst = []
    for u in uid_lst:
        req_url = "http://mo.yu.com/open/update/user?user_id={}".format(u)
        task_lst.append(gevent.spawn(update_user_info, req_url))
    print("开始执行", time.time())
    gevent.joinall(task_lst)
    print("执行结束", time.time())
```
按这个代码执行，并没有达到我们想要的效果，似乎每秒只能执行15-16条请求，那么到底是哪里设置不对呢?
而且有不止一个问题，接下来一一阐述原因和解决办法。
## 问题
1、并发控制问题，超出本机端口限制？  

2、数据读取问题，流式读取vs一次性读取？  
3、数据判断问题效率，列表 in 和dict get  
4、池问题，协程池，http连接池  
5、进度问题，执行多少条了，怎么有效统计，最后如何落盘到日志  
6、日志问题，不同级别日志怎么输出到对应的日志文件内；日志打印是否线程安全  
7、gevent问题，猴子补丁，greenlet结束阻塞  
8、优雅的设计脚本的问题，而不是面向过程  

执行19566条任务，耗时721.7475099563599秒

协程池40  http连接池100：
执行19566条任务，耗时569.7662620544434秒
并发不到40

协程池100  http连接池200：
很慢，因为在成功情况下打印日志，IO操作很废时间

协程池150  http连接池300：
10分钟未跑完，原因未知，好像并发被限制到了20多，未引入 monkey.patch_all()


协程池100  http连接池100：



1、技术方案
	多线程：速度慢，
	多进程+多协程：控制不住，耗尽机器所有内存
	单进程+多协程(协程池)：速度可控，大约60个请求/s，但是会超过65536个链接，会有很多失败，

2、请求返回json打印成日志后，无法使用json.loads
	使用eval()解决。https://www.jianshu.com/p/3a7dbd17e7b9
3、gevent导入问题：https://blog.csdn.net/a19990412/article/details/82966452
4、超过最大链接数：maximum recursion depth exceeded while calling a Python object
	
5、Python写入json文件到excel
	https://blog.csdn.net/destinymf/article/details/78096678
6、多进程+协程示例：https://segmentfault.com/a/1190000038437451
7、提高爬虫效率-多线程：https://zhuanlan.zhihu.com/p/55057487
8、golang操作excel：https://segmentfault.com/a/1190000037585645



参考
[Python requests接口测试小技巧](https://testerhome.com/topics/19899)
[基于协程的python网络库gevent](http://www.bjhee.com/gevent.html)