---
layout: photo
title: 一个脚本让你的Mac支持NTFS
date: 2016-06-12 13:45:17
tags:
- 效率工具
categories:
- Mac技巧分享
---
![](http://o88okth1x.bkt.clouddn.com/imac_cb7cf812966c16187c501a63dfc21c3c.png-960.jpg)
Mac使用了很多年了，对于不能在**Mac**下写入`NTFS`格式的磁盘，一直是一件让人觉得很不爽的事情，所以就去研究了一下。

<!--more-->

## 解决办法

> 解决方法有如下三种:

#### `第一种` 应用软件

![](http://o88okth1x.bkt.clouddn.com/imac_404c8169cf5ebd6649d9e0e7aaea0c16.png-960.jpg)

直接使用第三方软件，如 **Paragon NTFS for MAC** (需要软件的朋友移步本文`软件分享`部分)，**Tuxera NTFS** 等，不过大部分都是收费的。有一款免费的是 **Mounty**。

#### `第二种` 脚本命令

![](http://o88okth1x.bkt.clouddn.com/imac_98163d2ece928b00023417bf7d24c073.png-960.jpg)

执行我写好的脚本，命令如下：

    $ curl -O https://raw.githubusercontent.com/CraryPrimitiveMan/code-examples/master/shell/mac_ntfs.sh
    $ chmod +x ./mac_ntfs.sh
    $ ./mac_ntfs.sh

> 注：**执行时，需插入磁盘。**期间要输入你的本地密码授权写文件，然后你会发现在桌面出现了一个Volumes的快捷方式，点进去，就可以看到你的磁盘了。执行完之后，需要重新插入磁盘。

#### `第三种` 脚本命令

手动去开启 **Mac** 中隐藏的对`NTFS`的支持（`OSX 10.5`之后）。
这个也需要线插上磁盘，然后可以从`finder`或者使用以下命令查看到磁盘的`Volume Name`：

    $ diskutil list

显示结果如下：

    /dev/disk0 (internal, physical):
    #:                       TYPE NAME                    SIZE       IDENTIFIER
    0:      GUID_partition_scheme                        *500.3 GB   disk0
    1:                        EFI EFI                     209.7 MB   disk0s1
    2:          Apple_CoreStorage Macintosh HD            499.4 GB   disk0s2
    3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
    /dev/disk1 (internal, virtual):
    #:                       TYPE NAME                    SIZE       IDENTIFIER
    0:                  Apple_HFS Macintosh HD           +499.1 GB   disk1
                                 Logical Volume on disk0s2
                                 77AD0A71-82FD-4D1E-B074-CB1405FCD317
                                 Unlocked Encrypted
    /dev/disk2 (external, physical):
    #:                       TYPE NAME                    SIZE       IDENTIFIER
    0:     FDisk_partition_scheme                        *1.5 TB     disk2
    1:               Windows_NTFS TOSHIBA EXT             1.5 TB     disk2s1

可以看到，我的磁盘的 Volume Name 是TOSHIBA EXT。
紧接着更新 /etc/fstab文件

    $ sudo vim /etc/fstab

把以下内容写入进去

    $ LABEL=TOSHIBA\040EXT none ntfs rw,auto,nobrowse

> 下面来依次解释一下，其中的`\040`的意思是代替空格键，因为我的`Volume Name`是有空格的，所以必须把这个空格给转义了。后面的`Ntfs rw`表示把这个分区挂载为可读写的`ntfs`格式，最后`nobrowse`非常重要，因为这个代表了在`finder`里不显示这个分区，这个选项非常重要，如果不打开的话挂载是不会成功的。

编辑好以后重新插入磁盘，就能识别到了，但是这个时候有了一个最大的问题，因为这个分区在`finder`里不显示了，那么我们要怎么找到它呢，总不能一直用命令行把，解决办法其实很简单，因为这个分区是挂`/Volumes`下的，我们把这个目录在桌面做一个快捷方式就行了。

    $ sudo ln -s /Volumes ~/Desktop/Volumes

然后就可以在桌面上打开Volumes快捷方式，去使用了

#### 软件分享


**Paragon NTFS for MAC** [软件下载地址](https://vivian5t.github.io/2016/06/12/NTFS%20For%20Mac%E6%9C%80%E5%BC%BA%E5%A4%A7%E7%9A%84Mac%E8%AF%BB%E5%86%99%E5%B7%A5%E5%85%B7/#more)
