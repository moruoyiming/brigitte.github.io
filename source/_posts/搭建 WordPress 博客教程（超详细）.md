***本文转自：[Nonecy 的小黑屋](http://blog.studymany.com/2018/07/29/create-wordpress-blog/)***
***链接：**http://blog.studymany.com/2018/07/29/create-wordpress-blog/*

## **需要**

- 一台服务器
- 一个域名，直接通过ip访问好傻好傻的样子，哈哈。
- linux知识
- 肯折腾

## **具体步骤**

### 第一步购买服务器，国内阿里云的云服务器挺不错的，国外的就更多了，这一步就不介绍了，不懂得的自己上网搜。

接下来操作需要：

### **远程连接服务器**

**Windows 用户**

以Xshell为例。

1. 下载安装Xshell，[官网链接](https://link.jianshu.com/?t=http%3A%2F%2Fwww.netsarang.com%2Fproducts%2Fxsh_overview.html)。

2. 安装完成后新建会话（Alt+N）。依次填写图中信息。
   名称可以是Vultr或者其他，协议选择SSH，主机填写之前的IP Address，端口号选择22。

   <!-- more -->

连接

点击左侧的用户身份验证，填写信息。方法选择Password，用户名为之前的Username（一般都是root），密码为之前的Password（这个建议直接复制粘贴过来，系统给的有点复杂）

用户身份验证

填写完之后点击确定。然后点击连接。出现其他提示的话选择接受就可以了。这时你就可以看到一个命令控制台了。这时就算连接成功了。

**Mac OS 用户**

打开终端或者iTerm2等。

```
ssh root@45.32.195.77 
```

然后输入密码即可。

### **安装nginx，mysql，php**

建议使用lnmp一键安装包安装，方便快捷。如果不用一键安装包，我估计得研究这一块的东西大概一周吧。下面以一键安装包为例。

**获取lnmp一键安装包链接**

[lnpm官网链接](https://link.jianshu.com/?t=https%3A%2F%2Flnmp.org%2F)

找到下载页面选择最新的复制其链接。

写此文时最新版本信息如下：

```
LNMP 1.4 测试版
http://soft.vpser.net/lnmp/lnmp1.4beta.tar.gz  (131KB)
MD5：bd851e151b2ba13c3a32c435efb1a76c
最后更新: 2017年2月14日14:18 GMT+8
```

其中的`http://soft.vpser.net/lnmp/lnmp1.4beta.tar.gz`就是我们需要的链接，复制到剪贴板。

**安装**

```
# 下载，后边的路径直接粘贴就好。XShell上面复制快捷键是ctrl+insert，粘贴快捷键是Shift+insert，mac上面是我们熟悉的 command+c，command+v
wget http://soft.vpser.net/lnmp/lnmp1.4beta.tar.gz
# 解压
tar -zxvf lnmp1.4beta.tar.gz
# 进入lnmp目录
cd lnmp1.4
# 执行install.sh进行安装
./install.sh 
```

lnmp

依次输入你要安装的选项前的数字并回车即可下一步。

**MYSQL 选项**

```
You have 5 options for your DataBase install.
1: Install MySQL 5.1.73
2: Install MySQL 5.5.53 (Default)
3: Install MySQL 5.6.34
4: Install MySQL 5.7.16
5: Install MariaDB 5.5.53
6: Install MariaDB 10.0.28
7: Install MariaDB 10.1.190: DO NOT Install MySQL/MariaDB
Enter your choice (1, 2, 3, 4, 5, 6, 7 or 0): 
```

此处根据所需选择，如果使用的上述服务器，请选择2或者直接回车。我选择默认。

注意：安装MySql时，如果选择太高的版本安装会被拒绝，提示信息如下 `Memory less than 1GB, can't install MySQL 5.6, 5.7 or MairaDB 10!`。根据个人手动安装MySql5.7的经验来看，此768MB内存的服务器在运行一个nginx，mysql，php时还好，倘若再运行一个tomcat，mysql将会不定期down掉。所以此处选择一个低版本的5.5MySql即可。

```
You will install MySQL 5.5.53
===========================
Please setup root password of MySQL.(Default password: root)
Please enter: 
```

输入密码回车或直接回车，直接回车默认密码为root。此处做实验我选择默认，个人实际使用请修改。

```
MySQL root password: root
===========================
Do you want to enable or disable the InnoDB Storage Engine?
Default enable,Enter your choice [Y/n]: 
```

输入Y或者n然后回车或直接回车，直接回车默认启用InnoDB存储引擎。我选择默认。

```
No input,The InnoDB Storage Engine will enable.
===========================
You have 6 options for your PHP install.
1: Install PHP 5.2.17
2: Install PHP 5.3.29
3: Install PHP 5.4.45
4: Install PHP 5.5.38 (Default)
5: Install PHP 5.6.30
6: Install PHP 7.0.15
7: Install PHP 7.1.1
Enter your choice (1, 2, 3, 4, 5, 6 or 7): 
```

输入选项然后回车或者直接回车，直接回车默认安装PHP5.5.38版本。我选择默认。

```
You will install PHP 7.1.1
===========================
You have 3 options for your Memory Allocator install.
1: Don't install Memory Allocator. (Default)
2: Install Jemalloc3: Install TCMalloc
```

输入选项然后回车或者直接回车，直接回车默认不安装内存分配器。我选择默认。

此时出现

```
Press any key to install...or Press Ctrl+c to cancel
```

当然是摁任意键啦，一般都是回车咯。

然后出现一大堆信息。前几行如下：

```
You will install lnmp stack.
nginx-1.10.3
mysql-5.5.53
php-5.5.38
Enable InnoDB: y
Print lnmp.conf infomation...
Download Mirror: http://soft.vpser.net
Nginx Additional Modules: 
PHP Additional Modules: 
Database Directory: /usr/local/mysql/var
Default Website Directory: /home/wwwroot/default
CentOS release 6.8 (Final)
Kernel \r on an \m
```

这一堆东西你就不用管啦。本次实验的开始时间23:04……经过了漫长漫长漫长的等待之后……大概23:35结束。所以期间你去洗个澡看个电视剧都不是问题。然后我们看到屏幕上最后输出的信息如下。

```
The service command supports only basic LSB actions (start, stop, restart, try-restart, reload, force-reload, status). For other actions, please try to use systemctl.Removed symlink /etc/systemd/system/basic.target.wants/firewalld.service.Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.Add Startup and Starting LNMP...Add nginx service at system startup...Starting nginx...  doneAdd mysql service at system startup...Starting MySQL... SUCCESS! Add php-fpm service at system startup...Starting php-fpm  done
============================== Check install ==============================
Checking ...Nginx: OKMySQL: OKPHP: OKPHP-FPM: OKClean src directory...+------------------------------------------------------------------------+|          LNMP V1.4 for CentOS Linux Server, Written by Licess          |+------------------------------------------------------------------------+|           For more information please visit https://lnmp.org           |+------------------------------------------------------------------------+|    lnmp status manage: lnmp {start|stop|reload|restart|kill|status}    |+------------------------------------------------------------------------+|  phpMyAdmin: http://IP/phpmyadmin/                                     ||  phpinfo: http://IP/phpinfo.php                                        ||  Prober:  http://IP/p.php                                              |+------------------------------------------------------------------------+|  Add VirtualHost: lnmp vhost add                                       |+------------------------------------------------------------------------+|  Default directory: /home/wwwroot/default                              |+------------------------------------------------------------------------+|  MySQL/MariaDB root password: root                          |+------------------------------------------------------------------------++-------------------------------------------+|    Manager for LNMP, Written by Licess    |+-------------------------------------------+|              https://lnmp.org             |+-------------------------------------------+nginx (pid 715 713) is running...php-fpm is runing! SUCCESS! MySQL running (1247)Active Internet connections (only servers)Proto Recv-Q Send-Q Local Address           Foreign Address         State      tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN     tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     tcp6       0      0 :::22                   :::*                    LISTEN     
Install lnmp V1.4 completed! enjoy it.
```

简单说明一下，此安装过程安装完成便也启动了nginx，mysql，php-fpm并加入了开机启动项。如果重启服务器，不需要再单独手动开启相关的服务了。总的来说相当方便的。

*关于Linux服务，自己之前做的笔记分享给大家。[Linux 服务管理](https://www.jianshu.com/p/f896f42af246)*

这时候你在浏览器输入`http://IP` 例如 `http://45.32.195.77`便可以访问了。看到的内容如下：

访问页面

网站根目录路径`/home/wwwroot/default`,如果只用来放一些静态页面，那么，现在就足够了，直接将你的html，js，css等文件丢进去即可。这不是本文重点，在此不赘述了。

退出使用`ctrl+c`

### **安装WordPress**

**下载WordPress包**

[中文官方站点](https://link.jianshu.com/?t=https%3A%2F%2Fcn.wordpress.org%2F)[英文官方站点](https://link.jianshu.com/?t=https%3A%2F%2Fwordpress.org%2F)具体的根据自己的需求选择。下面以中文版为例。当前最新版本是4.7.2

为了方便，我们还是在用站点默认的路径，但是我们投机取巧一下。

```
# 进入根目录上一级目录
cd /home/wwwroot/
# 将default重命名为old
mv default old
# 下载WordPress包中文版wget https://cn.wordpress.org/wordpress-4.7.2-zh_CN.tar.gz
# 解压WordPress包
tar -zxvf wordpress-4.7.2-zh_CN.tar.gz 
# 查看解压后的文件夹名，此处是wordpress，估计应该都是吧，看看保险啊
[root@vultr wwwroot]# ls
old  wordpress  wordpress-4.7.2-zh_CN.tar.gz
# 将wordpress重命名为default
mv wordpress default
# 再次查看检验[root@vultr wwwroot]# ls
default  old  wordpress-4.7.2-zh_CN.tar.gz
```

**给相应目录授权**

```
# 目录以及目录下的文件授权[root@vultr wwwroot]# chown -R 755 /home/wwwroot
chown: changing ownership of ‘/home/wwwroot/old/.user.ini’: Operation not permitted
# 将目录的所有者分给www组下的www用户。
[root@vultr wwwroot]# chown -R www:www /home/wwwroot/
chown: changing ownership of ‘/home/wwwroot/old/.user.ini’: Operation not permitted
```

出现的提示大概是说有一个文件无法更改用户分组和权限。不会影响你的wordpress，忽略就好。

**创建一个数据库wordpress**

```
# 登录数据库
mysql -u root -p
# 输入密码默认的话就是root，否则就是你自己之前设置的那个
# 登录进来之后，看到这样一些东西
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.5.53-log Source distribution
Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.Oracle is a registered trademark of Oracle Corporation and/or itsaffiliates. Other names may be trademarks of their respective owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql> 
# 不用理会上面的，创建我们的数据库，比如名字为wordpress。记得加分号。
mysql> create database wordpress;
# 看一下，有没有我们创建的数据库
mysql> show databases;
# 大概看到如下内容。意味着这一步也没问题。
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| wordpress          |
+--------------------+
4 rows in set (0.01 sec)
# 退出mysql
exit
```

**配置WordPress**

这时候在此通过浏览器访问 `http://IP` 例如 `http://45.32.195.77`，浏览器将自动跳转到`http://45.32.195.77/wp-admin/setup-config.php`，这就是wordpress的配置页面了，看到的内容如下：

访问页面

点击现在就开始。这时候我们看到如下页面:

数据库配置

按照之前设置的，输入如下信息。

```
数据库名：wordpress
用户名：root
密码：root
数据库主机：localhost
表前缀：wp_
```

点击提交。

数据库连接完成

到这一步，基本上就意味着大功告成了，因为后边基本不会出错啦。

点击进行安装按钮。出现下图：

wordpress 设置

按照自己的需求填写，比如我这里填写如下：

wordpress 我的设置

点击安装WordPress按钮，然后登录设置啥的纯页面操作就不在这里过多介绍咯。

主页大概是这样的

## **后期问题解决**

有问题的反馈在此，我会进行补充。

### **主题只显示一个**

原因：php没有权限读取文件目录。

解决方案：编辑php.ini文件中的disable_functions字段，将其中的scandir去掉。

```
# 使用一键安装包安装的php的配置文件路径如下
vi /usr/local/php/etc/php.ini
# 查找disable_functions在当前的底行模式下输入 /disable_functions,便可以找到这样一行
disable_functions = passthru,exec,system,chroot,scandir,chgrp,chown,shell_exec,proc_open,proc_get_status,popen,ini_alter,ini_restore,dl,openlog,syslog,readlink,symlink,popepassthru,stream_socket_server
# 删掉其中的scandir，此处很容易搞乱，所以有必要会使用编辑模式，摁i进入编辑模式。就可以输入删除了。
# 退出编辑模式，并保存退出。esc退出编辑模式，:wq保存退出。
```

*更多的指令看我之前的一个简单的入门笔记吧。[Linux VIM 文本编辑器](https://www.jianshu.com/p/a78ec66b00f1)*

然后记得重启php-fpm服务

```
/etc/init.d/php-fpm restart
```

这样再刷新，就会发现主题不只有一个啦。

## **更多**

如果你使用MarkDown，那么请安装`JetPack`插件，如果你需要语法高亮，请安装`Crayon Syntax Highlighter`。

以后可能会深入研究一下，有机会的话会专门写一篇文章介绍WordPress主题与插件的哈。