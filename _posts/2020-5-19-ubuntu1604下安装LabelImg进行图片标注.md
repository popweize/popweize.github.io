---
title: ubuntu1604下安装LabelImg进行图片标注
description: 训练模型，就得有数据，还得标注出来
categories:
 - ubuntu 计算机视觉 深度学习
tags: 科技宅拯救世界
---

提前安装python3 和pip3

这个需要在国外站点下载一些文件，所以安装过程老是失败，我找了俩教程，也分不清哪个更好用了，都试试吧



**[官网下载LabelImg](https://github.com/tzutalin/labelImg)，**

**法1、官方推荐Python 3 + Qt5环境下使用**

`sudo apt-get install pyqt5-dev-tools `

`sudo pip3 install -r requirements/requirements-linux-python3.txt `

`make qt5py3 `

`python3 labelImg.py python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]`



**法2.下载后直接打开终端，并cd到解压路径下输入如下命令：**

`sudo apt-get install pyqt5-dev-tools`

`pip install --upgrade pip`

` pip install lxml`

`make qt5py3`

`python3 labelImg.py`

如果想再次打开LabelImg，重复最后一个步骤（`python3 labelImg.py`也可添加到快捷启动器）

**使用教程：（贼简单，体力活）**

https://pypi.org/project/labelImg/#description























