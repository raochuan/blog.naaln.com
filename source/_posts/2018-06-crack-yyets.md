---
layout: post
title: 去除人人影视广告
date: 2018-06-05 21:56:13
categories: 
  - 技术
tags: 
---

我平时都是在[人人影视](http://www.zimuzu.tv/)看电影。最近人人影视除了一个客户端，可以看电影，还可以自动下载收藏的电影，感觉还是挺不错的。

但是最近这个客户端开始加入了广告。于是我就想着如何可以去除这些广告。

![](http://pics.naaln.com/blog/2019-01-14-031633.jpg)

首先我用抓包广告抓取改软件发的请求，发现是通过`http://ctrl.zmzapi.net/app/ads`这个地址获取的广告信息。

![](http://pics.naaln.com/blog/2019-01-14-031635.jpg)

能发现 APP 里一共有4种广告。

发现广告的地址之后，去广告就有很多方法了。

*第一种 - 改HOST*

将广告的地址设置为不可用，

在 hosts 中加入 

```
127.0.0.1 ctrl.zmzapi.net
```

*第二种 - 改程序*

找到程序执行的下载广告的地方。

在 `yyets/人人影视.app/Contents/Helpers/RRPlayer` 中

修改里面的函数，将代码设置为不调用即可。

修改后即再也看不到广告了。