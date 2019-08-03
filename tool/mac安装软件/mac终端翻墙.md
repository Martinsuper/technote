# mac终端翻墙

## 在环境变量中设置

```bash
# shadowsocks 中监听端口1086
alias proxy='export all_proxy=socks5://127.0.0.1:1086'
alias unproxy='unset all_proxy'
```

使用的时候使用 `proxy` 翻墙，使用`unproxy` 

