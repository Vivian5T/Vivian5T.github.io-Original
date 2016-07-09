---
layout: photo
title: 『RIME』调效笔记
date: 2016-06-09 01:50:25
tags: 输入法, APP, 配置
---
![](http://o88okth1x.bkt.clouddn.com/imac_16ac871cb98e2dd5d8aecbbe863a4e8a.png)

# 『RIME』调效笔记
-转自**简书作者：scomper** [原文地址](http://www.jianshu.com/p/ef2d9442fb0c)

最开始只是想调整一下鼠须管的界面风格，让它变得小清新一点，结果周末的时间就都掉到鼠须管配置的这个「坑」里，改完了界面接着想解决候选词乱码的问题，然后是`模糊拼音`、`扩充词库`、`表情输入`、`符号输入`、`特殊符号直接上屏`等需求接踵而来。
[鼠须管官网](http://rime.im/)的介绍其实已经很全面了，还提供了很多[参照代码](https://gist.github.com/lotem)。但是设置的过程毕竟不是友好的图形界面，需要打开「用户设定」目录下的具体文件修改代码部分，所以过程并不顺畅，即便是简单的复制和粘贴，也要考虑语法缩进的问题。在没有更好的图形化配置界面出来以前，注定鼠须管是一个有一定学习成本的输入法，而要让它更好用只能学习并调教它。

<!-- more -->

![image-2](http://o88okth1x.bkt.clouddn.com/imac_370c65060cf7dec0c19b1aa06c42b7d3.png-960.jpg)

基本的调教并没有想象中的那么复杂，看完官网的帮助后就可以动手试试。由鼠须管的图标中选择「用户设定」（`~/Library/Rime/`）定位到具体文件，修改完成再执行一次「重新部署」就能看到修改后的效果。

![](http://o88okth1x.bkt.clouddn.com/imac_cc6a68a208fd09c217eefbd81f107623.png-960.jpg)

>方案特点：支持 `/dn` 方式的符号输出；常见拼写的容错处理；输入字母 v 开头的短语输出颜文字；词义关联模式的表情符号；#、\`、符号直接上屏；单引号输出「」；- +以及\< > 键翻页；上下箭头选择其他候选； 包含常用汉语、诗词和英文的词典。

**如果你平时用的就是「明月拼音·简化字」，可以跳过后续具体配置的介绍直接到文章最后下载附件，解压缩并将其中的文件放到「用户设定」目录「重新部署」即可。**

## 配置文件和基本思路
鼠须管的「用户设定」文件夹里包含很多文件，根据自己的输入要求定制的时候实际上涉及的文件只有固定的几个，一些是调整输入法外观和参数的，还有一大部份是扩展词库的文件。

![](http://o88okth1x.bkt.clouddn.com/imac_0f3adefd5a07791fc6a6cc57dc1013d4.png-960.jpg)

配置输入法的的外观和特性的几个文件：

- squirrel.custom.yaml ，自定义皮肤；
- default.custom.yaml ，设定备选词数量，定义输入方案；
- luna __\_pinyin__ simp.custom.yaml ，定义扩充词库、加载符号库、模糊拼音。明月拼音·简化字的输入方案配置文件，明月拼音对应的文件就是 luna__\__pinyin___.custom.yaml；
- installation.yaml，定义配置文件保存到 Dropbox 文件夹

以上几个以 .custom.yaml 作为后缀的文件，意味着是以补丁的方式来实现个性化定制的，输入法后续升级不会覆盖这些文件。所以自定义的文件配置中起始部分都会有patch:的字段，每个配置文件中有且只需要一行这个代码段。
扩展词库涉及到的几个配置文件，参照扩展词库的内容，你可以自己定义类似的词库：

- luna\_pinyin.extended.dict.yaml，扩展词库主文件，其他词库都需要在这个主文件中定义才能被调用，如果不想加载某个词库在此文件中注释掉即可（在所在行前加 # 井号）
- luna\_pinyin.cn\_en.dict.yaml，英文、中英文混合短语和名词
- luna\_pinyin.computer.dict.yaml，计算机术语
- luna\_pinyin.emoji.dict.yaml，表情符号
- luna\_pinyin.hanyu.dict.yaml，汉语大词典
- luna\_pinyin.kaomoji.dict.yaml，颜文字表情符号
- luna\_pinyin.movie.dict.yaml，电影名称
- luna\_pinyin.music.dict.yaml，音乐和歌曲名
- luna\_pinyin.name.dict.yaml，人名
- luna\_pinyin.poetry.dict.yaml，唐诗宋词、千家集、楚辞、诗经

词库文件是相对单独的，鼠须管中挂载词库的方式比以前更灵活，而且编辑起来也很方便，在`luna\_pinyin.extended.dict.yaml `这个词库主文件中定义和关联其他词库，而扩展词库的加载则是由 `luna\_pinyin\_simp.custom.yaml `这个文件来决定。

> 扩展词库文件被修改后需要「重新部署」才能生效。

鼠须管的配置中，重要的是主要外观和特性文件的设置，第一步是修改`default.custom.yaml` 确定你的输入方案，也就是按「control+\` 」时出现的可供选择的明月拼音、明月拼音·简化字、五笔等；第二步是修改输入法的外观 `squirrel.custom.yaml`；第三步就是修改你的输入方案的配置文件，例如：明月拼音·简化字，那么只需要修改` luna\_pinyin\_simp.custom.yaml `，输入方案的配置文件像是一个接口文件，模糊拼音、加载扩充词库、定义一些特殊符号的直接上屏、定义个性化的翻页按键等都在这个文件里。
安装完鼠须管后，用户文件夹里可能看不到上述提到的这些文件，简单的办法就是复制一个同样后缀的文件然后对照修改。下载的词库或配置文件中也可能直接包含这样的文件，如果从不同来源下载的文件中包含同样命名的文件，最好对照一下内容，不要盲目覆盖导致配置丢失。

## luna\_pinyin.extended.dict.yaml
词库部署的过程就是下载[扩充词库](https://github.com/rime-aca/dictionaries)（登录页面后点击右下角的「Download ZIP」），下载完成后解压缩并将 `luna\_pinyin.dict` 中的文件复制到你的「用户设定」目录。假如你和我一样是使用「明月拼音·简化字」，就不用复制文件夹中的`double\_pinyin.custom.yaml`这个文件。复制完成后重命名`luna\_pinyin.custom.yaml`为`luna\_pinyin\_simp.custom.yaml`。如果这个文件已经存在，那么需要将下载文件`luna\_pinyin.custom.yaml`中的内容合并到已有`luna\_pinyin\_simp.custom.yaml`文件当中。
英文常用词库（luna\_pinyin.cn\_en.dict.yaml）里自己尝试添加了一个 osx ☞ OS X，第一次失败是因为间隔之间没有用 tab 键，而是用空格，第二次失败是因为音节之间没有正确空格，**正确的规则是「文字-编码-权重频度」三个字段之间是 tab，编码如果是多个「音节」音节之间用空格分开，**权重数值的高低决定了音节相同时多个候选词在候选条上排列的先后顺序，当然全局性的词频拥有更高的优先级（候选条上高亮选中，然后 shift+fn+delete 可以删除记忆错误的词频调整）。

![](http://o88okth1x.bkt.clouddn.com/imac_7efbca7dd954a96e6c6cc271424f5e47.png-960.jpg)

> 编辑字典文件时，TextWrangler 编辑器可以「View-Text Display-Show Invisibles」将隐藏符号显示出来以便查错和参照。TextWrangler 「Edit - Text Options」设置里去掉「Auto-expend tabs」的勾选，输出的就是tab而不是4个空格。 
> 表情符号的问题，有几种解决方案，
> - 一种是把表情作为输入方案的一种选择，需要的时候像切换繁体和简体一样切换到表情输入；
> - 另一种是将表情加入到拼音方案中，但是这种方式每次都出来一堆表情，而且没法实现词频的调整，所以最后选择的是将表情作为字典来使用的方案，
> > 基于网友 @ lembacon 的表情文件制作了一份字典文件（luna\_pinyin.emoji.dict.yaml，已包含在文章后的下载中），需要注意的是新的表情字典，需要在扩展字典的主文件（luna\_pinyin.extended.dict.yaml）中添加一段代码：`- luna\_pinyin.emoji`。 

	name: luna_pinyin.extended
	version: "2014.10.28"
	sort: by_weight
	use_preset_vocabulary: 
	
此處爲明月拼音擴充詞庫（基本）默認鏈接載入的詞庫，有朙月拼音官方詞庫、明月拼音擴充詞庫（漢語大詞典）、明月拼音擴充詞庫（詩詞）、明月拼音擴充詞庫（含西文的詞彙）。如果不需要加載某个詞庫請將其用「#」註釋掉。

>雙拼不支持 luna\_pinyin.cn\_en 詞庫，請用戶手動禁用。

import\_tables:

  - luna\_pinyin
  - luna\_pinyin.hanyu
  - luna\_pinyin.poetry
  - luna\_pinyin.cn\_en
  - luna\_pinyin.emoji
  - luna\_pinyin.kaomoji
  - luna\_pinyin.music
  - luna\_pinyin.movie
  - luna\_pinyin.computer
  - luna\_pinyin.name
...

## default.custom.yaml
全局性的这个文件里，主要是定义输入方案和候选词的数量，输入方案上我选择了：明月拼音·简化字、明月拼音、明月拼音·语句流、五笔拼音混合輸入，候选词数量设置的是7个（page\_size: 7）。

	patch:
	  switcher:
		caption: 〔方案选单〕
		hotkeys:
		- Control+grave
	
	menu:
	  page_size: 
	  
	schema_list:
		- schema: luna_pinyin_simp
		- schema: luna_pinyin
		- schema: luna_pinyin_fluency  
		- schema: wubi_pinyin          # 五笔拼音混合輸入

## squirrel.custom.yaml
输入法外观的设定是在梁海方案的基础上修改的，并参照了 10.11 El Capitan 输入法的配色和字体。候选词条中如果出现生僻字无法显示（显示为框问号），可以在方案配色的字体指向上多加一个「 花园明朝」字体。 

	patch: show_notifications_when: appropriate # 状态通知，适当(appropriate)，开（always）关（never） 
	style: 
		color_scheme: apathy 
	preset_color_schemes: 
		apathy: 
		name: "冷漠 / Apathy" 
		author: "LIANG Hai " 
		horizontal: # 水平排列 
		inline_preedit: #单行显示，false双行显示 
		candidate_format: "%c\u2005%@\u2005" # 编号 %c 和候选词 %@ 前后的空间 
		corner_radius: #候选条圆角 
		border_height: border_width: 
		back_color: 0xFFFFFF #候选条背景色 
		font_face: "PingFangSC-Regular,H-SiuNiu" #候选词字体 
		font_point: #候选字词大小 
		text_color: 0x424242 #高亮选中词颜色 
		label_font_face: "PingFangSC-Light" #候选词编号字体 
		label_font_point: #候选编号大小 
		hilited_candidate_text_color: 0xEE6E00 #候选文字颜色 
		hilited_candidate_back_color: 0xFFF0E4 #候选文字背景色 
		comment_text_color: 0x999999 #拼音等提示文字颜色
		
> 外观设置中指向了 El Capitan 最新的字体「苹方」和「 花园明朝」，后者需要单独下载安装。