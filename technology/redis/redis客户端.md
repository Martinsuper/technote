# redis客户端

## 1 安装redis commander

```bash
docker run --rm --name redis-commander -d \
  -p 8081:8081 \
  rediscommander/redis-commander:latest
  
docker run --rm --name redis-commander -d \
  -p 8081:8081 \
  rediscommander/redis-commander:latest
  
  
docker run --rm --name redis-commander -d \
  --env REDIS_HOSTS=local:frp.martind.cn:6379,myredis:frp.martind.cn \
  -p 5001:8081 \
  rediscommander/redis-commander:latest
```



或者 npm 安装 [redis-commander](https://www.npmjs.com/package/redis-commander)

