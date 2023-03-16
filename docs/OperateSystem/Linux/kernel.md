# Linux内核学习


系统调用：就是针对操作系统提供的标准接口进行调用来满足业务需求
函数调用：针对用户写的程序进行调用

用户函数想调用内核数据，需要执行int中断，int中断是进入内核的唯一方法

socket是进程间通信协议，只不过比较特殊，可以跨主机
	那么socket是不是也可以进行同主机的通信？答案是OK的，因为你可以本机起socket客户端，然后本机起socket服务端，然后进行数据发送操作

[推荐-Linux 内核揭秘](https://xinqiu.gitbooks.io/linux-insides-cn/content/index.html)

[Linux操作系统内核学习](https://ty-chen.github.io/categories/Linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E5%86%85%E6%A0%B8%E5%AD%A6%E4%B9%A0/)