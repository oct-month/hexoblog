---
date: 2020-05-13 09:50:18
tags:
    - 有趣的编程实践
---

# MyQListWidget
QListWidget中的要支持拖拽添加和删除item项，则需要继承实现几个方法。
这是我自己写的一个支持双击编辑、拖拽添加文件，拖拽删除的子类。拖拽删除的实现借助了另一个控件。
```py
# listwidget.pyw
from typing import Optional
from PyQt5.QtWidgets import QListWidget, QWidget, QAbstractItemView, QListWidgetItem
from PyQt5.QtGui import QDragEnterEvent, QDropEvent, QDragMoveEvent, QKeyEvent
from PyQt5.QtCore import Qt, QModelIndex


class MyListWidget(QListWidget):
    """支持拖拽的QListWidget"""
    def __init__(self, parent: Optional[QWidget]=None) -> None:
        super().__init__(parent)
        # 拖拽设置
        self.setAcceptDrops(True)
        self.setDragEnabled(True)
        self.setDragDropMode(QAbstractItemView.DragDrop)            # 设置拖放
        self.setSelectionMode(QAbstractItemView.ExtendedSelection)  # 设置选择多个
        self.setDefaultDropAction(Qt.CopyAction)
        # 双击可编辑
        self.edited_item = self.currentItem()
        self.close_flag = True
        self.doubleClicked.connect(self.item_double_clicked)
        self.currentItemChanged.connect(self.close_edit)
    
    def keyPressEvent(self, e: QKeyEvent) -> None:
        """回车事件，关闭edit"""
        super().keyPressEvent(e)
        if e.key() == Qt.Key_Return:
            if self.close_flag:
                self.close_edit()
            self.close_flag = True

    def edit_new_item(self) -> None:
        """edit一个新的item"""
        self.close_flag = False
        self.close_edit()
        count = self.count()
        self.addItem('')
        item = self.item(count)
        self.edited_item = item
        self.openPersistentEditor(item)
        self.editItem(item)

    def item_double_clicked(self, modelindex: QModelIndex) -> None:
        """双击事件"""
        self.close_edit()
        item = self.item(modelindex.row())
        self.edited_item = item
        self.openPersistentEditor(item)
        self.editItem(item)
    
    def close_edit(self, *_) -> None:
        """关闭edit"""
        if self.edited_item and self.isPersistentEditorOpen(self.edited_item):
            self.closePersistentEditor(self.edited_item)

    def dragEnterEvent(self, e: QDragEnterEvent) -> None:
        """（从外部或内部控件）拖拽进入后触发的事件"""
        # print(e.mimeData().text())
        if e.mimeData().hasText():
            if e.mimeData().text().startswith('file:///'):
                e.accept()
        else:
            e.ignore()

    def dragMoveEvent(self, e: QDragMoveEvent) -> None:
        """拖拽移动过程中触发的事件"""
        e.accept()

    def dropEvent(self, e: QDropEvent) -> None:
        """拖拽结束以后触发的事件"""
        paths = e.mimeData().text().split('\n')
        for path in paths:
            path = path.strip()
            if len(path) > 8:
                self.addItem(path.strip()[8:])
        e.accept()

```

# QLabel垃圾桶
在界面中设置一个支持拽入的QLabel，设置背景为垃圾桶
然后拽入后的事件一律accept。

```py
# label.pyw
from typing import Optional
from PyQt5.QtWidgets import QWidget, QLabel, QDialog, QVBoxLayout
from PyQt5.QtGui import QDragEnterEvent, QDropEvent, QDragMoveEvent, QMouseEvent, QPixmap
from PyQt5.QtCore import Qt


class MyLabel(QLabel):
    """可接收拖拽的Label"""
    def __init__(self, parent: Optional[QWidget]=None) -> None:
        super().__init__(parent)
        self.setAcceptDrops(True)

    def dragEnterEvent(self, e: QDragEnterEvent) -> None:
        e.setDropAction(Qt.MoveAction)
        e.accept()

    # def dragMoveEvent(self, e: QDragMoveEvent) -> None:
    #     e.setDropAction(Qt.MoveAction)
    #     e.accept()

    def dropEvent(self, e: QDropEvent) -> None:
        e.setDropAction(Qt.MoveAction)
        e.accept()
```

# 使用示例
```py
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout
from PyQt5.QtGui import QPixmap
from PyQt5.QtCore import Qt

from listwidget import MyListWidget
from label import MyLabel


if __name__ == '__main__':
    app = QApplication(sys.argv)
    main_window = QWidget()

    labelw = MyLabel()
    labelw.setAlignment(Qt.AlignCenter)
    labelw.setPixmap(QPixmap('trash.jpg'))
    listw = MyListWidget()
    
    layout = QVBoxLayout()
    layout.addWidget(labelw)
    layout.addWidget(listw)
    main_window.setLayout(layout)
    
    main_window.setWindowTitle("test")
    main_window.show()
    sys.exit(app.exec_())

```
垃圾桶的图片：
![Trash](https://img-blog.csdnimg.cn/2020051309005233.jpg)
运行结果：
拖拽文件到QListWidget时会出现复制提示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513090155103.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
放下后文件路径便被添加到了item中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513090230913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
选中item拖拽到垃圾桶上便可删除
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513090428621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
双击item可编辑
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051309061279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

