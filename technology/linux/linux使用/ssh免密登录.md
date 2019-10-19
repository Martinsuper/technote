# ssh免密登录



实现本地主机免密登录远程服务器很简单

```bash
ssh-copy-id username@ip
```

这个操作自动会把本地主机的公钥追加到服务器的authorized_keys文件中

