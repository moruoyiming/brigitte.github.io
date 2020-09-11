---
title: Mac系统壁纸路径
thumbnail: /gallery/thumbnails/sculpture.jpg
categories: 
- Mac应用
tags:
- 壁纸路径
- Mac系统
---
在 Finder 中，菜单栏选取“前往”>“前往文件夹”，弹出的框里输入
/Library/Desktop Pictures/
或
/System/Library/Desktop Pictures/
然后回车即可打开该文件夹。

系统壁纸默认路径存在两个地方，当时去了第一个路径上找未找到，后来通过命令行获取到路径发现System 下也有一个Desktop Pictures 文件夹。

终端命令：显示壁纸所在路径（路径显示在屏幕对应壁纸上）：

> defaults write com.apple.dock desktop-picture-show-debug-text -bool TRUE;killall Dock

终端命令：隐藏该路径：

> defaults delete com.apple.dock desktop-picture-show-debug-text;killall Dock

