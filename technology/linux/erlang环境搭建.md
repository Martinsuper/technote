# erlang环境搭建

## apt安装

```bash
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
sudo dpkg -i erlang-solutions_1.0_all.deb
```



```bash
sudo apt-get update
sudo apt-get install erlang
```



## deb安装

1. 下载erlang安装包

```bash
wget https://packages.erlang-solutions.com/erlang/debian/pool/esl-erlang_22.0.4-1~ubuntu~xenial_amd64.deb
sudo dpkg -i esl*.deb
```

这个时候可能会报错如下：

```bash
(Reading database ... 30243 files and directories currently installed.)
Preparing to unpack esl-erlang_22.0.4-1~ubuntu~xenial_amd64.deb ...
Unpacking esl-erlang (1:22.0.4-1) over (1:22.0.4-1) ...
dpkg: dependency problems prevent configuration of esl-erlang:
 esl-erlang depends on libwxbase2.8-0 | libwxbase3.0-0 | libwxbase3.0-0v5; however:
  Package libwxbase2.8-0 is not installed.
  Package libwxbase3.0-0 is not installed.
  Package libwxbase3.0-0v5 is not installed.
 esl-erlang depends on libwxgtk2.8-0 | libwxgtk3.0-0 | libwxgtk3.0-0v5; however:
  Package libwxgtk2.8-0 is not installed.
  Package libwxgtk3.0-0 is not installed.
  Package libwxgtk3.0-0v5 is not installed.
 esl-erlang depends on libsctp1; however:
  Package libsctp1 is not installed.

dpkg: error processing package esl-erlang (--install):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 esl-erlang
```

2. 提示缺少依赖，然后执行

```bash
sudo apt-get -f install
sudo dpkg -i esl*.deb

```

3. 然后输入以下内容验证是否安装成功

```bash
erl -version
```

### 