# Flutter学习笔记
1、创建一个flutter项目
	flutter create 项目名

2、打开ios模拟器
	open -a Simulator

3、运行flutter项目
	进入项目
	cd proj/
	flutter run 

4、安装三方包，类似于pip install
	flutter pub add english_words


小记录

1、flutter应用中，所有元素都是widget，

2、每个widget，都有build()函数

看到没，Flutter 其实就是这么简单！你的关注点只要在：

1、创建你的 StatelessWidget 或者 StatefulWidget 而已。  
2、你需要的就是在 build 中堆积你的布局，然后把数据添加到 Widget 中，最后通过 setState 改变数据，从而实现画面变化。

[macos下安装flutter](https://flutterchina.club/setup-macos/)

[flutter实战](https://book.flutterchina.club/chapter1/dart.html#_1-4-1-%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E)

[fluuter游戏开发](https://juejin.cn/post/6856681993418211336)

《flutter实战》，
	https://book.flutterchina.club/chapter2/first_flutter_app.html  
	在拉钩教育上的课程：https://kaiwu.lagou.com/course/courseInfo.htm?courseId=251#/detail/pc?id=3518  
	编写第一个flutter应用：https://codelabs.flutter-io.cn/codelabs/first-flutter-app-pt2-cn/index.html#3  
