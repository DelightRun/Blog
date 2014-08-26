---
layout: post
title: "Octopress博客常用命令"
date: 2014-05-20 00:10:25 +0800
comments: true
categories: Octopress
---

###新建博文:
    rake new_post["title"]    

###新建页面:
    # 创建/source/directory/index.markdown
    rake new_page[directory]
    
    # 创建/source/directory/page.html
    rake new_page[directory/page.html]

###readmore长度控制
编辑你的博文或页面，在你想要的截断的地方的下一行添加
    <!-- more -->

<!-- more -->
    
###设置为草稿:
编辑你的博文或页面，
在`---`中间的元数据中添加下面一行
    published: false

###改变文章分类:
同样是在`---`中间添加内容，
添加的内容根据如下情况选择
    # 单个分类
    categories: your_category
    
    # 多个分类 - 方法1
    categories: [categories_1, categories_2, categories_3, etc.]

    # 多个分类 - 方法2
    categories:
    - categories_1
    - categories_2
    - categories_3
    - etc.

###生成、预览和部署:
    rake generate   # 生成博文和页面到`public`文件夹
    rake watch      # 查看`source/`和`sass/`的变更并重新生成
    rake preview    # 预览, 在浏览器中访问http://localhost:4000
    rake deploy     # 部署网站，如部署到github
