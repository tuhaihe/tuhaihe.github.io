---
layout: post
title:	"Mac OS X 不完全使用指南"
date:	2014-04-27
---

##购前

**1. 为什么购买Macbook？**

对我来说，目的很简单，就是为了获得Mac 
OS的体验，不至于仅仅是对Linux和Windows玩得熟练。目前Mac占全球的市场份额达到10%左右，周围的Macbook也是越来越多，而且大家对其较多称赞，这样的情况不能不让人产生好奇心。Macbook到底为什么会吸引人们，它到底有特性呢……这些疑问在多次苹果体验店里的徘徊中仍然得不到真实的答案。

Mac OS界面优雅，主题清爽，应用丰富，兼顾命令行使用习惯……虽有怪异之处，也是可以习惯的来的。在使用一段时间后，觉得购买Macbook是值得的，虽然其价格较普通PC稍贵。


**2. Macbook Air, Macbook Pro？**

Apple官方已经给出了Mac所有机型的对比（[地址][2]），我们当然是要选择[Macbook][3]。

MacBook分为两类：Macbook Air和Macbook Pro。相比Macbook Air，Macbook 
Pro更加适合视频编辑、图像处理等，工作能力更强；Macbook 
Air则在便携性（质量）上更胜一筹。大家可以根据官网给出的机型对比并结合自己的需求来选择。我选择的是13寸带Retina屏幕的Macbook 
Pro，Intel Core i5+4GB内存+128GB SSD，这应该属于低配了，不过可以满足我日常工作的需要。
[2]: http://www.apple.com/cn/mac/compare/
[3]: http://www.apple.com/cn/mac/compare/notebooks.html

**3. Retina屏幕？**

Retina，「视网膜」的意思，可以查看[Apple官网][4]对于Retina显示屏的介绍。相对来说，我个人推荐大家购买带有Retina屏幕的，显示效果相比普通屏幕更加优秀。

[4]: http://www.apple.com/cn/macbook-pro/features-retina/

**4. 二手还是全新？**

之前想在58或淘宝上寻一个二手，可找来找去都不称心，价格也便宜不了多少，主要是对于二手不放心。全新的MacBook，在中国拥有2年主要部件质量维修服务，权衡之后，还是购置了一台全新Macbook。不管是亚马逊还是苹果官网，都支持分期付款，如招行信用卡；如果你是学生，还可享受「教育计划」节省一些钱。在亚马逊购买，有优惠。

## 购后

**1. 周边设备配置**

+ 电脑包：更好地保护MacBook；
+ USB以太网转接器：笔记本过薄，没有常规的以太网插口；
+ Mini Displayport 至 VGA 转接器：还是笔记本过薄！

**2. Apple ID**

在Apple官网[注册Apple ID][5]，iCloud、App Store、iTunes Store都需要Apple 
ID，所以必须注册一个，否则这些服务都无法使用。

[5]: https://appleid.apple.com/cn/

**3. 系统设置**

如下具体介绍。同时，建议大家阅读[Mac在线支持文档][5]，快速了解使用Mac所需的基础知识。
[6]: http://www.apple.com/cn/support/mac/

## 系统设置

**问题1：OS X无Aero Snap功能**

OS X没有类似Windows 7的Aero Snap功能，就是无法在将应用程序拖到屏幕边缘时自动使窗口占用半屏。

解决：在这里为大家几款窗口管理器，如

+ Cinch 
+ iSnap 
+ Breeze

不过，这里还有2个技巧，需要大家注意下：

+ 使用鼠标拖着程序窗口，一直顶着屏幕左右边缘，即可将程序窗口移动到左右两侧的工作区
+ 双指双击Dock程序图标，则可显示所点击程序的所有窗口

**问题2：使用VPN时，遇到「IPSec 共享密钥丢失」问题**

解决：在/etc/ppp目录下新建一个文件，名称为「options」，填写下面内容：

	plugin L2TP.ppp
	l2tpnoipsec

保存后退出，然后在高级设置里面选中「通过VPN连接发送所有流量」即可。

**问题3：在OS X上建立共享Wifi热点**

在GNOME下的「系统设置|网络」可以轻松设置Wifi热点，在OS 
X下，该功能则在「系统偏好设置|共享」中。

**问题4：Nano编辑器无法设置自动换行**

解决：Nano的全局配置文件是/etc/nanorc，OS X默认搭载的与Linux下的参数有所差别，默认是没有开启自动换行的功能，对当前用户来说，可新建一个~/.nanorc文件：

	unset nowrap
	set fill -8

不过上面设置后，还是无法生效。我则使用「brew install homebrew/dupes/nano」安装了一个Nano，然后自定义了一个别名，该Nano则可以达到与Linux下的一致的体验了。

**问题5：brew update经常遇到无法更新的问题**

解决：因为brew update是使用Github的服务，遇到Github服务无法正常访问的情况实属正常，我个人是在使用Goagent作为代理服务，我们就可以通过下面设置Git使用Goagent代理：

打开~/.gitconfig文件，在文件末尾添加：

	[http]
        	proxy = http://127.0.0.1:8087

**问题6：遇到应用程序窗口僵死的情况，怎么强制退出？**

解决：在Linux下我们可以使用xkill，用鼠标点击僵死的窗口即可将其杀死，在OS 
X下，可以通过下面方法来解决：

+ kill -9 PID
+ 「活动监视器」：打开该工具，选中僵死的进程名称，点击左上角的叉号按钮即可
+ Command+Option+ESC：打开「强制退出应用程序窗口」，选择要强制退出的应用程序

**问题7：OS X顶部栏的时间点击无法显示日历**

解决：OS X本身默认的这个功能实在欠佳，我们可以在「系统设置|日期与时间」中取消勾选「在菜单栏中显示日期和时间」，然后安装Day-O这款软件即可。Day-O支持点击弹出当月日历，并显示在顶部的托盘处。


**问题8：Macbook经常在一段时间内硬盘温度急剧升高，并且硬盘轰轰作响**

解决：我们使用top命令或者「活动监视器」会发现，一个名叫mdworker的进程占用了大量资源。据查阅资料可知，mdworker，「metadata server worker」，是一个常驻进程，负责重建索引目录，第一次重建索引时会花费较长时间，以后则是增量索引。但实际情况是，如果文件变动情况较大，感觉还是很明显的。

如果文件索引建立不完整，就会遇到一些情况，如从Finder选择需要上传网络的文件时选择文件窗口会卡死，让你变得极其无奈。所以，关闭或停用文件索引，都不是一个好的办法，还是让其建立完整的文件索引最好。当然，我个人对Mac引以为特色的Spotlight功能不欣赏，索性将其关闭。


这里，大家可以了解下一个管理Spotlight索引的命令行工具[mdutils][1]，可开启/关闭文件索引等功能。

[1]: https://developer.apple.com/library/mac/documentation/Darwin/Reference/Manpages/man1/mdutil.1.html

**问题8：OS X有没有与APT、YUM类似的软件包管理工具？**

解决：答案是肯定的，目前有Fink、Macports和Homebrew三种方式，具体对比可参考文章[ITeye: 比较Fink, MacPorts和Homebrew][7]，总结起来说：

+ Fink更新不及时，软件包过旧；
+ [MacPorts][9]依赖关系多（不依赖系统过多关系），编译时间长；
+ [Homebrew][8]使用Git管理，尽量使用系统已有库，编译时间短，安装简单。

前两者，基本被用户抛弃，越来越多的人Homebrew。如果你通过安装MacPorts.dmg安装包来安装MacPorts时，务必先断开网络，否则会卡在最后一步，亲自验证。

安装Homebrew很简单，只需在终端执行下面命令：

	ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

不过，估计你会和我一样遇到安装问题，连接Git服务超时……建议先参考下问题5的解决方法，或许有效。安装完成后，运行`brew —help`可查看相关选项和参数，很容易上手。

这里，我们还要推荐一个工具，[Homebrew Cask][17]。Homebrew Cask，是对Homebrew的命令扩展，可以帮助我们来安装GUI应用程序，而不用去手动下载DMG格式安装包，或者在Mac Apple Store中等待慢速下载了：

	brew tap phinze/cask
	brew install brew-cask

安装完毕后，我们就可以使用`brew cask`安装软件了，如
	
	brew cask install thunder #安装迅雷
	brew cask install google-chrome #安装Google Chrome浏览器


[7]: http://tetsu.iteye.com/blog/1507524
[8]: http://brew.sh/index_zh-cn.html
[9]: http://www.macports.org/
[17]: https://github.com/phinze/homebrew-cask

**问题8：其他系统设置**

+ 「安全性与隐私|允许从以下位置下载的应用程序」：解锁，选择「任何来源」，然后就可以安装App Store之外的应用程序了；
+ 有的应用程序需要开启辅助功能，如Breeze活Cinch等，它们需要控制窗口，我们需要给它权限，则：「安全性与隐私|隐私|辅助功能」，解锁，将需要赋予权限的应用勾选上即可；
+ 启用Tab键移动键盘焦点：OS X默认没有启用，需在「键盘|快捷键」最下方，选择「所有控制」即可；
+ DNS设置：如果App Store下载很慢，建议尝试下[V2EX DNS][10]。
+ 在Finder文件管理器目录打开终端，可安装应用[Go2Shell][11]
+ 终端：默认Ctrl+D给出了退出提示但没有退出，可点击「终端|偏好设置|Shell」，选择「当Shell退出时|仅当有进程而不是登录Shell和以下项目时」。
+ 「系统偏好设置|键盘|输入源|自动切换到文稿的输入源」，选定该选项，可使中文输入法不会反复切换中英文输入模式


[10]: http://dns.v2ex.com/
[11]: https://itunes.apple.com/us/app/go2shell/id445770608?mt=12

## 系统快捷键

**键盘**

初用Mac，其反人类操作即在此：

+ 「control」：相当于Windows键盘的「Ctrl」
+ 「alt option」：相当于「Alt」
+ 「command」：相当于「Super」

不过部分用法也有特殊，可参考下面整理的快捷键列表。

+ delete：相当于「Backspace」键，向后删除字符
+ Fn+delete：则可以删除前面的字符，变态吧~
+ Fn＋↑：相当于「PageUp」
+ Fn＋↓：相当于「PageDown」
+ Command＋←：跳到行首
+ Command＋→：调到行尾
+ Fn＋←：跳到文档开头
+ Fn＋→：调到文档结尾

**截图**

+ Command+Shift+3：截取全屏
+ Command+Shift+4：截取选定区域
+ Command+Shift+4+空格：截取当前窗口
+ Control+空格：启用Spolight搜索

提示：所有的截屏按键加上Control，则相当于将截图放进粘贴板

**复制与粘贴**

+ Command+C：复制
+ Command+V：粘贴
+ Command+A：全选
+ Command+S：保存
+ Command+Z：撤消刚才的操作
+ Command+O：打开当前文件
+ Command+F：查找

**窗口操作**

+ Command+W：关闭当前应用程序窗口
+ Command+Q：退出当前应用程序
+ Command+M：最小化焦点所在窗口
+ Command+Tab：切换应用程序（从左到右，加上Shift，则从右到左，或者，此刻按下 Command+` 也可以从右向左切换程序）
+ Command+N：新建一个当前应用程序窗口
+ Command+Delete：直接删除选中的文件，是移动到回收站
+ Commmand+Shift+Delete：不一定在回收站中执行，在任何窗口，都会弹出对话框，询问是否彻底情况回收站
+ Command+Shift+Q：退出当前所有程序窗口，并注销
+ Command+T：新建标签页
+ Command+Shift+[ 和 Command+Shift+] 能实现大部分应用程序标签页（Tab）的切换

这里有个概念，需要解释下，在OS X上，关闭当前应用程序窗口，并不是退出该应用程序，只是关闭了该窗口而已，并没有将程序退出。

**Mission Control**

+ Ctrl＋↑：启用Misson Control，显示当前所有打开的程序窗口和工作区
+ Ctrl＋↓：显示当前应用程序的所有窗口
+ Ctrl＋→：切换到右侧工作区
+ Ctrl＋←：切换到左侧工作区
+ F11（需按下Fn键）或Command+F3：隐藏程序窗口，显示桌面
+ F12（需按下Fn键）：显示Dashboard
+ Shift+Command+电源按钮：快速锁定电脑
+ Space+选定文件：快速预览选定文件

**手势操作**

在「系统偏好设置|触控板」里面，好好学习下吧，不再赘述。


## 应用程序推荐


**文档**

+ Emacs：文本编辑器，不解释，不过只有在编辑较大文档时才启用，其余时间用Nano
+ Sublime Text3：好看好用、插件齐全
+ Nano：直接默认安装，我一直以来特别推荐的终端文本编辑器，够简便
+ PDF Reader：阅读PDF
+ Deckset：直接使用Markdown来制作演讲幻灯，可选择多个漂亮主题，可将幻灯导出为PDF
+ Wunderlist：GTD工具
+ Microsoft Office for Mac：除了iWorks套件外，微软也有Office Mac版本，凑合着用
+ Read CHM：CHM文件阅读工具

**互联网**

+ Google Chrome：有了Chrome和Firefox，对Safari直接无爱
+ Firefox
+ Foxmail：邮件客户端，支持导入Outlook邮件文件
+ 百度云同步盘：选用百度更放心，因为其他小厂随时可能中止服务
+ GoagentX：Goagent的GUI版本，可自动更新、添加代理规则、设置全局代理等
+ 印象笔记
+ 知了：知乎日报客户端

**影音图像**

+ 百度音乐
+ QQ音乐
+ 豆瓣FM
+ VLC：万能播放器
+ 快播：也有Mac版本
+ 印象笔记·圈点（Skitch）：简单编辑图片
+ Adobe Photoshop：图片编辑

**通讯工具**

+ QQ for Mac：不用折腾Wine了，这是最大的感受
+ Skype
+ 微信Mac桌面版
+ RTX：企业IM工具
+ WeiboX：微博客户端
+ IRC客户端：LimeChat

**系统工具**

+ 爱壁纸HD：壁纸软件
+ Manico：可以给你类似Ubuntu Unity的功能，『Alt+数字/字母』快速切换应用程序
+ The Unarchiver：解压缩多种压缩格式文件
+ VirtualBox：虚拟机工具
+ Flux：随时间变化屏幕色调，保护眼睛
+ 腾讯电脑管家Mac版本：平常不太用，有时候用来清理下系统垃圾
+ zsh：终极Shell，不可或缺，配上oh-my-zsh，效果就达到了
+ iTerm2：终端模拟器
+ [TotalTerminal][18]：OS X默认搭载终端的一个插件，可实现类似Linux下Guake弹出式终端效果
+ TimeOut：类似Linux下的WorkRave的软件，休息提醒工具　

[18]: http://totalterminal.binaryage.com/

**更新**

+ 2014.04.28：感谢小伙伴 [@Hualet][19] 补充了很多Mac 
Tips，留他微博的原因就是他的粉丝太少了……


[19]: http://weibo.com/u/1957105860
