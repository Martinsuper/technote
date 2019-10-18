# docker安装

## 1 centos安装docker

### 1.1 安装依赖

```bash
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

### 1.2 添加仓库

```bash
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### 1.3 安装docker

```bash
sudo yum install docker-ce
```

### 1.4 启动docker

```bash
sudo systemctl enable docker.service &&
sudo systemctl start docker.service &&
sudo usermod -aG docker $(whoami)
```



### 1.4 一键安装脚本

```shell
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2 &&
sudo yum-config-manager \
    --add-repo \
   https://download.docker.com/linux/centos/docker-ce.repo &&
sudo yum install docker-ce
sudo systemctl enable docker.service &&
sudo systemctl start docker.service &&
sudo usermod -aG docker $(whoami)
```
docker安装脚本
```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

package docker-ce-3:19.03.3-3.el7.x86_64 requires containerd.io >= 1.2.2-3, but none of the providers can be installed

