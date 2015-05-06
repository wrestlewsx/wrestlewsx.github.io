---
layout: post
title: Qt5 in Linux
category: 技术
tags: Qt
description: 配置Qt的时候出现的问题
---

## Linux of Qt5
<p>在Ubuntu编译Qt5工程时出现了 
<br>`can not find -lGL`<br>
<p>这是为什么?在Qt4时代并没有这种情况<br>
<p>经过查找,发现Qt5在这个版本自动加入了openGL的支持,而有的平台并没有默认拥有
<br><strong>(Windows默认有openGL,Linux却没有完全)<strong/>
<p>那么我们可以通过安装 `libglut-dev` 来进行修复
<br>`sudo apt-get install libglut-dev`
<br>
<p>稍微解读一下也能知道-lGL==>-linkopenGL的意思
