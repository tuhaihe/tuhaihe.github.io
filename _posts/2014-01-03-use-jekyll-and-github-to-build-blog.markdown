---
layout: post
title:  "【更新】我的博客历程与最终选择：Github+Jekyll"
date:   2014-07-09
---

# 经历回顾

如果有人能够帮助你维护博客平台，你只需要自由酣畅地书写，那绝对是一件幸
福的事情。自己来维护博客系统，短时间还可以撑得住，时间一长，便有了倦怠。
这应该就是像博客园、CSDN、51CTO的博客还是一直那么火的原因，它们提供了大
家自由书写的条件，而无需去考虑如何保证博客能够正常运行、服务器是否挂掉
这样的事情。

对我来说，也一直在寻找一个适合自己的内容管理系统，过程也很波折。

起初，对比了[Joomla]、[Drupal]和[WordPress]这三个CMS系统，WordPress安装
简单、插件丰富、主题丰富，比较符合一开始的需求，便使用了有2～3年的时间。
不过，令人苦恼的事情也出现了：数据库越来越大，插件越来越多，还有不断的
升级，致使WordPress越来越臃肿，数据迁移也不方便。所以，就开始了寻找更加
轻型CMS的过程。目前，国内WordPress是比较流行的CMS系统，前二者国内用户较
少。

同时，因为使用WordPress构建了笨兔兔博客，还接受过至今为止唯一一次对我个
人的采访，记得当时我主要表达的意思就是：坚持写，真实记录自己。可是，这
篇采访现在已经很难搜到完整的内容了，不过邮件还在，那也是陈年老账了。现
在看来，真实是必要的，但还是不要那么真实为妙。有时，无需说出口的话，就
不必说，即使让他人误解，也最好用淡淡一笑置之；即使看穿别人的心思，也不
要讲出来，过于直白就打破了朦胧，“人艰不拆”。不过，现在倒是经常有各种生
活的体悟，若是向别人讲出来，就是“心灵鸡汤”之类的吧。话题有些跑远。

接着，尝试自己写HTML，无评论系统、无数据库，使用Github进行版本控制。这
应该解决了数据库和CMS升级的问题。可手写HTML，或借助工具生成HTML文件，毕
竟也不是长久之计：累。而且，页面也相当简陋。我曾一度将“简陋”与“简约”混
为一谈，以为“破”就是“朴素”，其实不然。简约，需要有恰当的功能；简陋，则
缺乏应有的功能。

后来，又使用Emacs的Org-Mode来写作，然后导出HTML、自动索引。后来，专门写
了总结，介绍[如何使用Emacs Org-Mode制作静态网站]。不过，相比Markdown，
Org-Mode的语法相对复杂了些。Org-Mode给我印象最深的就是其大纲模式
（Outline），可以进行段落折叠。现在，如果写作比较长的文章，还是会进入
Emacs的Org-Mode。在Microsoft Word中，常用“大纲模式”有益身心健康。至于编
辑器，平常与代码接触少，自然是使用[Nano]来完成的。哎，可惜一直对Vi/Vim
浅尝辄止，近期也有愿望学习下基本操作，毕竟很多时候是没有Nano或Emacs的。

后来，又在Github上寻得Perl写的一个类似Jekyll的静态站点生成器
[Markablog]。使用Bootstrap搭界面，用脚本来将Markdown格式的文档转换为
HTML，并自动索引，其实它已经与Jekyll的实现思路一样了。顺便给作者推了一
个补丁，把生成索引文章顺序错乱的问题给整好了。

从上面可以看出，大体发展趋势是：

* 以Git作为版本控制系统、使用Github进行内容托管；
* 逐渐偏向使用Markdown编辑内容，然后将其转换为HTML；
* 远离数据库
* 静态

那么，为什么不选择使用Jekyll来在Github提供的Pages服务上来搭建自己的博客
呢？这个方法满足了上述三点要求，而且Jekyll定制性也比较高，选择Jekyll已
经成为必然的选择。下面简单介绍下使用Github+Jekyll搭建个人博客的几个步骤。

## 1. 创建仓库

在Github上，新建一个仓库，命名为‵username.github.io‵。将username替换为
你的Github用户名，如果不使用你的Github用户名，将不会生效。

## 2. 克隆已创建的仓库

	$ git clone https://github.com/username/username.github.io
	$ git checkout master

## 3. “Hello, world!”

	$ cd username.github.io
	$ echo "你好，世界！" > index.html
	$ git add --all
	$ git commit -m '第一次提交'
	$ git push

打开 username.github.io，已经可以看到“你好，世界！”了。我们的第一步已经
顺利完成，下面开始Jekyll的安装。如果你有独立域名，想要将此域名转到该站
点，须在该仓库下新建一个名为 CNAME 的文件，里面填写独立域名，如:

	tuhaihe.com

同时，还要设置DNS，将原域名的 A 记录指向IP地址：204.232.175.78。这样在
访问 tuhaihe.com 的时候，就会转到新建的站点。

## 4. 安装Jekyll

	$ sudo yum install ruby-devel
	$ sudo yum install gem
	$ gem install jekyll


## 5. 生成基本站点

在 tuhaihe.github.io 上一层目录执行下面命令，新生成的基础内容会覆盖我们
刚才里面的“Hello, world!”：

	$ jekyll new tuhaihe.github.io 

然后，运行`jekyll serve`，在浏览器中打开 `0.0.0.0:4000`，即可查看效果。
当然，这只是一个最基本的效果，你如果需要其他更加好看地界面，可以去搜索
一些Jekyll模板，或者自己折腾。

OK，基本过程完成！

# 参考资料

* [Jekyll官网]

* [Github Pages]


[Jekyll官网]: http://jekyllrb.com/
[Github Pages]: http://pages.github.com/
[Joomla]: http://www.joomla.org
[Drupal]: http://drupal.org
[WordPress]: http://cn.wordpress.org
[如何使用Emacs Org-Mode制作静态网站]: http://tuhaihe.com/2013/06/17/use-emacs-orgmode-generate-website.html
[Nano]: http://tuhaihe.com/2013/04/21/gnu-nano.html
[Markablog]: https://github.com/tuhaihe/Markablog

------
# 更新：增加多说评论框【2014-07-09】

一直没有为这个复活的博客增加评论功能，今天终于终于增加了，使用多说评论来实现，参考教程：[《Jekyll+多说，建立属于你的轻博客》][3]

[3]: http://www.ituring.com.cn/article/114888
