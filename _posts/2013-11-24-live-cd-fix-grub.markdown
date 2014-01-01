---
layout: post
title:  "使用Live CD修复Grub引导"
date:   2013-11-24
---

本文以 Ubuntu Live CD 修复 Grub 引导为例，已在 /dev/sda3 安装 Fedora。

1. 制作 Ubuntu 启动 USB
	
{% highlight bash %}
sudo dd if=ubuntu-13.10-desktop-amd64.iso of=/dev/sdb #/dev/sdb 为 USB 盘符
{% endhighlight %}

2. 使用启动 USB 进入 Ubuntu 试用环境

3. 查看硬盘分区状况，获取 Linux 系统安装分区编号

    <pre class="prettyprint">
<code>
    sudo fdisk -l
</code>
</pre>

    查看输出结果，然后根据文件类型和分区大小来判定 Linux 系统安装在哪块硬盘和安装的分区。我的电脑是在 /dev/sda3 安装了 Fedora。

    或者，打开 *Gparted* 图形化工具来查看分区信息也可以。

4. 挂载 Fedora 安装分区

    已知 Fedora 安装在了 /dev/sda3 上，所以我们可以用下面命令来挂载 Fedora 安装分区。你需要将 /dev/sda3 换成自己的 Linux 安装分区。

    <pre class="prettyprint">
<code>
    sudo mount /dev/sda3 /mnt
</code>
</pre>  

5. 挂载其他所需的目录（使用 --bind）

    <pre class="prettyprint">
<code>
    sudo mount --bind /dev /mnt/dev
    sudo mount --bind /proc /mnt/proc
    sudo mount --bind /sys /mnt/sys
</code>
</pre>

6. Chroot 到硬盘上的 Linux 系统

    <pre class="prettyprint">
<code>
    sudo chroot /mnt
</code>
</pre>

7. 安装&更新 Grub

    <pre class="prettyprint">
<code>
    grub2-install /dev/sda
    grub2-mkconfig -o /boot/grub2/grub.cfg
</code>
</pre>

8. Grub 已经修复成功，我们还需要退出 chroot 环境、卸载已经挂载的设备与目录：

    <pre class="prettyprint">
<code>
    exit #退出 chroot 环境
    sudo umount /mnt/dev
    sudo umount /mnt/proc
    sudo umount /mnt/sys
    sudo umount /mnt
</code>
</pre>

9. 重启！
