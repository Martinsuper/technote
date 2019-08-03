# hexo安装使用

## 安装hexo

```shell
npm install -g hexo-cli
hexo init
npm install
```

## 安装主题

```shell
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

## 启用next主题

在 `_config.yml`中修改默认主题

```yml
theme: next
```

## hexo使用

### hexo 启动

```
hexo -p 80 server
```



### 添加分类页

```shell
hexo new page categories
```

编辑新生成的`index.md`添加`type`字段

```yaml
---
title: 分类
date: 2019-02-14 13:28:21
type: "categories"
---
```

### 添加标签页

```shell
hexo new page tags
```

编辑新生成的 `index.md` 添加 `type` 字段

```yaml
type: "tags"
```

### 设置阅读全文

在 `_config.yml` 中修改

```yml
auto_excerpt:
  enable: ture
  length: 150
```



## 主题使用

```
npm install hexo-renderer-pug --save
npm install hexo-renderer-sass --save
```

