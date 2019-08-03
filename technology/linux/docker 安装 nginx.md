# docker 安装 nginx



```shell
docker pull nginx
docker run --name test -d nginx
docker cp test:/
```

```
/etc/nginx/nginx.conf
/etc/nginx/conf.d/default.conf
/usr/share/nginx/html
/var/log/nginx
```



```
mkdir -p nginx/conf nginx/conf.d nginx/logs

docker cp test:/etc/nginx/nginx.conf $PWD/conf/nginx.conf
docker cp test:/etc/nginx/conf.d/default.conf $PWD/conf.d/default.conf
docker cp test:/var/log/nginx $PWD/logs
docker cp test:/usr/share/nginx/html $PWD/

docker run -p 8080:80 --name mynginx -v $PWD/html:/usr/share/nginx/html -v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf -v $PWD/logs/nginx:/var/log/nginx -v $PWD/conf.d/default.conf:/etc/nginx/conf.d/default.conf -v $PWD/logs/nginx:/var/log/nginx -d nginx

docker /etc/nginx/nginx.conf

```

