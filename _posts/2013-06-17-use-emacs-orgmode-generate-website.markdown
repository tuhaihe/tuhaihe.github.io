---
layout: post
title:  "使用 Emacs Org 制作静态网站"
date:   2013-06-17
---

## 关于 Org

  Org 模式可用来做笔记，用作 GTD 工具（记录 TODO 列表）等，它也是一个优秀的编辑、排版系统。这里主要介绍如何使用 Emacs Org Mode 来制作静态网页、组织静态站点。其实，这也就是本站点的生成方法。

 Emacs 已经默认安装 Org，不过，我们也可以通过下面方式来安装最新的 Org(推荐)。

+ [官方站点](http://orgmode.org/)下载 Org 最新版本的归档文件，在配置文件 ~/.emacs 进行配置：

    <pre class="prettyprint">
<code>
;;~/path/to/orgdir 换成 org 文件夹实际路径
(add-to-list 'load-path "~/path/to/orgdir/lisp")
</code>
</pre>

更多安装方法，可参考[官方文档](http://orgmode.org/org.html#Installation)。
 
## 配置 Org

Emacs 22.2 版本以来，支持默认使用 Org 模式打开 .org 文件，如果使用早期的 Emacs 版本，我们需要将下面一句加入到 ~/.emacs 文件：

<pre class="prettycode">
<code>
(add-to-list 'auto-mode-alist '("\\.org\\'" . org-mode))
</code>
</pre>

  同时，也将下面内容添加到 ~/.emacs 中：

  <pre class="prettycode">
<code>
;;使用 Org 的其他功能, 全局按键设置
(global-set-key "\C-cl" 'org-store-link)
(global-set-key "\C-cc" 'org-capture)
(global-set-key "\C-ca" 'org-agenda)
(global-set-key "\C-cb" 'org-iswitchb)

;;设置 Org 文件自动换行
(add-hook 'org-mode-hook
	  (lambda () (setq truncate-lines nil)))
</code>
</pre>

## 站点设置

1. 文件目录结构：做好规划

  我们把 .org 格式源文件与导出的 html 文件分开，方便管理。

  以本博客为例： .org 文件存放在 ~/blog/www/ 文件夹中，导出的 html 文件存放在 ~/blog/public_html/ 文件夹中。同时， ~/blog/www/ 下还有 css 文件夹（本博客[css文件](https://github.com/tuhaihe/blog/tree/master/www/css)，用于存在样式表和脚本。如果你的站点需要图片，则可以新建一个 img 文件夹。

  你可以根据站点的情况来设计自己站点的文件目录结构。

2. 配置 org-publish-project

  将下面内容添加到 ~/.emacs 中：

  <pre class="prettyprint">
<code>
(require 'org-publish)
(setq org-publish-project-alist
;notes组件
  '((
         "org-notes"
         :base-directory "~/blog/www/" ;设置存放.org文件位置 
         :base-extension "org" ;仅处理 .org 格式文件
         :publishing-directory "~/blog/public_html/" ;导出html文件位置
         :recursive t
	 :publishing-function org-publish-org-to-html
         :headline-levels 4 ;Just the default for this project.
	 :auto-preamble t
         :auto-sitemap t                  ;自动生成 sitemap.org
         :sitemap-filename "sitemap.org"  ;默认名称
         :sitemap-title "Sitemap"         
         :export-creator-info nil    ;禁止在 postamble 显示"Created by Org"
         :export-author-info nil     ;禁止在 postamble 显示 "Author: Your Name"
         :auto-postamble nil         
         :table-of-contents nil      ;禁止生成文章目录，如果要生成，将 nil 改为 t
         :section-numbers nil        ;禁止在段落标题前使用数字，如果使用，将 nil 改为 t
         :html-postamble "<p class=\"postamble\">Update time: %d.</p> " ;自定义 postamble 显示字样
         :style-include-default nil  ;禁用默认 css 样式,使用自定义css
        )
;;static 组件
        ("org-static"
         :base-directory "~/blog/www/"
         :base-extension "css\\|js\\|png\\|jpg\\|gif\\|pdf\\|mp3\\|ogg\\|swf"
         :publishing-directory "~/blog/public_html/"
         :recursive t
         :publishing-function org-publish-attachment
         )
;;publish 组件
        ("org" :components ("org-notes" "org-static"))
))
</code>
</pre>

3. 设置：css 样式&其他信息

  我们在第一步已经设置好 CSS 样式文件，它们会控制导出的 HTML 文件外观。除了控制外观之外，还有一些信息也需要我们进行设置。为了方便每次 .org 文件设置，我们在 ~/blog/www/css/ 文件夹下新建一个文件，名为 level-0.orgcss（可自定义），将下面内容复制到该文件中(根据你的个人情况进行修改)：

    <pre>
     #+AUTHOR: tuhaihe
     #+EMAIL: 1132321739qq AT gmail DOT com
     #+LINK_HOME: index.html
     #+LINK_UP: index.html
     #+STYLE: <link href="css/org.css" rel="stylesheet" type="text/css">
     #+STYLE: <link href="css/bootstrap.min.css" rel="stylesheet" media="screen">
     #+STYLE: <link href="css/bootstrap-responsive.min.css" rel="stylesheet">
</pre>

4. 发布

   + 首先，在 ~/blog/www/ 文件夹下新建 index.org 文件，并在其开始添加下面头信息：

   <pre>
       #+SETUPFILE: css/level-0.orgcss
       #+TITLE: 随便写个标题
       
       Hello, world!
   </pre>

   + 导出 HTML 文件
    
   输入 `M-x org-publish-project`，接着输入`org` 回车，OK。Org 已经将 index.org 导出为 index.html 文件了。用浏览器打开该文件，查看下效果吧。趁着热情，新建一个 hello.org ，同样先添加上面的文件头信息，然后洋洋洒洒抒发激动心情吧。此时，可以输入 `M-x org-publish-current-file`，将其导出为 hello.html 文件。
  
## 相关链接

  + [Org Mode 官网](http://orgmode.org)
  + [Publishing Org-mode files to HTML](http://orgmode.org/worg/org-tutorials/org-publish-html-tutorial.html)：比本篇文章更详细的教程 
  + [The compact Org-mode Guide](http://orgmode.org/guide/)：Org-mode 语法文档
  
