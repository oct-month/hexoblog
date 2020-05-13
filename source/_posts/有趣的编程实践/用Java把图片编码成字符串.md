---
date: 2019-12-22 11:34:18
tags:
    - 有趣的编程实践
---

# 目的
直接把图片以二进制存到数据库中不太合适，存放路径又不方便管理。
若是把图片编码存入，再译码取出。不仅便于管理，也减少了信息泄露的风险。

# 源码
```java
import java.io.*;
import java.util.Base64;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;

public class Img
{
    static private Base64.Decoder decoder = Base64.getDecoder();
    static private Base64.Encoder encoder = Base64.getEncoder();
    //编码图片
    public static String encodeFile(byte[] bytes)
    {
        return encoder.encodeToString(bytes);
    }
    //编码图片
    public static String encodeFile(InputStream in)
    {
        String s = null;
        try {
            System.out.println("读取图片...");
            BufferedImage bi = ImageIO.read(in);
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            ImageIO.write(bi, "png", baos);
            byte[] bytes = baos.toByteArray();
            System.out.println("编码...");
            s = encoder.encodeToString(bytes);
            baos.close();
        }
        catch(IOException e) {

        }
        return s;
    }
    //编码图片
    public static String encodeFile(String path)
    {
        String s = null;
        File file = new File(path);
        try {
            BufferedImage bi = ImageIO.read(file);
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            ImageIO.write(bi, "png", baos);         //把图片的二进制编码传入字节流
            byte[] bytes = baos.toByteArray();
            s = encoder.encodeToString(bytes);      //编码成字符串
            //System.out.println(s);
            baos.close();
        }
        catch(IOException e) {
            System.out.println("找不到文件!!!");
        }
        return s;
    }
    //译码图片
    public static byte[] decodeFile(String s)
    {
        return  decoder.decode(s);
    }
    //写出图片文件，写入path路径下
    public static void loadFile(String imag_bytes, String path)
    {
        try {
            byte[] bytes = decoder.decode(imag_bytes);       //把字符串译码为二进制
            ByteArrayInputStream bais = new ByteArrayInputStream(bytes);
            BufferedImage bi = ImageIO.read(bais);

            File w2 = new File(path);
            ImageIO.write(bi, "png", w2);           //写文件

            bais.close();
        }
        catch(IOException e) {
            System.out.println("写入图片文件失败!!!");
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
		//编码
		String s = Img.encodeFile("图片路径/输入流/byte数组");
		//译码
		byte[] bytes = Img.decodeFile(s);
		//写入文件
		Img.loadFile(s, "保存图片的路径")
	}
}
```

# 注释
这个类是为png格式的图片编写的
要支持其它格式，只要改一下 ImageIO.write() 函数中的 "png" 参数就行
