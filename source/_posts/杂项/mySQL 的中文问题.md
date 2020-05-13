---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

MySQL的默认编码是 latin1
而这个编码是不识别中文的。

解决方案：
1、
```
sudo nano /etc/mysql/conf.d/mysql.cnf
```
修改如下：
```
[mysqld]
character_set_server = utf8
```

2、（可以不设置）
```
sudo nano  /etc/mysql/mysql.conf.d/mysqld.cnf
```
在 [mysqld] 里添加如下位置：
```
character-set-server = utf8
```

3、
建立数据库时默认数据库编码是latin1
更改方式：
```
alter database <库名> character set utf8;
```
