## shell 脚本语法



### 获取当前目录

```bash
$(pwd)
```

获取正在执行的脚本的路径

```bash
basepath=$(cd `dirname $0`; pwd)
```

