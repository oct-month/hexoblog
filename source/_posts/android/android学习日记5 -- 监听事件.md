---
date: 2020-03-22 15:34:18
tags:
    - android
---

# 注册监听器
```java
Button button = (Button)findViewById(R.id.button);
button.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v)
	{
		//...
	}
}
```
传入的参数是一个View.onClickListener对象。
所以还有另一种写法：
# 实现View.onClickListener接口
```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener
{
	@Override
    protected void onCreate(Bundle savedInstanceState)
	{
		//...
		Button startNormal = (Button)findViewById(R.id.start_normal_activity);
        startNormal.setOnClickListener(this);
        Button startDialog = (Button)findViewById(R.id.start_dialog_activity);
        startDialog.setOnClickListener(this);
        Button startagain = (Button)findViewById(R.id.start_again);
        startagain.setOnClickListener(this);
        //...
	}

    @Override
    public void onClick(View v)
    {
        Intent intent;
        switch(v.getId())
        {
            case R.id.start_normal_activity:
                intent = new Intent(MainActivity.this, NormalActivity.class);
                startActivity(intent);
                break;
            case R.id.start_dialog_activity:
                intent = new Intent(MainActivity.this, DialogActivity.class);
                startActivity(intent);
                break;
            case R.id.start_again:
                intent = new Intent(MainActivity.this, MainActivity.class);
                startActivity(intent);
                break;
            default:
                break;
        }
    }	
}
```
