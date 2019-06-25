# JavaIO
##JavaIO����������

#### 1. ʲô��IO
����һ�����ݵ�����Դͷ��Ŀ�ĵء������ļ���������������������������ˡ��������Ǵ��ļ��ж�ȡ���ݵ��洢������`(process)`�У�������Ǵӽ����ж�ȡ����Ȼ��д�뵽Ŀ���ļ���

#### 2. �ֽ������ַ���������
�ֽ�����JDK1.0�оͱ������ˣ����ڲ�������`ASCII`�ַ����ļ���JavaҲ֧���������ַ���`Unicode`Ϊ�˶�ȡ����`Unicode`�ַ����ļ���Java�����������JDK1.1���������ַ�����`ACSII`��Ϊ`Unicode`���Ӽ�������Ӣ���ַ����ļ�������ʹ���ֽ���Ҳ����ʹ���ַ�����

#### 3. Java������ĳ�����Ҫ����Щ?
>* java.io.InputStream
>* java.io.OutputStream
>* java.io.Reader
>* java.io.Writer

#### 4. FileInputStream��FileOutputStream��ʲô?
�����ڿ����ļ�������ʱ�򣬾����õ������ࡣ�ڴ���С�ļ���ʱ�����ǵ����ܻ������ڴ��ļ������ʹ��`BufferedInputStream(��BufferedReader)`��`BufferedOutputStream(��BufferedWriter)`
##### ���У�
```Java
	//ʵ���ļ��Ŀ���
	public class InputAndOutputBuffering{
		public static void main(String[] args){
			//����Java7������ try-with-resource;
			//���ã�try-with-resource�����Զ��ر���Դ 
			try(
				FileInputStream fis=new FileInputStream("aaa.txt");
				BufferedInputStream bis=new BufferedInputStream(new FileInputStream(fis);//������ ----> ������  
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

#### 5. �ֽ������ַ��������ϲ��ʹ���ĸ�
������˵����ϲ��ʹ���ַ�������Ϊ���Ǹ���һЩ��������ַ����д��ڵ����ԣ��ֽ����в����ڡ�����ʹ��BufferedReader������BufferedInputStreams��DataInputStream��ʹ��newLine()��������ȡ��һ�У��������ֽ�����������Ҫ������Ĳ�����

#### 6.���ķ��෽ʽ
���ķ��෽ʽ|������   
:------:|:------:  
�����ķ����|������������� 
�����������|�ֽ������ַ��� 
�����Ĺ��ܷ�|�ڵ����ʹ����� 

#### 7. System.out.println()��ʲô��
println��PrintStream��һ��������out��һ����̬PrintStream���͵ĳ�Ա������System��java.lang���е���,���ں͵ײ����ϵͳ���н�����

#### 8. ʲô��Filter����
Filter Stream��һ��IO����Ҫ������������һЩ���ڵ������Ӷ���Ĺ��ܣ����Ŀ���ļ�����Դ�ļ��в����ڵ��������������ӿ����Ĺ��ܡ�

#### 9. ����Щ���õ�Filter����
��`java.io`������Ҫ���ĸ����õ�`filter Stream`�������ֽ�`filter Stream`�������ַ�`filter Stream` ���ֱ���`FilterInputStream`��`FilterOutputStream`��`FilterReader`��`FilterWriter`��Щ���ǳ�����࣬���ɱ�ʵ������

##### ��չ�� ����ЩFilter�������ࣿ
>* `LineNumberInputStream` ��Ŀ���ļ������кš�
>* `DataInputStream`��Щ����ķ����磺`readInt()`,`readDouble()`��`readLine()` �ȿ��Զ�ȡһ��`int`��`double`��һ��`String`һ���Եġ�
>* `BufferedInputStream`�����������ܡ�
>* `PushbackInputStream`����Ҫ����ֽڵ��ڴ��С�

#### 10. SequenceInputStream�����ã�
�ڿ�������ļ���һ��Ŀ���ļ���ʱ��ǳ����á������ú��ٴ���ʵ�֡�
##### ����
```Java
	public class TwoFiles{
		public static void main(String[] args){

			try(
				//���������ļ�������
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
#### 11. ������������
>* ѡ��Ŀ��Դ����Ŀ���ļ�����
>* ѡ�������ߣ���ѡ�ĸ�����ʵ�֣���
>* ѡ�������ʽ�������뵽���򣬻���������ļ�����һ��һ���ַ��Ĳ���������һ��һ�еĲ���������һ��һ�����ݲ�������
>* �ͷ���Դ�������� `close()`��������

#### 12. ˵˵PrintStream��PrintWriter
���������Ĺ�����ͬ���������ڲ�ͬ�ķ��ࡣ�ֽ������ַ��������Ƕ���`println()`������

#### 13. �ڿ����ļ�ʱ��������������������
���ֽ�����ʱ��ʹ��`BufferedInputStream`��`BufferedOutputStream`��
���ַ�����ʱ��ʹ��`BufferedReader`��`BufferedWriter`��

#### 14. ˵˵�ܵ�����Piepd Stream��
�����ֹܵ������ֱ���`PiepdInputStream`��`PiepdOutputStream`��`PiepdReader`��`PiepdWriter`�������ڶ���̻߳�����д������ݵ�ʱ��ܵ����ǳ����á�

#### 15. ˵˵File��
������IO����Ҳ�������ļ�����������Ҫ����֪��һ���ļ������ԡ����ļ��Ĵ�С���ļ���Ȩ�޵�Ȩ�ޡ�

#### 16. ˵˵RandomAccessFile
����`java.io`���µ�һ��������࣬�Ȳ���������Ҳ����������������߶���������������Object��ֱ�����ࡣͨ����˵��һ����ֻҪһ�����ܣ�Ҫô����Ҫôд������`RandomAccessFile`�ȿ��Զ��ļ���Ҳ����д�ļ���`DataInputStream`��`DataOutputStream`���еķ�������`RandomAccessFile`��Ҳ�����С�


### �ܽ� Java����/�������ϵ�г��õ�������
|   ����   |   �ֽ�������   |   �ֽ������   |   �ַ�������   |   �ַ������   |
|:----:|:----:|:----:|:----:|:----:|
|�������|FileInputStream|FileOutputStream|Reader|Writer|
|�����ļ�|FileInputStream|FileOutputStream|FileReader|FileWriter|
|��������|ByteArrayInputStream|ByteArrayOutputStream|CharArrayReader|CharArrayWriter|
|���ʹܵ�|PiepdInputStream|PiepdOutputStream|PiepedReader|PiepedWriter|
|�����ַ���|--|--|StringReader|StringWriter|
|������|BufferedInputStream|BufferedOutputStream|BufferedReader|BufferedWriter|
|ת����|--|--|InputStreamReader|OutputStreamWriter|
|������|ObjectInputStream|ObjectOutputStream|--|--|
|�������|FilterInputStream|FilterOutputStream|FilterReader|FilterWriter|
|��ӡ��|--|PrintStream|--|PrintWriter|
|�ƻ�������|PushbackInputStream|--|PushbackReader|--|
|������|DataInputStream|DataOutputStream|--|--|




 ### ��Щ֪ʶ����һ����������֪����ѧϰ����һ���������ڡ����Java���塷��ѧϰ������һЩ����������Ƶ��ѧϰ����л���ǣ�����Ϊ����֪�����ƽ̨����������д���Ȿ�鱾��������ʦ�ĵ���Щѧϰ��Ƶ���Ҳ���֪����ô�����JavaIO��֪ʶ�㣬лл!

