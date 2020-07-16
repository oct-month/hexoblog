---
date: 2020-06-12 18:17:45
tags:
    - 杂项
---

eclipse官方的镜像比较慢，所以采用国内的tuna镜像。

# 查看eclipse版本
eclipse点击help->about eclipse查看版本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180206159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
我这里是2020-3版本

# 登录官网语言包
地址：[http://www.eclipse.org/babel/downloads.php](http://www.eclipse.org/babel/downloads.php)

# 找到对应的包的地址
这里有3个版本，好像没有2020-3版本的语言包，那就选2019-12版本。（可能会有兼容性问题，自行选择是否要尝试）
注意这个地址，接下来就要打开清华的镜像了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180357442.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

# 找到清华镜像地址
打开地址：[https://mirrors.tuna.tsinghua.edu.cn/eclipse/technology/babel/update-site](https://mirrors.tuna.tsinghua.edu.cn/eclipse/technology/babel/update-site)
找到刚才的链接对应的那个位置，一路找下去就行。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180609437.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180704515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
就是这个网址：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180741347.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

# 使用镜像地址安装语言包

然后eclise打开 Help->Install New Software，点击add
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612181009646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

名称这里随便填，位置这里填之前找到的清华的网址。然后点添加。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061218103994.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
Work with 这里选中刚才添加的url，等待它加载一会儿。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612181219378.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
然后在出现的选项里选择这个：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612181311125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
之后就点下一步，各种确定安装就行。
右下角会显示安装进度：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612181443442.png)


如果出现这种提示，选择Install anyway就行。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200612180934431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
之后eclipse会提示重启eclipse，重启就能看到汉化效果了。
