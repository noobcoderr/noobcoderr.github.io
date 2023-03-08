# 使用golang遇到的那些问题及解决方案


## module xxx@latest found, but does not contain package xxx/yyy
示例: google.golang.org/grpc/naming: module google.golang.org/grpc@latest found (v1.47.0), but does not contain package google.golang.org/grpc/naming

分析: 就是本地环境的依赖是最新版本，而有一个模块在最新版本已经被移除了，所以需要更换一个老版本

解决命令：
go mod edit -replace google.golang.org/grpc=google.golang.org/grpc@v1.29.0

参考:  
https://github.com/fullstorydev/grpcurl/issues/237  
[Go学习笔记（十）老项目迁移 go module 大型灾难记录](https://razeen.me/posts/accidents-of-migrating-to-go-modules/)

## go版本的切换
背景：需要升级到新版本，但是又不想升级到最新    
brew upgrade go 会直接升级到最新，而最新版本和之前的版本差异较大

解决命令：  
brew uninstall go  卸载老版本的go  
brew install go@1.17   下载指定版本的go  
brew link go@1.17 -f     系统环境变量更新   
当然后续还得改go的goroot环境变量


## go版本升级到1.17后带来的问题
1、下载依赖由go get xxx 变为go install xxx
[Go语言之讲解GOROOT、GOPATH、GOBIN](https://cloud.tencent.com/developer/article/1200612)

