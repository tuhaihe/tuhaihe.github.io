---
layout: post
title:  "Xterm 配置小结"
date:   2013-10-16
---

Xterm 是 X 系统标配的终端模拟器，原先对这个丑陋的家伙并没有入眼。用它打开后，显示中文一堆乱码，“不堪入目”。前几天便有好奇心，如何解决它的中文显示乱码问题呢？于是，开始了对 Xterm 的探索之旅。

## 背景：Xresources 文件

Xterm 的配置文件就是 Xresources，一般为 ~/.Xresources。Xresources 支持：

 + 定义终端颜色
 + 配置终端首选项
 + 字体设置
 + Xcursor 游标主题设置
 + xscreensaver 屏保主题
 + 其他 X 应用首选项设置，如 xclok……

在使用 ~/.Xresouces 之前，常用 ~/.Xdefaults 这个文件来做设置，不过现在后者已经基本被废弃，大家更常用 ~/.Xresources。所以，Xterm 的配置也要写在 ~/.Xresources 里面。显示管理器登录系统时，会自动读取该文件，以加载配置。当然，我们还需要熟悉下面的两个命令：

   <pre class="prettyprint">
<code>
xrdb ~/.Xresources #重新加载 .Xresouces 文件，不保留原先配置
xrdb -merge ~/.Xresources #重新加载 .Xresouces 文件，保留原先配置
</code>
</pre>

## Xterm配置

1. UTF-8
     
   让Xterm将输入的数据解释为UTF-8编码：<pre>xterm*locale:true</pre>

2. 修复“Alt”按键
     
   如果你使用“Alt”作为 Meta 键，需要设置：<pre>xterm*metaSendsEscape:true</pre>
     
3. 滚屏
     
   可通过鼠标滚轮，或者触摸板边缘上下滚动，或者使用 Shift+PageUp/PageDown 来滚动。
  
4. 字体
     
   我们一开始面对的就是中文乱码，这个特别恼人，所以要在这里解决：

   <pre class="prettyprint">
<code>
xterm*faceName: DejaVu Sans Mono:style=Book:antialias=false
xterm*faceNameDoublesize: WenQuanYi Micro Hei
xterm*faceSize: 8
</code>
</pre>     

   上面的“DejaVu Sans Mono”和“WenQuanYi Micro Hei”都可以换成自己喜欢的字体，当然，还可以设置它们是否为粗体（Bold），或者斜体（Italic）等。
     
5. 色彩
     
   Xterm 默认是“白底黑字”，我们可以如下简单的设置：

   <pre class="prettyprint">
<code>
xterm*foreground: rgb:b2/b2/b2
xterm*background: rgb:08/08/08
</code>
</pre>     

6. 复制与粘贴
     
   默认情况，Xterm 的选中与粘贴：鼠标高亮选中的文本，就是要复制的文本，在 Xterm 按下“Shift+Insert”或者按鼠标中键就可以直接粘贴。在 X 下，高亮选中的文本被复制到了一个叫做“PRIMARY”的缓冲区，如果继续高亮选中其他文本，则用新高亮选中的文本来代替之前保存的文本。当然，与上面的“PRIMARY”相比，还有一种“CLIPBOARD”：使用“Ctrl+c”或“Ctrl+x”来进行文本复制和剪切，然后“Ctrl+v”进行复制，这就用到了“CLIPBOARD”。

   可以使用下面设置共用这两种方式：

   <pre class="prettyprint">
<code>
XTerm*VT100.translations: #override <Btn1Up>: select-end(PRIMARY, CLIPBOARD, CUT_BUFFER0)
</code>
</pre>
     
   如果我们要启用“Ctrl+v”来复制，可以结合上面设置：

   <pre class="prettyprint">
<code>
xterm*VT100.Translations: #override \
       <Btn1Up>: select-end(CLIPBOARD,PRIMARY,CUT_BUFFER0) \n\
       Ctrl <KeyPress> V: insert-selection(CLIPBOARD,PRIMARY,CUT_BUFFER0)
</code>
</pre>

## 相关链接

  + [Archlinux wiki: Xterm](https://wiki.archlinux.org/index.php/Xterm)
  + [Archlinux wiki：Xresources](https://wiki.archlinux.org/index.php/X_resources)
  + [我的Xterm配置](https://gist.github.com/tuhaihe/6992626)


