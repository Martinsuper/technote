# vscode免密登录到服务器



首先将自己的公钥追加到远程服务器上，允许免密登录

```
ssh-copy-id username@ip
```

编辑vscode的`/etc/ssh/ssh_config`下的配置文件

```
Host 自己随便起名
	User root
	HostName 服务器ip地址
	IdentityFile ~/.ssh/id_rsa # 私钥地址
```

