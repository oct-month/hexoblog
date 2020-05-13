---
date: 2020-03-22 13:34:18
tags:
    - android
---

# 显式intent
```java
Intent intent = new Intent(FirstActivity.this,SecondActivity.class);
//第一个参数为启动活动的Context, 第二个为想要启动的活动的 Class
startActivity(intent);      //启动活动
```
在FIrstActivity的基础上打开SecondActivity
startActivity() 执行intent

# 隐式intent
app/src/res/AndroidManifest.xml
```xml
<activity android:name=".SecondActivity">
     <intent-filter>
            <action android:name="com.example.activitytest.ACTION_START" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="com.example.activitytest.MY_CATEGORY" />
     </intent-filter>
</activity>
```
action标签指明当前活动可以响应“com.example.activitytest.ACTION_START”这个Action。
category标签进一步精确指明。
只有俩标签能同时匹配时，该活动才能响应intent
```java
Intent intent = new Intent("com.example.activitytest.ACTION_START");    //隐式intent
intent.addCategory("com.example.activitytest.MY_CATEGORY");    //添加category
startActivity(intent);      //启动活动
```
startActivity会自动把"android.intent.category.DEFAULT"添加到 intent 中
action只能指定一个，而category可以指定多个

# 调用系统的intent
1、打开系统浏览器
```java
Intent intent = new Intent(Intent.ACTION_VIEW);	 //Android的内置动作
intent.setData(Uri.parse("http://baidu.com"));		//将网址解析为Uri对象，再传入intent 中
startActivity(intent);
```
2、打电话
```java
Intent intent = new Intent(Intent.ACTION_DIAL);
intent.setData(Uri.parse("tel:10086"));
startActivity(intent);
```
# 响应intent
```xml
<intent-filter>
          <action android:name="android.intent.action.VIEW"/>
          <category android:name="android.intent.category.DEFAULT"/>
          <data android:scheme="http"/>
</intent-filter>
```
data标签指定当前的活动可以响应什么类型的数据
android:scheme="http"指定了数据的协议必须是http 协议

# 向下一个活动传递数据
FirstActivity:
```java
String data = "第二个活动";
Intent intent = new Intent(FirstActivity.this,SecondActivity.class);
intent.putExtra("extra_data", data);   //第一个参数是键，第二个是传递的数据
```
SecondActivity:
```java
Intent intent = getIntent();            //获取用于启动本活动的Intent
String data = intent.getStringExtra("extra_data");  //根据键获取String数据
```

# 返回数据给上一个活动
FirstActivity:
```java
startActivityForResult(intent, 1);  //1 为请求码，具有唯一性
```
与startActivity的区别：这种启动活动的方式期望返回一个结果
当SecondActivity被销毁后，会回调上一个活动的onActivityResult方法
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data)
//第一个参数为请求码，第二个为返回的处理结果：Result_OK、Result_CANCEL之类的
//第三个参数为或许携带着数据的intent
{
    super.onActivityResult(requestCode, resultCode, data);
    switch(requestCode)
    {
        case 1:
            if(resultCode == RESULT_OK)
            {
                String returnedData = data.getStringExtra("data_return");
                Toast.makeText(FirstActivity.this, returnedData, Toast.LENGTH_SHORT).show();
            }
           default:
    }
}
```


SecondActiviry:
```java
@Override
public void onBackPressed()	//重写了按Back键的方法
{
    Intent intent = new Intent();
    intent.putExtra("data_return", "你好老二");
    setResult(RESULT_OK, intent);   //向上一个活动返回处理结果和数据
    finish();
}
```
