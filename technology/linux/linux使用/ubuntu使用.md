# linux基本概念和基本使用（ubuntu）



查看系统内核版本号

```bash
uname -r
```



## 分层设计的linux体系结构

* linux操作系统采用的是单内核模式的操作系统
* 它包含4层：硬件系统，Linux内核，操作系统服务，用户应用程序
* linux每层只能与它相邻的层通信，层次间具有从上到下的依赖关系，上层依赖下层，但是下层并不依赖上层

## linux版本

> linux版本分为两种：内核版本和发行版本
>
> linux是一个内核，内核是一个提供硬件抽象层、磁盘及文件系统控制、多任务等功能的系统软件；内核并不是一个完整的操作系统。一套基于linux内核的完整操作系统成为linux操作系统。
>
> linux发行版本，对于操作系统来说仅仅有内核是不够的，还需要配备基本的应用软件，而linux发行版本就是包含这些常用的软件，或者成百上千的应用程序可以选择。

## ubuntu更新命令

```bash
# 更新软件列表
sudo apt-get update
# 将本地已经安装软件和软件列表中最新的软件进行对比，如果有更新就更新软件
sudo apt-get upgrade
# 安装软件，如
sudo apt-get install gcc
```



## centos更新命令

```bash
# 升级所有包的同时也升级软件和系统内核
yum update
# 只升级包，不升级软件和系统内核
yum upgrade
# 安装软件，如
yum install gcc
```



## 常用命令

```bash
# 重启
sudo reboot
# 立刻关机
sudo shutdown -h now
# 查看shell环境
echo $SHELL
# 进入目录
cd + 路径
# 列出当前路径下文件内容，无法显示隐藏文件
ls
# 显示所有内容，包括隐藏文件
ls -a 
# 显示文件权限，文件创建者，所有者，创建日期等信息
ll
# 解压文件
tar -xvf *.gz
# 移动文件,path1文件所在位置，path2，文件要移动到的位置
mv path1 path2
# 复制文件,path1文件所在位置，path2，文件要复制到的位置
cp path2 path2
# 创建文件
touche filename
# 创建文件夹
mkdir projectName
# 创建多级目录,例如
mkdir -p /home/martin
# 删除文件或者文件夹
rm -rf filename/project
# 显示当前路径
pwd
# 查看文件内容
cat filename
# 显示更多内容，空格键翻页，回车键滚动一行
more 选项 文件名 
# Pgup,Pgdn前后翻页，上下光标移动一行
less 选项 文件名
# 在屏幕显示文件的开头若干行或若干个字符，-n 行数，-c字数
head 选项 文件名
head -n num 文件名
head -c num 文件名
# 动态显示文件最后内容，如看系统日志文件
tail -f 文件名
# tail 命令和head命令类似
# 将文件以八进制形式转存标准输出
od 选项 文件名
# 文件内容查找,-i表示忽略大小写，-x表示强制整行匹配，-w表示强制关键字完全匹配，-e用于定义正则表达式，-m定义多少次匹配后停止搜索，-n指定输出的同时打印行号，-H为每一匹配项打印文件名，-r在指定目录中进行递归查询
grep 选项 文件名，
grep -i '字符串' 文件

```

### 文件内容比较

```bash
# 显示相同的行
comm 文件1 文件2
# 逐行比较两个文件的不同之处
diff 文件1 文件2
```



### 文件内容

```bash
# 文件内容排序
sort 选项 文件名列表
# 文件字数统计
wc 选项 文件名列表
```



## shell脚本

```bash
# 调用历史命令
history
# !加数字可以执行编号为几的命令
!num

```

* <kbd>Ctrl</kbd> + <kbd>D</kbd> 关闭终端

* 输入多行命令可以使用 `;`分割开，也可以使用 `\` 将命令持续到下一行

* <kbd>Ctrl</kbd> + <kbd>C</kbd> 强制中断当前运行的命令或程序

* 输入重定向 `<` 

  ```bash
  # 统计含有多少行，字数，字符数
  wc < filename
  ```

* 输出重定向 `>` 会覆盖，如果想要追加的话可以使用 `>>`

  ```
  ls > t.lst
  ```

* 管道，一次命令作为另外一次命令的输入 `|`

  ```bash
  ps -ef | grep java
  ```

* 命令替换，与输入重定向类似，命令2的输出作为命令1的参数

  ```bash
  cd `pwd`
  ```

* 给脚本可执行权限

  ```bash
  chmod +x filename
  ```

  

## 切换用户

```bash
# 切换到root用户
sudo -i
sudo su root
# 切换到已存在用户
su 用户名
# 修改用户密码或启用root用户
sudo passwd root

```

