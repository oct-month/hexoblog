---
date: 2020-03-22 16:34:18
tags:
    - android
---

# TextView
显示一段文字
```xml
<TextView
	 android:layout_width="match_parent"
	 android:layout_height="wrap_content"
	 android:gravity="center_vertical|center_horizontal"
	 android:textSize="24sp"
	 android:textColor="#00ff00"
	 android:text="This is a normal activity"
	 />
```

# Button
按钮
```xml
<Button
	android:id="@+id/buNo"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:text="Button"
	android:textAllCaps="false"
	/>
```

# EditText
文本输入框
```xml
<EditText
	android:id="@+id/edit_text"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:hint="请输入..."
	android:maxLines="2"
	 />
```
在主程序中获取文本值：
```java
EditText edit_text = (EditText)findViewById(R.id.edit_text);
String value = edit_text.getText().toString();
```

# ImageView
插入图片
```xml
<ImageView
	android:id="@+id/image_view"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:src="@drawable/img_1"
	/>
```
在主程序中更改图片来源：
```java
ImageView image = (ImageView)findViewById(R.id.image_view);
image.setImageResource(R.drawable.img_2);   //更改图片来源
```

# ProgressBar
进度条
默认是转圈圈，可以通过style设置为条条
```xml
<ProgressBar
	android:id="@+id/pro_bar"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	style="?android:attr/progressBarStyleHorizontal"
	android:max="100"
	/>
```
设置显示和隐藏的方法（也适用于其它控件）
```java
ProgressBar probar = (ProgressBar)findViewById(R.id.progress_bar);
if(probar.getVisibility() == View.GONE)
	probar.setVisibility(View.VISIBLE);
else probar.setVisibility(View.GONE);
```
View.GNOE是移除
View.INVISIBLE则是不可见，没有移除
View.VISIBLE是可见

更改进度条的方式：
```java
int pro = probar.getProgress();
pro += 10;
probar.setProgress(pro);
```

屏蔽用户与界面交互的方法：
```java
probar = new ProgressBar(NormalActivity.this);
//屏蔽
getWindow().setFlags(WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE, WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE);
probar.setVisibility(View.VISIBLE);
//恢复
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE);
probar.setVisibility(View.GONE);
```

# AlertDialog
在当前界面弹出一个对话框，屏蔽掉其它控件的交互能力。
用于提示一些很重要的内容或者警告信息。
```java
AlertDialog.Builder dialog = new AlertDialog.Builder(NormalActivity.this);
dialog.setTitle("你好hentai");    //设置标题
dialog.setMessage("有点重要的事和你说。");    //设置内容
dialog.setCancelable(false);    //能否取消
//设置俩按钮的点击事件和文字
dialog.setPositiveButton("我知道了", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which)
    {
        Toast.makeText(NormalActivity.this, "OK", Toast.LENGTH_SHORT).show();
    }
});
dialog.setNegativeButton("滚你md", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which)
    {
        Toast.makeText(NormalActivity.this, "我可以给你当羊，但你要给我草！", Toast.LENGTH_SHORT).show();
    }
});
dialog.show();  //显示
```



