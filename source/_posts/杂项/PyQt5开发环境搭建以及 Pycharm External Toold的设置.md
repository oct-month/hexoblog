---
date: 2020-05-13 09:48:18
tags:
    - 杂项
---

# 安装依赖
由于pyqt5-tools依赖的pyqt5版本不是最新，因此在主环境中安装pyqt5-tools，在虚环境中安装 pyqt5 和 pyqt5-stubs。
```sh
# 主环境
pip3 install pyqt5-tools
```
```sh
# （虚环境）使用pipenv工具安装
pipenv install pyqt5 pyqt5-stubs --skip-lock
```

# 安装pycharm
[官方下载地址](https://www.jetbrains.com/zh-cn/pycharm/download/#section=windows)
pycharm有专业版和社区版，做pyqt5的开发社区版完全够了。如果愿意花钱或者是学生的话可以用专业版。

# External Tools的设置
pycharm中有一个External Tools的功能，我们可以把QtDesigner，和pyUIC添加进去。
打开settings->Tools->External Tools
在这里可以添加扩展工具

1、QtDesigner的设置大概像这样：
Name字段自取，Program改为designer.exe程序所在位置， Working directory设置为\$FileDi\$即可。
designer.exe是在安装了pyqt5-tools之后才有的，一般在 "用户目录"\AppData\Local\Programs\Python\Python37\Lib\site-packages\pyqt5_tools\Qt\bin\designer.exe下。
 ![QtDesigner的设置](https://img-blog.csdnimg.cn/20200513074924871.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
设置好以后就可以在pycharm左侧的文件树中右键->External Tools直接打开了。

2、PyUIC的设置大概像这样
Name字段自取，Program设置为python.exe所在的位置，一般是 "用户目录"\AppData\Local\Programs\Python\Python37\python.exe
Arguments字段设置为 -m PyQt5.uic.pyuic -o \$FileNameWithoutExtension\$.pyw \$FileName\$，然后Working directory设置为\$FileDir\$。
![PyUIC的设置](https://img-blog.csdnimg.cn/20200513075645967.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
设置好后就可以直接右键QTDesigner产生的ui文件，External Tools->PyUIC在同一目录下生成pyw文件了。

# Hello World
用QtDesigner产生一个test.ui文件后，再用PyUIC转换成test.pyw文件
然后主程序大概是这样：
```py
from test import Ui_MainWindow

if __name__ == '__main__':
    app = QApplication(sys.argv)
    main_window = QMainWindow()
    ui = Ui_MainWindow()
    ui.setupUi(main_window)
    main_window.setWindowTitle("test")
    main_window.show()
    sys.exit(app.exec_())
```
运行即可看到界面了。
