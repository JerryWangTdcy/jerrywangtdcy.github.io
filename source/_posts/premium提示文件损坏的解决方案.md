---
layout: mac下载navicat
title: premium提示文件损坏的解决方案
date: 2021-04-30 14:10:43
tags:
---

### premium提示文件损坏的解决方案
首先打开终端，执行：
```sudo bash```
这时会提示你输入你的账户密码， 输入完后就切换到了 root 用户，然后执行：
```xattr -cr /Applications/Navicat\ Premium.app/```
然后就可以了