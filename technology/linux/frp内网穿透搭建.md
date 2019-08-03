# frp内网穿透搭建



## frps 服务器端配置

```ini
[common]
bind_port = 7000
vhost_http_port = 8000
bind_udp_port = 7001
dashboard_port = 7500
dashboard_user = Martin
dashboard_pwd = dly3230
kcp_bind_port = 7000
subdomain_host = martind.cn
```

### 运行

```shell
./frps -c frps.ini
```

