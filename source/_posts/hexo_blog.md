---
title: Hexo搭建github.io
categories: 
  - 配置
tags: 
  - Hexo
date: 2020-02-16 00:00:00
---
Hexo搭建github.io创建blog,分为以下四步:
<!--more-->
1. github创建repo
2. Node.js安装
3. Hexo安装
4. Hexo主题更换

此处省略第一二步，有时间再补

## Hexo 安装
1. npm安装hexo
``` bash
$ npm install -g hexo-cli
```
2. hexo初始化: 命令貌似需要在根目录执行，否则会报错
``` bash
$ hexo init blog
```
3. 进入blog文件
``` bash
$ hexo generate (hexo g)
$ hexo server (hexo s)
```
4. 更新到remote
``` bash
$ hexo deploy (hexo d)
```

## Hexo主题更换
hexo的主题url: https://hexo.io/themes/ (点主题下方的name可以进入对应的git repo)
以下拿next举例:
1. 安装主题
``` bash
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```
2. 修改_config.yml
theme: next

3. 测试部署
``` bash
$ hexo clean
$ hexo g
$ hexo s
$ hexo d
```

## Hexo设置categories/tags

1. 在根目录下scaffolds/post.md中，添加一行 categories:
2. new page
``` bash
$ hexo new page categories
$ hexo new page tags
```
3. 在categories/index.md最后加
```
type: "categories"
layout: "categories"
```
tags同理
4. 编写md文章的时候，在开头加上categories: 的标签
```
title: Hexo搭建github.io
categories: 
  - 配置
tags: 
  - Hexo
date: 2020-02-16 00:00:00
```
## Hexo插入图片
1. 安装插件
```bash
$ npm install hexo-asset-image --save
```
2. hexo的配置文件 _config.yml
post_asset_folder: true

3. 自动生成文章同名文件夹用于存放照片
```bash
$ hexo new <file-name>
```
4. 