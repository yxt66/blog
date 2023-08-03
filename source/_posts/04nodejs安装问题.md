---
title: nodejs 安装问题
date: 2022-11-09
tag:
- nodejs
categories:
- Software Install
---

{% note success::nodejs安装%}



<!-- more -->



## 1.下载地址

```js
//下载地址
https://nodejs.org/zh-cn/download/releases/
```

## 2.新建两个文件放node的模块和缓存

```bash
npm config set prefix "D:\nodesjs\node_global"
npm config set cache "D:\nodesjs\node_cache"

npm config list //查看是否配置成功

```

## 3.将下面路径添加到系统环境变量中

```js
D:\nodesjs\node_global//添加到环境变量中
```



![](https://raw.githubusercontent.com/yxt66/img/main/img/image-20221109093705324.png)

## 4.配置淘宝镜像和cnpm

```bash
npm config set registry https://registry.npm.taobao.org/
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 5.vue-admin-template-master

```js
//我nodejs@18运行模板出现nodejs版本不兼容问题，通过降低nodejs版本到@16后，仍然出现core-js问题，通过安装指定core-js@3版本解决。
```



