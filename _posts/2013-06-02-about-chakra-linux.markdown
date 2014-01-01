---
layout: post
title:  "Chakra：GTK Free！"
date:   2013-06-02
---

## 关于 Chakra

[Chakra project](http://www.chakra-project.org) 最显著的特点：它是一个“GTK free”（去 GTK 化）、纯 KDE 发行版本，主要运行基于 Qt 的应用程序。

Chakra 安装程序使用图形化安装工具 [Tribe][1]，帮助大家轻松进行初始化配置，并将 Chakra 安装到硬盘上。相比 Arch Linux 文本安装界面来说，对用户更加友好。关于 Chakra 的历史，官方给了相关介绍：

+ Arch Linux 与 KDEmod：2006 年 6 月，KDEmod 项目诞生。随着该项目的流行，2008 年 12 月开发者开发了一款安装器（Tribe）并以 Arch+KDEmod+Tribe 模式发布了第一个 ISO。此时，还只是 Arch Linux 套上了一层 KDEmod 外壳。
+ 随着发布了几个版本，项目主要创始人 Jan Mette（于2010年去世）希望将项目从 Arch 脱离出来建立一个独立的 LiveCD。2010 年 5 月份开发者发布了第一个构建版本。同时，项目组结束了 KDEmod 的开发，转为“Chakra 项目”。由此，Chakra 项目诞生。

Chakra 一词源自梵文，在印度瑜伽体系中指分布于人体各部位的[能量中枢][2]。

## Bundle 系统：让非 Qt 程序顺利运行

既然 Chakra 是一个 GTK free 项目，那么一些关键的 GTK 应用怎么安装呢？于是，就引入了“Bundle 系统”来满足这样的需求。目前 Bundle 管理器已有 30 多款可用的 GTK 应用程序，如 Emacs、Firefox、Skype、GIMP 等。

更多关于 Bundle 系统的信息，可查看 [wiki](http://www.chakra-project.org/wiki/index.php?title=Bundles)。

*更新(2013.5.4)*：Bundle 系统已经被 `[extra]` 软件仓库代替。原先的 Bundle 软件包管理器已经无法使用，Cinstall 里面也看不到可用的 GTK 软件列表。

解决方法：

+ 添加 extra 软件仓库

   <pre class="prettyprint">
<code>
$ sudo nano /etc/pacman.conf #打开配置文件
</code>
</pre>

   在该配置文件中添加下面几行内容：

   <pre>
   [extra]
   Include = /etc/pacman.d/mirrorlist
   
   [testing]
   Include = /etc/pacman.d/mirrorlist
    </pre>

+ 安装 filesystem-extra

   <pre class="prettyprint">
<code>
$ sudo pacman -Sy filesystem-extra
</code>
</pre>    

+ 重启系统。即可从 extra 软件仓库中安装 GTK 应用程序了。
    

### 关于 [extra](http://chakra-project.org/bbs/viewtopic.php?id=10278)

EXTRA 目录是一个全新的文件目录结构，包括一系列的配置文件，允许用户安装并使用 Gtk 程序和软件包。大体文件结构如下：

<pre class="prettyprint">
<code>
/extra
/extra/etc
/extra/bin
/extra/lib
/extra/usr
/extra/opt 
</code>
</pre>

## 基本配置

1. 配置升级源

   我们需要将 Chakra 默认升级源改为中国服务器，在终端打开文件 `/etc/pacman.d/mirrorlist` ，选择位于中国的一个服务器。同时，将文件末尾的美国服务器全部注释掉。

<pre>
	# China
	Server = http://oss.ustc.edu.cn/kdemod/$repo/x86_64
	#Server = http://debian.cn99.com/kdemod/$repo/x86_64
	#Server = http://mirrors.163.com/kdemod/$repo/x86_64
	...
	# United States
	#Server = http://chakra.hostingxtreme.com/$repo/x86_64
	#Server = http://mirror.rit.edu/kdemod/$repo/x86_64
	#Server = ftp://mirror.dacentec.com/chakra/$repo/x86_64
	#Server = http://mirror.dacentec.com/chakra/$repo/x86_64
</pre>

2. 安装中文输入法 fcitx

   <pre class="prettyprint"> 
<code>
$ sudo pacman -S fcitx kcm-fcitx fcitx-rime fcitx-sunpinyin fcitx-googlepinyin
</code>
</pre>

3. 安装 Plasma 部件：显示桌面部件

   <pre class="prettyprint">  
<code>
$ sudo pacman -S kdeplasma-addons-applets-showdesktop
</code>
</pre>

[1]: http://www.chakra-project.org/wiki/index.php?title=Tribe
[2]: http://zh.wikipedia.org/wiki/%E6%9F%A5%E5%85%8B%E6%8B%89

在这种纯种 KDE 的环境中，如果你长期习惯于 GNOME 软件使用，你会感到不舒服。不过，真的有人是很讨厌GNOME的……
