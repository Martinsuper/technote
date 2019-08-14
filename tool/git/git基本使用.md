# git基本概念和使用

## 常用命令

初始化仓库
```bash
git init
```
查看用户名和邮箱
> 这个是提交代码的时候可以看到提交人
```bash
git config user.name
git config user.email
```
设置用户名和邮箱
```bash
git config user.name "username"
git config user.email "email@xx.com"
```
设置全局用户名和邮箱
> 在初始化仓库的时候如果没有设置单独的配置的话会读全局的配置

```bash
git config --global user.name "username"
git confgi --global user.email "email@xx.com"
```
查看本地已经添加的仓库
```bash
git remote -v
```
添加远程仓库
```bash
# git remote add 自己定义仓库名 仓库地址 ，例如
git remote add gitee git@gitee.com:martind/go.git
```
删除远程仓库
```bash
git remote remove 仓库名（如origin）
```

从github上或者gitee上克隆仓库
```bash
git clone git@gitee.com:martind/go.git
```

从github上拉代码
```bash
# origin是本地仓库名，可以是其他的名字，master是分支名，这里是主分支
git pull origin master
```

提交代码
```bash
git push -u origin master
```

## 高级使用

> 如何每次上传代码都免密登录？

首先本地主机要生成一个ssh公钥，然后把这个公钥放到github上或者gitee上
```bash
# 生成公钥，遇到询问直接回车即可
ssh-keygen
# 查看公钥，并复制下来
cat ~/.ssh/id_rsa.pub
```
到gitee个人，设置里面找到ssh公钥设置，把生成的公钥粘贴进去即可
克隆仓库的时候注意要选择ssh路径的，如下图

![2019-08-14 23-46-36 的屏幕截图](http://qn.martind.cn/2019-08-14%2023-46-36%20的屏幕截图.png)