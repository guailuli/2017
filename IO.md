### I/O流的典型使用方式

#### 1.缓冲输入文件

如果想要打开一个文件用于字符输入，可以使用以String或File对象作为文件名的FileInputReader。为了提高速度，我们希望对那个文件进行缓冲，那么我们将所产生的引用传递给一个BufferReader构造器。由于BufferReader也提供readLine()方法，所以这是我们的最终对象和进行读取的接口。当readLine()将返回null时，你就到达了文件末尾。

```java
import java.io.*;
public class BufferedInputFile{
  //Throw exceptions to console:
  public static String read(String filename) throws IOException{
    //Reading input by lines:
    BufferedReader in = new BufferedReader(new FileReader(filename));
    String s;
    StringBuilder sb = new StringBuilder();
    while((s = in.readLine())!=null)
      sb.append(s+"\n");
    in.close();
    return sb.toString();
  }
  public static void main(String[] args)
    throws IOException {
      System.out.println(read("BufferedInputFile.java"));
    }
  }
```

#### 2.从内存输入

从下面的示例中，从BufferedInputFile.read()读入的String结果被用来创建一个String.Reader。然后调用read()每次读取一个字符，并把它发送到控制台。

```java
import java.io.*;
public class MemoryInput{
  public static void main(String[] args) 
  throws IOException{
    StringReader in = new StringReader(BufferedInputFile.read("MemoryInput.java"));
    int c;
    while((c=in.read())!=0)
      System.out.println((char)c);
  }
}
```

#### 3.格式化内存输入

要读取格式化数据，可以使用DataInputStream,它是一个面向字节的I/O类(不是面向字符的)。因此我们必须使用InputStream而不是Reader类。当然，我们可以用InputStream以字节的形式读取任何数据(例如一个文件)。

```java
impor java.io.*;
public class FormattedMemoryInput{
  public static void main(String[] args)
  throws IOException{
    try{
      DataInputStream in = new DataInputStream(new ByteArrayInputStream(BufferedReader.read("FormattedMemoryInput.java").getBytes()));
      while(true)
        System.out.println((cahr)in.readByte());
      
    }catch(EOFException e){
      System.out.println("End of stream");
    }
    
  }
}
```

```java
import java.io.*;
//Testing for end of file while reading a byte at a time
public class TestEOF{
  public static void main(String[] args) throws IOException{
    DataInputStream in = new DataInputStream(new BufferedInputStream(new FileInputStream("TestEOF.java")));
    while(in.available!=0)
      System.out.println((char)in.readByte());
  }
}
```

#### 4.基本的文件输出

FileWrite对象可以向文件写入数据。首先，创建一个与指定文件连接的FileWriter。实际上，我们通常会用BuferedWriter将其包装起来用以缓冲输出。在本例中，为了提供格式化机制，它被装饰成了PrintWriter。按照这种方式创建的数据文件可作为普通文本文件读取。

```java
import java.io.*;
public class BasicFileOutput{
  static String file = "BasicFileOutput.out";
  public static void main(String[] args) throws IOException{
    BufferedReader in = new BufferedReader(
    new StringReader(
    BufferedInputFile.read("BasicFileOutput.java")));
    PrintWriter out = new PrintWriter(
    new BufferedWriter(new FileWriter(file)));
    int lineCount =1;
    String s;
    while  
  }
}
```