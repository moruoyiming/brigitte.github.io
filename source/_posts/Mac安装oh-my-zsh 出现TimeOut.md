---
title: Mac安装oh-my-zsh出现TimeOut
thumbnail: /gallery/thumbnails/sculpture.jpg
categories: 
- Mac应用
tags:
- 壁纸路径
- Mac系统
---
mac终端 安装 oh-my-zsh
sh -c "$(curl -fsSL [https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh](https://links.jianshu.com/go?to=https%3A%2F%2Fraw.githubusercontent.com%2Frobbyrussell%2Foh-my-zsh%2Fmaster%2Ftools%2Finstall.sh))"

提示错误

curl: (7) Failed to connect to raw.githubusercontent.com port 443: Operation timed out

用这个连接
wget [https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Frobbyrussell%2Foh-my-zsh%2Fraw%2Fmaster%2Ftools%2Finstall.sh) -O - | sh

