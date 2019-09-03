# `docker` 安装 `mysql`

```
docker pull mysql
```

执行

```console
docker run --name mysql -e MYSQL_ROOT_PASSWORD=dly3230 -p 3306:3306 -d mysql:latest
```

```bash
docker run --detach --hostname gitlab.xxx.com --publish 444:443 --publish 81:80 --publish 23:22 --name gitlab --restart always --volume /srv/gitlab/config:/etc/gitlab --volume /srv/gitlab/logs:/var/log/gitlab --volume /srv/gitlab/data:/var/opt/gitlab
```