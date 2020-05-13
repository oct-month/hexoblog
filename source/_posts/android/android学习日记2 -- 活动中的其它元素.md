---
date: 2020-03-22 12:34:18
tags:
    - android
---

# Toast
```java
import android.widget.Toast;
```
```java
Toast.makeText(FirstActivity.this, "test", Toast.LENGTH_SHORT).show();
```
第一个参数为活动本身，第二个为消息内容，第三个是显示时长（Toast.LENGTH_SHORT, Toast.LENGTH_LONG）。

该段代码会弹出一些短小的通知信息 'test' 。

# Menu
1、在res目录下新建一个menu文件夹
2、右键menu, New - Menu resource file
3、输入文件名完成创建 xml
示例：
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id = "@+id/add_item"
        android:title = "Add"/>
    <item
        android:id = "@+id/remove_item"
        android:title = "Remove"/>
    <item
        android:id = "@+id/exit"
        android:title = "exit"/>
</menu>
```
item 标签用来创建具体的一个菜单项
android:id 指定标识符
android:title 指定名称

4、回到主方法的文件
Ctrl + o 选择onCreateOptionsMenu(Menu menu)
重写该方法
示例：
```java
    @Override
    public boolean onCreateOptionsMenu(Menu menu)
    {
        getMenuInflater().inflate(R.menu.main, menu);
        //第一个参数指定文件， 第二个指定添加到哪一个对象
        return super.onCreateOptionsMenu(menu);
        //return true表示允许菜单显示出来
        //return false 则菜单不显示
    }
```

5、让按钮响应事件
重写 onOptionsItemSelected(@NonNull MenuItem item) 方法
示例：
```java
@Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item)
    {
        switch (item.getItemId())
        {
            case R.id.add_item:
                Toast.makeText(FirstActivity.this,"Add",Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(FirstActivity.this,"Remove",Toast.LENGTH_SHORT).show();
                break;
            case R.id.exit:
                finish();		//销毁当前活动
            default:
        }
        return super.onOptionsItemSelected(item);
    }
```

# 销毁当前活动
```java
finish();
```

# 补充
（1）@NotNull：用在基本类型上，不能为null，但可以为空字符串

（2）@NotEmpty：用在集合类上，不能为null，并且长度必须大于0

（3）@NotBlank：只能作用在String上，不能为null，而且调用trim()后，长度必须大于0

（4）@NonNull：在方法或构造函数的参数上使用，生成一个空值检查语句。用于指明所修饰的参数，字段或方法的值不可以为null。


