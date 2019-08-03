# linux下go安装及环境变量设置

## 1.安装

首先到go官网下载go的安装包，解压，放到指定目录（这里放到了`/usr/local/`下了）

## 2.配置环境变量

`GOROOT`环境变量设置

```bash
export PATH=$PATH:/usr/local/go/bin
```

`GOPATH`环境变量设置（go工作目录）

```bash
export GOPATH=/home/coding/workspace/code/chapter2/sample
export PATH=$PATH:$GOPATH/bin
```

