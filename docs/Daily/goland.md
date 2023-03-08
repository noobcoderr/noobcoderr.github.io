# Goland使用问题

## 问题：macOS点开goland无响应
goland之前一直使用破解版，但是最近更新了macos系统到12.1之后，频繁闪退
先是pycharm破解的专业版一直闪退，导致我直接换为了社区版，也勉强够用
但是现在goland没有社区版，就只能另寻他法，先删掉了破解版，然后装了最新的goland。

但是发现有个问题就是，一直打不开安装的最新版goland，我以为是系统问题，然后我又再一次更新了系统到12.4
结果还是没有好转，然后我就搜网上的案例，发现可能是之前破解版设置的一些环境变量没删干净，接下来发下解决办法

1、首先确认下是环境问题
命令执行： `/Applications/GoLand.app/Contents/MacOS/goland`  这个命令是使用命令行打开goland，如果报错
zhangjie@bogon bin % `/Applications/GoLand.app/Contents/MacOS/goland`
2022-06-28 00:40:13.641 goland[2909:41637] allVms required 1.8*,1.8+
2022-06-28 00:40:13.644 goland[2909:41641] Current Directory: /Applications/GoLand.app/Contents/bin
2022-06-28 00:40:13.644 goland[2909:41641] parseVMOptions: GOLAND_VM_OPTIONS = (null)
2022-06-28 00:40:13.644 goland[2909:41641] fullFileName is: /Applications/GoLand.app/Contents/bin/goland.vmoptions
2022-06-28 00:40:13.644 goland[2909:41641] fullFileName exists: /Applications/GoLand.app/Contents/bin/goland.vmoptions
2022-06-28 00:40:13.644 goland[2909:41641] parseVMOptions: /Applications/GoLand.app/Contents/bin/goland.vmoptions
2022-06-28 00:40:13.644 goland[2909:41641] parseVMOptions: /Applications/GoLand.app.vmoptions
2022-06-28 00:40:13.647 goland[2909:41641] parseVMOptions: /Users/zhangjie/Library/Application Support/JetBrains/GoLand2022.1/goland.vmoptions
2022-06-28 00:40:13.648 goland[2909:41641] parseVMOptions: platform=17 user=4 file=/Users/zhangjie/Library/Application Support/JetBrains/GoLand2022.1/goland.vmoptions
Error opening zip file or JAR manifest missing : /Users/zhangjie/Pojie/Goland/jetbrains-agent.jar

即找不到jar包，那就基本上可以确认问题

2、找到这个文件，删掉之前破解时指定的破解jar包
这里Library/Application Support路径中间有空格，要不转译一下
cd /Users/zhangjie/Library/Application\ Support/JetBrains/
要不路径放字符串里
cd '/Users/zhangjie/Library/Application Support/JetBrains/' 即可
然后vim一下删掉加的那行即可

zhangjie@bogon GoLand2022.1 % cat goland.vmoptions
# custom GoLand VM options

-Xmx2048m
-Djava.net.preferIPv4Stack=true
-Djdk.attach.allowAttachSelf

# -javaagent:/Users/zhangjie/Pojie/Goland/jetbrains-agent.jar

3、再次执行`/Applications/GoLand.app/Contents/MacOS/goland` 生效

参考文档：[详述 Mac GoLand 安装后打不开（闪退）的解决方法](https://www.361shipin.com/blog/1510251852946472960)