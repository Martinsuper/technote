# mino安装

> minio是一个开源的对象存储软件



docker快速安装

```bash
docker run -p 9000:9000 --name minio1 \
  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE" \
  -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" \
  -v $(pwd)/file:/data \
  -v $(pwd)/config:/root/.minio \
  minio/minio server /data
```

