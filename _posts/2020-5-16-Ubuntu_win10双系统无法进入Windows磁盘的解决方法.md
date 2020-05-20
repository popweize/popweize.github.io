---
title: Ubuntu_win10双系统无法进入Windows磁盘的解决方法
description: 双系统需要进行文件交换，但是有时会出现磁盘无法访问的额情况           
categories:
 - linux
 - ubuntu
tags: 科技宅拯救世界
---

就是不能让你好好工作！！

![QQ图片20200518152414](/home/chen/图片/QQ图片20200518152414.png)

那就解决掉它！



1.ctrl+alt+t打开终端查看是否安装ntfs-3g

`locate ntfs-3g`

2.没安装的话就装一下

`sudo apt-get install ntfs-3g` 

3.修复显示的出问题的分区（每个人分区号可能不一样，注意更改）

`sudo ntfsfix /dev/sda6`



**搞定！**



















