# docker 安装 redis



```bash
docker pull redis
```



```bash
docker run -p 6379:6379 -v $PWD/redis.conf:/usr/local/etc/redis/redis.conf --name myredis redis redis-server /usr/local/etc/redis/redis.conf
```



```bash
docker exec -it myredis redis-cli
```

redis客户端安装

```bash
sudo snap install redis-desktop-manager
```

