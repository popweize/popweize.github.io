---
title:双系统重装windows后bios无法引导进入ubuntu系统
description:win10_ubuntu双系统重装windows系统后，ubuntu系统文件都还在，但是系统引导没了，bios无法再选择进入ubuntu系统，可以选择重装ubuntu不过比较麻烦，就需要重新建立ubuntu引导。             
categories:
 - linux ubuntu
tags: 科技宅拯救世界
---

1.用Boot-repair修复双系统引导

连接网络后我们打开终端，依次输入下面的内容，每行之后都要按回车

`sudo -i`

`add-apt-repository ppa:yannubuntu/boot-repair && apt-get update`

`apt-get install -y boot-repair && boot-repair`

第一行表示进入root账户模式

第二行添加软件源并更新系统

第三行为安装boot-repair并在安装完成后启动软件。

![img](https://img-blog.csdnimg.cn/20181208101734214.png)

点击第一个选项Recommended repair

剩下的软件会自己操作，不需要人为干预

视电脑配置，花费的时间不等。

电脑启动后的确找到Windows和Ubuntu的引导了，但是多了几项多余的启动项，容易形成干扰。

`su 　　　　# 获取root权限`

`cd /boot/grub`

`cp grub.cfg grub.cfg_backup　　#先备份一下`

`cat grub.cfg > tmp　　#将内容重定向到其他文件，便于修改`

`gedit tmp　　#或者vim tmp`

＃将下面这些内容全部删掉

***

\### BEGIN /etc/grub.d/25_custom ###

　menuentry "Windows UEFI bootmgfw.efi" {

　search --fs-uuid --no-floppy --set=root 84F5-6727

　chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi

　}

　menuentry "Windows Boot UEFI loader" {

　search --fs-uuid --no-floppy --set=root 84F5-6727

　chainloader (${root})/EFI/Boot/bkpbootx64.efi

　}

　... 

 menuentry "Windows Boot UEFI recovery bkpbootx64.efi" {

 search --fs-uuid --no-floppy --set=root 5686-D913

 chainloader (${root})/efi/Boot/bkpbootx64.efi

 }

\### END /etc/grub.d/25_custom ###

***

 其实就是删掉对应的中间那几项

　删掉之后再：

`cat tmp > grub.cfg`

` reboot`



不过这个也不一定保证成功，系统环境有时候出的问题比较奇葩，不行的话就重装吧，所以每次大动系统之前把文件备份好。。省得哭鼻子

























