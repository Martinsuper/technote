# git hook实现自动发布项目



> 想要每次git push代码后实现项目的自动部署，今天才发现git竟然还有这种功能，下面就是实现



## 添加公钥到服务器

```bash
ssh-copy-id username@ip
```



## 服务器创建裸仓库

```bash
git init --bare registryName.git
cd registryName.git/hooks
vim post-receive
```

在 `post-receive`文件中添加要执行的脚本内容

```bash
#!/bin/bash


```



## 本地仓库操作

在你的笔记本上的项目仓库添加远程仓库（你创建的那个仓库）

```bash
git add remote deploy root@martind.cn:/root/web/vblog
git push deploy
```

