# redis集群搭建

## 主从模型
> redis主从模型主要是将redis数据库分为主数据库和从数据库，主数据库可以进行读写操作，当写操作导致数据变化的时候会自动同步给从数据库。而从数据库一般只是读取的，并接受主数据库同步过来的数据。一个主数据库可以拥有多个从数据库，而一个从数据库只能拥有一个主数据库。

主数据库不用任何修改，从数据库`redis.conf`配置文件中添加如下即可
```bash
slaveof 主数据库地址 主数据库端口
```
然后启动从数据库即可
如果要查看Replication节点的相关信息，连接redis服务器后，输入如下
```bash
info replication
```
下面是一个主数据库，2个从数据库

主数据库信息
```bash
# Replication
role:master
connected_slaves:2
slave0:ip=106.13.186.161,port=6379,state=online,offset=16161,lag=1
slave1:ip=117.78.2.106,port=6379,state=online,offset=16161,lag=0
master_replid:0912468f9adec19fc0c2657105245499311bf726
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:16161
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:16161
```
从1信息

```bash
# Replication
role:slave
master_host:martind.cn
master_port:6379
master_link_status:up
master_last_io_seconds_ago:1
master_sync_in_progress:0
slave_repl_offset:16189
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:0912468f9adec19fc0c2657105245499311bf726
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:16189
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:16189
```
从2信息

```bash
# Replication
role:slave
master_host:martind.cn
master_port:6379
master_link_status:up
master_last_io_seconds_ago:0
master_sync_in_progress:0
slave_repl_offset:16231
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:0912468f9adec19fc0c2657105245499311bf726
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:16231
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:16162
repl_backlog_histlen:70
```
这个时候两个从数据库只能读取，并不能写入，只有主数据库可以写入，从数据库写入会报错
`(error) READONLY You can't write against a read only replica.`
如果想要开启写入也很简单，`slave-read-only no`就可以了，但是最好不要这样做，因为对从数据库的任何更改都不会同步给任何其他的数据库，并且一旦主数据库中更新了对应的数据就会覆盖从数据库中的改动。

除了可以通过改配置或命令行参数设置slaveof，还可以在运行时使用slaveof命令修改：
```
redis> SLAVEOF 127.0.0.1 6379
```
如果该数据库已经是其他主数据库的从数据库了，slaveof命令会停止和原来数据库的同步转而和新数据库同步。此外对于从数据库来说，还可以使用`SLAVEOF NO ONE`命令来使当前数据库停止接收其他数据库的同步，并转换成主数据库。
##### 主从模型原理
主从模型复制过程主要包括2个阶段：
复制初始化阶段：当一个从数据库启动后，会向主数据库发送SYNC命令。同时主数据库接收到SYNC命令后会开始在后台保存快照（即RDB持久化的过程），并将保存快照期间接收到的命令缓存起来。当快照完成后，redis会将快照文件和所有缓存的命令发送给从数据库。从数据库接后，会载入快照文件并执行收到的缓存命令。
复制同步阶段：当复制初始化结束后，主数据每当收到写命令的时候就会将命令同步给从数据库，从而保证主从数据库的一致。同步的过程中从数据库不会阻塞，而是可以继续处理客户端发来的命令。默认情况下，从数据库会用同步前的数据对命令进行相应。可以配置 `slave-serve-stale-data no` 来使从数据库在同步完成前对所有命令都回复错误。复制同步阶段会贯穿整个主从同步过程的始终，直到主从关系终止为止
> 可以通过telnet命令连接主数据库，然后通过发送sync命令可以查看同步过程。

::: tip
redis采用了乐观复制的复制策略，容忍在一定时间内主从数据库的内容是不同的，但是两者的数据最终会同步。redis主从数据库之间复制数据的过程是异步的，主数据库执行完客户端请求的命令后悔立即将命令在主数据库执行的结果返回给客户端，并异步地将命令同步给从数据库，而不等待从数据监控接收到该命令后再返回给客户端。这个特性保证了主数据库的性能不会受到影响，但是会产生一个主从数据库数据不一致的时间窗口
:::
##### 从数据库持久化
持久化是一个相对耗时的操作，为了提高性能，可以通过复制功能建立一个从数据库，并在从数据库中启用持久化，同时主数据库禁用持久化。当从数据库崩溃重启后主数据库会自动将数据同步过来，不用担心数据丢失问题。
如果主数据库崩溃了，首先，从数据库使用`SLAVEOF NO ONE`将从数据库提升为主数据，继续提供服务；然后，启动之前崩溃的主数据库，然后使用`SLAVEOF`命令将其设置成新的主数据库的从数据库，即可将数据同步回来。
> 主数据库重启的时候要注意，因为主数据没有开启数据持久化，这个时候数据重启主数据库，会清空主数据库的数据，而从数据库会同步主数据库的数据，这个时候重启会导致从数据库也会被清空，所以不要在从数据库和主数据库解除关系之前重启主数据库。
##### 无硬盘复制

redis主从模型是基于RDB方式的持久化实现的
优点：可以显著简化逻辑，复用已有的代码
缺点：
* 当主数据库禁用RDB快照时，如果执行复制初始化操作，redis会依然生成RDB快照，所以下次启动主数据库会以该快照回复数据，因为复制发生的时间不能确定，使得恢复的数据可能是任何时间点的。
* 复制初始化需要在硬盘中创建RDB快照，如果硬盘性能很慢时这个过程会对性能产生影响。当系统使用一主多从的集群架构的时候，每次和从数据库同步，redis都会执行一次快照，同时对硬盘进行读写，导致性能降低。

##### 增量复制
当从数据库连接断开后，从数据库会发送SYNC命令来重新进行一次完整复制操作，即使数据变化很小也要把数据库中所有数据重新快照并传送一次，这种效率很差，于是redis在2.8之后的版本实现了主从断线重连的情况下的增量复制。

增量复制的条件：
* 从数据库保存的主数据库run id必须和现在主数据库的run id一致。每次实例重启后，就会自动生成一个新的run id
* 在复制同步阶段，主数据库每将一个命令传送给从数据库时，都会同时吧该命令放到一个积压队列中，并记录当前积压队列中存放的命令的偏移量范围；从数据库接受到著数据库传来的命令时，会记录下该命令的偏移量。判断从数据库最后同步成功的命令偏移量是否在积压队列中，如果在则可以执行增量同步，并将积压队列中相应的命令发送给从数据库，如果不满足则会进行一次全量同步。
> 默认情况下积压队列的大小设置为1MB，可以通过设置`repl-backlog-size`选项来调整

## 哨兵
> 哨兵的作用就是监控Redis系统的运行状况。它的功能是：
> * 监控主数据库和从数据库是否正常运行
> * 主数据库出现故障时自动将从数据库转换为主数据库
>
> 哨兵是一个独立的进程，在一主多从的redis系统中，可以使用多个哨兵进行监控任务以保证系统足够稳健；哨兵不仅会同时监控主数据库和从数据库，哨兵之间也会相互监控。

