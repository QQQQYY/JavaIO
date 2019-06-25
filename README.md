# JavaIO
##JavaIO基础面试题

#### 1. 什么是IO
它是一种数据的流从源头到目的地。比如文件拷贝，输入流和输出流都包括了。输入流是从文件中读取数据到存储到进程`(process)`中，输出流是从进程中读取数据然后写入到目标文件。

#### 2. 字节流与字符流的区别
字节流在JDK1.0中就被引进了，用于操作包含`ASCII`字符的文件。Java也支持其他的字符如`Unicode`为了读取包含`Unicode`字符的文件，Java语言设计者在JDK1.1中引入了字符流。`ACSII`作为`Unicode`的子集，对于英文字符的文件，可以使用字节流也可以使用字符流。

#### 3. Java中流类的超类主要是哪些?
>* java.io.InputStream
>* java.io.OutputStream
>* java.io.Reader
>* java.io.Writer

#### 4. FileInputStream和FileOutputStream是什么?
这是在拷贝文件操作的时候，经常用的两个类。在处理小文件的时候，它们的性能还不错，在大文件是最好使用`BufferedInputStream(或BufferedReader)`和`BufferedOutputStream(或BufferedWriter)`
##### 案列：
```Java
	//实现文件的拷贝
	public class InputAndOutputBuffering{
		public static void main(String[] args){
			//运用Java7新增的 try-with-resource;
			//作用：try-with-resource可以自动关闭资源 
			try(
				FileInputStream fis=new FileInputStream("aaa.txt");
				BufferedInputStream bis=new BufferedInputStream(new FileInputStream(fis);//处理流 ----> 缓冲流  
				FileOutputStream fos=new FileOutputStream("bbb.txt");
				BufferedOutputStream bos=new BufferedOutputStream(fos);
			){
				int temp=0;
				while((temp=bis.read())!=-1){
					bos.write((char)temp);
					System.out.print((char)temp);
				}
			}catch(Exception e){
				e.printStackTrace();	
			}
		}
	}
```

#### 5. 字节流与字符流，你更喜欢使用哪个
个人来说，更喜欢使用字符流，因为他们更新一些。许多在字符流中存在的特性，字节流中不存在。比如使用BufferedReader而不是BufferedInputStreams或DataInputStream，使用newLine()方法来读取下一行，但是在字节流中我们需要做额外的操作。

#### 6.流的分类方式
流的分类方式|分类结果   
:------:|:------:  
按流的方向分|输入流和输出流 
按流的种类分|字节流和字符流 
按流的功能分|节点流和处理流 

#### 7. System.out.println()是什么？
println是PrintStream的一个方法，out是一个静态PrintStream类型的成员变量，System是java.lang包中的类,用于和底层操作系统进行交互。

#### 8. 什么是Filter流？
Filter Stream是一种IO流主要作用是用来对一些存在的流增加额外的功能，像给目标文件增加源文件中不存在的行数，或者增加拷贝的功能。

#### 9. 有哪些可用的Filter流？
在`java.io`包中主要有四个可用的`filter Stream`，两个字节`filter Stream`，两个字符`filter Stream` ，分别是`FilterInputStream`，`FilterOutputStream`，`FilterReader`，`FilterWriter`这些都是抽象基类，不可被实例化。

##### 扩展： 有哪些Filter流的子类？
>* `LineNumberInputStream` 给目标文件增加行号。
>* `DataInputStream`有些特殊的方法如：`readInt()`,`readDouble()`和`readLine()` 等可以读取一个`int`，`double`和一个`String`一次性的。
>* `BufferedInputStream`可以增加性能。
>* `PushbackInputStream`推送要求的字节到内存中。

#### 10. SequenceInputStream的作用？
在拷贝多个文件到一个目标文件的时候非常有用。可以用很少代码实现。
##### 案例
```Java
	public class TwoFiles{
		public static void main(String[] args){

			try(
				//创建两个文件输入流
				FileInputStream fis1=new FileInputStream("a.txt");
				FileInputStream fis2=new FileInputStream("b.txt");
				SequenceInputStream sistream =new SequenceInputStream(fis1,fis2);
				FileOutputStream fos=new FileOutputStream("c.txt");
			){
					int temp=0;
					while((temp=sistream.read())!=-1){
						System.out.println((char)temp); //to print at Dos prompt
						fos.write((char)temp);//to write to file
					}
			}catch(Exception e){
				e.printStankTrace();
			}
			
		}
	}
```
#### 11. 操作流的流程
>* 选择目标源（即目标文件）。
>* 选择流工具（即选哪个流来实现）。
>* 选择操作方式（是输入到程序，还是输出到文件，是一个一个字符的操作，还是一行一行的操作，还是一块一块数据操作）。
>* 释放资源（即调用 `close()`方法）。

#### 12. 说说PrintStream和PrintWriter
他们两个的功能相同，但是属于不同的分类。字节流和字符流。他们都有`println()`方法。

#### 13. 在拷贝文件时，哪种流可以提升性能
在字节流的时候：使用`BufferedInputStream`和`BufferedOutputStream`。
在字符流的时候：使用`BufferedReader`和`BufferedWriter`。

#### 14. 说说管道流（Piepd Stream）
有四种管道流，分别是`PiepdInputStream`，`PiepdOutputStream`，`PiepdReader`，`PiepdWriter`，他们在多个线程或进程中传递数据的时候管道流非常有用。

#### 15. 说说File类
它不是IO流，也不属于文件操作，它主要用于知道一个文件的属性。如文件的大小、文件的权限等权限。

#### 16. 说说RandomAccessFile
它是`java.io`包下的一个特殊的类，既不是输入流也不是输出流，它两者都可以做到。它是Object的直接子类。通常来说，一个流只要一个功能，要么读，要么写。但是`RandomAccessFile`既可以读文件、也可以写文件。`DataInputStream`和`DataOutputStream`中有的方法，在`RandomAccessFile`中也可以有。


### 总结 Java输入/输出流体系中常用的流分类
|   分类   |   字节输入流   |   字节输出流   |   字符输入流   |   字符输出流   |
|:----:|:----:|:----:|:----:|:----:|
|抽象基类|FileInputStream|FileOutputStream|Reader|Writer|
|访问文件|FileInputStream|FileOutputStream|FileReader|FileWriter|
|访问数组|ByteArrayInputStream|ByteArrayOutputStream|CharArrayReader|CharArrayWriter|
|访问管道|PiepdInputStream|PiepdOutputStream|PiepedReader|PiepedWriter|
|访问字符串|--|--|StringReader|StringWriter|
|缓冲流|BufferedInputStream|BufferedOutputStream|BufferedReader|BufferedWriter|
|转换流|--|--|InputStreamReader|OutputStreamWriter|
|对象流|ObjectInputStream|ObjectOutputStream|--|--|
|抽象基类|FilterInputStream|FilterOutputStream|FilterReader|FilterWriter|
|打印流|--|PrintStream|--|PrintWriter|
|推回输入流|PushbackInputStream|--|PushbackReader|--|
|特殊流|DataInputStream|DataOutputStream|--|--|




 ### 这些知识点有一部分来自于知乎的学习，有一部分来自于《疯狂Java讲义》的学习，还有一些是来自于视频的学习，感谢他们，正因为有了知乎这个平台，有了作者写了这本书本，有了老师拍的这些学习视频，我才能知道这么多关于JavaIO的知识点，谢谢!

