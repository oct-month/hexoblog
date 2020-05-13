---
date: 2020-03-22 14:34:18
tags:
    - android
---

# 返回栈
Android中的活动是栈式管理（Task）的，每启动一个新活动，就会将新活动入栈，按back键又会销毁最上面的活动，而Android显示的活动就是栈顶活动。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112171306622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
# 关于生存期的回调方法
onCreate()
onStart()
onResume()
onPause()
onStop()
onDestroy()
onRestart()
可以在类中重写这些方法。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112171910686.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
# 活动被系统回收的处理方式
重写活动的onSaveInstanceState方法，将数据保存到Bundle里.
```java
@Override
protected void onSaveInstanceState(Bundle outState)
{
    super.onSaveInstanceState(outState);
    String tmpdata = "要保存的东西";
    outState.putString("data_key", tmpdata);	//设定数据的键值
}
```
这样，在活动再次创建时，便可从Bundle参数中获取数据了。
```java
@Override
 protected void onCreate(Bundle savedInstanceState)
{
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    if(savedInstanceState != null)
    {
        String tmp = savedInstanceState.getString("data_key"); //根据键值获取数据
        Log.e(TAG, tmp);
    }
}
```

# 活动的启动模式
## standard
默认的启动模式，每当启动一个活动，它就会在返回栈中入栈，并处于栈顶位置。因此栈顶可能会有好几个相同的活动。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112172632395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

## singleTop
在启动活动时发现栈顶已有该活动时不会创建新活动。
但是它只检查栈顶。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112173004218.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
## singleTask
这种模式会检查整个返回栈，如果发现要创建的活动已存在，则会把这个活动之上的所有活动通通出栈。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112173204788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
## singleInstance
这种模式会启用一个新的返回栈来管理这个活动，这样其它的应用程序就可以共同来访问这个活动。
但是按back键可能会有意外的结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191112173444860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)

## 修改启动模式
在AndroidManifest.xml中修改：
```xml
<activity
	android:launchMode="singleTop">
</activity>
```

# 自己管理活动
这是在另一个文件中定义的类，用于管理活动。
这样，你就可以按自己的需求停止活动了。
```java
import android.app.Activity;
import java.util.ArrayList;
import java.util.List;

public class ActivityCollector
{
    public static List<Activity> activities = new ArrayList<>();
    public static void addActivity(Activity activity)
    {
        activities.add(activity);
    }
    public static void removeActivity(Activity activity)
    {
        activities.remove(activity);
    }
    public static void finishAll()
    {
        for(Activity activity: activities)
        {
            if(!activity.isFinishing())
            {
                activity.finish();
            }
        }
    }
}
```
为了配合这个类，在活动中应该这样写：
```java
@Override
protected void onCreate(Bundle savedInstanceState)
{
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ActivityCollector.addActivity(this);
    //...
}

@Override
protected void onDestroy()
{
    super.onDestroy();
    ActivityCollector.removeActivity(this);
}
```


