# linux下部署springboot项目到服务器



> 树莓派终于安装上ubuntu和jdk8了，接下来我想要部署我的springboot项目到服务器

首先maven项目要先`clean`一下然后`install`之后把生成的`target`目录下的项目文件拷贝到服务器，然后运行如下即可：

```bash
java -jar *.jar
```

