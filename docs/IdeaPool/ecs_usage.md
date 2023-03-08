# 点子池
记录那些灵光一现的点子，期望能开发有意思的APP  
用一句话描述就是：主要面向xx用户，提供yy功能，具有zz特色

| 点子描述 | 例如：疫情期间屯菜屯货指南         |
| -------- | ---------------------------------- |
| 灵感来源 | 详细介绍                           |
| 市场调研 | 市面暂无同类型应用，或不具有xx功能 |
| 功能描述 | 根据用户xx要求，返回对应指南       |
| 面向用户 | 当然要尽可能广                     |


## 每日挑战

用户登录应用，就会收到一个挑战，用户接受挑战，则该挑战会被发布到广场，其他用户浏览或者点赞该记录，都会提醒发布用户，用户完成挑战，填写挑战结果，

随机活动api:https://www.free-api.com/use/340


很多时候，我们说我要每天干什么多少次，但是往往坚持不了多久，我们期望改变，但是大脑是懒惰的，不会主动给自己找事，不自律的人三天之后，大脑就不会乐意再告诉你今天要干什么了


1、随机挑战，记录，发帖

受众：
那些每天处于三点一线的生活重压下的人们，
那些有很多想做的事情，却一直没机会做的人们
像我一样长期宅，出门不知道做什么事情的人们

功能：
每天给每位用户分配一个挑战。在每天结束之前，用户可以选择完成挑战或者失败挑战，挑战结束都可以进行评论，附上挑战的结果，图片、文字、感悟等等
并以动态的形式展示在个人主页以及广场。其他人看到后，仅支持点赞功能。
每个挑战都可以按#键进行搜索，即可以看到该

支持登录：手机号+验证码、手机号一键登录、邮箱登录、

[坚持每天给自己一个小挑战](https://www.jianshu.com/p/f154fd6fc8e9)

[30天挑战](https://zhuanlan.zhihu.com/p/28277044)



## 文章生成器
蹭热点

1、狗屁不通文章生成器  
2、营销号文章生成器
3、抖音文案生成器

## TOCHALLENGE
一个每日挑战的应用，有一些积极向上的挑战，每天分配给自己去完成

原因:因为自己有拖延症，希望自己做出改变，但是每次都无法持之以恒，所以打算换个思路，不给自己制定详细而冗长的自律计划了，而是将挑战目标放在一个池子里，每天随机给自己分配一个完成即可。

需要：写一个服务端(go gin)，一个客户端(flutter)

功能：创建一个挑战池，针对挑战可以增加/删除/修改

个人IP：为持续性混吃等死，间歇性踌躇满志的人打鸡血？

受众人群？持续性混吃等死，间歇性踌躇满志的人？



内容(知乎、微博热榜)+工具(查快递、等等) + 广告


## 云服务器使用场景

云服务器目的
1、写引流软件，吸引流量，通过接入的广告进行赚钱
	原神抽卡分析
	王者荣耀昵称工具

2、小程序后端  
3、小游戏后端:原神moba  
4、测试demo

部署结构  
为了保证云服务器到期后，其上运行的程序、数据能平滑地迁移到下一个服务器上，考虑
部署的代码采用git打tag，然后使用tag对应的docker进行部署？
周期性dump数据到本地

## 域名思考

ACurdGuy
moyuto.top

## 磁力搜索下载APP
体验了下ios上的和googleplay上的，感受
主要从核心功能以及附加功能上进行分析
核心功能搜索，搜索源是不是足够多、搜索结果是否整洁、搜索结果是否可排序、搜索结果的质量是否可以一起给出。
ios上的，基本无免费的可用，都需要订阅才行，不知道是不是和applestore上的政策有关？因为ios上连迅雷都没有

google上的则太多了
种子搜索
	基本功能
	搜索
		1、按关键字进行搜索
		2、对搜索结果排序
		3、复制搜索结果
		4、显示文件大小、热度、track

评论区反馈
1、搜索历史
2、

闲谈 Spring Cloud + Netty 打造分布式可集群部署的 DHT 磁力爬虫（开源
	https://www.v2ex.com/t/541321
	https://github.com/shiyanhui/dht

6、自写DHT爬虫，爬取种子
	gude - 一个C++编写的DHT爬虫，用于爬取DHT网络上的torrent文件  
		https://github.com/bifang-fyh/gude
		https://www.jcdi.cn/yunjisuan/52946.html
		http://chu-studio.com/posts/2021/%E5%AE%9E%E7%8E%B0DHT%E7%BD%91%E7%BB%9C%E4%B8%8A%E7%9A%84%E7%A7%8D%E5%AD%90%E7%88%AC%E8%99%AB
	磁力获取命令行工具
		https://github.com/chenjiandongx/torrent-cli
		https://github.com/shiyanhui/dht
	https://studygolang.com/articles/9025



## 个人博客
捣鼓过程
写博客，记录日常学习
1、openwrite

2、图床问题
	1、白嫖七牛云10g OSS存储
	2、替换自定义域名
		https://www.i4k.xyz/article/weixin_39117963/102417032
	3、picgo安装问题，安装没问题，只是打开自动最小化，让我感觉没打开成功
	4、pico设置图床配置时，区域我填的华南，应该填z2
		https://zhuanlan.zhihu.com/p/141610018
	至此，图床问题解决
	后续：公共图床存在盗刷问题，需要解决，防止产生额外费用
	https://blog.csdn.net/weiwosuoai/article/details/90318488

3、产出
仍然是使用typora编辑

hugo+nginx+云服务器初步搭建博客记录
	https://www.gohugo.org/
	https://v3u.cn/a_id_81
	https://blog.csdn.net/weixin_34405332/article/details/93111057
	https://www.jianshu.com/p/ea2c3b2827ef
	解决403权限不足问题：https://segmentfault.com/a/1190000039420612、https://www.cnblogs.com/tujietg/p/10753041.html
	https://aiopsclub.com/nginx/nginx_static_file/
	https://tonybai.com/2015/09/23/intro-of-gohugo/
	ico图片制作：http://www.ico51.cn/、https://www.bitbug.net/
	chrome浏览器更换favicon.ico后不更新缓存：https://blog.csdn.net/Nightliar/article/details/54412718

## 描述生命
[假如知道自己的寿命，生命倒计时的软件](https://v2ex.com/t/834157#reply40)


## flutter实现账号支付客户端

CP名称、头像
用flutter创建SDK demo客户端
登录页面展示
1、游客登录
2、手机号密码登录
3、手机号验证码登录
4、渠道登录

用户管理
1、用户信息查询
2、绑定手机号
3、解绑手机号


支付页面展示
1、获取支付列表
2、拉起支付

订单管理
1、订单号查询

## 每日面经
收集互联网上的面经，整理成一定的格式，然后每天早上通过邮箱/短信/推送等方式推送到个人手机上
每次推送一条

