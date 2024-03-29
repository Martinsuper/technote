# RabbitMQ基础

> 消息是指在应用之间传递的数据，消息队列是指利用高效可靠的消息传递机制进行与平台无关的数据交流，并基于数据通信来进行分布式系统的集成。
>
> 一般包括两种模式：点对点模式，发布/订阅模式
>
> 主要负责接收、存储、转发消息



## 消息中间件的作用

> - 解耦
> - 冗余（存储）
> - 扩展性
> - 削峰
> - 可恢复性
> - 顺序保证
> - 缓冲



## 相关概念

- RabbitMQ是一个生产者与消费者模型，主要负责消息的接收、存储、转发。
- 消息一般包括2部分：消息体和标签
- Producer：生产者，投递消息的一方
- Consumer：消费者，接收消息的一方
- Broker：消息中间件的服务节点
- RabbitMQ消息只能存储在队列中
- 多个消费者订阅同一个队列，这时队列中的消息会被平摊（轮询）给多个消费者进行处理，并不是每个消费者都能接收到消息
- RabbitMQ不支持队列层面的广播消费
- Exchange：交换器；生产者将消息发送到Exchange，由交换器将消息路由到一个或者多个队列中，如果路由不到，可能返回给生产者或者直接丢弃。
- RoutingKey：路由键。生产者将消息发送给交换器的时候，一般会指定一个RoutingKey，用来指定这个消息的路由规则，而这个RoutingKey需要与交换器类型和绑定键BindingKey联合使用才能生效
- Binding：绑定。RabbitMQ中通过绑定将交换器与队列关联起来，在绑定的时候一般会指定一个绑定键，这样RabbitMQ就知道如何正确的将消息路由到队列了。

> 交换器相当于投递包裹的邮箱， RoutingKey相当于填写在包裹上的地址， BindingKey相 当于包裹 的 目 的地， 当填写在包裹上 的地址和实际想要投递的地址相匹配时， 那么这个包裹就会被正确投递到 目的地， 最后这个目 的地的"主人"一一队列可以保留这个包裹。如果填写的地址出错，邮递员不能正确投递到目的地， 包裹可能会回退给寄件人，也有可能被丢弃。

### 交换器类型：fanout、direct、topic、headers

- fanout：会把所有发送到该交换器的消息路由到所有与该交换器绑定的队列中
- direct：把消息路由到那些BindingKey和RoutingKey完全匹配的队列中
- topic：会报消息发送到那些BindingKey和RoutingKey匹配的队列中，但是它可以是模糊匹配的，“*”匹配一个单词，”#“匹配多规格单词，多个单词用”.“分开
- headers：不依赖于路由键的匹配规则来路由消息，而是根据发送的消息内容中的headers熟悉进行匹配。在绑定队列和交换器时制定一组键值对，当发送消息到交换器时，RabbitMQ会获取到该消息的headers，对比其中的键值对是否完全匹配队列和交换器绑定时。性能很差， 不常用

> 无论生产还是消费者都需要和RabbitMQ Broker建立连接，这个连接就是一条TCP连接，TCP连接建立起来，客户端紧接着可以创建一个AMQP信道，每个信道都会被指派一个唯一的ID。引用信道的原因是为了TCP复用，因为建立一个TCP的开销很大。 

### AMQP协议
AMQP是一个通信协议，AMQP协议包含三层：

- Module Layer：位于协议最高层，主要定义了一些供客户端调用的命令，客户端可以利用这些命令实现自己的业务逻辑。
- Session Layer：位于中层，负责把客户端的命令发送给服务端，再将服务端的应答返回给客户端，主要为了服务端和客户端之间通信提供可靠性同步机制和错误处理。
- Transport Layer：位于最底层，主要传输二进制数据流，提供帧的处理、信道复用、错误检测和数据表示等。