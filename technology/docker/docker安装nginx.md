# docker 安装 nginx

首先安装docker

docker安装nginx

```shell
docker pull nginx
```

```
docker run --name test -d nginx
```

nginx 配置路径

```
/etc/nginx/nginx.conf
/etc/nginx/conf.d/default.conf
/usr/share/nginx/html
/var/log/nginx
```

主机创建文件夹

```shell l
mkdir -p nginx/conf nginx/conf.d nginx/logs
```

从docker拷贝配置文件

```shell
docker cp test:/etc/nginx $PWD/conf/
docker cp test:/var/log/nginx/ $PWD/conf/logs/
docker cp test:/usr/share/nginx/html $PWD/
```

执行docker

```shell l
docker run -p 80:80 --name mynginx -v $PWD/html:/usr/share/nginx/html -v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf -v $PWD/logs/nginx:/var/log/nginx -v $PWD/conf.d/default.conf:/etc/nginx/conf.d/default.conf -v $PWD/logs/nginx:/var/log/nginx -d nginx
```

修改配置文件

```
server {
    listen       80;
    server_name  localhost;
    index index.php index.html index.htm default.php default.htm default.html;
    root   /usr/share/nginx/html/image;
    charset utf-8;
    location / {
	    autoindex on;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```





```
docker pull nginx &&
docker run --name test -d nginx &&
docker cp test:/etc/nginx/ $PWD/conf &&
docker cp test:/var/log/nginx/ $PWD/logs &&
docker cp test:/usr/share/nginx/html $PWD/ &&
docker stop test && docker rm test &&
docker run -p 80:80 --name mynginx -v $PWD/html:/usr/share/nginx/html -v $PWD/conf:/etc/nginx -v $PWD/logs:/var/log/nginx -d nginx
```



## 修改配置 `conf.d/default.conf`

```ini
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html/file;
        index  index.html index.htm;
        # 这个是重点，添加这个即可
        autoindex on;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```

