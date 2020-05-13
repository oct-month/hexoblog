---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

## 使用putty远程登陆虚拟机以及传文件

1、 安装SSHD: sudo apt-get install openssh-server
2、 连接虚拟机
3、 开始->运行->cmd，在windows下切换到pscp.exe 所在的位置。
 
__1__、本地文件上传到远程服务器
命令：pscp 本机文件路径 root@ xxx.xxx.xxx.xxx:虚拟机路径
__2__、本地目录以及目录中的文件上传到远程服务器
 命令：pscp -r 本机文件路径 root@ xxx.xxx.xxx.xxx:虚拟机路径
 __3__、远程服务器中的文件下载到本地
命令：pscp  root@ xxx.xxx.xxx.xxx:虚拟机路径 本机路径
__4__、远程服务器中的目录以及目录中的文件复制到本地
命令：pscp -r root@ xxx.xxx.xxx.xxx:虚拟机路径 本机文件路径
