---
date: 2019-12-22 11:34:18
tags:
    - 有趣的编程实践
---

# 使用第三方jar包
包名：commons-net-3.6.jar

[下载地址](http://mirror.bit.edu.cn/apache//commons/net/binaries/commons-net-3.6-bin.zip)

# 引入方式
```java
import org.apache.commons.net.ftp.*;
```

# 源代码
```java
import java.io.*;
import java.net.SocketException;
import org.apache.commons.net.ftp.*;

public class FTP
{
    private FTPClient ftpclient;        //ftp连接对象
    private String ip, user, password;  //ftp服务器的ip，用户名，密码
    private int port;                   //ftp服务器的端口
    //初始化
    public FTP(String ip,int port, String user, String password)
    {
        this.ip = ip;
        this.port = port;
        this.user = user;
        this.password = password;
    }
    //连接并获取FTPClient对象
    private FTPClient getFTPClient()
    {
        FTPClient ftpclient = null;
        try {
            ftpclient = new FTPClient();
            System.out.println("连接ftp服务器...");
            ftpclient.connect(ip, port);
            if(!FTPReply.isPositiveCompletion(ftpclient.getReplyCode()))
            {
                System.out.println("连接失败!!!");
                ftpclient.disconnect();
                ftpclient = null;
            }
            else
            {
                System.out.println("登陆ftp服务器...");
                if(!ftpclient.login(user, password))
                {
                    System.out.println("登陆失败!!!");
                    ftpclient.logout();
                    ftpclient.disconnect();
                    ftpclient = null;
                }
                else 
                {
                    ftpclient.setControlEncoding("utf-8");      //更改控制台的编码
                    ftpclient.setFileType(FTPClient.BINARY_FILE_TYPE);  //设置为字节传输
                    ftpclient.enterLocalPassiveMode();      //使用被动模式
                    System.out.println("FTP连接已建立");
                }
            }
        }
        catch(SocketException e) {
            System.out.println(e);
        }
        catch(IOException e) {
            System.out.println(e);
        }
        return ftpclient;
    }
    //断开连接
    private void breakConnect()
    {
        try {
            if(ftpclient.isConnected())
            {
                System.out.println("断开连接...");
                ftpclient.logout();
                ftpclient.disconnect();
            }
        }
        catch(IOException e) {
            System.out.println(e);
        }
        finally {
            ftpclient = null;
        }
    }
    //返回服务器的ftpPath路径下的所有文件名 s[0]放目录名，s[1]放文件名
    public String[][] getListFiles(String ftpPath)
    {
        FTPFile[] files = null;
        String[][] s = null;
        ftpclient = getFTPClient();
        if(ftpclient==null) return s;

        try {
            System.out.println("定位到指定文件夹...");
            if(!ftpclient.changeWorkingDirectory(ftpPath))
            {
                System.out.println("定位ftp目录失败!!!");
                breakConnect();
            }
            else 
            {
                System.out.println("获取文件列表...");
                files = ftpclient.listFiles();
                String file = "";
                String dire = "";
                for(FTPFile f: files)
                {
                    if(f.isFile()) file += f.getName()+"/";
                    else if(f.isDirectory()) dire += f.getName()+"/";
                }
                s = new String[2][];
                s[1] = file.split("/");
                s[0] = dire.split("/");
            }
        }
        catch(IOException e) {
            System.out.println(e);
        }
        return s;
    }
    //把本地的文件upfile上传到ftp服务器的ftpPath路径下，命名为filename，找不到目录并且makeDir为true则会根据ftpPath建立目录
    public boolean uploadFile(String ftpPath, String filename, File upfile, boolean makeDir) 
    {
        boolean flag = false;
        FileInputStream input = null;

        try {
            System.out.println("建立上传文件流...");
            input = new FileInputStream(upfile);
        }
        catch(IOException e) {
            System.out.println("文件上传流建立失败!!!");
            input = null;
            System.out.println(e);
            return flag;
        }

        try {
            ftpclient = getFTPClient();     //连接
            if(ftpclient==null)     //连接失败
            {
                input.close();
                return flag;
            }
            System.out.println("定位到指定文件夹...");
            if(!ftpclient.changeWorkingDirectory(ftpPath))      //更改ftp的目录
            {
                System.out.println("定位ftp目录失败!!!");
                if(makeDir)     //更改失败则级联创建目录
                {
                    System.out.printf("建立目录中... ");
                    ftpclient.changeWorkingDirectory("/");
                    String[] dirs = ftpPath.split("/");
                    for(String dir: dirs)       //找不到文件夹
                    {
                        if(dir!=""&&dir!=null)
                        {
                            System.out.print("/"+dir);
                            ftpclient.makeDirectory(dir);   //创建目录
                            ftpclient.changeWorkingDirectory(dir);
                        }
                    }
                }
                else        //不创建目录
                {
                    input.close();
                    return flag;
                }
            }
            System.out.println("写入文件到ftp："+ftpPath+"/"+filename+"  ...");
            if(ftpclient.storeFile(filename, input)) flag = true;  //将input文件流写到服务器，filename为保存后的文件名
            
            else System.out.println("文件写入失败!!!");
            
            input.close();
            //ftpclient.completePendingCommand();
        }
        catch(IOException e) {
            System.out.println(e);
        }
        finally {
            breakConnect();
        }
        
        return flag;
    }
    //从ftp服务器的ftpPath路径下下载ftpFileName，保存到本地的localPath下，命名为localFileName
    public File downloadFile(String ftpPath, String ftpFileName, String localPath, String localFileName)
    {
        File down = null;

        try {
            ftpclient = getFTPClient();
            if(ftpclient==null) return down;
            System.out.println("定位到指定文件夹...");
            if(!ftpclient.changeWorkingDirectory(ftpPath))      //切换服务器的路径
            {
                System.out.println("定位ftp目录失败!!!");
                breakConnect();
                return down;
            }

            down = new File(localPath+File.separator+localFileName);    //设定本地路径及文件名
            OutputStream os = new FileOutputStream(down);   //实例化输出流
            System.out.println("写入文件到本地："+down.toPath()+"  ...");
            if(!ftpclient.retrieveFile(ftpFileName, os))    //写入文件
            {
                System.out.println("文件写入失败!!!");
                os.close();
                down.delete();
            }
            else os.close();
            //breakConnect();
        }
        catch(IOException e) {
            System.out.println(e);
        }
        finally {
            breakConnect();
        }

        return down;
    }
    //删除ftp服务器下的ftpFileName文件
    public boolean deleteFile(String ftpPath, String ftpFileName)
    {
        boolean flag = false;

        try {
            ftpclient = getFTPClient();
            if(ftpclient==null) return flag;
            System.out.println("定位到指定文件夹...");
            if(!ftpclient.changeWorkingDirectory(ftpPath))
            {
                System.out.println("定位ftp目录失败!!!");
                //breakConnect();
                return flag;
            }
            System.out.println("删除文件...");
            if(!ftpclient.deleteFile(ftpFileName))
            {
                System.out.println("文件删除失败!!!");
            }
            //ftpclient.completePendingCommand();
            flag = true;
        }
        catch(IOException e) {
            System.out.println(e);
        }
        finally {
            breakConnect();
        }

        return flag;
    }
    //把ftp服务器ftpPath路径下的ftpFileName重命名为newName
    public boolean renameFile(String ftpPath, String ftpFileName, String newName)
    {
        boolean flag = false;

        try {
            ftpclient = getFTPClient();
            if(ftpclient==null) return flag;
            System.out.println("定位到指定文件夹...");
            if(!ftpclient.changeWorkingDirectory(ftpPath))
            {
                System.out.println("定位到ftp目录失败!!!");
                return flag;
            }
            System.out.println("重命名文件...");
            if(ftpclient.rename(ftpFileName, newName)) flag = true;
            else System.out.println("重命名文件失败!!!");
        }
        catch(IOException e) {
            System.out.println(e);
        }
        finally {
            breakConnect();
        }

        return flag;
    }
}
```

# 使用方法
```java
public class Main
{
	public static void main(String[] args)
	{
		//提供IP、端口、用户名、密码
		FTP ftp = new FTP("127.0.0.1", 21, "user", "password");	//连接
		//之后便可以
		ftp.某方法(参数);
	}
}
```
