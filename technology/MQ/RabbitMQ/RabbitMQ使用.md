# RabbitMQ 使用
> rabbitMQ安装好了之后如何使用呢？接下来介绍RabbitMQ的使用

## 常用命令
启动
```bash
rabbitmq-server start
```
管理插件

```bash
# 查看已安装插件列表
rabbitmq-plugins list
# 启用管控台,管理端口是15672
rabbitmq-plugins enable rabbitmq_management
```
网页访问http://ipAddress:15672

这个时候是无法登录的，要设置用户名和密码才能登录

``` bash
# 查看用户列表
rabbitmqctl list_users
# 添加用户
sudo rabbitmqctl add_user duan dly3230
# 给用户设置权限
sudo rabbitmqctl set_user_tags duan administrator
```
设置权限

```bash
rabbitmqctl add_vhost duan
rabbitmqctl set_permissions -p / duan  ".*" ".*" ".*"
```

