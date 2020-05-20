---
title: Ubuntu_win10双系统彻底删除ubuntu引导
description: 第一次装系统往往会出很多问题，需要装很多次，那么上一次安装时产生的引导文件怎么删除让电脑变干净呢         
categories:
 - linux
 - ubuntu
tags: 科技宅拯救世界
---

见不得电脑有半点垃圾文件的我

1、查看电脑分区信息**

右键我的电脑，单击管理，打开磁盘管理器，可以看到相应分区信息，具体如下图(根据个人分区方式会不同)：

![stickPicture](/home/chen/下载/stickPicture.png)

这里说明下，磁盘1中标红色的为Ubuntu下各分区信息，分别为：swap分区，EFI分区，/home分区，/usr分区和/分区。这里可以直接删除swap分区，/home分区，/usr分区和/分区。接下来要做的就是删除EFI分区以及修改win10EFI分区(不修改的话还会有Ubuntu启动项)。

**2、删除ubuntu分区**

要删除Ubuntu系统下的EFI分区，有各种软件和方法，这里推荐直接用windows下的diskpart来删除，省得安装第三方流氓软件。

首先用管理员权限打开cmd，输入【diskpart】，利用【list disk】查询磁盘信息。

这里我们Ubuntu装在磁盘1中，所以选择磁盘1【select disk 1】，然后查看磁盘1下所有分区信息【list partition】，可以看到我们Ubuntu的EFI分区为488MB，根据分区大小这里选择分区4【select partition 4】。然后删除它【delete partition override】。如下图所示：

![stickPicture (1)](/home/chen/下载/stickPicture (1).png)

删除之后就会发现磁盘1中多出了一块200G的未分配空间。

**3、修改win10启动项**

如果这样结束，开机按F9或F12会发现启动项里还会有Ubuntu启动项：

![stickPicture (2)](/home/chen/下载/stickPicture (2).png)

这是因为在安装Ubuntu后，Ubuntu的引导信息也写在了win10的EFI启动分区里。如果不删除的话，以后再安装Ubuntu会出现很多个Ubuntu启动项。

在win10下我们无法访问EFI分区，因为没有盘符。如图所示：

![stickPicture (3)](/home/chen/下载/stickPicture (3).png)

这里我们还是利用diskpart来操作，首先进入磁盘0为EFI分区分配盘符，【remove letter=p】这一步先不做，先不要按照图里的把盘符删除。

1. 先选择磁盘0【select disk 0】即win10系统所在的磁盘。
2. 查看分区列表以确定具体分区【list partition】。
3. 根据容量(这里是260MB)选择分区【select partition 1】。
4. 为win10的EFI分区分配盘符【assign letter=p】这里p为盘符，字母A~Z应该都可以(大小写无关，自动转成大写)，不要和已有的盘符重复即可。

![stickPicture (4)](/home/chen/下载/stickPicture (4).png)

这时再次查看win10磁盘会发现有个p盘，就是我们刚刚分配的EFI分区，如下图：

![stickPicture (5)](/home/chen/下载/stickPicture (5).png)

直接打开我们会发现权限不够，打不开。这里我们要运用一个小技巧，先用管理员权限打开记事本，然后通过记事本菜单栏里的【打开】来访问P盘，会发现P盘里有个EFI文件夹，打开EFI文件夹，发现如下目录(电脑不一样可能会稍有不同)：

![stickPicture (6)](/home/chen/下载/stickPicture (6).png)

这里直接删除ubuntu文件夹就可以了。

此时再回到diskpart删除EFI分区盘符P【remove letter=p】。

注：这里利用记事本是借用能用管理员权限打开记事本，记事本就被赋予了管理员权限，相当于使用管理员权限访问p盘，其他能用管理员权限的软件应该也都可以，因为记事本方便且简单所以这里采用记事本。![stickPicture (7)](/home/chen/下载/stickPicture (7).png)

1. 打开win10的搜索界面输入需要打开的软件，打开记事本软件，鼠标右键菜单中选择【以管理员身份运行】找到需要修改的文件， 进行编辑和修改后，保存文件即可。



















