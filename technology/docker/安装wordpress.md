# 安装wordpress



``` bash
docker run --name mywordpress -e WORDPRESS_DB_HOST=mysql.martind.cn -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=dly3230 -e WORDPRESS_DB_NAME=wordpress -p 5000:80 -d wordpress 
```

``` bash
docker run --name wordpress --link mariadb:mysql -p 80:80 -d wordpress
docker run --name mariadb --env MYSQL_ROOT_PASSWORD=dly3230 -d mariadb
```

