---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# 服务安装
安装
```shell
sudo yum install vsftpd ftp
```
开机自启
```shell
sudo chkconfig vsftpd on
```
防火墙设置
```shell
sudo firewall-cmd --permanent --add-service=ftp
sudo service firewalld restart
```
# 配置文件
/etc/vsftpd/vsftpd.conf
```
#禁止匿名用户
anonymous_enable=NO
#启用本地用户
local_enable=YES
#启用写权限
write_enable=YES
#用户上传文件的权限设置，反向
local_umask=000
#根目录的设置
local_root=/home/share
#显示目录说明文件
dirmessage_enable=YES

xferlog_enable=YES

connect_from_port_20=YES

xferlog_std_format=YES
#将用户禁锢在主目录，主目录不能有W权限
chroot_local_user=YES
#允许主目录有W权限
allow_writeable_chroot=YES

listen=YES
#监听ip
listen_address=0.0.0.0
#监听端口
listen_port=21

listen_ipv6=NO

pam_service_name=vsftpd
#只允许出现在user_list中的用户访问，user_list文件需自行配置
userlist_enable=YES
userlist_deny=NO

#被动模式，不设置则浏览器无法访问
pasv_enable=YES
pasv_addr_resolve=YES
#配置端口范围
pasv_min_port=20020
pasv_max_port=20020
#j监听地址
pasv_address=0.0.0.0
#是否屏蔽对pasv的安全检查，ftp连接后有问题可以试试打开
#pasv_promiscuous=YES
```
如果打算使用/sbin/nologin用户登录，需要在shells文件中添加一行
/sbin/nologin
```shell
sudo vi /etc/shells
```

打开对应端口
```shell
sudo firewall-cmd --permanent --add-port=20020/tcp
```
# 重启
```shell
sudo service vsftpd restart
```
