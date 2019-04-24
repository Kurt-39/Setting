# ElasticSearch配置文件解析

## 常用的配置项如下：

cluster.name:
配置elasticsearch的集群名称，默认是elasticsearch。建议修改成一个有意义的名称。
node.name:

节点名，通常一台物理服务器就是一个节点，es会默认随机指定一个名字，建议指定一个有意义的名称，方便管
理
一个或多个节点组成一个cluster集群，集群是一个逻辑的概念，节点是物理概念，后边章节会详细介绍。
path.conf: 设置配置文件的存储路径，tar或zip包安装默认在es根目录下的config文件夹，rpm安装默认在/etc/
elasticsearch path.data: 设置索引数据的存储路径，默认是es根目录下的data文件夹，可以设置多个存储路径，
用逗号隔开。 path.logs: 设置日志文件的存储路径，默认是es根目录下的logs文件夹 path.plugins: 设置插件的存
放路径，默认是es根目录下的plugins文件夹
bootstrap.memory_lock: true 设置为true可以锁住ES使用的内存，避免内存与swap分区交换数据。
network.host: 设置绑定主机的ip地址，设置为0.0.0.0表示绑定任何ip，允许外网访问，生产环境建议设置为具体
的ip。 http.port: 9200 设置对外服务的http端口，默认为9200。
transport.tcp.port: 9300 集群结点之间通信端口
node.master: 指定该节点是否有资格被选举成为master结点，默认是true，如果原来的master宕机会重新选举新
的master。 node.data: 指定该节点是否存储索引数据，默认为true。
discovery.zen.ping.unicast.hosts: ["host1:port", "host2:port", "..."] 设置集群中master节点的初始列表。
discovery.zen.ping.timeout: 3s 设置ES自动发现节点连接超时的时间，默认为3秒，如果网络延迟高可设置大些。
discovery.zen.minimum_master_nodes:
主结点数量的最少值 ,此值的公式为：(master_eligible_nodes / 2) + 1 ，比如：有3个符合要求的主结点，那么这
里要设置为2。
node.max_local_storage_nodes:
单机允许的最大存储结点数，通常单机启动一个结点建议设置为1，开发环境如果单机启动多个节点可设置大于1.