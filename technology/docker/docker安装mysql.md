# `docker` 安装 `mysql`

```
docker pull mysql
```

执行

```console
docker run --name mysql -e MYSQL_ROOT_PASSWORD=dly3230 -p 5306:3306 -d mysql:latest
```

