# zookeeper安装



## 单机模式

将zookeeper目录下的`config/zoo_simple.cfg` 修改为 `config/zoo.cfg`

执行`bin/zkServer.sh`

然后执行telnet命令测试是否启动成功

```bash
telnet 127.0.0.1 2181
srvr #查看zookeeper信息
```



如果执行失败，尝试开启端口试试

```bash
firewall-cmd --add-port=2181/tcp --permanent
firewall-cmd --reload
```

