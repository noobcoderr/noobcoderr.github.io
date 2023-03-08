# 一些Nginx实践经验
在云服务器上部署服务时，Nginx部署是必不可少的，在使用过程中遇到了一些问题，在此记录下来。

## 一些基础的前置知识
1、服务器上安装nginx

2、nginx的启动、停止、重启、重载配置  
启动:  
停止:   
重启:   
重载配置: nginx -s reload


## 一些场景的使用 
### 1、为新起的服务配置端口转发
云服务器上新起了个服务，端口在8080，域名为test.me.com
那么我们需要配置一个新的server
```json
{
      server {
        listen 80;
        server_name test.me.com;
        location / {
           proxy_pass http://127.0.0.1:8080/;
        }
    }
}
```
nginx -s reload之后，我们访问test.me.com域名即可访问这个新服务的接口了。