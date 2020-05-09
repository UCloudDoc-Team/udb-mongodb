# 副本集架构



UCloud云数据库MongoDB副本集架构：

![image](/images/mongodb001.png)

默认一键副本集三节点包含主节点(Primary)、副本节点(Secondary)、仲裁节点(Arbiter)，客户可以跟据业务需求情况，在控制台上可自主增减Secondary节点和Arbiter节点。

主节点(primary)负责整个副本集的读写，用户也可根据业务需求情况设置全部或部分读请求到副本节点(Secondary)；副本集实时同步数据，如果主节点出现故障或宕机，副本节点就会选举一个新的主节点，这一切对于应用服务器不需关心。

仲裁节点不存储数据，只负责故障转移的群体投票，这样就少了数据复制的压力。UCloud MongoDB产品中，仲裁节点(Arbiter)免费。
