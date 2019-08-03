# centos 安装kafka

## 首要条件

安装 `jdk`，`zookeeper`

## 安装kafka

首先到官网下载kafka，然后解压



## 修改 `config/server.properties`

```bash
# 允许远程连接服务器
listeners = PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://frp.martind.cn:9092
```

## 启动kafka

```bash
./kafka-server-start.sh ../config/server.properties
# 后台运行
./kafka-server-start.sh -daemon ../config/server.properties
```

## 添加，查看，删除topic

```bash
# 添加
bin/kafka-topics.sh --create --zookeeper martind.cn:2181 --replication-factor 1 --partitions 1 --topic test

# 查看
bin/kafka-topics.sh --list --zookeeper martind.cn:2181

# 删除
bin/kafka-topics.sh --zookeeper zk1:9092 --delete --topic test
```



## 测试生产者和消费者

```bash
# 生产者
bin/kafka-console-producer.sh --broker-list martind.cn:9092 --topic test
# 消费者
./kafka-console-consumer.sh --bootstrap-server martind.cn:9092 --topic test --from-beginning
```

