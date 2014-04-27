---
layout: post
title:	"Mac OS X使用记录"
date:	2014-04-27
---

##购前选择

## Macbook Air、Macbook Pro？Retina？

## Apple ID注册

## 系统设置

+  OS X的Aero Snap功能

问题1：OS X没有类似Windows 7的Aero Snap功能，就是可以使应用程序拖到屏幕右侧边缘自动占用半屏的功能

解决：在这里为大家几款窗口管理器，如： 

+ Cinch 
+ iSnap 
+ Breeze

问题2：使用VPN时，遇到『IPSec 共享密钥丢失』

解决：在/etc/ppp目录下新建一个文件，名称为「options」，填写下面内容：

> plugin L2TP.ppp
> l2tpnoipsec

问题3：在OS X上建立共享Wifi热点



问题4：Nano编辑器无法设置自动换行

解决：Nano的全局配置文件是/etc/nanorc，OS X默认搭载的与Linux下的参数有所差别，默认是没有开启自动换行的功能，对当前用户来说，可新建一个~/.nanorc文件：

>unset nowrap
>set fill -8

不过上面设置后，还是无法生效。我则使用「brew install 
homebrew/dupes/nano」安装了一个Nano，然后自定义了一个别名，该Nano则可以达到与Linux下的一致的体验了。

问题5：brew update经常遇到无法更新的问题

解决：因为brew 
update是使用Github的服务，遇到Github服务无法正常访问的情况实属正常，我个人是在使用Goagent作为代理服务，我们就可以通过下面设置Git使用Goagent代理：

打开~/.gitconfig文件，在文件末尾添加：

>[http]
>        proxy = http://127.0.0.1:8087

问题6：遇到应用程序窗口僵死的情况，怎么强制退出？

解决：在Linux下我们可以使用xkill，用鼠标点击僵死的窗口即可将其杀死，在OS 
X下，可以通过下面方法来解决：

+ kill -9 PID
+ 「活动监视器」：打开该工具，选中僵死的进程名称，点击左上角的叉号按钮即可

问题7：OS X顶部栏的时间点击无法显示日历

解决：OS 
X本身默认的这个功能实在欠佳，我们可以在「系统设置|日期与时间」中取消勾选「在菜单栏中显示日期和时间」，然后安装Day-O这款软件即可。Day-O支持点击弹出当月日历，并显示在顶部的托盘处。


问题8：Macbook经常在一段时间内硬盘温度急剧升高，并且硬盘轰轰作响

解决：我们使用top命令或者「活动监视器」会发现，一个名叫mdworker的进程占用了大量资源。无法文件索引建立不完整，就会遇到一些情况，如从Finder选择需要上传网络的文件时选择文件窗口会卡死，让你变得极其无奈。所以，关闭或停用文件索引，都不是一个好的办法，还是让其建立完整的文件索引最好。

## 系统快捷键

截图

+ Command+Shift+3：截取全屏
+ Command+Shift+4：截取选定区域
+ Command+Shift+4+空格：截取当前窗口
+ Control+空格：启用Spolight搜索

复制与粘贴

+ Command+C：复制
+ Command+V：粘贴
+ Command+A：全选

窗口操作

+ Command+W：关闭当前应用程序窗口
+ Command+Q：退出当前应用程序
+ Command+M：最小化焦点所在窗口

这里有个概念，需要解释下，在OS X上，关闭当前应用程序窗口，并不是退出该应用程序，只是关闭了该窗口而已，并没有将程序退出。

## 应用程序推荐

+ 百度云同步盘：选用百度更放心，因为其他小厂随时可能中止服务
+ 印象笔记·圈点（Skitch）：简单编辑图片
+ Emacs：文本编辑器，不解释，不过只有在编辑较大文档时才启用，其余时间用Nano
+ Nano：直接默认安装，我一直以来特别推荐的终端文本编辑器，够简便
+ 百度音乐
+ QQ音乐
+ QQ for Mac：不用折腾Wine了，这是最大的感受
+ 爱壁纸HD：壁纸软件
+ Manico：可以给你类似Ubuntu Unity的功能，『Alt+数字/字母』快速切换应用程序




## 体验

+ 
Mac的设计确实有自己的理念在里面，但不是所有的设计都是那样令人满意，不是与人不一样就是高贵上档次了。Macbook不是上档次的象征，不要因为OS 
X的一些不合群甚至不合理的设置，就可以将自己分类了。该改还得改。
