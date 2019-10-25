# FAQs



## MongoDB实例功能和开源MongoDB有区别吗？

MongoDB实例和原生MongoDB完全一致。

## MongoDB实例是否使用物理机搭建？

MongoDB实例使用物理机搭建，并采用高性能磁盘以及使用RAID1确保数据安全。

## MongoDB的安全性如何？

### 访问安全性

MongoDB实例仅支持通过云主机进行内网登陆且按账户进行隔离，因此仅有同一账户的云主机能够对MongoDB实例进行登录。

MongoDB实例是强制鉴权的，只能通过认证的。

### 数据安全性

所有的MongoDB实例的数据文件所存放的硬盘都进行了RAID1保护。

MongoDB实例每天都会进行数据备份，同时也提供了手工备份功能，以便用户能够在特定时间点主动对数据进行备份。

MongoDB实例（Master）支持创建从库（搭建在与主库不同的物理机上），从库与主库自动进行数据同步，提供数据灾备的能力。

## 如何备份与恢复？

MongoDB实例支持手动备份，用户可以保存某些关键时间点的重要数据备份，当前手工备份的允许保留个数为3个，如果超过3个，会自动删除最早的手动备份。创建手动备份时，用户只需要输入备份名称，后台会立刻开始进行备份工作。

备份可以下载至本地或云主机。

如果要恢复MongoDB实例，建议用户先将备份文件下载至本地，由专业人员确认无误后导入MongoDB实例中，以规避数据风险。

## MongoDB实例类型有哪些？

满足高可用和水平扩展的要求，支持单点、副本集、分片集群的多种架构演进。

所有的数据节点都是内置副本集的，即使单点也是一个副本集，所以副本集按类型划分可以细分为单点副本集和多点副本集，其中单点副本集只包含一个primary，多点副本集包含一个primary和若干个secondary或者arbiter。

关于副本集可参考：

<http://docs.mongodb.org/manual/core/replica-set-members/>

## 怎么查看MongoDB的统计信息？

MongoDB实例管理页可以查看统计信息。

## MongoDB集群包括哪些组件？

集群按规模可以划分为两种：

副本集：一个primary+若干个secondary+若干个arbiter，副本集提供高可用特性。

分片集群：具有分片功能的多副本集的分布式架构，支持scale-out特性，其中每个分片指的就是副本集，集群包括一个或多个分片（数据存储），一个或三个configsvr（集群元数据管理），和一个或多个Mongos（路由）。

当生产环境的数据规模、性能或载荷等因素超过单副本集的限制，建议启用分片。生产环境完整的分片集群架构包括：

分片集群的基本概念可参考：

<http://docs.mongodb.org/manual/core/sharding/>

## 配置文件有哪些？

提供两个默认配置文件，分别是shardsvr默认配置文件和configsvr默认配置文件，它们用于创建不同类型的实例，其中：

shardsvr配置文件：支持单点副本集、多点副本集、sharding的分片服务器实例。

configsvr配置文件：支持sharding的配置服务器实例。

用户可以从默认配置文件修改配置参数，另存为自定义的配置文件，供这些实例使用。

## 如何创建secondary和arbiter？

1、支持一键创建三节点副本集，如果需要更多节点，根据自身需求可以增加，方法如下：

进入控制台MongoDB实例管理页，选中primary节点，在右边的弹框中选中“创建节点”按钮进行创建。

![image](/images/mongodbv4node01.png)

2、在“创建节点”的弹框中选择节点类型secondary或arbiter。创建完成后，新增节点将按指定的角色加入到primary节点的副本集中。同个副本集的所有节点共享相同的管理员账号和密码。

![image](/images/mongodbv4node02.png)

## 如何使用鉴权？

从数据安全性和可维护等角度，MongoDB实例是强制鉴权的，所有实例均采用keyfile认证，等效于auth=true。MongoDB实例的管理员账号和密码是申请时所填写的管理员用户名和密码。

MongoDB实例统一使用keyfile

    ymSs/7YgMlxlMMTR9K3B6eKyopWD98MX1KIuySyI8Kk1Coqw1sYZp2Nh4nN5yrul+0J21pIpNOzXU3Mbbl2zihF/qMEkofAWJPeORzZd2VR0c2rwHG4xxuxNRFOK3BSTTSIyAgMfnBVTPwC671E18SJi3r/RohfGxy8NveipsZCqTTRDVcGXKqFf4i3vBRLXil+it1oxPb63ayjYJ7Uz1piVQQRtHlD+KzUEaTzhl/CW9Da8xhq1Lm2bxNUWov/ltDfJSyke+a+a1OlbpGTYwD5WeYINbGYYbJMpC1P6ELCQ2kD1c/Dyae7WNLcDO3ICJSOvGigKIGo3om5M8CeiUJ/xHA67RkJak2idSlXOopIEdjjAxtFRPWaF8jEoMgtOSty2OQMBpBYDYcwgRRFL8+fQQvHd1c6sQoXUoN1JbBqhtNxpvlm05keinIP9Al+EeIA1itZjUBcjC5zZgAAPHbXe803TosCupq/jS2W6K8MBEOUg+42u4r8g4Sp2LKdbqqdza1PlBHFQmExSz2pAN61DwZPKjMlBArlCpa5Kk/44DzOc9Lc3bW51AdieG5xFad6d9qS0LLFFeG4tB5HcbUCCKWkVdUM5ocCb0TTRfJ2KNTRaJUTfKq4WLCe1zrIeHCvQIbKVJLgyo/3HHgse331daqVRm+rAAPWwgXVKbo/+XfYkS28ftDMOA6spIN1Vsba+UGdLjGFiq40xLSCA5z0RvB88oYouuyw16VAQuv1JzUk4tzZ9f5Snr1MlyI5rrjO6DZeDT3WYOK9TGRDshWHuVjDCtvDTYPjACy0Jy4Uhikze+pz9gAUbmJNUeU14CZb5EA1/mkICjpbIJigG1lduERa1g5OFv3cS4UIyh8V/zE11rjVdLva0Fq58w713kO6t40xG2QWbpTX/D5VWVH7j0Uq4QX3xSUPvCzIrcGXV0whPRM93BGCgEZVIkdOfDv2+VGDMDmL3mWyJ8/ysjaN1VOnf

## 如何访问MongoDB实例？

申请MongoDB实例后会获取一个IP和Port。

### 命令行操作

登录云主机，在命令行中输入：

    mongo --host $ip --port $port --authenticationDatabase $db --username $admin --password $admin_passwd

例如：

    mongo --host 10.4.12.80 --port 27017 --authenticationDatabase admin --username root --password root

或者：

    mongo $ip:$port/$db -u $admin -p $admin_passwd

例如：

    mongo 10.4.12.80:27017/admin -u root -p root

### API操作

用户可以使用开源的MongoDB API库来连接MongoDB，出于安全性考虑，MongoDB仅能在内网进行访问。

## 如何访问业务MongoDB？

因为在MongoDB安全机制作用下，刚开始用户是无法直连业务db的，否则一直提示无权限，这时需要通过以下步骤：

1、登录到admin库。

2、切换到业务db，如game。

3、使用createUser（2.6版本及更新版本支持）或者 addUser（2.4版本支持）新增用户。

4、使用mongo客户端连接到业务库，如：

    mongo 10.4.12.80:27017/game -u root -p root

MongoDB的2.6版本开始对安全机制做了比较多改进，具体方法可以参见， 注意角色的概念：

<http://docs.mongodb.org/master/reference/method/db.createUser/>

2.4版本见：

<http://docs.mongodb.org/v2.4/reference/method/db.addUser/#db.addUser>

## 如何搭建分片集群？

目前，UCloud支持shardsvr、configsvr和mongos，可以在控制台页面申请。

## 如何访问shardsvr？如何访问configsvr？如何连接集群？

访问shardsvr/configsvr、连接集群的方式与连接mongodb实例的方式一致：

    mongo $mongos-ip:$mongos-port/admin -u $admin -p $admin_password

注意：这里使用的管理员和密码是configsvr统一采用的管理员和密码。如：

    mongo 10.4.4.50:27017/admin -u root -p root

## 如何开启分片？

搭建分片集群和启用分片是前后两个步骤，搭建分片集群是基础，启用分片才真正开始均衡分片的数据分布。步骤包括：

1、启动mongos；

2、使用客户端mongo连接到mongos；

3、使用sh.addShard注册分片，方法参见：

<http://docs.mongodb.org/manual/reference/method/sh.addShard/>

4、使用sh.enableSharding启用某个库的分片功能，方法参见：

<http://docs.mongodb.org/manual/reference/method/sh.enableSharding/>

5、使用sh.shardCollection均衡某个集合的数据分布，注意选择合理的片键，方法 参见：

<http://docs.mongodb.org/manual/reference/method/sh.shardCollection/>

6、使用sh.status查看集合的数据分布，方法参见：

<http://docs.mongodb.org/manual/reference/method/sh.status/>

**如何迁移数据到MongoDB？**

可以通过以下方法迁移数据到MongoDB，包括：

1、使用mongodump和mongorestore工具导出源数据，再导入到副 本集的primary或者分片集群的mongos；

2、如果源db是部署在uhost上，可以在内网通过副本集的复制机制同步数据到UCloud的MongoDB；

**MongoDB的内存是如何管理？**

MongoDB使用mmap管理内存，内存使用率经常是100%，也有时候经过备份
操作（自动备份和手动备份），内存也会立即升到100%，通常情况下无需担心。内存上升后，通常情况下是不会主动释
放的。

如果是平时的工作载荷，内存使用出现瓶颈，建议是在线升级内存。

**MongoDB的磁盘是如何管理？**

MongoDB采用预分配机制分配大文件用于存放数据，drop、remove、
compact等操作是不会释放磁盘空间的，但是可以使预分配的空间重用。如果磁盘使用率过高，这时候需要注意
是否会100%。如果磁盘空间使用率接近100%，建议采用以下方法克服：

1、升级磁盘；

2、创建secondary，通过复制方式将数据从primary同步到
secondary，这时候secondary的存储空间往往会较小一些，然后执行一次主从切换；

3、修复db，执行db.repairDatabase，这会阻塞住整个实例的读写服务，不建议使用；

## 如何管理和查看慢查询？

在业务库执行db.setProfilingLevel()启动和关闭慢查询，方法参见：

<http://docs.mongodb.org/manual/reference/method/db.setProfilingLevel/>

执行db.getProfilingStatus()查看慢查询设置状态。

执行db.system.profile.find() 查看收集到的慢查询，有助于查询优化的工作。

**怎么查到MongoDB的统计信息?**

统计可以在 MongoDB管理页面看到，包括CPU使用率、内存使用、内存使用率、连接数、各类QPS指标等。

**如何使用mongostat监控？**

mongostat是官方提供的一种监控工具，使用方法是:

    mongostat -h $ip --port $port --authenticationDatabase admin -u $admin -p $admin_password --discover

如:

    mongostat -h 10.4.4.50 --port 27017 --authenticationDatabase admin -u root -p root  --discover

**如何查看副本集属性信息与同步状态？**

使用客户端mongo连接到primary节点，执行命令rs.status()查 看副本集属性，其中“set”字段是副本集的id。

执行命令rs.printReplicationInfo() 查看oplog的使用情况。

使用客户端mongo连接到
secondary节点，执行命令rs.printSlaveReplicationInfo()查看与primary节点的同
步状态，可以看到是否落后primary。

## 如何使用API创建Mongos？

如果 uhost自建mongos比较麻烦，也可以通过API调用来创建mongos，具体方法可以参见
CreateUDBRouteInstance。

**如何实现跨机房热迁移MongoDB？**

要求是将
MongoDB从X机房热迁移至Y机房，基本原理是将Y机房的MongoDB实例加入到X机房MongoDB的副本集中，通过复制的方式迁移数据，同步完成后，提升Y机房的MongoDB实例为primary节点。

为保证迁
移过程不会出现单点故障或者无法选举primary等导致不可用，要求X机房的MongoDB副本集是多点的，节点数维持奇数个，在热迁移完成之前，不能停机。确保应用层链接db并非使用固定ip，而是驱动。MongoDB官网可以查看如何连接副本集，利用高可用特性。过
程包括：

在Y机房创建一个primary节点；

在Y机房的primary节点创建若干个从节点或者仲裁节点；

联系我们提供协助，将Y机房的所有db实例加入到X机房的副本集；

观察Y机房db的同步状态；

如果完成后，则可以对副本集重置，提升Y机房的某个节点为新primary节点；

登陆到Y机房的新primary节点重置副本集，逐台remove X机房的db实例；

按需要，完成迁移后，可以在控制台删除X机房的db实例；

## 利用HAproxy外网访问UDB-MONGO

与使用MySQL-Proxy使UDB-MYSQL能够被外网访问一样，可以通过使用HAproxy来使UDB-MONGO被外网进行访问。

具体流程如下：

    安装HAproxy
    
    # yum install -y haproxy
    
    根据如下内容修改配置文件，默认的配置文件路径： /etc/haproxy/haproxy.cfg 
    
        global
           log         127.0.0.1 local2
           chroot      /var/lib/haproxy
           pidfile     /var/run/haproxy.pid
           maxconn     4000    
           user        haproxy
           group       haproxy
           daemon    
           stats socket /var/lib/haproxy/statsdefaults
        defaults
           log                     global   
           option                  dontlognull
           option http-server-close
           option                  redispatch
           retries                 3
           timeout http-request    10s
           timeout queue           1m
           timeout connect         10s 
           timeout client          1m 
           timeout server          1m
           timeout http-keep-alive 10s
           timeout check           10s
           maxconn                 3000
       listen mongod    
           bind uhost-ip:27017
           mode tcp    
           balance roundrobin
           server mongo1 mongodb-ip:27017
       listen mongo-web    
           bind uhost-ip:28017
           mode http
           balance roundrobin
           server mongo1 mongodb-ip:28017
    
     配置中的uhost-ip为云主机的内网IP，mongodb-ip为UDB-MONGO的内网IP。

重启服务

```
# service haproxy restart
# chkconfig haproxy on
```

在防火墙中开启相应端口

在这个配置中，由于外网客户端需要通过27017和28017端口访问haproxy所在的UHost的机器（参考配置中两行bind语句），请编辑这台UHost机器所属的防火墙配置，放开端口27017和28017的访问限制。

通过公网连接MongoDB

```
# mongo uhost-eip:27017/admin -u root -p
```

公网访问MongoDB的WEB控制台地址：<http:%%//%%uhost-eip:28017>

## 在云主机上使用wget下载云数据库的Log时报错，如何解决？

在云主机上下载云数据云数据库的Log备份时需要在url前后加上双引号。

例：下载地址为：<http://udbbackup.ufile.ucloud.cn/udb-3u022a/>

    wget -O ppp.tgz "http://udbbackup.ufile.ucloud.cn/udb-3u022a/"

\-O 设置本地名称

## 如何修改local库的大小？

一旦DB申请成功后，不再支持修改oplogSize的大小，只支持申请DB之前修改。

如果是普通的sharding
server，我们UDB的默认local库大小是5G。如果您需要设置成指定的大小，可以在新建MongoDB时前，先新建一个自定义配置文件，修改oplogSize大小来设置，并使用该自定义配置文件来创建DB。

如果写操作比较频繁，建议根据申请的磁盘容量适当调大oplogSize的大小。

如果是config server，系统会默认生成一个大概几十M的local库，即使申请DB阶段设置local库大小也无效

## 如何查询MongoDB实例的服务器端版本和其他安装信息？

登陆Mongo shell，运行如下指令查看。

    udb-test:PRIMARY> db.serverBuildInfo()
    {
      "version" : "2.4.9",
      "gitVersion" : "52fe0d21959e32a5bdbecdc62057db386e4e029c",
      "sysInfo" : "Linux ip-10-2-29-40 2.6.21.7-2.ec2.v1.2.fc8xen #1 SMP Fri Nov 20 17:48:28 EST 2009 x86_64 BOOST_LIB_VERSION=1_49",
      "loaderFlags" : "-fPIC -pthread -rdynamic",
      "compilerFlags" : "-Wnon-virtual-dtor -Woverloaded-virtual -fPIC -fno-strict-aliasing -ggdb -pthread -Wall -Wsign-compare -Wno-unknown-pragmas -Winvalid-pch -Werror -pipe -fno-builtin-memcmp -O3",
      "allocator" : "tcmalloc",
      "versionArray" : [2, 4, 9, 0],
      "javascriptEngine" : "V8",
      "bits" : 64,
      "debug" : false,
      "maxBsonObjectSize" : 16777216,
      "ok" : 1
    }

## mongoDB-3.2备份文件解压

linux环境：

mongoDB-3.2的备份文件为.tgz格式，解压时执行如下命令：

    gunzip -c xxxxxxxxxx.tgz > xxxxxxx.mongoarchive

手动恢复的命令如下：

``` 
mongorestore -h <host> -u <user> -p <pwd> --archive=xxxxxxx.mongoarchive 
```

Windows环境：

下载的mongoDB-3.2的备份文件的后缀名是.tgz，将后缀名改为mongoarchive.gz，然后再通过解压软件解压缩。

## 如何连接MongoDB云数据库？

### 连接副本集

如果MongoDB采用的是副本集方式，那么连接MongoDB时需要设置一个正确的连接URI，这样后续Primary节点宕机才可以成功的进行漂移，应用层无需变更连接设置，自动具有高可用。各类语言的驱动都支持URI连接。一般副本集连接的URI字符串格式如下，包括账户、密码和副本集各个节点的IP和端口。

    URI: mongodb://user:password@ip1:port1,ip2:port2,…

假如URI的内容如下：

    mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test

那么正确的连接方式是：

    client=MongoClient('mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test')

MongoDB只支持在Primary节点上进行写操作，不过读操作可以有以下几种，客户可以根据自身业务需求选择合适的读取策略。

primary：默认设置，所有的读操作都在Primary节点

primaryPreferred：优先读取Primary节点，Primary不可用的话读取Secondary节点

secondary：所有的读操作都读取Secondary节点

secondaryPreferred：优先读取Secondary，Secondary不可用的情况下读取Primary

nearest：读取网络延迟最低的节点

举个例子，假如需要实现读写分离，即优先读取Secondary节点，连接超时为500ms，那么URI配置如下：

    mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test?connectTimeoutMS=500&readPreference=secondaryPreferred

### 连接分片集群

连接到分片集群的方式和连接到普通MongoDB实例的方式完全相同，不过当存在多个mongos实例的情况下，即使URI里写全了mongos实例的IP也无法自动做到mongos本身的高可用和负载均衡，通常这个可以通过搭建HaProxy或者LVS的方式实现。
假设存在三个mongos节点，分别为IP1，IP2，IP3，而HaProxy的代理IP为IP4，采用简单的roundrobin轮询策略，则连接URI举例如下：

    mongodb://uclouder:edFO09SkdU@IP4:27017/test?connectTimeoutMS=500&readPreference=secondaryPreferred
