---
title: Mac使用终端登录谷歌云
thumbnail: /gallery/thumbnails/sculpture.jpg
categories: 
- Mac应用
tags:
- 谷歌云
- 蓝牙开发
---
1.网页SSH进入谷歌云，切换到root角色
 sudo -i
 2.修改SSH配置文件/etc/ssh/sshd_config
 vi /etc/ssh/sshd_config
 修改PermitRootLogin和PasswordAuthentication为yes

\# Authentication:
 PermitRootLogin yes //默认为no，需要开启root用户访问改为yes

\# Change to no to disable tunnelled clear text passwords
 PasswordAuthentication yes //默认为no，改为yes开启密码登陆
 3.给root用户设置密码
 passwd root
 4.重启SSH服务使修改生效
 /etc/init.d/ssh restart
 5.启动mac终端
 ssh root@ip
 输入密码即可进入SSH。
