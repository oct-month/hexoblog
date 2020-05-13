---
date: 2019-12-22 11:34:18
tags:
    - 有趣的编程实践
---

# 游戏截图

![截图](https://img-blog.csdnimg.cn/20190430130627792.?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjkxMQ==,size_16,color_FFFFFF,t_70)
# 游戏说明
- 标准的W S A D 移动方式，空格射子弹，子弹数有限，击毁一架敌机+1。按P或Q暂停以及退出操作。
- score:后是当前分数，zidan:是剩余的子弹数。
- 相关的游戏参数可在程序的宏定义处修改。
# 源程序

```javascript
#include<conio.h>
#include<windows.h>
#include<ctime>
#include<iostream>
#include<algorithm>
using namespace std;
#define high 20//游戏高 
#define wide 27//游戏宽 
#define dijisu 5//敌机数 
#define v0 24//敌机速度（越大越小）
#define ZZ 30//初始子弹数 
int wox,woy;
struct zidanjih
{
	int y;
	int x;
}zid[high],dij[dijisu];
struct Rule
{
	bool operator()(const zidanjih &S1,const zidanjih &S2)
	{
		return S1.y>S2.y;
	}
};
int ming;
int score;
int speed;//敌机速度，越大越小 
int z;
char tu[high][wide];
void pr()
{
	HANDLE han=GetStdHandle(STD_OUTPUT_HANDLE);//获取句柄
	COORD po;
	po.X=0;
	po.Y=0;
	SetConsoleCursorPosition(han,po);
	for(int i=0;i<high;i++)
	{
		for(int j=0;j<wide;j++)
			putchar(tu[i][j]);
		putchar('\n');
	}
	printf("score: %d \tzidan: %d \n",score,z); 
}
void start()
{
	system("cls"); //清屏
	speed=v0; 
	memset(zid,0,sizeof(zid));
	srand(time(NULL));
	for(int i=0;i<dijisu;i++)
	{
		dij[i].y=-i;
		dij[i].x=rand()%(wide-2)+1;
	}
	wox=wide/2;
	woy=high-2;
	ming=1;
	score=0;
	z=ZZ;
	CONSOLE_CURSOR_INFO inf={1,0};
	SetConsoleCursorInfo(GetStdHandle(STD_OUTPUT_HANDLE),&inf);
	/*初始化地图*/
	for(int i=0,j=0;j<wide;j++)
		tu[i][j]='#';
	for(int i=1;i<high-1;i++)
	{
		tu[i][0]='#';
		tu[i][wide-1]='#';
	}
	for(int j=0;j<wide;j++)
		tu[high-1][j]='#';
	for(int i=1;i<=high-2;i++)
		for(int j=1;j<=wide-2;j++)
			tu[i][j]=' ';
	tu[woy][wox]='+';
	pr();
	COORD po;
	po.X=(wide-13)/2+1;
	po.Y=high/2;
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),po);
	printf("Loading......");
	Sleep(1000);
}
void zide(int y,int x)
{
	if(y>1)
	{
		int i;
		for(i=0;zid[i].y;i++);
		zid[i].y=y-1;
		zid[i].x=x;
		if(i)sort(zid,zid+high,Rule());
	}
}
void shanghai()
{
	for(int i=0;i<dijisu;i++)
	{
		for(int j=0;zid[j].y;j++)
		{
			if(dij[i].y==zid[j].y||dij[i].y==zid[j].y+1)
			{
				if(dij[i].x==zid[j].x)
				{
					dij[i].y=-1;
					dij[i].x=rand()%(wide-2)+1;
					zid[j].y=0;
					sort(zid,zid+high,Rule());
					score++;
					z++;
				}
				break;
			}
		}
		if(dij[i].x==wox&&dij[i].y==woy)ming=0;
	}
} 
int within()
{
	if(kbhit())
	{
		char ch=getch();
		switch(ch)
		{
			case 'w':
			case 'W':
			case 72:if(woy>1)woy--;break;
			case 's':
			case 'S':
			case 80:if(woy<high-2)woy++;break;
			case 'a':
			case 'A':
			case 75:if(wox>1)wox--;break;
			case 'd':
			case 'D':
			case 77:if(wox<wide-2)wox++;break;
			case ' ':if(z){zide(woy,wox);z--;}break;
			case 'q': 
			case 'p':return 1; 
		}
	}
	return 0;
}
void without()
{
	for(int i=1;i<high-1;i++)
		for(int j=1;j<wide-1;j++)
			tu[i][j]=' '; 
	tu[woy][wox]='+';
	shanghai();
	for(int i=0;i<dijisu;i++)
	{
		if(dij[i].y>0)tu[dij[i].y][dij[i].x]='*';
		if(!speed)dij[i].y++;
		if(dij[i].y==high-1)
		{
			dij[i].y=0;
			dij[i].x=rand()%(wide-2)+1;
		}
	}
	if(!speed)speed=v0;
	for(int i=0;i<high;i++)
	{
		if(!zid[i].y)break;
		tu[zid[i].y][zid[i].x]='|';
		zid[i].y--;
	}
	speed--;
}
int youzidan()
{
	for(int i=1;i<high-2;i++)
		for(int j=1;j<wide-1;j++)
			if(tu[i][j]=='|')return 0;
	return 1;
}
int main()
{
	/*窗口最大化*/
	system("title 打飞机");
	HWND window;
	window=FindWindow(NULL,"打飞机");
	ShowWindow(window,SW_MAXIMIZE);
	HANDLE han=GetStdHandle(STD_OUTPUT_HANDLE);
	COORD po;
	CONSOLE_CURSOR_INFO inf={1,0};
	char a('\0');
	while(1)
	{
		start();
		while(1)
		{
			if(!ming||(!z&&youzidan()))break;
			if(within())
			{	
				po.X=(wide-29)/2+1;
				po.Y=high/2;
				SetConsoleCursorPosition(han,po);
				printf("Game pause!按q退出，按p继续。");
				while(1)
				{
					a=getch();
					if(a=='p'||a=='q')break;
				}
				SetConsoleCursorInfo(han,&inf);
				if(a=='q')break;
			}
			without();
			pr();	
		}
		if(a=='q')return 0;
		po.X=(wide-28)/2;
		po.Y=high/2;
		SetConsoleCursorPosition(han,po);
		printf("Game Over!按q退出，按p继续。");
		while(1)
		{
			a=getch();
			if(a=='q')return 0;
			else if(a=='p')break; 
		} 
	}
	return 0;
} 
```
# 备注
- 如果是用VC编译器，编译可能会报错，建议使用Dev-C或Code::Blocks。
- 如果发现程序有Bug，欢迎在评论区留言。
- 如果喜欢这篇文章，记得点个赞哦。(>▽<)

