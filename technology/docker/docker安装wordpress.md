# `docker` 安装 `wordpress`



```
docker pull wordpress

docker run --name some-wordpress --link some-mysql:mysql -d wordpress

docker run --name wordpress -e WORDPRESS_DB_HOST=123.207.87.4:5306 \
    -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=dly3230 -p 80:80 -d wordpress
    


docker run -d  --name wordpress --link mysql -p 80:80 -e WORDPRESS_DB_PASSWORD=root -e MYSQL_DATABASE=mysql wordpress
```

