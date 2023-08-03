---
title: _config.yml 配置问题
date: 2022-11-05
tag:
- Hexo Config
categories:
- Software Install
---

{% note success::blog配置%}


 
<!-- more -->



# blog配置问题

## 1._config.yml配置

```js
deploy:
  type: 部署类型(git)
  branch: 分支名(master)
  repo: 部署路径(git@github.com:name/name.git)

//URL此处配置错误将编译后文件路径会出现问题
//io后面没有/blog会导致搜索出现问题
//If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'

url: "https://yxt66.github.io/blog"
root: /blog/
```

## 2.安装hexo脚手架

```js
npm i hexo-cl
```





