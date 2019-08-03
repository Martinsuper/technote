# v2ray 使用

## 1 centos使用

```shell
wget http://martind.cn:8080/software/v2ray/v2ray-linux-64.zip &&
yum install zip unzip &&
unzip v2ray-linux-64.zip -d v2ray
wget -P $(pwd)/v2ray http://martind.cn:8080/software/v2ray/configss.json &&
```

```bash
sudo nohup $(pwd)/v2ray/v2ray -config=$(pwd)/v2ray/configss.json >/dev/null 2>&1 &
```



```
alias proxy='export all_proxy=socks5://127.0.0.1:2333'
alias unproxy='unset all_proxy'
```

