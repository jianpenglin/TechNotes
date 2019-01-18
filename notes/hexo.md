# hexo 教程

## 安装教程

- 安装git
- 安装nodejs
- 寻找一个目录执行
```
npm install -g hexo-cli
hexo init blog
cd blog
npm install
hexo server
```
- localhost:4000访问地址
- 切换主题
在theme目录下执行
```
git　clone https://github.com/iissnan/hexo-theme-next
```
修改`_config.yml`
```
theme: hexo-theme-next
```
- 部署
修改`_config.yml`
```
deploy:
  type: git
  # repository: https://github.com/xxx.com.git
  repository: #远程仓库，需要注册完GITLAB，然后新建一个项目。
  branch: master  #自己的分支名称。
```
执行
```
hexo clean
hexo generate
npm install --save hexo-deployer-git
hexo deploy
```
完成部署
修改_config.yml
```
url:    #GITLAB给我们生成的域名
root: /test    #域名的根目录，其实就是我们的项目名称
```

## 配置教程

### 配置菜单

- 添加关于页面
`themes/<theme_name>/_config.yml`里面的menu一项修改成需要的内容，**注意路径**
```
menu:
  home: / || home
  #about: /about/ || user
  #tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
```
- 添加分类标签
使用 `hexo new page categories`  新建分类页，默认是没有的需要手动创建
文章需要增加所属分类
```
---
title: 分类测试
categories:
- hexo                       （这个就是文章的分类了）
---
```
- 修改`/categories/index.md`文件，增加`type: categories`配置
```
---
title: categories
date: 2019-01-18 19:18:56
type: categories
comments: false
---
```

### 发表文章

- `hexo new "HELLOTEST"`
- 打开HELLOTEST.md文件,输入下面内容
```
---
title: 文章1
date: 2018-03-21 12:01:19
categories: blog
tags: [文章] #文章标签，多于一项时用这种格式，只有一项时使用tags: blog
---
这里是正文，用markdown写，你可以选择写一段显示在首页的简介后，加上
<!--more-->，在<!--more-->之前的内容会显示在首页，之后的内容会被隐藏，需要点击Read more才能看到。
```
- 执行`hexo g`
- 执行`hexo w`

### 优化

- 增加github链接
点击这里或者[这里](http://tholman.com/github-corners/)挑选自己喜欢的样式，并复制代码然后粘贴刚才复制的代码到`themes/next/layout/_layout.swig`文件中
(放在<div class="headband"></div>的下面)，并把href改为你的github地址


### 提交搜索引擎
