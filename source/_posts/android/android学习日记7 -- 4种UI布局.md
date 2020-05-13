---
date: 2020-03-22 17:34:18
tags:
    - android
---

# 线性布局
示例代码：
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <EditText
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:hint="输入一些东西用的。。。"
        />
    <Button
        android:id="@+id/buNo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textAllCaps="false"
        android:text="Button 1"/>

</LinearLayout>
```
其中的android:orientation="vertical" 表示垂直（从上到下）排列
android:orientation="horizontal" 表示水平（从左到右）排列

# 相对布局
示例：
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/bu1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:textAllCaps="false"
        android:text="Button 1"
        />
    <Button
        android:id="@+id/bu2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_alignParentBottom="true"
        android:textAllCaps="false"
        android:text="Button 2"
        />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/bu1"
        android:layout_toRightOf="@id/bu1"
        android:textAllCaps="false"
        android:text="Button 3"
        />

</RelativeLayout>
```
这里的布局都是相对其它控件而言的，可以相对父元素，也可以相对其它控件。

# 帧布局
示例：
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="This is TextView"
        />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="This is a button" />

</FrameLayout>
```
所有的控件都会默认摆放在左上角，后添加的会压在已有的控件上。


# 百分比布局
先要在app目录下的build.gradle文件中添加依赖：
```gradle
implementation 'androidx.percentlayout:percentlayout:1.0.0'
```
然后gradle sync同步一下

示例:
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.percentlayout.widget.PercentFrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:layout_gravity="left|top"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:textAllCaps="false"
        android:gravity="center"
        android:text="Button 1"
        />

    <Button
        android:layout_gravity="right|top"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:textAllCaps="false"
        android:gravity="center"
        android:text="Button 2"
        />

    <Button
        android:layout_gravity="left|bottom"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:textAllCaps="false"
        android:gravity="center"
        android:text="Button 2"
        />

    <Button
        android:layout_gravity="right|bottom"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:textAllCaps="false"
        android:gravity="center"
        android:text="Button 2"
        />

</androidx.percentlayout.widget.PercentFrameLayout>
```

# 打开AS时的默认布局
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".test">

    <ImageView
        android:id="@+id/title_bg"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        app:layout_constraintTop_toTopOf="parent"
        android:background="@mipmap/ic_launcher"
        />
    
    <ImageView
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:src="@mipmap/ic_launcher_round"
        app:layout_constraintTop_toBottomOf="@id/title_bg"
        app:layout_constraintBottom_toBottomOf="@id/title_bg"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginStart="20dp"
        />

</androidx.constraintlayout.widget.ConstraintLayout>
```
这是一个新布局，也是AS默认的布局。
还在研究。。。。。
