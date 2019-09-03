# `docker` 基本使用

## docker 推送镜像到 Docker hub
``` bash
# 登录Docker hub账号
docker login 
# 更改镜像名称为 用户名/镜像名
docker tag 镜像名 用户名/镜像名
# 推送到Docker hub上
docker push 
```