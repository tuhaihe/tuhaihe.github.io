---
layout: post
title:  "Debian Wheezy(Xfce)启用触摸板点击功能"
date:   2013-05-09
---

## 问题描述

+ 系统：Debian Wheezy Xfce。

+ 具体情况：虽然安装了 Xorg 触摸板输入的驱动(synaptics)，但是“点击”触摸板中间部分，仍然无法启用其相当于鼠标的“单击”功能。

## 解决方法

1. 首先，保证安装了 synaptics 驱动：

   <pre class="prettyprint">
<code>
$ sudo apt-get install xserver-xorg-input-synaptics
</code>
</pre>

2. 复制 /usr/share/X11/xorg.conf.d 到 /etc/X11：

   <pre class="prettyprint">
<code>
$ sudo cp -R /usr/share/X11/xorg.conf.d/ /etc/X11
</code>
</pre>

3. 将原 /etc/X11/xorg.conf.d/50-synaptics.conf 配置文件下面同一部分内容改为：

   <pre class="prettyprint">
     Section "InputClass"
            Identifier "touchpad catchall"
	    Driver "synaptics"
            MatchIsTouchpad "on"
            MatchDevicePath "/dev/input/event*"
	    Option "TapButton1" "1"
	    Option "TapButton2" "2"
	    Option "TapButton3" "3"
	    Option "VertEdgeScroll" "1"
     EndSection
</pre>

    关于上面文件中 `TapButton` 的使用，man 手册里面的解释为：

> Option "TapButton1" "integer"
>    Which mouse button is reported on a non-corner one-finger tap.  Set  to
>    0 to disable. Property: "Synaptics Tap Action"
> 
> Option "TapButton2" "integer"
>    Which  mouse button is reported on a non-corner two-finger tap.  Set to
>    0 to disable. Property: "Synaptics Tap Action"
>
> Option "TapButton3" "integer"
>    Which mouse button is reported on a non-corner three-finger  tap.   Set
>    to 0 to disable. Property: "Synaptics Tap Action"

4. 重启系统

## 关于 synaptics

synaptics 是触摸板的 Xorg 输入驱动。即使触摸板也可以由 evdev 或鼠标驱动处理，但该驱动能够允许触摸板实现更多的功能。synaptics 这个名称属历史沿袭，在 Linux 下，特定硬件有内核处理，但该驱动适用于任何触摸板。如果设备为“PS/2 Mouse”或更古老，内核驱动可能不会支持这样的设备，该驱动也会提供有限支持的功能。不过，适用于任何设备，不管功能多少，都是非常不错了。

*synaptics 部分功能列表* ：

+ 非线性加速触摸运动
+ 通过短暂触摸，实现单击/双击事件
+ 多指触摸：需要硬件支持

关于 synaptics 的更多内容，可以在终端运行 `man synaptics` 进行查看。

### synclient

除了运用上面方法进行设置之外，我们还可以使用命令 *synclient* 进行设置。synclient 就是查询、更改 Synaptics 驱动选项的一个命令行工具。不过该命令的设置只能在当前登录的会话中有效，如果注销或重启系统，则配置失效。可用参数有：

+ -l，列出当前用户设置

我们可以使用下面命令在当前会话实现上述设置：

<pre class="prettyprint">
<code>
$ synclient TapButton1=1
$ synclient TapButton2=2
$ synclient TapButton3=3
</code>
</pre>
