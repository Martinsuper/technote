# RabbitMQ安装

> RabbitMQ安装有两种方式，一种是docker安装，另外一种是直接安装，不过直接安装要搭建 `erlang`环境，RabbitMQ环境安装可以参考RabbitMQ官网参考安装

## RabbitMQ apt安装

> 注意，首要条件就是要先安装好erlang

首先，添加秘钥文件

```bash
wget -O - "https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey" | sudo apt-key add -
```

然后使用官网推荐的[安装脚本](https://packagecloud.io/rabbitmq/rabbitmq-server/install)

```bash
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.deb.sh | sudo bash
```

安装rabbitmq

```bash
sudo apt-get install rabbitmq-server
```

## RabbitMQ 传统安装

> 首要条件要先安装好erlang

### 安装rabbitMQ

1. 下载rabbitMQ

```bash
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.15/rabbitmq-server_3.7.15-1_all.deb
```

2. 安装deb包

   ```bash
   sudo dpkg -i rabbitmq-server_3.7.15-1_all.deb
   ```

3. 同样提示缺少依赖

   ```bash
   sudo apt-get -f install
   sudo dpkg -i rabbitmq-server_3.7.15-1_all.deb
   ```


## 一键安装脚本

`vim rabbitmq`把下面内容粘贴进去

```bash
#!/bin/bash
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
sudo dpkg -i erlang-solutions_1.0_all.deb
sudo rm -rf erlang-solutions_1.0_all.deb
sudo apt-get update
sudo apt-get install erlang
wget -O - "https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey" | sudo apt-key add -
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.deb.sh | sudo bash
sudo apt-get install rabbitmq-server
```

然后 `chmod +x rabbitmq`给脚本可执行权限

最后  `./rabbitmq`即可

