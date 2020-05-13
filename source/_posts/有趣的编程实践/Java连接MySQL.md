---
date: 2019-12-22 11:34:18
tags:
    - 有趣的编程实践
---

# 第三方的jar包
我用的是 mysql-connector-java-8.0.18.jar
请根据自己的MySQL版本选择适合自己的jar
[下载地址](https://dev.mysql.com/downloads/connector/j/)

# 引入
新版的应该是用第一种
```java
Class.forName("com.mysql.cj.jdbc.Driver");
```
旧版的可能要用第二种
```java
Class.forName("com.mysql.jdbc.Driver");
```

# 源码
根据自己的情况修改参数
```java
import java.sql.*;

public class Mysql
{
    private String user = "user";
    private String password = "password";
    private String dbname = "databasename";
    private String uri = "jdbc:mysql://127.0.0.1:3306/"+dbname+"?useSSL=true&characterEncoding=utf-8";
    private Connection connection;
    private Statement sql;

    public Mysql()
    {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            try {
                System.out.println("连接mysql...");
                connection = DriverManager.getConnection(uri, user, password); //连接数据库
                connection.setAutoCommit(false);                               //关闭自动提交模式
                sql = connection.createStatement();                            //创建查询接口
            }
            catch(SQLException e) {
                connection = null;
                sql = null;
                System.out.println("mysql连接失败!!!");
            }
        }
        catch(ClassNotFoundException e) {
            connection = null;
            System.out.println("mysql模块载入失败!!!");
        }
    }

    public boolean execute(String s)
    {
        try {
            sql.execute(s);
            return true;
        }
        catch(SQLException e) {
            System.out.println("sqlError："+e);
            return false;
        }
    }

    public boolean executeUpdate(String s)
    {
        try {
            sql.executeUpdate(s);
            return true;
        }
        catch(SQLException e) {
            System.out.println("sqlError："+e);
            return false;
        }
    }

    public int lastID()     //获取自增值
    {
        int n = 0;
        try {
            ResultSet rs = sql.executeQuery("select LAST_INSERT_ID()");
            if(rs.next())
            {
                n = rs.getInt(1);
            }
            return n;
        }
        catch(SQLException e) {
            System.out.println("sqlError："+e);
            return 0;
        }
    }

    public void close()             //关闭连接
    {
        try {
            connection.commit();
            System.out.println("断开数据库连接...");
            sql.close();
            connection.close();
        }
        catch(SQLException e) {
            System.out.println("sqlError："+e);
        }
    }
}
```

# 使用
```java
public class Main
{
	public static void main(String[] args)
	{
		Mysql sql = new Mysql();	//连接
		sql.executeUpdate("SQL语句");
		sql.close();				//关闭连接
	}
}
```
功能尚不完善
