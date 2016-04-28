---
title: Django+sqlite3+apache2+wsgi在ubuntu14.04上搭建
date: 2016-04-27 10:50:55
tags: 
- Django
- Python
categories: Django
---
因为不同的版本配置不同，本文仅限在当时配置下完成的，同时也是：
- 一、为自己的配置做个记录，
- 二、为同样google的童鞋做个参考，
- 三、也请各位大牛指点一二。

# 配置 #
1.Python 2.7.6 
> \>>python -V

2.Django 1.9.2 
	在python命令行下：
> \>>import django 
> \>>django.VERSION

3.Apache2 2.4.7(Ubuntu)
> \>>apache2 -V

4.sqlite3 3.8.2
	进入sqlite3命令行下
> \>>.v

# 安装服务器 #
## 首先更新apt ##
```shell
sudo apt-get update
sudo apt-get upgrade
```
## 各种安装 ##
一般而言python是预装的，可以用以上的命令查看版本号。
然后安装apache2, wsgi, [django](https://www.djangoproject.com/download/)(1.6前后数据库更新语句会不同)，sqlite3，
```
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi
sudo pip install Django==1.9.2
sudo apt-get install sqlite3
```

# 设置apahce2文件夹权限 #
在安装完apache2以及wsgi之后：

```
cd /etc/apache2
sudo nano apache2.conf

```

找到全选配置项：
```
<Directory />
        Options FollowSymLinks
        AllowOverride None
        #Require all denied 这个是阻止了所有的请求
        Allow from all #新增 因为我们用它作为服务器，所以允许所有的请求
</Directory>
```
不然在后续启动站点的时候会有：
![](http://i.imgur.com/qujGgX7.png)
# 建立Django项目 #
```
sudo mkdir /home/django
sudo mkdir /home/django
```

我先在home文件下创建了django文件夹来存放等下我们的项目。
```
cd /home/django
django-admin startproject mySite
```
这样我们就创建了我们的项目
![](http://i.imgur.com/UzIWgj3.png)
# 建立WSGI #

## 什么是wsgi ##
PythonWeb服务器网关接口（Python Web Server Gateway Interface，缩写为WSGI)是Python应用程序或框架和Web服务器之间的一种接口，已经被广泛接受, 它已基本达成它的可移植性方面的目标

## 在项目中建立一个wsgi ##
```
sudo nano /home/django/apache/django.wsgi
```
编写以下内容：
```
import os
import sys
path = '/home/django/mySite'
if path not in sys.path:
    sys.path.insert(0, '/home/django/mySite')
os.environ['DJANGO_SETTINGS_MODULE'] = 'mySite.settings'
from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
```
## 建立站点配置文件 ##
```
cd /etc/apache2/site-available
sudo nano mySite.conf
```
编写以下内容
```
<VirtualHost *:80>
	#ServerName
    DocumentRoot /home/django/mySite 
    <Directory /home/django/mySite>  
        Order allow,deny
        Allow from all
    </Directory>
    WSGIDaemonProcess mydjangosite processes=2 threads=15 display-name=%{GROUP}
    WSGIProcessGroup mydjangosite
    WSGIScriptAlias / /home/django/mySite/apache/django.wsgi
</VirtualHost>
```

如果要添加域名可以再ServerName 设置

如果这里使用80端口，那么在site-available文件下找到000-default.conf
修改此文件的端口。

## 启动站点 ##
```
sudo a2ensite mySite
sudo service apache2 reload
```

这个时候就能正常访问站点了
![](http://i.imgur.com/m0vPrzT.png)

# Tips #
查看apache2 的log文件 
```
cd /var/log/apache2
tail error.log
```
