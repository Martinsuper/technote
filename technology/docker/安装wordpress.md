# 安装wordpress



```
docker run --name mywordpress -e WORDPRESS_DB_HOST=mysql.martind.cn -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=dly3230 -e WORDPRESS_DB_NAME=wordpress -p 5000:80 -d wordpress 
```

