---
layout: post
title:  "fdisk: 磁盘分区命令"
date:   2013-05-11
---

## 简介

fdisk 是 Linux 分区表操作工具。在一般 Linux 系统安装过程中，如 Debian 等系统图形界面安装过程中有很好的图形工具，一般不会用它，但在尝试 Gentoo 过程中，就遇到该工具了。目前，ArchLinux 安装过程也会用到 fdisk 命令进行磁盘分区。当然，在 FreeBSD 中也会用到。涉及到磁盘的重新规划，如果我们对该命令不熟悉，又会经常遇到它，那么磁盘中的数据随时都有可能被误删除，非常危险。所以，我们下面对这一命令进行下学习。

## 常用参数简介

<pre class="prettyprint">
<code>
$ fdisk -l [设备名称]
</code>
</pre>

这里的设备，通常是下列之一：

+ /dev/hd[a-h]
+ /dev/sd[a-p]

/dev/hd[a-h] 指 IDE 硬盘，/dev/sd[a-p] 指 SCSI 硬盘（常见）。

+ 例一
<code>
 $ sudo fdisk -l #该命令会列举出系统内所有可以找出的设备分区
</code>
+ 例二
<code>
 $ sudo fdisk -l /dev/sda #该命令输出指定设备 /dev/sda 上所有的分区
</code>

## 实战：使用 fdisk 创建&删除分区

以 8G U盘作为实验对象，U 盘设备名称是 /dev/sdc。输入下面命令即可进入 fdisk 的交互界面。

<pre class="prettyprint">
<code>
 $ sudo fdisk /dev/sdc
</code>
</pre>

我们会看到相应的输出结果：

<pre>
  [tuhaihe@localhost ~]$ sudo fdisk /dev/sdc
  Welcome to fdisk (util-linux 2.22.2).
  
  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.
  
  Command (m for help): ①
</pre>
  
我们在 ① 处输入 m，可以查看到许多操作参数，和我们最密切的有下面五个：

+  d   delete a partition，删除分区
+  n   add a new partition，新建分区
+  p   print the partition table，输出当前分区表
+  q   quit without saving changes，退出，但不保存对现有分区作出的任何更改
+  w   write table to disk and exit，将对分区表的更改写入磁盘（慎用！）
   
具体创建分区、删除分区步骤，可参考[鸟哥私房菜站点](http://vbird.dic.ksu.edu.tw/linux_basic/0230filesystem_3.php#fdisk)， 多练习几次就可以熟悉了。

*建议*

我们初学该命令，如果一开始就在真机上操作，那么很有可能造成误操作！我们可以建立一个虚拟机，在虚拟机进行测试，这样不会对数据造成毁灭性破坏。这里指出，大家要慎用 w 参数。如果对自己的操作捏不准干脆“q”一走了之。在创建完分区，[格式化分区](http://vbird.dic.ksu.edu.tw/linux_basic/0230filesystem_3.php#format)时，注意交换分区(swap)分区格式化(`mkswap /dev/[设备名]`)后，还需要执行 `swapon` 启用交换分区。

该命令应用实例也可参考 [Gentoo 手册：准备磁盘](http://www.gentoo.org/doc/zh_cn/handbook/handbook-x86.xml?part=1&chap=4)。

## cfdisk：更加直观的分区命令

相比 fdisk，cfdisk 的界面更加直观和容易操作。可在二者之间选择一个更加适合自己的工具。不过，对于超过 2T 大小的硬盘进行分区，fdisk 就无能为力了。fdisk 目前仅支持 MBR，不支持 GPT 分区表，所以对于超过 2T 的硬盘分区可以选择 parted 命令。

parted 命令支持读取包括 MS-DOS 和 GPT 在内的多种分区表格式，关于该命令，可查看更多：`man parted`。

![cfdisk使用截图](http://i.imgur.com/ceSKYRJ.png)
