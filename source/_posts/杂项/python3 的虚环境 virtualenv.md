---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

## 虚环境的安装
很简单的一条命令：
```
pip3 install virtualenv
```

## 虚环境的搭建
```
virtualenv venv -p python3
```
该命令会在当前目录下建立一个venv文件夹
venv是默认名称，也可以指定其他名称，单最好用默认的
./venv/bin  下包含了当前虚环境的可执行文件

## 进入虚环境 
```
source ./venv/bin/activate
```
在虚环境中安装的组件会在./venv/lib 目录中，而不会影响系统的python3 环境
## 退出虚环境 
```
deactivate
```
