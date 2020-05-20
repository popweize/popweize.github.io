---
title: ubuntu_win10双系统时间错误 
description: 从外部应用（如WPS Presentation）打开连接后，chrome只显示一个空的标签，不会自动跳转           
categories:
 - ubuntu
tags: 科技宅拯救世界
---

出现这个问题跟 google-chrome.desktop 有关，它缺少一个参数 %U。

1.打开文件：

/home/chen/.local/share/applications/google-chrome.desktop

注意：不同用户路径不一样，不能复制粘贴，找到用户目录即chen下的.local文件夹即可

2.编辑google-chrome.desktop

可以终端内用代码：

`gedit /home/chen/.local/share/applications/google-chrome.desktop`

也可手动

3.找到下面这行:

Exec=/opt/google/chrome/chrome

在末尾添加一个空格和%U:

Exec=/opt/google/chrome/chrome %U

然后保存文件即可





























