---
title: SSH通用命令
categories: 
- 科学上网
tags:
- ss
- 翻墙
- ssh
---

## Quick Start

### 查看当前ss服务器所开放的端口

``` bash
$ ss -lntp | grep ssserver
```

### 查看当前ss服务器的密码，通过以下命令可见ss的配置文件

``` bash
$ ps aux | grep ssserver
```
<!-- more -->
### 用cat查看下配置文件

``` bash
$ cat /etc/shadowsocks.json
```

### 修改ss密码

``` bash
$ vi /etc/shadowsocks.json
```
按i键进入编辑模式，修改密码为123456
"password":"123456",
### 重启ss即可

``` bash
$ service shadowsocks restart
```

启动：service shadowsocks start
停止：service shadowsocks stop
重启：service shadowsocks restart
状态：service shadowsocks status

