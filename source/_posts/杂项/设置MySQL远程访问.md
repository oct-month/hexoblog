---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# 1、修改配置文件
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
将bind-address = 127.0.0.1注释掉（即在行首加#）
除了注视掉这句话之外，还可以把后面的IP地址修改成允许连接的IP地址。


# 2、删除匿名用户
```
use mysql;
delete from user where user=''";
```

# 3、增加外部用户
```
grant all privileges on db_name.* to 'user'@'%' identified by 'password' with grant option;
sudo service mysql restart
```

## 附：MySQL配置文件位置
```
/etc/mysql/conf.d/mysql.cnf
/etc/mysql/mysql.conf.d/mysqld.cnf
```

## 附：Navicat Premium 12工具的安装
[https://www.cnblogs.com/jpfss/articles/9193967.html](https://www.cnblogs.com/jpfss/articles/9193967.html)
