# Python使用Lua问题记录
业务中有些使用Redis的场景，可以引入Lua脚本    
1、遍历查询Redis批量用户信息，将用户列表在Lua脚本内遍历查询Redis以减少连接Redis的次数    
2、支付扣款发货等事务场景需要保证前后操作的原子性，将事务操作放置在Lua脚本内可以达到效果    


## Lua的基本语法
`EVAL script numkeys key [key ...] arg [arg ...]`

说明：
1、script是第一个参数，为具体的Lua脚本。    
2、第二个参数numkeys指定后续参数有几个key，对于确定参数个数场景可以使用这个，注意，就算后面没有参数，也要传0 
3、key [key ...]，是要操作的键，可以指定多个确定数量的参数，在lua脚本中通过KEYS[1], KEYS[2]获取
4、arg [arg ...]，参数，在lua脚本中通过ARGV[1], ARGV[2]获取，对于不定长度参数场景可以使用这个，例如不定长用户列表。 

示例：
`EVAL script 2 zhangsan lisi wangwu sunliu liqi`    
`2`指定了后面有2个参数，即`zhangsan`和`lisi`  可以通过KEYS[1]和keyS[2]获取到这俩值  
再往后的`wangwu`和`sunliu`、`liqi`则是不定长参数列表内容，可以通过`ARGV`获取完整的列表，也可以使用ARGV[1]、ARGV[2]、ARGV[3]获取每个单独的值


## 常见场景及解决办法
### 1、(error) ERR value is not an integer or out of range   
该报错出现于未指定传参数量，即未传递numkeys，就算是0个参数，也需要在其位置传递0

### 遍历传入的列表，然后将查询结果至于列表内返回
如果使用Lua于处理批量数据，可以选择的数据结构就是列表，lua里的列表用法为
参数传递情况
`EVAL script 0 10001 10002 10003`
lua内接收变量为`ARGV`，其实就等于 `[10001, 10002, 10003]`
在lua内遍历使用时, 使用`ipairs`遍历`ARGV`即可
```markdown
local result = {}
for i,v in ipairs(ARGV) do
    result[#result + 1] = redis.call("hget", "user:" .. v, "userId")
end
```

# 参考文档
[Lua教程-菜鸟教程](https://www.runoob.com/lua/lua-basic-syntax.html)    
[Redis使用Lua脚本](https://www.cnblogs.com/52fhy/p/9786720.html)    
[Redis 执行 Lua 脚本](https://blog.csdn.net/weixin_39927848/article/details/110831116)

