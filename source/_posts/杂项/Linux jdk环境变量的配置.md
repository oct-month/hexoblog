---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

# 谨慎操作
将tar.gz文件解压缩到/usr/soft/中
然后在/etc/profile的最下方添加如下：
```
#java
export JAVA_HOME=/usr/soft/jdk1.8.0_60
export CLASSPATH=.:$JAVAHOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin
```
JAVA_HOME是jdk的安装目录，要填上自己的安装目录

# 提醒
Linux中的环境变量是以 : 分隔的，而不是windows下的 ; 
Linux中引用另一个变量是用 $ ，而windows是用% %
设置PATH时不能覆盖掉原有的系统变量，不然就等着重装系统或者进救援模式吧。
注意大小写哦。
