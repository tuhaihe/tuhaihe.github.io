---
layout: post
title:  "Fedora 18 配置备忘"
date:   2013-06-25
---

Fedora 是 Red Hat 赞助的社区发行版本，倡导“FREEDOME, FRIENDS, FEATURES, FIRST”。其最新版本 Fedora 19 预计将在 2013.07.02 发布。

下面是 Fedora 18 体验过程中我遇到的问题。下面给出了解决方法，以作备忘。
  
## 配置

### 触摸板无法实现“点击”功能

该问题解决方法与文章《Debian Wheezy Xfce 触摸板启用点击》一文中的解决方法一致。
  
### Adode flash 播放器

因 Adobe Flash 插件不是自由和开源软件，所以无法预装在 Fedora 中。

[解决方法][1]

[1]: https://fedoraproject.org/wiki/Flash

1. 64&32 位安装方法

   *X86_64(64 位)*

   <pre class="prettyprint">
<code>
  sudo yum install http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm -y
</code>
</pre>

    *X86(32 位)*

    <pre class="prettyprint">
<code>
  sudo yum install http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm -y
</code>
</pre>

2. 导入 Adobe Flash 插件仓库 GPG 密钥并安装
   <pre class="prettyprint">
<code>
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
sudo yum install flash-plugin -y
</code>
</pre>

### 多媒体编码解码器

1. 下载并安装 Free&Nonfree 仓库

   Free 软件仓库为开源软件仓库，Fedora 项目因为其他原因无法搭载；
Nonfree 仓库主要存放非开源但可重新分发的软件。

    <pre class="prettyprint">     
<code>
sudo 'yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm'
</code>
</pre>

2. 安装多媒体编解码器

   <pre class="prettyprint">
<code>
  sudo yum makecach #创建元数据缓存
  sudo yum install ffmpeg ffmpeg-libs gstreamer-ffmpeg xvidcore libdvdread libdvdnav lsdvd gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-ugly
</code>
</pre>

3. 添加当前用户到管理组

   如果在安装过程中没有将创建的用户添加到管理组，则无法在命令前面使用 sudo。可用下面方法将当前用户添加至管理员组：

    <pre class="prettyprint">
<code>
$ su #切换到 root 用户
echo 'fedora ALL=(ALL) ALL' >> /etc/sudoers #fedora为当前用户名
</code>
</pre>

## YUM 常用选项

  YUM 是基于 RPM 的软件包管理器，可用来更新、升级、安装或卸载软件包。

<pre>
  命令格式： yum [选项] 命令
</pre>

<table>
<tr><td>可用命令</td><td>功能说明</td><td>apt“类似”命令(不完全对应)</td></tr>
<tr><td>remove</td><td>移除软件包</td><td>apt-get remove</td></tr>
<tr><td>install</td><td>安装软件包</td><td>apt-get install</td></tr>
<tr><td>info</td><td>显示关于软件包或组的详细信息</td><td>apt-cache show</td></tr>
<tr><td>makecache</td><td>创建元数据缓存</td><td>apt-get update</td></tr>
<tr><td>reinstall</td><td>重新安装一个包</td><td>apt-get install <pkg> --reinstall</td></tr>
<tr><td>search</td><td>搜索包含指定字符的软件包</td><td>apt-cache search</td></tr>
<tr><td>update</td><td>更新系统</td><td>apt-get upgrade</td></tr>
<tr><td>upgrade</td><td>更新软件包（考虑软件包取代关系）</td><td>apt-get dist-upgrade</td></tr>
</table>
