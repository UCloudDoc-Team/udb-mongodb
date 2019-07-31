# 规格版本

{{indexmenu_n>3}}

### 产品版本

MongoDB副本集及分片集群支持MongoDB 2.4、MongoDB 2.6、MongoDB 3.0、MongoDB 3.2、MongoDB3.4、MongoDB 3.6和MongoDB 4.0。

用户可以根据需求选择相应的云数据库版本。

### 各版本新功能介绍

**MongoDB3.4版本：**

初始化同步的时候，同步建立所有的索引。

支持配置 Primary 追数据的时间。

增加了⼤量的aggregation操作符，功能更强大，比如$graphLookup能支持更复杂的关系运算。

**MongoDB3.6版本：**

3.6版本将认证机制MONOGDB-CR更新为SCRAM，安全性加强。

增加了更多的聚合操作符，如：$arrayToObject,$objectToArray,$mergeObjects 等。

添加了replSetResizeOplog 命令，WiredTiger存储引擎可以动态调整oplog的⼤小。

**MongoDB4.0版本：**

引入多文档事务，支持副本集内部跨一或多个集合的多文档事务，保证针对多个文档的更新的原子性。

wt引擎的数据节点，不允许设置storge.journal.endbled为false。

通过读snapshot解决从库应用oplog加全局锁导致业务读与应用oplog相互阻塞的问题。
