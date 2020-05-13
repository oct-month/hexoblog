---
date: 2020-03-22 18:34:18
tags:
    - android
---

# 示例
先在drawable目录下新建了一个back.xml文件：
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
    <!-- 背景色 -->
    <solid android:color="#000"/>
    <!-- 边框色 -->
    <stroke android:width="0.5dip" android:color="#000" />
</shape>

```

然后layout目录下新建了一个title.xml文件：
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/title_back"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="top|center"
        android:background="@drawable/back"
        android:text="Back"
        android:textAllCaps="false"
        android:textColor="#fff"
        android:textSize="20dp"
        />
    <Button
        android:id="@+id/title_text"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_gravity="top|center"
        android:layout_weight="1"
        android:background="@drawable/back"
        android:gravity="center"
        android:text="Title Text"
        android:textColor="#fff"
        android:textAllCaps="false"
        android:textSize="20dp"
        />
    <Button
        android:id="@+id/title_edit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="top|center"
        android:background="@drawable/back"
        android:text="Edit"
        android:textAllCaps="false"
        android:textColor="#fff"
        android:textSize="20dp"
        />


</LinearLayout>
```

然后就可以在其它地方用include引用了：
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <include layout="@layout/title"/>

</LinearLayout>
```

另一种引用的方式：
写一个布局的类
```java
package com.example.anothertest;

import android.content.Context;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.LinearLayout;

public class TitleLayout extends LinearLayout
{
    public TitleLayout(Context context, AttributeSet attrs)
    {
        super(context, attrs);
        LayoutInflater.from(context).inflate(R.layout.title, this);
    }
}

```
在xml中这样引用：
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.example.anothertest.TitleLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        />

</LinearLayout>
```


# 隐藏默认的标题栏
由于我做的是一个标题栏，因此还需隐藏AS默认的绿色标题栏：
```java
//第一种
import androidx.appcompat.app.ActionBar;

@Override
protected void onCreate(Bundle savedInstanceState)
{
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_normal);
    ActionBar acbar = getSupportActionBar();
    if(acbar != null)acbar.hide();
}

//第二种
import android.view.Window;

@Override
protected void onCreate(Bundle savedInstanceState)
{
    super.onCreate(savedInstanceState);
    supportRequestWindowFeature(Window.FEATURE_NO_TITLE);
    setContentView(R.layout.activity_normal);
}
```
