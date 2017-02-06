---
layout: post
title: "Linux Mysql yum 安装方式及配置"
categories:
- Linux
- Mysql
tags:
- Linux 
- Mysql

---


##安装mysql 
这里使用5.6，如果需要其他版本，请到[http://dev.mysql.com/downloads/repo/](http://dev.mysql.com/downloads/repo/)下载对应版本后，安装mysql

{% codeblock lang:bash %}
[xjliao@li539-59 ~] sudo wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
[xjliao@li539-59 ~] sudo rpm -ivh mysql-community-release-el6-5.noarch.rpm
[xjliao@li539-59 ~] sudo yum -y install mysql-server
[xjliao@li539-59 ~] sudo yum -y install mysql-devel
[xjliao@li539-59 ~] sudo service mysqld start 
{% endcodeblock %}

##默认设置,修改root用户默认密码
{% codeblock lang:bash %}
[xjliao@li539-59 ~]$ mysql_secure_installation
[xjliao@li539-59 ~]$ sudo service mysqld restart
{% endcodeblock %}

##开启远程连接权限
{% codeblock lang:bash %}
[xjliao@li539-59 ~]$ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 22
Server version: 5.1.73 Source distribution 
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> grant all privileges on *.* to root@'%' identified by 'root';
mysql> flush privileges;
{% endcodeblock %}

##设置mysql服务开机启动
{% codeblock lang:bash %}
[xjliao@li539-59 ~]$ sudo chkconfig mysqld on
[xjliao@li539-59 ~]$ chkconfig --list mysqld
[xjliao@li539-59 ~]$ sudo service mysqld restart
{% endcodeblock %}

