# git基本概念和使用
::: tip 目标：
* 在github或gitee上创建一个自己的代码仓库（可以创建一个私密仓库）
* 添加ssh秘钥到git平台上，实现免密下载更新代码
* 学会使用git的基本命令，会提交代码到代码仓库，更新本地代码
* 设置git提交的用户名和邮箱信息
* 查看添加删除远程仓库
:::
> git 提交代码，首先是要 `git add` 提交到缓存区，然后`git commit`提交到本地仓库，最后通过`git push` 命令提交到远程仓库
> git 更新代码主要是，`git pull` 下拉代码到本地

## 基本概念
工作区：我们可见的代码
缓存区：`git add` 操作后，自动把代码放到缓存区中，当我们修改代码也是放到缓存区
本地仓库：`git commit` 操作后，自动把代码提交到本地仓库，这个时候还没有提交到远程仓库
远程仓库：`git push` 操作是把本地仓库的代码提交到远程仓库

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
添加代码到缓存
```bash
git add filename
```
提交代码到本地仓库
```bash
git commit -m "提交信息"
```
提交代码
```bash
git push -u origin master
```

## 添加ssh公钥

> 如何每次上传代码都免密登录？

首先本地主机要生成一个ssh公钥，然后把这个公钥放到github上或者gitee上
```bash
# 生成公钥，遇到询问直接回车即可
ssh-keygen
# 查看公钥，并复制下来
cat ~/.ssh/id_rsa.pub
```
到gitee个人，设置里面找到ssh公钥设置，把生成的公钥粘贴进去即可(github也是一样的方法)
如果要实现免密克隆仓库或者提交代码，克隆仓库的时候注意要选择ssh路径的，不然不生效，如下图
![2019-08-14 23-46-36 的屏幕截图](http://qn.martind.cn/2019-08-14%2023-46-36%20的屏幕截图.png)


