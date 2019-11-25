# zookeeper 使用

## 创建

```bash
# -s 顺序节点 -e 临时节点，不添加默认是持久节点，acl是指权限控制，缺省不做任何权限控制
create [-s] [-e] path data acl
```

## 读取

```bash
# 列出该路径下所有子节点，只能查看第一级子节点
ls path [watch]
# 获取指定节点的数据内容和属性信息
get path [watch]
```

## 更新

```bash
# 更新路径内容值，version是指哪个版本
set path data [version]
```

## 删除

```bash
# 删除指定节点
delete path [version]
```