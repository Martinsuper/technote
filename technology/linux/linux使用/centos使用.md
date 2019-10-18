# centos使用

centos最小化安装后没有配置网络，无法上网
``` bash
vi /etc/sysconfig/network-scripts/ifcfg-ens33
# 将ONBOOT=no 修改为 
ONBOOT=yes
```

centos8国内可用镜像源

``` bash
cd /etc/yum.repos.d/
rm -f CentOS-Base.repo CentOS-AppStream.repo CentOS-PowerTools.repo CentOS-centosplus.repo CentOS-Extras.repo
curl -o CentOS-Base.repo https://raw.githubusercontent.com/hackyoMa/docker-centos/8/CentOS-Base.repo
yum makecache
```
centos8安装docker

``` bash
dnf --disablerepo=AppStream install docker-ce
```