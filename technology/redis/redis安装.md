# redis安装

## 1 docker安装redis


```bash
docker pull redis &&
mkdir redis &&
touch $PWD/redis.conf&&
docker run -p 6379:6379 -v $PWD/redis/redis.conf:/usr/local/etc/redis/redis.conf --name myredis redis redis-server /usr/local/etc/redis/redis.conf &&
```


## 2 编译安装redis



```bash
wget http://download.redis.io/releases/redis-5.0.5.tar.gz &&
tar -xvf redis-5.0.5.tar.gz && 
rm -rf redis-5.0.5.tar.gz &&
make MALLOC=libc &&
make PREFIX=/usr/local/redis install
cp redis.conf /usr/local/redis # 把redis配置文件直接拷贝到redis安装目录下
```

### 运行

```
./redis-server redis.conf
```
### 伪分布式

伪分布式模式，创建多个文件夹

```bash
mkdir 7001 7002 7003 7004 7005 7006
```

每个文件夹下创建`redis.conf`文件，内容如下：

```
port 7001 # 不同端口注意要修改
cluster-enabled yes 
cluster-config-file nodes_7001.conf # 不同端口注意修改
cluster-node-timeout 5000 
appendonly yes
daemonize yes # 后台模式运行
protected-mode no # 保护模式
# bind 127.0.0.1 要注释掉这个，不然不允许远程访问
pidfile  /var/run/redis_7001.pid # 不同端口注意要修改
```

启动节点

```shell
#!/bin/bash
/usr/local/redis/bin/redis-server /root/redis-cluster/7001/redis.conf
/usr/local/redis/bin/redis-server /root/redis-cluster/7002/redis.conf
/usr/local/redis/bin/redis-server /root/redis-cluster/7003/redis.conf
/usr/local/redis/bin/redis-server /root/redis-cluster/7004/redis.conf
/usr/local/redis/bin/redis-server /root/redis-cluster/7005/redis.conf
/usr/local/redis/bin/redis-server /root/redis-cluster/7006/redis.conf
```

启动集群

```shell
#!/bin/bash
/usr/local/redis/bin/redis-cli --cluster create 10.112.74.239:7001 10.112.74.239:7002 10.112.74.239:7003 10.112.74.239:7004 10.112.74.239:7005 10.112.74.239:7006 --cluster-replicas 1
```

关闭集群

```shell
#!/bin/bash
/usr/local/redis/bin/redis-cli -p 7001 shutdown
/usr/local/redis/bin/redis-cli -p 7002 shutdown
/usr/local/redis/bin/redis-cli -p 7003 shutdown
/usr/local/redis/bin/redis-cli -p 7004 shutdown
/usr/local/redis/bin/redis-cli -p 7005 shutdown
/usr/local/redis/bin/redis-cli -p 7006 shutdown
```

