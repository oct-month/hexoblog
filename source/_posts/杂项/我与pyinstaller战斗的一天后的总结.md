---
date: 2020-05-13 09:51:18
tags:
    - 杂项
---

# 遇到的打包不成功的原因
1、setuptools的版本太高，出现脚本执行失败的错误
2、第三方库有自己用到的其它文件，比如 .json .txt .html，pyinstaller打包的时候不会检测这些文件，出现找不到文件的错误
3、缺少一些库，比如 pypiwin32之类的与系统相关类库

# 解决方式
这应该能解决大多数问题
1、尝试将setuptools降低至44.0.0版本
1、pyinstaller打包时候不要用-F选项，这样有路径问题可以自行解决
2、打包时候可以用-c选项显示命令框，以便查看报错信息查错，确认无错后再用-w选项屏蔽命令框
3、报错显示找不到文件的话，去库文件里找到这些文件，然后复制粘贴到对应的报错路径下。建议将这个目录下的文件都放过去，第三方库用到的文件一般都在这里。
4、打包前将上次打包产生的文件全部删掉


# 战斗的过程

## jieba
打包运行后报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513092351638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
可以看到是缺少了dict.txt文件，dist/app是我们生成的exe的位置，只要在这里建立一个jieba文件夹，再把dict.txt复制过来就行。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513092544634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
可以看到在sites-packages/jieba目录下找到了dict.txt文件，把它复制过去在运行试试
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513092804972.png)
报错信息已经改变，我们再去找idf.txt文件
找到后再放到报错信息所指的目录下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513092842872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
问题解决！



## pyecharts
打包运行后报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513093002929.png)
还是找到对应文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513093120568.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
可以看到json文件不只一个，我们全部复制过去，py文件不要复制

再次运行报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513094621706.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
再找到对应文件，可以看到有很多，而且都不是py文件，那就全部复制过去
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513094645240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
问题解决！

