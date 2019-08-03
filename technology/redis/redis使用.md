# redis 使用

- [ ] redis 基本概念
- [ ] redis 基本使用
- [ ] redis 源码学习



## redis基本概念

### redis 基本数据类型

- string(字符串)
- hash(哈希)
- list(列表)
- set(集合)
- zset(有序集合)

## redis 使用

### 连接到redis服务器

```bash
./redis-cli -h 127.0.0.1 -p 6379
```



### 字符串

> 用于保存键值对
>
> 字符串类型键允许存储的数据最大容量是512M

```bash
# 赋值
set key value
# 取值
get key 
# 对于integer数值+1
incr key
# 增加指定的整数
incrby key increment
# 减少1
decr key
# 减少指定整数
decrby key decrement
# 增加指定浮点数
incrbyfloat key increment
# 向尾部追加值
append key value
# 获取字符串长度
strlen key
# 同时获取多个key
mget key ...
# 同时设置多个key value
mset key value ...
# 判断key是否存在
exists key
# 获取符合规则的键名列表
keys pattern
# 删除key
del key
# 获取key类型
type key
```



```bash
# 保存字符串
SET name "hello"
# 获取key
GET name
# 删除
DEL name
```

位操作

```bash
# 获取字符串指定为二进制位的值
getbit key offset
# 设置字符串指定位置二进制值
setbit key offset value
# 获取字符串类型键中值是1的二进制位个数
bitcount key [start] [end]
# 对多个字符串类型键进行位运算，并将结果存储在destkey参数指定的键中
bitop operation destkey key [key ...]
```



### 哈希

> 用于保存键值对集合，适合存储对象，每个hash可以存储 `2^32 -1`个键值对

```bash
# 存多个键值对集合
HMSET key field1 value1 field2 value2 ...
# 取多个
HMGET  key field  key1 field1
# 存单个
hset key filed value
# 取单个
hget key filed
# 判断字段是否存在
hexists key field
# 当字段不存在时赋值
hsetnx key field value
# 增加数字
hincrby key field increment
# 删除字段
hdel key field [field ...]
# 只获取字段名
hkeys key
# 只获取字段值
hvals key
# 获取字段数量
hlen key
# 获取hash散列包含的所有键值对
hgetall key

```

### 列表

> 保存简单的字符串列表，最多可以存储`2^32-1`个元素



```bash
# 向列表左边添加元素
lpush key value [value ...]
# 向列表右边添加元素
rpush key value [value ...]
# 从列表两端弹出元素
lpop key
rpop key
# 获取列表中元素个数
llen key
# 获取列表片段
lrange key start stop
# 删除列表中指定的值
lrem key count value
# 获取/设置指定索引的元素值
lindex key index
lset key index value
# 只保留列表指定片段
ltrim key start end
# 向列表中插入元素
linsert key before|after pivot value
# 将元素从一个列表转移到另外一个列表中
rpoplpush source destination

```



```bash
127.0.0.1:6379> lpush duan redis
(integer) 1
127.0.0.1:6379> lpush duan is
(integer) 2
127.0.0.1:6379> lrange duan 0 1
1) "is"
2) "redis"
127.0.0.1:6379> lrange list 0 -1
1) "C++"
2) "java"
3) "redis"
127.0.0.1:6379> linsert list after C++ python
(integer) 4
127.0.0.1:6379> lrange list 0 -1
1) "C++"
2) "python"
3) "java"
4) "redis"
```



### 集合

> 添加一个 string 元素到 key 对应的 set 集合中，成功返回1，如果元素已经在集合中返回 0，如果 key 对应的 set 不存在则返回错误。集合中最大的成员数为`2^32-1`个



```bash
# 增加和删除元素
sadd key member [member ...]
srem key member [member ...]
# 获取集合中的所有元素
smembers key
# 判断元素是否在集合中
sismember key member

# 集合差集
sdiff key [key ...]
# 集合交集
sinter key [key ...]
# 集合并集
sunion key [key ...]
# 进行集合运算并将结果存储
sdiffstore destination key [key ...]
sinterstore destination key [key ...]
sunionstore destination key [key ...]
# 从集合中随机获得元素
srandmember key [count]
# 从集合总弹出一个元素
spop key
```



```bash
127.0.0.1:6379> sadd set 1
(integer) 1
127.0.0.1:6379> sadd set 2
(integer) 1
127.0.0.1:6379> sadd set 3
(integer) 1
127.0.0.1:6379> smembers set
1) "1"
2) "2"
3) "3"
```



### 有序集合

> 集合中元素根据分数从小到大排列

```bash
# 增加/修改元素
zadd key score member [score member ...]
# 获得元素分数
zscore key member
# 获取排名在某个范围的元素列表
zrange key start stop [withscores]
# 获取指定分数范围的元素
zrangebyscore key min max [withscores] [limit offset count]
# 增加某个元素的分数
zincrby key increment member
# 获取集合中元素的数量
zcard key
# 获取指定分数范围内的元素个数
zcount key min max
# 删除一个或多个元素
zrem key member [member ...]
# 按照排名范围删除元素
zremrangebyrank key start stop
# 获得元素排名(从小到大排序)
zrank key member
```

```bash
127.0.0.1:6379> zadd zset 0 a
(integer) 1
127.0.0.1:6379> zadd zset 0 c
(integer) 1
127.0.0.1:6379> zadd zset 1 e
(integer) 1
127.0.0.1:6379> zadd zset 4 a
(integer) 0
127.0.0.1:6379> zrangebyscore zset 0 1000
1) "c"
2) "e"
3) "a"
127.0.0.1:6379> zrangebyscore zset 60 +inf limit 1 3
1) "pysical"
2) "english"
3) "math"
```



## 事务

### `multi...exec`

> redis事务保证一个事务中的命令要么都执行，要么都不执行
>
> 语法错误，可以保证事务
>
> 运行错误无法保证事务，比如如果出现命令与数据类型不匹配的时候，在实际执行之前redis是无法发现的，所以其他的命令会依次执行

### `watch` 

> 可以监控一个或多个键，一旦其中有一个键被修改或删除，之后的事务就不会执行。监控一直持续到`exec` 命令，执行过`exec`命令后会取消所有键的监控

## 过期时间
```bash
# 设置过期时间(单位：s) expire 也可以修改过期时间
expire key timeout
# 功能类似expire，区别是单位：ms
pexpire key timeout
# 获取剩余过期时间
ttl key
# 修改过期时间为不过期
persist key
```

## 排序

```bash
sort listKey [desc] [limit offset count]
```



```
127.0.0.1:6379> lpush lnum 1 3 4 1 5 3 90 13 8 4 3 4
(integer) 12
127.0.0.1:6379> sort lnum
 1) "1"
 2) "1"
 3) "3"
 4) "3"
 5) "3"
 6) "4"
 7) "4"
 8) "4"
 9) "5"
10) "8"
11) "13"
12) "90"
```

