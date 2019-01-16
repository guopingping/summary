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
	list
---
 #### 2. 如何使用Redis？
