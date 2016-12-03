# land
test github
IO流
IO技术主要的作用是解决设备和设备之间的数据传输问题。

sun使用了一个File类描述了文件或者文件夹。File类只能读取文件的属性数据，而读取文件内容数据则需要使用IO流技术。

File类的构造方法：
	File（String pathname)  //指定文件或者文件夹的路径创建一个File文件。
	File（File parent,String child) //根据parent抽象路径名和child路径名字，创建一个File对象。
	File (String parent,String child) 

目录分隔符：【\\是因为\有特殊含义】在windows机器上是\    linux上是/
File.seperator
注意：在windows上面\与/都可以使用作为目录分隔符。而且，如果写/的时候只需要写一个即可。可以说windows上面一个/相当于\\


路径问题：
	绝对路径：该文件在硬盘上的完整路径，绝对路径一般都是以盘符开头的。
	相对路径：资源文件相对于当前程序所在的路径。注意：如果程序当前所在的路径和资源文件不是在同一盘下面的，是没法写相对路径的。
	.   当前路径
	..  上一级路径


创建文件：
	createNewFile()	在指定位置创建一个空文件，成功就返回true，如果已存在就不创建然后返回false
	mkdir()			在指定位置创建目录，这只会创建最后一级目录，如果上级目录不存在就抛异常。
	mkdirs()		在指定位置创建目录，这会创建路径中所有不存在的目录。
	renameTo(File dest)	【同级重命名，不同级剪切，而且不同级只能操作文件，不能是文件夹。】重命名文件或文件夹，也可以操作非空的文件夹，文件不同时相当于文件的剪切,剪切时候不能操作非空的文件夹。移动/重命名成功则返回true，失败则返回false。
【如果目标文件与源文件在同一路径下，那么renameTo的作用是重命名，如果不是在同一文件夹，那么renameTo的作用是剪切，而且不能操作文件夹，只能操作文件。】


删除：
	delete()		删除文件或一个空文件夹，如果是文件夹且不为空，则不能删除，成功返回true，失败返回false。
	deleteOnExit()	在虚拟机终止时，请求删除此抽象路径名表示的文件或目录，保证程序异常时创建的临时文件也可以被删除

判断：
	exists()		文件或文件夹是否存在。
	isFile()		是否是一个文件，如果不存在，则始终为false。
	isDirectory()	是否是一个目录，如果不存在，则始终为false。
	isHidden()		是否是一个隐藏的文件或是否是隐藏的目录。
	isAbsolute()	测试此抽象路径名是否为绝对路径名。


获取：
getName()		获取文件或文件夹的名称，不包含上级路径。
getPath()       返回绝对路径，可以是相对路径，但是目录要指定
getAbsolutePath()	获取文件的绝对路径，与文件是否存在没关系
length()		获取文件的大小（字节数），如果文件不存在则返回0L，如果是文件夹也返回0L。
getParent()		返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回null。
lastModified()	获取最后一次被修改的时间。
	文件夹相关：
staic File[] listRoots()	列出所有的根目录（Window中就是所有系统的盘符）
list()				 返回目录下的所有文件或者目录名，包含隐藏文件。对于文件这样操作会返回null。
list(FilenameFilter filter)	返回指定当前目录中符合过滤条件的子文件或子目录。对于文件这样操作会返回null。
listFiles()			返回目录下的文件或者目录对象（File类实例），包含隐藏文件。对于文件这样操作会返回null。
listFiles(FilenameFilter filter)	返回指定当前目录中符合过滤条件的子文件或子目录。对于文件这样操作会返回null。


list与listFiles都是查看目录下的文件夹，推荐使用listFile.因为listFiles返回一个File数组。
对于listFiles的文件过滤程序，推荐使用过滤器的方式。




IO流技术：
解决问题：解决设备与设备之间的数据传输问题。 内存--->硬盘   硬盘--->内存
判断使用输入流还是输出流的依据：以当前程序（内存）作为参照物，观察数据是流入还是流出，如果流出则使用输出流，如果是流入程序则使用输入流。

IO输入流：

IO输出流：

按照处理的单位划分：
	字节流：字节流读取的都是文件中二进制数据，读取到的二进制是不会经过处理的。

	字符流：字符流读取的数据是以字符为单位的，字符流也是读取文件中的二进制数据，不过会把这些二进制转换成我们能识别的字符。
	字符流=字节流+解码；

输入字节流：
-----------| InputStream 所有输入字节流的基类    抽象类
------------------| FileInputStream 读取文件数据的输入字节流
------------------| BufferedInputStream 缓冲输入字节流，缓冲输入字节流的出现主要是为了提高读取文件的其实效率。其实该类内部只不过是维护了一个8Kb的字节数组实现的。

-----------| OutputStream 是所有输出字节流的基类 抽象类
------------------| FileOutputStream 

使用FileInputStream读取文件数据的步骤:
	1.找到需要读取数据的目标文件。
	2.建立通道。
	3.读取文件中的数据。【read(buf)读取的数据已经放到了byte[] buf数组中了。而read方法的返回值是表示本次读取了几个字节数据到字节数组中】用read()会抛出一个IOException，避免读数据的时候硬盘坏了。
	4.关闭资源。



例程：
	//1 读取一个字节     无法读取一个完整的文件 已淘汰
	public static void readTest() throws IOException
	{
		File file=new File("F:\\aaa\\bbb\\b.txt");
		FileInputStream fileInputStream=new FileInputStream(file);
		int content=fileInputStream.read();
		System.out.println((char)content);
		fileInputStream.close();
	}
	
	//2 循环读取数据
	public static void readTest1() throws IOException
	{
		File file=new File("F:\\aaa\\bbb\\b.txt");
		FileInputStream fileInputStream=new FileInputStream(file);
		int content=0;
		while ((content=fileInputStream.read())!=-1)
		{
			System.out.print((char)content);
		}
		fileInputStream.close();
	}
	//3 使用缓冲数组读取数据  //不推荐 缓冲限制
	public static void readTest2() throws IOException
	{
		File file=new File("F:\\aaa\\bbb\\b.txt");
		fileInputStream = new FileInputStream(file);  //fileInputStream是一个静态变量，所以不用声明类型。
		byte[] buf=new byte[3];
		int length=fileInputStream.read(buf);
		
		String contentString=new String(buf,0,length);  //定义参数0到length是为了防止浪费多余的内存空间。【而且此时默认会将数据编码用GBK】
		System.out.println(length+" 内容："+contentString);
		
	}

	//4 循环加上缓冲数组  相对来说效率最高的
	public static void readTest3() throws IOException
	{
		File file=new File("F:\\aaa\\bbb\\b.txt");
		fileInputStream=new FileInputStream(file);
		int length=0;
		byte[] buf=new byte[1024];   //缓冲数组一般是1024的倍数，与计算机的处理倍数有关。理论上，缓冲数组越大，效率越高。
		while ((length=fileInputStream.read(buf))!=-1)
		{
			System.out.println("内容："+new String(buf, 0, length));//要加length，因为read是以覆盖的形式存储的。
		}
	}


问题1：读取一个文件的数据的时候，不关闭资源有什么影响？
	不关闭资源，则会一直占用资源，导致其他程序无法使用该资源。




写数据：
FileOutputStream如何使用：
	1.找到目标文件。
	2.建立数据的输出通道。
	3.把数据转化成字节数组写出。
	4.关闭资源。

注意的细节：
	1.使用FileOutputStream的时候，如果目标文件不存在，那么自动创建目标文件。
	2.使用FileOutputStream写数据的时候，如果目标文件存在，那么会先清空目标文件中的数据，然后在写入数据。
	3.使用FileOutputStream写数据的时候，如果目标文件已经存在，需要在原来数据基础上追加数据的时候应该使用new FileOutputStream（file，true)构造函数，第二个参数为true。
	4.使用FileOutputStream的write方法写数据的时候，虽然接收的是一个int类型的数据，但是真正写出的是一个字节的数据，只是把低八位的二进制数据写出，其他二十四位数据全部丢弃。


每创建一个FileOutputStream的时候，默认情况下FileOutputStream的指针指向了文件的开始位置。每写出一次，指向都会相应移动。【如果有数据需要在FileOutputStream中加第二个个参数true，如果没有数据可以不加第二个参数。】


异常处理：
	【注意：必须先把数据流的声明都为null，此时异常处理才能处理，否则找不到变量。】把try{ }catch(IOException e){ throw new RuntimeException(d); }finally{如果数据流为空，则将数据流关闭。需要相同的异常处理方法，抛出RuntimeException。} 把IOException传递给RuntimeException包装一层，然后再抛出，目的是为了让调用者使用得更加灵活。首先异常不用再声明，而调用者可以处理也可以不处理。

例程：
	public static void copyImage()
	{
		FileInputStream fileInputStream = null;
		FileOutputStream fileOutputStream = null;	
		try
		{
			File file = new File("F:\\aaa\\bbb\\1.jpg");
			File desFile = new File("E:\\1.jpg");
			fileInputStream = new FileInputStream(file);
			fileOutputStream = new FileOutputStream(desFile);
			byte[] buf = new byte[1024];
			int length = 0;
			while ((length = fileInputStream.read(buf)) != -1)
			{
				fileOutputStream.write(buf, 0, length);
			}
		} catch (Exception e)
		{
			System.out.println("failed to open file!");
			throw new RuntimeException(e);

		} finally
		{
			try
			{
				if (fileInputStream != null)
				{
					System.out.println("close fileInputStream successful!");
					fileInputStream.close();
					
				}
			} catch (Exception e2)
			{
				System.out.println("failed to close fileInputStream!");
				throw new RuntimeException(e2);
			} finally
			{
				try
				{
					if (fileOutputStream!=null)
					{
						System.out.println("close fileOutputStream successful!");
						fileOutputStream.close();
					}
				} catch (Exception e3)
				{
					System.out.println("failed to close fileOutputStream!");
					throw new RuntimeException(e3);
					
				}
			}
		}

	}



使用BufferedInputStream的步骤：
	1.找到目标文件。
	2.

注意：凡是缓冲流都不具备读写文件能力！
创建BufferedInputStream需要传递FileInputStream，是因为缓冲流本身是不具备读文件的能力，所以需哟啊借助FileInputStream来读文件数据。

FileInputStream与BufferedInputStream都是读取一个字节的数据，那么高效率从何而来？
因为BufferedInputStream会一次性将硬盘中的数据以8Kb为单位放到内存中，然后程序在到内存中依次读取数据，知道8Kb读完，然后再次重装8Kb的数据到内存。而程序到内存的读取速度是远快于程序到硬盘的读取速度，所以效率得以提高。


