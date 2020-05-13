---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# 安装
下载地址：
[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)
选择 RPM Bundle 版本，里面包含了所有的依赖包。
不过网速可能。。。
建议去百度网盘找。

下载后解压缩，得到一堆的rpm包，安装顺序：
```
rpm -ivh mysql-community-common*.rpm
rpm -ivh mysql-community-libs*.rpm
rpm -ivh mysql-community-client*.rpm
rpm -ivh mysql-community-server*.rpm
```
其中可能包含 comcat 包，好像是用于解决依赖关系的。

如果无法连接mysql服务，可以试试：
```
chmod 777 -R /var/lib/mysql/ 
service mysqld restart 
```

# 改密码
MySQL安装时自动生成了root密码，获取方式：
```
grep 'temporary password' /var/log/mysqld.log
```
输出的最后一串奇奇怪怪的字符就是密码了。

登录后改密码为123456：
```
set global validate_password_policy=0;
set global validate_password_length=1;
alter user 'root'@'localhost' identified by '123456';
```

# 配置文件
位置在 /etc/my.cnf
```
[client]
default_character_set=utf8

[mysqld]
port=3306
collation_server = utf8_general_ci
character_set_server = utf8
```

# 设置远程连接
redhat 的系统是有防火墙的，3306端口默认不开放。
```
firewall-cmd --permanent --add-port=3306/tcp
service firewalld restart
```

