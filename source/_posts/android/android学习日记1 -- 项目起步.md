---
date: 2020-03-22 11:34:18
tags:
    - android
---

# 创建项目
1、选择 Add No Activity
2、配置gradle，jcenter
[https://blog.csdn.net/weixin_44972911/article/details/102727132](https://blog.csdn.net/weixin_44972911/article/details/102727132)
3、右上角sync 按钮等待项目创建完毕

# 创建活动
app/src/main/java/com.example.*
右键 New-Activity-Empty Activity
勾选Generate Layout File 表示创建一个对应的xml
勾选Launcher Activity 表示设置为主活动

# 创建布局
1、
pp/src/main/res
右键 New-Derictory   新建layout  目录
右键layout  New-xml-layout XML File
2、
布局有两个窗口
Design   预览
Text		  代码
3、
示例
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="test"
        />

</LinearLayout>

```
match_parent  表示和当前父元素一样
wrap_content   表示自适应大小

# 加载布局
打开活动的java 文件
示例：
```java
package com.example.test;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;
import android.view.View;

public class FirstActivity extends AppCompatActivity
{
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.first_layout);      //加载布局
        Button but1 = (Button)findViewById(R.id.button_1);		//引用xml中的元素
        but1.setOnClickListener(
                new View.OnClickListener()
                {
                    @Override
                    public void onClick(View v)
                    {
                        Toast.makeText(FirstActivity.this, "test", Toast.LENGTH_SHORT).show();
                    }
                }
        );
    }
}

```

# 注册活动
所有的活动都要在 app/src/main/AndroidMainfest.xml 中注册才能生效
示例：
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.test">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".FirstActivity"
            android:label="test">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>

</manifest>
```
activity 标签为注册标签
intent-filter 标签中的内容表示将活动注册为主活动
android:label 指定活动中标题栏的内容，给主活动指定的label不仅会成为标题栏中的内容，还会成为启动器中应用程序显示的名称。

# 快捷键
Alt + enter  	可以自动解决import 问题
Ctrl + o		选择重写方法
