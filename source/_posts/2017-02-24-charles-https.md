---
layout: post
title: 'Charles https'
categories:
- Others
tags:
- Others

---

环境:
>Charles 3.10.1、OS X 10.11.4、IOS 10.2.1


##1.安装证书  
![58b01076ac58f](https://ooo.0o0.ooo/2017/02/24/58b01076ac58f.png)

##2.SSL proxy设置  
![58b0106b330c2](https://ooo.0o0.ooo/2017/02/24/58b0106b330c2.png)  
![58b0106894c82](https://ooo.0o0.ooo/2017/02/24/58b0106894c82.png)

到此为止电脑上浏览器代理设置好后，是能代理https了，但是手机端呢？下面是手机设置

##3.手机端https代理设置
>手机已将Charles设置为了代理

![58b010783e27c](https://ooo.0o0.ooo/2017/02/24/58b010783e27c.png)  
![58b0107b29ab7](https://ooo.0o0.ooo/2017/02/24/58b0107b29ab7.png)

用Safari访问<http://charlesproxy.com/getssl>下载安装证书,如果没有将Charles设置为代理将无法下载安装证书。