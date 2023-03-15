> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.jianshu.com](https://www.jianshu.com/p/c7d2cffa1998)

用 kodbox 假装是个图形界面， 方便小白管理文件之类的。

具体操作

1. 安装 wget

```
pkg install wget
```

![](http://upload-images.jianshu.io/upload_images/2861088-f6d2e5c16f84bb66.gif)

2. 官网地址下载 kodbox 最新版本，解压，改权限。

```
wget https://static.kodcloud.com/update/download/kodbox.1.26.zip
unzip kodbox.1.26.zip  -d $PREFIX/share/nginx/html/kod2 && cd $PREFIX/share/nginx/html/kod2  && chmod -Rf 777 ./*
```

![](http://upload-images.jianshu.io/upload_images/2861088-95725166ff5355cd.gif)

直接运行上面代码就可以，具体做了下面 4 个操作。

2.1 下载最新版本代码：`wget https://static.kodcloud.com/update/download/kodbox.1.26.zip`

2.2 解压到指定目录：`unzip kodbox.1.26.zip -d $PREFIX/share/nginx/html/kod2`

2.3 进入到指定目录：`cd $PREFIX/share/nginx/html/kod2`

2.4 修改权限：`chmod -Rf 777 ./*`

结束之后直接打开链接：

[http://192.168.0.52:8080/kod2/](https://links.jianshu.com/go?to=http%3A%2F%2F192.168.0.52%3A8080%2Fkod2%2F)

会出现安装页面各种下一步都选默认吧，然后就看到图形的后台了。

![](http://upload-images.jianshu.io/upload_images/2861088-1e4c6000a5ac4545.png)

![](http://upload-images.jianshu.io/upload_images/2861088-524a719b145c95ff.gif)

![](http://upload-images.jianshu.io/upload_images/2861088-d6f1a8cd466adac9)

![](http://upload-images.jianshu.io/upload_images/2861088-624687511b50c5da.gif)

一些常用目录：

nginx 的 html 目录：`/data/data/com.termux/files/usr/share/nginx/html/`

根目录：`/data/data/com.termux/files/home/`

![](http://upload-images.jianshu.io/upload_images/2861088-c32b2f135fcea966)

![](http://upload-images.jianshu.io/upload_images/2861088-458a040922f33d4e.gif)

小白就可以简单方便进行操作文件

------------------------------------------ 分割线 ------------------------------------------

为啥我用了 kod2，

本来是准备安装该公司的另一个产品 kodexplorer 的，因为主要用到它的文件管理功能

安装命令：

```
wget https://static.kodcloud.com/update/download/kodexplorer4.47.zip
unzip kodexplorer4.47.zip -d $PREFIX/share/nginx/html/kod && cd $PREFIX/share/nginx/html/kod && chmod -Rf 777 ./*
```

![](http://upload-images.jianshu.io/upload_images/2861088-f3b5afcc490ef2c5.gif)

运行时候发现出问题

貌似最新的 php 版本太高 8.0 以上出现如下问题，

![](http://upload-images.jianshu.io/upload_images/2861088-a1dfc2ca46947bab.png)

![](http://upload-images.jianshu.io/upload_images/2861088-cbc2aac39e573867.gif)

我的解决方案是 把 php 和 php-fpm 改到 7 版本

```
pkg install php7
pkg install php7-fpm
```

![](http://upload-images.jianshu.io/upload_images/2861088-3467db9cd53177b7.gif)

新人就不要考虑版本问题了，直接用 kodbox 也可以。

kodexplorer 页面

![](http://upload-images.jianshu.io/upload_images/2861088-e8f5156d46077f5b)

![](http://upload-images.jianshu.io/upload_images/2861088-375216b31b5999ef.gif)