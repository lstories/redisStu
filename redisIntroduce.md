# redis
## 下载
- 下载地址：https://github.com/tporadowski/redis/releases
- 解压压缩包，进入文件夹
- 打开cmd，输入命令```redis-server.exe redis.windows.conf```
出现下面界面，即成功启动
![image](https://user-images.githubusercontent.com/91355013/231044734-90366770-5d4e-4601-b350-e5084adad6cb.png)
- 再打开另一个cmd，输入命令```redis-cli.exe -h 127.0.0.1 -p 6379``` 进入操作端
- 在输入命令```set key lstory11```，设置键值对
- 在输入命令```get key```，获取键值对的值
![image](https://user-images.githubusercontent.com/91355013/231045577-3fad6c9a-841f-4dac-99ea-9ccf4c5be83d.png)
## 数据类型
### String 字符串
实例：使用了 Redis 的 SET 和 GET 命令。键为 runoob, 一个键最大能存储 512MB。
```
SET runoob "靓仔"
返回OK
GET runoob
"靓仔"
```
### Hash(哈希)
实例:
```DEL runoob``` 用于删除前面测试用过的 key，不然会报错：```(error) WRONGTYPE Operation against a key holding the wrong kind of value```
```
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> HMSET runoob field1 "Hello" field2 "World"
"OK"
redis 127.0.0.1:6379> HGET runoob field1
"Hello"
redis 127.0.0.1:6379> HGET runoob field2
"World"
```
实例中我们使用了 Redis HMSET, HGET 命令，HMSET 设置了两个 field=>value 对, HGET 获取对应 field 对应的 value。

### List(列表)
Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）。
实例:
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> lpush runoob redis
(integer) 1
redis 127.0.0.1:6379> lpush runoob mongodb
(integer) 2
redis 127.0.0.1:6379> lpush runoob rabbitmq
(integer) 3
redis 127.0.0.1:6379> lrange runoob 0 10
1) "rabbitmq"
2) "mongodb"
3) "redis"

### Set(集合)
Redis 的 Set 是 string 类型的无序集合
集合是通过哈希表实现的, 所以添加, 删除, 查找 的复杂度都是O(1).
#### sadd命令
添加一个String元素到Key对应的set集合中, 成功返回1, 如果元素已经在集合中了返回0.
```
sadd key member
```
实例:
```
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> sadd runoob redis
(integer) 1
redis 127.0.0.1:6379> sadd runoob mongodb
(integer) 1
redis 127.0.0.1:6379> sadd runoob rabbitmq
(integer) 1
redis 127.0.0.1:6379> sadd runoob rabbitmq
(integer) 0
redis 127.0.0.1:6379> smembers runoob

1) "redis"
2) "rabbitmq"
3) "mongodb"
```

### zset(sorted set:有序集合)
- Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
- 不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
- zset的成员是唯一的,但分数(score)却可以重复。
#### zadd命令
添加元素到集合, 元素在集合中存在则更新对应score
```
zadd key score member
```
实例:
```
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> zadd runoob 0 redis
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 mongodb
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 rabbitmq
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 rabbitmq
(integer) 0
redis 127.0.0.1:6379> ZRANGEBYSCORE runoob 0 1000
1) "mongodb"
2) "rabbitmq"
3) "redis"
```













