{{indexmenu_n>4}}

## 配置节点

对于mongodb3.2及以下版本，可以通过创建配置节点、路由节点构建分片集群。

1、在控制台选择云数据库UDB\>MongoDB管理，“更多”中点击“创建配置节点”，到达新建配置节点页面中，选择所在地域及可用区，基础配置可选择：数据库机型、内存、硬盘固定20G、版本、配置文件，付费方式和数量，系统会根据选择计算费用，页面右侧会显示所需支付费用。创建MongoDB配置节点时会使用默认配置文件，若有特殊需要，用户可以上传自定义配置文件。

![image](/images/config.png)

![image](/images/mongodbv406.png)

2、确认支付完成后，页面跳转回MongoDB实例管理页，MongoDB实例进行初始化，待初始化完成之后即可使用。在MongoDB实例管理页，列出了所有MongoDB实例信息，包括实例名称、属性、IP地址、机型、配置、状态、操作等。

![image](/images/mongodbv408.png)

3、创建Mongos路由节点：在控制台选择configsvr属性的MongoDB实例，点击操作项中的创建路由节点，在新建页面选择内存及配置文件确认支付。

![image](/images/mongodbv409.png)

![image](/images/mongodbv410.png)

![image](/images/mongodbv411.png)

4、选择某一个MongoDB实例后，点击名称或详情、跳转到其二级详细页面，详情页面可以查看实例信息、监控数据和进行常用数据库管理操作。

![image](/images/mongodbv404.png)
