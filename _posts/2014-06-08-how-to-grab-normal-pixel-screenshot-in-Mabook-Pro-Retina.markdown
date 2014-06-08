---
layout: post
title:	"[技巧]在Macbook Retina屏幕下截取常规分辨率截图"
date:	2014-06-08
---

## 问题描述

Macbook Retina屏幕提供了超高分辨率，导致截图相比常规的尺寸过大，在传输截图时不方便。

## 解决方法

OS X提供了一个截图命令：screencapture，可以使用该命令进行截图然后对截图进行缩放，以此得到一个常规大小的截图。网络搜索到一个方法，利用OS X的“Automator”工作流管理工具来完成这一目标。下面是配置步骤，实验成功：

+ 启动 Automator；
+ 在弹出的 Automator 对话框中，选择“服务”这一文稿类型，点击“选取”确定；
+ 点击左侧面板，选择“实用工具 | 运行 Shell 脚本”；在右侧设置面板中，将“服务收到选定的文本”改为“没有输入”，“位于”仍为“任何应用程序”；
+ 设置默认运行 Shell 为 `/bin/bash`，然后将[Shell脚本代码][2]复制到输入框中保存；
+ 点击“运行”进行下测试，可成功运行；
+ 打开“系统偏好设置 | 键盘 | 快捷键”，选择“服务-通用”，就可以看到我们刚才创建的服务，为该服务创建一快捷键。

创建的该服务保存位置是 ~/Library/Services。


## 参考文章

+ [Downscale Screenshot at high resolution on retina macbook pro][1]

[1]: http://blog.lanceli.com/2012/08/downscale-screenshot-at-hight-resolution-on-retina-mackbook-pro.html
[2]: https://gist.github.com/tuhaihe/0bb13ec1b6a2710b360a