# RabbitMQ 集群搭建
> RabbitMQ集群可以保证出现单点故障的时候可以继续运行，当失去一个 RabbitMQ节点时，客户端能够重新连接到集群中的任何其他节点并继续生产或者消费。
> 不过 RabbitMQ 集群不能保证消息的万无一失 ， 即将消息、队列、交换器等都设置为可持久化，生产端和消费端都正确地使用了确认方式。当集群中一个 RabbitMQ 节点崩溃时，该节 点上的所有队列中的消息也会丢失。 RabbitMQ 集群中 的所有节点都会备份所有的元数据信息， 包括以下内容,不会备份消息
> * 队列元数据 : 队列的名称及属性 ;
> * 令交换器:交换器的名称及属性 :
> * 绑定关系元数据 : 交换器与队列或者交换器与交换器之 间 的绑定关系 ;
> * vhost元数据:为 vhost 内的队列、交换器和绑定提供命名空间及安全属性。  
> 
> 基于内存和性能的考虑，在RabbitMQ集群中创建队列，集群只会在单个节点而不是在所有节点上创建队列的进程并包含完整的队列信息，所有其他非所有者节点只知道队列的元数据和指向该队列存在的那个节点的指针。因此当集群节点崩时，该节点的队列进程和关联的绑定都会消失。附加在那些队列上的消费者也会丢失其所订阅的信息，并且任何匹配该队列绑定信息的新消息也会消失。