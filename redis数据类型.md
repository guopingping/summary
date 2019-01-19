 #### 1. Redis是什么？ 
 -----------------------------------------------
 		Remote Dictionary Server
 		被称为数据结构服务器。
 		完全开源、非关系型、高性能的key-value存储系统。
 		支持5中数据类型：存储string、list、set、zset和hash
----------
#### 2.Redis的特点
 ----------------------------------------------------
```
	redis是单线程的，操作是安全的；
	redis支持数据的持久化，可将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用；
	redis支持key-value，并提供list、set、zset、hash等数据结构的存储；
	redis支持数据的备份，即master-slave模式的数据备份；
	redis单个value的最大限制1GB；
```
-----
 		
#### 3.五种数据类型介绍及使用场景
------
	1) String 
				key-value，可以包含任何数据，一个键最大能存储512MB。
				比如图片或者序列化的对象。
			
			set：设置存储在指定键中的值；
			get：获取存储在指定键中的值；
			del：删除存储在指定键中的值；

	使用场景:
		incr 自增 ；eg：生成id；
		decr 减少；eg：库存；
		计数器缓存；
		缓存–过期时间设置，模拟session；

	使用案例：
		![string使用](https://img-blog.csdnimg.cn/20190116225059670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21vXzI0Nw==,size_16,color_FFFFFF,t_70)
	
	2） List
        redis列表，按照插入顺序可以添加一个元素到列表的头部或尾部。

        rpush：将给定值推入列表的右端；
        lrange：获取列表在指定范围上的所有值；
        lindex：获取列表在指定范围上的单个元素；

        使用场景：
            多任务调度队列；

    3）Set
        string类型的无序集合。集合是通过哈希表实现的，增删查复杂度都是O(1)

        sadd：将给定元素添加到集合；
        smembers：返回集合包含的所有元素；
        sismember：检查指定元素是否存在于集合中；

        使用场景：
            微博关注数。

    4）hash
        键值对集合。是string类型的field和value的映射表，适用于存储对象。

        hset：散列里面关联起指定的键值对；
        hget：获取指定散列键的值；
        hgetall：散列包含的所有键值对
        hdel：如果给定键存在于散列中，移出这个键；

        使用场景：
            购物车

    5）zset
        集合，不允许重复的成员。每个元素都会关联一个double类型的分数。
        redis通过分数来为集合中成员进行从小到大的排序。
        zset的成员是唯一的，但分数却可以重复。

        zadd：将一个带有给定分值的成员添加到有序集合里面；
        zrange：根据元素在有序排列中所处的位置，从有序集合里面获取多个元素；
        zrangebyscore：获取有序集合在给定分值范围内的所有元素；
        zrem：如果指定成员存在于有序集合中，那么移出这个成员

        使用场景
            排行榜

---
 #### 2. 如何使用Redis？
