# Shell使用大全

## xargs


## grep
基础用法
`grep xxx filename`

或用法:使用\|
`grep 'A\|B' filename`

正则用法: 使用-E 开启正则
`grep -E 'pattern1|pattern2' filename`

使用 egrep ，等价于 grep -E

参考[grep使用](https://blog.csdn.net/jackaduma/article/details/6900242)

## sed：利用脚本来处理、编辑文本文件

	例子1：去除字符串内的所有空格
	"my name" | sed 's/ //g'
	此处替换使用到的是  
	s/old/new/g：将当前行所有的old替换成new，s是substitute，g是global  
	例子2: 在文件头部追加内容(比如追加变更到git的CHANGELOG.md)  
	sed -i '0 i  somethingyouwanttoinsert ' file  
	例子3: 查看文件的第100行  
	sed -n '100p'  data.txt   
	

## tee：

	例子：将数据写入文件
	"pay log" | tee pay.log


## vim
	例子：将第二行开始的xxx改为squash
	:2,$s/pick/squash/g
	此处替换使用到的是：
	:1,10s/old/new/g：将第1到第10行所有的old替换成new，最后一行的话将10换为$

## wc:word count的简写，为统计指定文件中的字节数、字数、行数，并将统计结果显示输出
	例子: 计算文件的行数
	wc -l sample.txt

## awk: 
	例子1: 获取文件的行数，只返回数字，原理是获取最后一行的行号
	awk 'END {print NR}' sample.txt 
	例子2: 查看文件的第100行
	awk 'NR==100' data.txt 

## 参考链接
[vim文本替换](https://segmentfault.com/a/1190000004443210)
[linux sed命令](https://www.runoob.com/linux/linux-comm-sed.html)
[Linux 中查看文件第n行内容的命令](https://blog.csdn.net/u011138533/article/details/76919635)

shell程序中的2> /dev/null代表什么意思
	https://www.zhihu.com/question/53295083