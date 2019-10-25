# git 远程仓库创建及使用
 
 
## 创建远程仓库

```
mkdir 仓库名.git
cd 仓库名.git
git init --bare
# 如果创建的仓库地址是 /root/git/shell.git 那么仓库地址应为(root用户) root@ip:git/shell.git
```

## 钩子
> 有没有遇到过这种情况，当git上传文件到远程仓库后，每次都要手动部署很是麻烦，其实git提供有一个hook，当你提交代码的时候可以自动触发hook里面的脚本，这样的话就不用手动去部署了。

