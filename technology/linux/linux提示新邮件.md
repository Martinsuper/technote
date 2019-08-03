# linux 提示 you have new mail

解决办法：

```bash
sudo rm -rf /var/mail/*
echo "unset MAILCHECK">> /etc/profile
source /etc/profile
```

