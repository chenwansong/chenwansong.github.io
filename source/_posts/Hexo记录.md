---
layout: post
title:  Hexo操作笔记
date:   2017-12-13 00:00:00 +0800
categories: Hexo
tags:
  - Hexo
---

### 一、Hexo相关资料
- [Hexo官网](https://hexo.io/zh-cn/docs/)
- [Next主题](http://theme-next.iissnan.com/)
- [github配置Hexo](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more)


### 二、常用Hexo命令
- 注意：  
```
所有的命令必须在根目录下执行
```

- 本地预览
```
$ hexo s -debug
```

- 生成静态文件
```
$ hexo generate
简写为:
$ hexo g
```

- 生成静态文件之后立即部署
```
$ hexo g -deploy
简写为:
$ hexo g -d
```

- 部署
```
$ hexo deploy
简写为：
$ hexo d
```

- hexo切换本地端口
```
$ hexo server -p 4001
```

- 清除缓存
```
$ hexo clean
```

- 显示Hexo版本
```
$ hexo version
```

### 三、写文档流程

1. 创建 xx.md
2. 生成静态文件 `$ hexo g`
3. 本地预览 `$ hexo s --debug`
4. 部署：`$ hexo d`
5. 重要！推送到Hexo分支，避免更换电脑，找不到原文了！