---
date: 2019-12-22 11:34:18
tags:
    - 有趣的编程实践
---

# 读取
## 代码
```java
import java.io.*;
import java.util.zip.*;
import java.nio.charset.Charset;

public class zipRead
{
    private ZipFile zipfile;
    private Charset charset;
    
    public zipRead(File file)
    {
        try {
            System.out.println("读取zip文件...");
            zipfile = new ZipFile(file);
            charset = Charset.forName("utf-8");
        }
        catch(IOException e) {
            zipfile = null;
            System.out.println("文件不存在!!!");
        }
    }

    public zipRead(String path)
    {
        try {
            System.out.println("读取zip文件...");
            zipfile = new ZipFile(path);
            charset = Charset.forName("utf-8");
        }
        catch(IOException e) {
            zipfile = null;
            System.out.println("文件不存在!!!");
        }
    }

    public void setCharset(String charset)      //改编码
    {
        this.charset = Charset.forName(charset);
    }

    public boolean isExists(String name)       //测试zip中name文件是否存在
    {
        ZipEntry entry = zipfile.getEntry(name);
        if(entry!=null)return true;
        else return false;
    }

    public long getSize(String name)            //返回文件大小B
    {
        ZipEntry entry = zipfile.getEntry(name);
        if(entry==null)return 0;
        return entry.getSize();
    }
    
    public String getContent(String name)      //获取zip文件中name文件的文本内容，去除头和尾的空白字符
    {
        String s = "";
        ZipEntry entry = zipfile.getEntry(name);
        if(entry==null)return s;
        try {
            InputStreamReader ir = new InputStreamReader(zipfile.getInputStream(entry), charset);
            BufferedReader rd = new BufferedReader(ir);
            String tap = null;
            while((tap=rd.readLine())!=null)
            {
                s += tap+"\n";
            }
            s = s.trim();
            rd.close();
            ir.close();
        }
        catch(IOException e) {
            System.out.println("在zip中找不到文件!!!");
        }
        return s;
    }

    public byte[] getBytes(String name)     //获取zip中name文件的字节流
    {
        byte[] bytes = null;
        ZipEntry entry = zipfile.getEntry(name);
        if(entry==null)return bytes;
        try {
            InputStream in = zipfile.getInputStream(entry);
            ByteArrayOutputStream out = new ByteArrayOutputStream();
            byte[] tap = new byte[1024*10];
            int n = 0;
            while((n=in.read(tap))!=-1)
            {
                out.write(tap, 0, n);
            }
            bytes = out.toByteArray();
        }
        catch(IOException e) {
            System.out.println("无法读出输入流!!!");
        }
        return bytes;
    }

    public InputStream getInputStream(String name)      //获取zip文件中name文件的输入流
    {
        InputStream in = null;
        ZipEntry entry = zipfile.getEntry(name);
        if(entry==null)return in;
        try {
            in = zipfile.getInputStream(entry);
        }
        catch(IOException e) {

        }
        return in;
    }

    public void close()         //关闭zip文件
    {
        try {
            zipfile.close();
        }
        catch(IOException e ) {
        }
    }
}
```

## 使用
```java
public class Main
{
	public static void main(String[] args)
	{
		zipRead read = new zipRead("文件路径");	//初始化
		read.setCharset("GB2312");				//设定编码。默认utf-8
		read.函数调用(参数);
		read.close();							//关闭文件
	}
}
```


# 解压缩
## 代码
```java
import java.util.Enumeration;
import java.util.zip.ZipEntry;
import java.util.zip.ZipFile;
import java.io.*;

public class unzip
{
    //把zip解压缩到path下
    public static boolean unzipByFile(File file, String path)   //path后无/
    {
        try {
            ZipFile zip = new ZipFile(file);
            for(Enumeration<?> entries = zip.entries(); entries.hasMoreElements(); )
            {
                ZipEntry entry = (ZipEntry)entries.nextElement();
                String name = entry.getName();
                System.out.println("解压："+name);
                if(entry.isDirectory())
                {
                    File dir = new File(path+File.separator+name);
                    dir.mkdir();
                }
                else 
                {
                    File unfile = new File(path+File.separator+name);
                    if(!unfile.getParentFile().exists())unfile.getParentFile().mkdir();
                    unfile.createNewFile();
                    InputStream in = zip.getInputStream(entry);
                    FileOutputStream fos = new FileOutputStream(unfile);
                    int len;
                    byte[] buf = new byte[1024];
                    while((len=in.read(buf))!=-1)fos.write(buf, 0, len);
                    fos.close();
                    in.close();
                }
            }
            zip.close();
            return true;
        }
        catch(IOException e) {
            return false;
        }
    }
}
```

## 使用
```java
import java.io.*;

public class Main
{
	public static void main(String[] args)
	{
		try {
			File file = new File("文件路径");
			unzip.unzipByFile(file, "（解压到）某文件夹的路径");
		}
		catch(IOException e) {
		}
	}
}
```
