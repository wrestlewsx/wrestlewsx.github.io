---
layout: post
title: Python相关
category: 技术
tags: Python
description: 介绍Python库以及出现的问题解决
---
#  Python 
## 安装第三方库(Linux::Ubuntu 14.04 LTS)
   关于一个gui的库 SimpleGUICS2Pygame <br />
   所有的命令均在 root 权限下执行 <br />
### 安装前提:
   1. 使用easy_install 工具 `apt-get install easy_install`
   2. 安装pip `easy_install pip`

### 开始安装
   1. 在 https://pypi.python.org/pypi/SimpleGUICS2Pygame 下载.egg格式的安装包 <br />
   2. 使用命令 `easy_install name.egg #name.egg 为下载的第三方库的egg包名称`
   3. 我们这里可以使用 `easy_install *.egg #代表安装所有的egg包,方便快捷,不用输入完整的名字`
   4. 我们可以通过 `pip freeze` 查看所安装的包

### 使用错误
   1. 当我们 `import simplegui`时,却出现 `...importError: No module named simplegui` <br />
   此时,我们应该使用这个语句块替换: <br />
   <pre><code>
   try:
       import simplegui 
   except:
       import SimpleGUICS2Pygame.simpleGUICS2Pygame as simplegui
   </code><pre>
   2. 作者给出的解释是由于内部冲突所以会导致这种现象的产生

   
