# zookeeper

## zookeeper 的设计目标

​		Apache ZooKeeper 是一个高可靠的分布式协调中间件。前生是Google Chubby，主要是为了解决分布式一致性问题的组件，同时也是一个粗粒度的分布式锁服务。

### 分布式一致性问题

​		在一个分布式系统中，有多个节点，每个节点都会提出一个请求，但是在所有节点中只能确定一个请求被通过。而这个通过是需要所有节点达成一致的结果，所以所谓的一致性就是在提出的所有请求中能够选出最终一个确定请求，并且这个请求选出来以后，所有节点都需要知道。

​		所以：分布式一致性的本质，就是在分布式系统中，多个节点就某一个提议如何达成一致。

​		zookeeper 通过leader-follower 主从机制来确定主节点，在通过主节点来同步各个子节点的一致性。

### 分布式锁服务

​		从另一个层面，zookeeper 提供了创建节点表示加锁操作。创建成功表示抢占到锁。



## zookeeper 设计猜想

​		基于zookeeper 本身的一个设计目标，zookeeper 主要是解决分布式环境下的服务协调问题而产生的，需要满足一下功能：

### 防止单点故障

​		首先，在分布式架构中，任何的节点都不能以单点的方式存在，常见的解决单点问题的方式就是集群。那这个集群需要满足如下功能：

1. 要有主从节点
2. 要能数据同步，主节点出现问题从节点顶替主节点工作的前提是数据一致
3. 主节点故障后，从节点如何顶替工作



#### leader 角色

leader 服务器是整个服务集群的核心，主要的工作

1. 事务请求的唯一调度和处理者，保证集群事务处理的顺序性
2. 集群内部各服务器的调度者

#### follower 角色

follower  角色的主要职责是

1. 处理客户端非事务请求、转发事务请求给 leader 服务器
2. 参与事务请求的投票（需要半数以上服务器通过才能通知Leader服务器进行commit）
3. 参与leader 选举的投票

#### observer角色

作为优化角色，主要的职责是

1. 同步leader数据
2. 接受非事务请求
3. 不参与事务请求投票、leader选举投票



#### 数据同步

​		leader 节点如何和其他节点保证数据一致性，并且要求是强一致的。在分布式系统中，每一个机器节点虽然都能够明确知道自己进行的事务操作过程是成功和失败，但是却无法直接获取其他分布式节点的操作结果。所以当一个事务操作涉及到跨节点的时候，就需要用到分布式事务，分布式事务的数据一致性协议有 2PC 协议和 3PC 协议





## zookeeper 安装部署

先安装jdk环境

### 单机模式

1. 下载zookeeper 安装包
2. tar -zxvf 解压
3. 切换到`conf`目录下，`cp zoo_simple.cfg zoo.cfg`
4. 常用命令
   - 启动zk服务： `sh zkServer.sh start`
   - 查看zk状态：`sh zkServer.sh status`
   - 停止zk服务：`sh zkServer.sh stop`
   - 重启zk服务：`sh zkServer.sh restart`
   - 连接服务器：`sh zkCli.sh -timeout 0 -r -server ip:port`



### 集群模式

1. 复制一份zoo.cfg，修改配置文件

   ```shell
   server.1=IP1:2888:3888 
   server.2=IP2:2888:3888
   server.3=IP3:2888:3888
   # server.A=B:C:D
   # A:服务器id
   # B:服务器ip
   # C:数据交换端口
   # D:选举端口
   ```

   

2. 安装目录下新建`dataDir`目录，在该目录下新增myid文件，内容对应上述配置服务器id

3. 关闭防火墙，或者防火墙打开对应端口

4. 启动zookeeper































