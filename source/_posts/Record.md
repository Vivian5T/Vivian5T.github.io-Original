---
layout: photo
title: Github Page - Process Record
date: 2016-06-04 12:52:17
tags:
---

![](http://o88okth1x.bkt.clouddn.com/imac_2232948dd3e4d0b5c9b26441dd6c6234.png-960.jpg)
>摘要：这是一篇关于自己搭建Github page的记录，内容包括github和Hexo设置等过程。我想将我搭建独立博客的过程在一篇文章中尽可能详细地写出来，希望也能给后来者一个有益的指引。  

<!-- more -->

## 关于本人
本人为一名视觉设计师，没有任何代码基础；作为一名技术小白，网上的各种也是搞的云里雾里，各种莫名其妙。。。可见做一名“程序员”还真是一件非常之不易的事情！所以，在我搭建完成自己的博客以后，我决定要将整个过程记录下来，其中有的资料可能引用他人的文章，在本文的最后我也将列出参考资料，并感谢！

## 为啥要搭建自己的博客  
* 属于独立&自己的空间，不用受各种框架的限制。
* 自我的展示&分享平台。

## 为啥用Github Page?
* 免费当然是最大的吸引力！－300M的Free空间，资料独立管理。
* 可以绑定自己域名、支持静态脚本、DIY自由发挥！
* 顺带学习如何使用Github为自己的工作增效！
* 拓展自己的眼界，多见多学总是好的！

### 关于Github Page
>Git：一个开源分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。
>
>Github：一个托管课中Git库的站点

![Github-Page](http://o88okth1x.bkt.clouddn.com/githubpage.png)

## 安装工具
* [Git](https://git-scm.com/)
* [Node.js](https://nodejs.org/en/)

### 技术基础
* html+css+javascript
* git基本语法
* markdown语法

gdfgdfgdfg


### Github创建仓库
1. 登录github账号：在github首页点击Sign in按钮进入登录页面。填写用户名或邮箱和密码，点击Sign in按钮登录。
2. 点击创建仓库：点击在登录的用户图像左边的+号和下三角符号按钮。
3. 填写创建仓库信息。
4. 填写好相关信息，点击Create repository(创建仓库)按钮。

![](http://o88okth1x.bkt.clouddn.com/imac_531433c0abd2a1da73a6672201a4206a.png-960.jpg)

## 配置SSH
* **首先我们需要检查你电脑上现有的ssh key,打开终端：**

	```
	$ cd ~/. ssh 检查本机的ssh密钥
	```
	如果提示：No such file or directory 说明你是第一次使用git。

* **生成新的SSH Key：**

	```
	$ ssh-keygen -t rsa -C "邮件地址@youremail.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):
	```
	>注意: 此处的邮箱地址，你可以输入自己的邮箱地址；注意2: 此处的「-C」的是大写的「C」
	
	然后系统会要你输入密码：
	
	```
	Enter passphrase (empty for no passphrase):<输入加密串>
	Enter same passphrase again:<再次输入加密串>
	```
	到这里就成功设置ssh key了
	
* **添加公钥到github：**
	- 点击用户头像，然后点击显示的Settings(设置)选项；  
	![](http://o88okth1x.bkt.clouddn.com/imac_149ff6cf70dbb12a886cbaf39c5a6bf2.png-960.jpg)
	
	- 在用户设置栏，点击`SSH and GPG keys`选项，然后点击`New SSH key`(新建SSH)按钮；
	- 把你本地生成的密钥复制到里面（key文本框中）， 点击`add key`就ok了
	
* **测试SSH：**

	```
	$ ssh -T git@github.com
	```
	接下来会出来下面的确认信息：

	```
	The authenticity of host 'github.com (207.97.227.239)' can't be established. 
	RSA key fingerprint is 17:24:ac:a5:76:28:24:36:62:1b:36:4d:eb:df:a6:45.
	Are you sure you want to continue connecting (yes/no)?
	```
	输入`yes`后回车。

	然后显示如下信息则OK(其中的Vivian5T是用户名)。
	
	```
	Hi Vivian5T! You've successfully authenticated, 
	but GitHub does not provide shell access.
	```

---
### 安装HEXO
```
$ npm install -g hexo
```
### 部署HEXO
在电脑中建立一个名字叫“Blog”的文件夹，然后打开终端进入该文件夹目录

```
$ cd blog
```

初始化&建立“HEXO”所需文件

```
$ hexo init
```

现在我们已经搭建起本地的hexo博客了。
本地预览已经建立的博客，执行以下命令，然后到浏览器输入localhost:4000看看。

```
$ hexo generate
$ hexo serve
```

## 安装HEXO主题
首先执行清理缓存

```
$ hexo clean
```
到[Hexo theme](https://hexo.io/themes/)选择一个自己喜欢的主题克隆到本地。

```
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### 启用主题
当克隆完成后，打开`站点配置文件`_config.yml， 找到`theme`字段，并将其值更改为`next`。 
### 调试主题
首先启动Hexo本地站点`$ hexo serve`，并开启调试模式（即加上`--debug`），整个命令是`hexo serve --debug`。 在服务启动的过程，注意观察命令行输出是否有任何异常信息，如果你碰到问题，这些信息将帮助他人更好的定位错误。 当命令行输出中提示出： 

```
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```

此时即可使用浏览器访问`http://localhost:4000`，检查站点是否正确运行。
### 搭建完成！
至此，独立博客就算搭建完成，如需进步一完善请在参看以下文章。

>参考文章：
>
>[如何搭建一个独立博客——简明Github Pages与Hexo教程 - 简书](http://www.jianshu.com/p/05289a4bc8b2)
>
>[手把手教从零开始在GitHub上使用Hexo搭建博客教程(一)-附GitHub注册及配置](http://www.jianshu.com/p/f4cc5866946b)