---
layout: post
title:  "Tar、zipg2、zip用法简介"
date:   2013-05-13
---

## Tar(tape archiver)

它起初被用来在磁带上创建归档文件。Tar 最基本的功能就是把众多文件集合在一个文件中（生成归档文件），避免文件零散摆放，并不包括压缩功能（降低文件硬盘占有空间）。Tar 只有和其他压缩命令结合在一起，才能发挥压缩文件功能。

常用参数： 

+ -c, --create		建立新归档文件
+ -t, --list 		列出归档中的文件目录
+ -x, -extract		解包/解压缩
+ -j, --bzip2, --bunzip2	用bzip2压缩/解压缩归档 			
+ -z, --gzip, --ungzip 	用gzip压缩/解压缩归档
+ -v, --verbose		详细显示处理的文件
+ -f, --file		指定归档文件
+ -C, --directory DIR	解压到指定目录
+ -Z, --(un)compress

了解了上面常用的参数选项后，基本了解了如何归档/压缩/解压缩日常面临的对应文件了。

## 压缩命令 gzip

使用 gzip 压缩后的文件名后缀常为 .gz；解压缩支持由 gzip、zip、compress 产生的压缩文件格式，所以支持 .gz, -gz, .z, -z, _z, .Z 结尾并具有正确标志头的文件。同时，它也可以识别 .tgz(-> .tar.gz) 和 .taz(-> .tar.Z)

我们总结下，结尾包括下列的压缩文件皆可用 gzip 解压：

+ .gz
+ -gz
+ .z
+ -z
+ _z
+ .Z
+ tar.gz(解为 tar 包, tar 解压缩时结合参数 -z)

## 压缩命令 bzip2

bzip2 支持解压缩的文件格式：
	
+ .bz2
+ .bz
+ .tbz2（tar 解压缩时结合参数 -j）
+ .tbz(同上)

## 使用举例

1. 解开 *.tar

```sh
abc.tar : tar xvf abc.tar
```

2. 解压缩 *.tar.gz / *.tgz

```sh
abc.tar.gz : tar zxvf abc.tar.gz
abc.tgz : tar zxvf abc.tar.gz
```

3. 解压缩 *.tar.bz2 / *.tbz

```sh
abc.tar.bz2 : tar jxvf abc.tar.bz2
abc.tbz : tar jxvf abc.tbz
```

4. 解压缩 *.tar.Z

```sh
abc.tar.Z : tar -Zxvf abc.tar.Z 
```

## zip & rar

tar 和 gzip\bzip2 往往联合使用，后者常针对单个文件进行解压/压缩，但无“打包”功能。zip：pacakge and comrepss(archive) files.

*提示*

使用 tar 解压缩文件时，有时候我们会针对不同的压缩文件格式记忆不同的参数，其实，最新版本的 tar 就不必这样麻烦了。我们只需要执行`tar xvf *.tar.Z/*.tar.gz/*.tgz/*.tbz/*.tar.bz2`这样就可以了！真的相当方便！

## 参考链接

+ [鸟哥的私房菜](http://vbird.dic.ksu.edu.tw/linux_basic/0240tarcompress_3.php)
+ [GNU/Linux Command Line Tools Summary: Archiving Files](http://tldp.org/LDP/GNU-Linux-Tools-Summary/html/backing-up-files.html)
+ [Archlinux Wiki:Tar](https://wiki.archlinux.org/index.php/Tar)
