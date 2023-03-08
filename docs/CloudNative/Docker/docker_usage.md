#docker使用

## 一、和docker容器进行文件交互
1、获取docker容器id  
2、本机往docker容器内复制 docker cp 本机路径/文件名 容器id:/目标路径/文件名  
2、docker往本机复制文件 docker cp 容器id:/目标路径/文件名 本机路径/文件名

## 二、docker 容器内配置修改
docker内的文件是只读的，但是提供了一种方式  
KONG_ + 配置名 = 期望值  
比如我要设置go插件可执行目录为/usr/local/bin  
那么启动docker kong的时候  
-e "KONG_GO_PLUGINSERVER_EXE=/usr/local/bin/go-pluginserver" \

前2步可以将生成的插件文件复制到容器内的指定目录，然后通过启动时的配置，完成要求的配置更改。







