## Redis

## 部署架构
参考下文

## 备份策略
AOF和RDB

## 业务中对Redis的使用

### 基础数据结构的使用
string  

使用的最多

### 分布式锁


## 问题
瓶颈问题

随着用户数的增长，并发读写数据库成为瓶颈。为什么呢？

随着用户数量增长，为什么数据库IO会成为瓶颈呢？我好像想通过，但是后来忘了

现代服务器的性能瓶颈在IO

Redis的性能瓶颈在IO上

使用 Memcached 作为本地缓存，使用 Redis 作为分布式缓存



[大Key问题](https://www.51cto.com/article/701990.html)

## 参考文章
[Redis部署架构](https://www.lanmper.cn/redis/t9372)
