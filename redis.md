总体特征
===
- 高性能的键值存储服务
- 多种数据结构
- 丰富的功能
- 高可用、分布式支持
- 开源
  
特性总览
===
- 速度快  
  1）存储于内存中  
  2）使用C语言编写  
  3）单线程 
- 持久化
- 多种数据结构
- 功能丰富
- 简单

应用场景
---
- 可作为缓存系统（不能说他是缓存）  
    ![cache](./assets/redis/cache.png)
- 计数器    
  1）微博、视频网站的点赞计数  
- 消息队列系统  
- 排行榜    
  1）(使用有序集合)
- 社交网络    
  1）粉丝数、关注数
- 实时系统  
  1）垃圾邮件处理系统等（使用bitmap）

启动方法
---
- 验证是否启动  
    1）`ps -ef | grep redis`  
    2）`net -antpl | grep redis`  
    3）`redis-cli -h host -p port ping`  
- 最简启动：`redis-server`  
- 动态参数启动：`redis-server --port 6380`  
- 配置文件启动：`redis-server config` 如 `redis-server /etc/redis.conf` 

常用配置项
---
- daemonize：是否是守护进程
- port：redis对外端口
- logfile：redis系统日志
- dir：redis工作目录

通用命令
---
- KEYS [patten]：枚举key    O(n)  
- DBSIZE：返回当前数据库key的数量   O(1)
- EXISTS KEY：KEY是否存在   O(1)
- DEL KEY：删除KEY  O(1)
- EXPIRE KEY SECONDS：给KEY设置过期时间 O(1)
- TYPE KEY：KEY的类型   O(1)
  
单线程为什么这么快
---
- 纯内存（主要原因）
- 非阻塞IO
- 避免线程切换和竞态消耗  
  
一次只运行一条命令，所有命令都像是在一条单向公路上排队


一对键值对占用空间 <=100k 较好

list
---
- LPUSH/RPUSH KEY VALUE
- LPOP/RPOP KEY
- LINSERT KEY before/after value newValue在值value前/后插入newValue
- LREM KEY count VALUE删除队列中值为value的元素
- LTRIM KEY start end删除从start到end的部分，下标从0开始
- LRANGE KEY start end  时间复杂度O(n)
- LLEN KEY 时间复杂度O(1)
- LSET KEY index value将下标index的元素值设为value
- 应用：  
  1)LPUSH + LPOP = 栈  
  2)LPUSH + RPOP = 队列  
  3)LPUSH + LTRIM = 指定数量的队列    
  4)LPUSH + BRPOP = 消息队列


set
---
特性：无序，无重复  
可计算集合之间的交集、差集、并集  
主要命令：  
- smembers：枚举全部元素
- srandmember/spop：随机返回一个元素/随机返回并移除一个元素
- tag：给key打上标签
- sadd + sinter = 社交相关的（比如共同关注）  
  
