---
layout: post
title:  全面的Android文件目录解析和获取方法(包含对6.0系统的说明)
date:   2017-09-10 00:00:00 +0800
categories: Android
tag:   
    - Android文件目录
---

* content
{:toc}

来源：<http://blog.csdn.net/zhangbuzhangbu/article/details/23257873>
一直以来对Android系统目录的获取方法和具体代表含义没有掌握清楚，今天特意整理了一下，分享给大家，对自己也是一个总结。
在android 6.0以前，你可以只关注外置存储是否挂载即可，但是从6.0以后，也就是M系统后，还需要判断是否有读写权限，只有具备这些权限才可以读写外置存储（6.0系统权限机制不在本文讨论范围，大家可以阅读我写的另外一篇博文-android M上可能需要开发者注意的权限大全）。下面就开始一一介绍：

1，Context.getFilesDir
---------------------------
获取路径：/data/user/0/应用包名/files
该目录是应用的文件存储目录，应用被卸载时，该目录一同被系统删除。默认存在，默认具备读写权限(6.0系统可以不用向用户申请)

2,Context.getCacheDir
---------------------------
获取路径：/data/user/0/应用包名/cache
该目录是应用的文件缓存目录，应用被卸载时，该目录一同被系统删除。默认存在，默认具备读写权限。不同于getFileDir，该目录下的文件在系统内存紧张时，会被清空文件，来腾出空间供系统使用，著名的图片加载库ImageLoader就是在没有外置存储读写权限时使用此文件夹。getFileDir，不会因为系统内存不足而被清空。(6.0系统可以不用向用户申请)

3，Context.getObbDir
---------------------------
获取路径：/storage/emulated/0/Android/obb/应用包名 
该目录是应用的数据存放目录，一般被用来存放游戏数据包obb文件。默认存在，可读写(6.0系统可以不用向用户申请)

4，Context.CodeCacheDir
---------------------------
获取路径：/data/user/0/应用包名/code_cache
默认存在，可读写。(6.0系统可以不用向用户申请)

5，Context.getExternalFilesDir
---------------------------
获取路径:(以下载目录为准) /storage/emulated/0/Android/data/应用包名/files/Download
默认存在，可读写。(6.0系统可以不用向用户申请)

6，Context.getExternalCacheDir
------------------------------
获取路径：/storage/emulated/0/Android/data/应用包名/cache
默认存在，可读写。(6.0系统可以不用向用户申请)

7，Context.getDatabasePath
---------------------------
获取路径：/data/user/0/应用包名/databases/参数名
默认不存在，可读写。(6.0系统可以不用向用户申请)

8，Context.getDir
---------------------------
获取路径：/data/user/0/应用包名/app_参数名
默认存在，可读写。分为Private等三个权限，private代表仅能自己访问。(6.0系统可以不用向用户申请)

9，Context.getPackageCodePath
---------------------------
获取路径：/data/app/应用包名-1/base.apk
默认存在，获取apk包路径

10，Context.getRootDirectory
---------------------------
获取路径：/system
默认存在，不可读写（除非具备root权限）

11,Environment.getExternalStorageDirectory
---------------------------
获取路径：/storage/emulated/0
默认存在，声明权限则可读写（6.0和以后系统还需要向用户申请同意才可以）

12，Environment.getExternalStoragePublicDirectory
---------------------------
获取路径：/storage/emulated/0/Download（以下载目录为例）
默认存在，声明权限则可读写（6.0和以后系统还需要向用户申请同意才可以）

13，Environment.getDownloadCacheDirectory
---------------------------
获取路径：/cache
默认存在，声明权限则可读写（6.0和以后系统还需要向用户申请同意才可以）

14,Context.getFileStreamPath
---------------------------
获取路径：/data/data/应用包名/files/download（示例download）
该目录是应用的文件存储目录，应用被卸载时，该目录一同被系统删除。默认存在，默认具备读写权限(6.0系统可以不用向用户申请)

附注：

1）
---------------------------
上述路径是通过getAbsulotePath方法获得，一般情况下等同于getPath

2）
---------------------------
配置targetsdk为19，compilesdk为22，可以避免在6.0手机上的权限限制

