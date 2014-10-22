---
layout: post
title: IntelliJ IDEA基本界面配置
date: 2014-10-22 22:17:46 +0800
comments: true
categories: IntellijIDEA, Java, Ubuntu
---

IntelliJ IDEA是一款非常优秀的Java IDE，很多人认为它比Eclipse更优秀。
但是，在Ubuntu下安装后第一次打开，其界面只能用**惨不忍睹**来形容。
因此，我们需要对其字体进行一些基本设置。

<!-- more -->

### 打开字体抗锯齿

编辑`~/.bashrc`，添加如下行：

~~~
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'
~~~

重启IntelliJ IDEA，字体的毛刺就消失了

### 切换主题

IntelliJ IDEA的默认主题其实挺丑的，不过它自带的`Darcula`主题不错

    File->Setting->Appearance->Theme

选择`Darcula`并Apply即可

### 换字体

字体分为`IDE字体`和`编辑器字体`，首先设置`IDE字体`：
   
    在刚才的`Theme`选项下面，勾选`Override default fonts by`，
    然后选择`WenQuanYi Micro Hei`，字体大小看自己喜好

然后设置`编辑器字体`：

    File->Setting->Editor->Colors & Fonts->Font

首先在最上面的`Scheme`处选择`Darcula`（为了和上面主题统一），
然后点右边的`Save As`，起个你喜欢的名字，这时候下面的字体就可以选了：

    去掉`Show Only monospaced fonts`选择，在`Primary font`处选择个你喜欢的,
    然后在`Secondary font`中选择`文泉驿微米黑`

### 其他

还有许多其他设置如`行号`、`空白符`等，看你自己喜好设置吧。。。

当然最漂亮还是Mac OS X下的IntelliJ IDEA，土豪请无视本文，出门右拐Apple商店。
