# IO流

## 本节内容：

- 运用File类进行文件操作？
- 理解流，标准输入/输出流的概念？
- 运用FileInputStream和FileOutputStream类读写文本文件
- 运用BufferedReader和BufferedWriter类读写文本文件
- 运用DataInputStream和DataOutputStream类读写二进制文件
- 序列化&反序列化

## section 1 文件操作

**文件的概念：**

文件可认为是相关记录或放在一起的数据的集合

**File类：**

表示文件或者目录

**构造方法：**

File file = new File();

**重要方法：**

file.exists()
file.isFile()
file.isDirectory()
file.getName()
file.getPath()
file.getAbsolutePath()
file.lastModified()
file.length() 

### 演示案例1：递归现实文件夹下内容

```
import java.io.File;
import java.util.ArrayList;
import java.util.List;
public class ListDirectory {
    public static void showDirectory(File file){
        File[] files = file.listFiles();
        for(File a:files){
            System.out.println(a.getAbsolutePath());
            if(a.isDirectory()){
                showDirectory(a);
            }
        }
    }

    public static void main(String[] args) {
    File file = new File("E:\\aaa");    
    showDirectory(file);
    }
}
```

## section 2 字节流

**什么是流：**

流是指一连串流动的字符,是以先进先出方式发送信息的通道

![流](markdown-image\流.PNG)



**流的分类：**

字节流：InputStream OutputStream
   8 位 

字符流：  Reader   Writer
   16 位 Unicode

###  演示案例1 使用FileInputStream读取文件

**关键代码：**

File file = new File()

FileInputStream fis = new FileInputStream(file);

int c = fis.read()

while(c != -1){

(char)c

c = fis.read()

}



### 演示案例2 使用FileOutputStream写文件

**关键代码：**

FileOutputStream fos = new FileOutputStream()

String str ="好好学习Java";
byte[] words  = str.getBytes();
fos.write(words, 0, words.length);
fos.close(); 



### 演示案例3  拷贝文件

结合案例1，案例2 进行文件拷贝操作

## Section 3 字符流

演示案例1 使用FileReader读取文件

演示案例2 使用FileWriter写入文件

演示案例3 使用BufferedRead读取文件

关键代码：

readLine()

演示案例4 使用BufferedWriter写入文件

关键代码：

bw.newLine();

bw.flush()

bw.close()

演示案例5 使用缓冲流复制文件，文件名由命令行传入

### Section 4 读取二进制文件

演示案例1 使用DataOutputStream写入二进制文件

演示案例2 使用DataInputStream读取二进制文件



### Section 4 序列化和反序列化

**序列化：**

一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。

**序列化的实现：**

将需要被序列化的类实现Serializable接口，然后使用一个输出流(如：FileOutputStream)来构造一个ObjectOutputStream(对象流)对象，接着，使用ObjectOutputStream对象的writeObject(Object obj)方法就可以将参数为obj的对象写出(即保存其状态)，要恢复的话则用输入流。

#### 演示案例1 序列化与反序列化

```
public class Cat implements Serializable {
        private String name;
        public Cat () {
                this.name = "new cat";
        }
        public String getName() {
                return this.name;
        }
        public void setName(String name) {
                this.name = name;
        }
}

```

```
Cat cat = new Cat();
try {  FileOutputStream fos = new FileOutputStream("catDemo.out");
          ObjectOutputStream oos = new ObjectOutputStream(fos);
          System.out.println(" 1> " + cat.getName());
          cat.setName("My Cat");                        
          oos.writeObject(cat);
          oos.close();                        
} catch (Exception ex) {  ex.printStackTrace();   }
try { 
         FileInputStream fis = new FileInputStream("catDemo.out");
         ObjectInputStream ois = new ObjectInputStream(fis);
         cat = (Cat) ois.readObject();
         System.out.println(" 2> " + cat.getName());
         ois.close();
} catch (Exception ex) {}

```

## 内容总结：

- File 类用于访问文件系统
- 流是指一连串流动的字符,是以先进先出方式发送信息的通道
- 流可以分为输入输出流，也可以分为字节流和字符流
- 运用FileInputStream和FileOutputStream可以读写文本文件
- 运用BufferedReader和BufferedWriter也可以读写文本文件，且性能较高
- 运用DataInputStream和DataOutputStream可以读写二进制文件
- 序列化需要实现接口Serializable 。

