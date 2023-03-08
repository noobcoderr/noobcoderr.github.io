# protobuf学习记录
我的理解，protobuf就是一个类似于json的数据结构，或者协议？

## 基本结构
该类型文件以.proto结尾  
文件内容基本为
```proto
syntax = "proto3";  //定义protobuf协议版本

package account;    //指定包名，防止多个proto文件内有同样的结构体 

option go_package="protobuf/account"; //指定为go语言，以及输出位置

//定义接口请求参数的结构体
message LoginBySnsReq {
    string app_id = 1;
    string package_name = 2;
    string client_id = 3;
    string sns_type = 4;
    string sns_id = 5;
    string sns_token = 6;
}

//定义接口返回参数的结构体
message LoginBySnsResp {
    string code = 1;
    string info = 2;
    string data = 3;
}

```

## 参考
[Protobuf 终极教程](https://colobu.com/2019/10/03/protobuf-ultimate-tutorial-in-go/)  
[一文了解protoc的使用](https://juejin.cn/post/6949927882126966820)  
