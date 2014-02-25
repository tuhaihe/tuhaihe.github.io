---
layout: post
title:  "(解决)在GNOME 3.8使用网络管理器无法创建有效Wi-Fi热点"
date:   2014-02-25
---

*问题描述*

在GNOME 3.8下使用网络管理器无法创建可连接的Wi-Fi热点，也就是，在网络管理器“Wi-Fi”中可以点击“用作热点”按钮来创建Wi-Fi热点，但是在Android手机中搜索不到，无法建立到热点的网络连接。

Debian/Ubuntu下的对应版本都会这一问题。在Fedora 20的GNOME 3.10版本下没有这一问题。

*解决方法*

仍旧按照原先建立Wi-Fi热点的方法创建热点。然后打开网络连接编辑器，点击刚刚建立热点，将其“IPV6”的获取方法设为“忽略”（Ignore）。如下图：

<img src="http://i.imgur.com/a8dJ4fc.png" title="设置IPV6获取方法为“忽略”" align="center">


##参考

* [Askubuntu：Cannot make Wi-Fi hotspot][1]

[1]: http://askubuntu.com/questions/76981/cannot-make-wi-fi-hotspot

