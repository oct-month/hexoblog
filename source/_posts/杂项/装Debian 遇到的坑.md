---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

1、Debian 安装的时候要网，不然会卡在装软件的步骤，镜像用iso-1
2、Debian 有两个账户，普通账户有些命令是无法使用的，root专用命令在/usr/sbin/ 里面，而普通账户是不包括这个文件夹路径的。
解决方案：sudo ln -s /usr/sbin/* /usr/bin/ 
3、ctrl + alt +t 是不能打开终端的，要设置自定义快捷方式 gnome-terminal
