# linux常用



编译安装

```bash
# 指定安装路径
./configure -prefix=/usr/local/git
make && make install
```



ssh 免密登录

```bash
ssh-keygen -t rsa -C "mrtduan@gmail.com"
ssh root@ip "echo \"`cat ~/.ssh/id_rsa.pub`\" >> .ssh/authorized_keys"
```

