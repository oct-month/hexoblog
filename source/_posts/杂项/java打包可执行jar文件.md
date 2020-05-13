---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# 示例
## 文件夹结构（仅为示例）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191108205247400.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
## 在caculat目录外编写一个 mf 文件：
test.mf  :
```
Manifest-Version: 1.0
Main-Class: caculat.run
Created-By: 1.8
```
其中的Main-Class: 指定了jar 包中的主类


## 然后在caculat 目录外运行命令：
```
jar -cvfm caculat.jar test.mf caculat\*.class caculat\stack\*.class
```
caculat.jar 是生成的包名，test.mf 即编写的打包信息，后面是打包要包括的.class文件。
注：如果是Linux系统，要把 \ 替换为 / 。

## 运行
cmd命令
```
java -jar caculat.jar
```
便可运行刚才打包的jar 文件

windows下双击jar文件应该也能直接运行。
