<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!--**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*-->

- [CH09 Java 7特性](#ch09-java-7%E7%89%B9%E6%80%A7)
  - [9.1 异常处理改进](#91-%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86%E6%94%B9%E8%BF%9B)
    - [9.1.1 使用`try-with-resources`自动释放资源](#911-%E4%BD%BF%E7%94%A8try-with-resources%E8%87%AA%E5%8A%A8%E9%87%8A%E6%94%BE%E8%B5%84%E6%BA%90)
    - [9.1.2 应对`“处理异常时抛出的新异常”`场景](#912-%E5%BA%94%E5%AF%B9%E5%A4%84%E7%90%86%E5%BC%82%E5%B8%B8%E6%97%B6%E6%8A%9B%E5%87%BA%E7%9A%84%E6%96%B0%E5%BC%82%E5%B8%B8%E5%9C%BA%E6%99%AF)
    - [9.1.3 捕获多个异常：`catch(ExceptionA|ExceptionB e)`](#913-%E6%8D%95%E8%8E%B7%E5%A4%9A%E4%B8%AA%E5%BC%82%E5%B8%B8catchexceptionaexceptionb-e)
    - [9.1.4 简化处理反射方法时的异常：`catch(ReflectiveOperationException e)`](#914-%E7%AE%80%E5%8C%96%E5%A4%84%E7%90%86%E5%8F%8D%E5%B0%84%E6%96%B9%E6%B3%95%E6%97%B6%E7%9A%84%E5%BC%82%E5%B8%B8catchreflectiveoperationexception-e)
  - [9.2 使用文件](#92-%E4%BD%BF%E7%94%A8%E6%96%87%E4%BB%B6)
    - [9.2.1 取代`File`类的`Path`接口](#921-%E5%8F%96%E4%BB%A3file%E7%B1%BB%E7%9A%84path%E6%8E%A5%E5%8F%A3)
      - [(1) 绝对路径：`Paths.get()`](#1-%E7%BB%9D%E5%AF%B9%E8%B7%AF%E5%BE%84pathsget)
      - [(2) 路径解析：`p.resolve(q)`，`p.resolveSibling(q)`，`p.relativize(q)`，`p.normalize()`](#2-%E8%B7%AF%E5%BE%84%E8%A7%A3%E6%9E%90presolveqpresolvesiblingqprelativizeqpnormalize)
      - [(3) 路径拆分：`p.getParent()`，`p.getFileName()`，`p.getRoot()`](#3-%E8%B7%AF%E5%BE%84%E6%8B%86%E5%88%86pgetparentpgetfilenamepgetroot)
    - [9.2.2 文件操作](#922-%E6%96%87%E4%BB%B6%E6%93%8D%E4%BD%9C)
      - [(1) 读取和写入小文件](#1-%E8%AF%BB%E5%8F%96%E5%92%8C%E5%86%99%E5%85%A5%E5%B0%8F%E6%96%87%E4%BB%B6)
      - [(2) 读取和写入大文件](#2-%E8%AF%BB%E5%8F%96%E5%92%8C%E5%86%99%E5%85%A5%E5%A4%A7%E6%96%87%E4%BB%B6)
      - [(3) 创建文件和目录](#3-%E5%88%9B%E5%BB%BA%E6%96%87%E4%BB%B6%E5%92%8C%E7%9B%AE%E5%BD%95)
      - [(4) 创建临时文件和目录](#4-%E5%88%9B%E5%BB%BA%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%92%8C%E7%9B%AE%E5%BD%95)
      - [(5) 复制、移动、和删除文件](#5-%E5%A4%8D%E5%88%B6%E7%A7%BB%E5%8A%A8%E5%92%8C%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6)
  - [9.3 简化`equals`、`hashCode`和`CompareTo`方法的编写](#93-%E7%AE%80%E5%8C%96equalshashcode%E5%92%8Ccompareto%E6%96%B9%E6%B3%95%E7%9A%84%E7%BC%96%E5%86%99)
    - [9.3.1 使用`Objects.equals(Object, Object)`简化`equals`方法的编写](#931-%E4%BD%BF%E7%94%A8objectsequalsobject-object%E7%AE%80%E5%8C%96equals%E6%96%B9%E6%B3%95%E7%9A%84%E7%BC%96%E5%86%99)
    - [9.3.2 使用`Objects.hash(Object ...)`简化`hashCode`方法的编写](#932-%E4%BD%BF%E7%94%A8objectshashobject-%E7%AE%80%E5%8C%96hashcode%E6%96%B9%E6%B3%95%E7%9A%84%E7%BC%96%E5%86%99)
    - [9.3.3 使用`Integers.compare(Integer, Integer)`等方法来简化`compareTo`的编写](#933-%E4%BD%BF%E7%94%A8integerscompareinteger-integer%E7%AD%89%E6%96%B9%E6%B3%95%E6%9D%A5%E7%AE%80%E5%8C%96compareto%E7%9A%84%E7%BC%96%E5%86%99)
  - [9.4 安全需要](#94-%E5%AE%89%E5%85%A8%E9%9C%80%E8%A6%81)
  - [9.5 其他改动](#95-%E5%85%B6%E4%BB%96%E6%94%B9%E5%8A%A8)
    - [9.5.1 修复字符串”+123“转换为数字时的问题](#951-%E4%BF%AE%E5%A4%8D%E5%AD%97%E7%AC%A6%E4%B8%B2123%E8%BD%AC%E6%8D%A2%E4%B8%BA%E6%95%B0%E5%AD%97%E6%97%B6%E7%9A%84%E9%97%AE%E9%A2%98)
    - [9.5.2 全局Logger](#952-%E5%85%A8%E5%B1%80logger)
    - [9.5.3 null检查](#953-null%E6%A3%80%E6%9F%A5)
    - [9.5.4 替代`Runtime.exec`的`ProcessBuilder`](#954-%E6%9B%BF%E4%BB%A3runtimeexec%E7%9A%84processbuilder)
    - [9.5.5 `URLClassLoader`的改进](#955-urlclassloader%E7%9A%84%E6%94%B9%E8%BF%9B)
    - [9.5.6 BitSet](#956-bitset)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# CH09 Java 7特性

> 除了`字符串switch语句`、`二进制数字表示`、`下划线数字表示`、`改进的类型推断等`，还包括如下非常有用的改进

## 9.1 异常处理改进

### 9.1.1 使用`try-with-resources`自动释放资源

该语句可以自动释放资源，并且可以指定多个资源，例如

> ```java
> try {
>    	// Scanner类实现了AutoClosable接口
>    	// 当抛出异常，或者try块内的代码运行完毕后，都会调用scanner.close()方法来释放资源
>    	try (Scanner scanner = new Scanner(Paths.get("/usr/share/dict/words"))) {
>    		int count = 0;
>    		while (scanner.hasNext() && ++count < 4) {
>    			System.out.println(LOG_PREFIX + scanner.next().toLowerCase());
>    		}
>    		// a
>    		// a
>    		// aa
>    	}
> 
>    	// 可以指定多个资源，如下面的in和out
>    	try (
>    		Scanner in = new Scanner(Paths.get("not_existed.txt"));
>    		PrintWriter out = new PrintWriter("/tmp/out.txt")
>     	) {
>    		while (in.hasNext()) {
>    			out.println(in.next().toLowerCase());
>    		}
>    	}
> } catch (IOException ex) { // Separate try-with-resources from try/catch
>    	System.out.println(LOG_PREFIX + "exception from try-with-resources clause: " + ex);
>    	// exception from try-with-resources clause: java.nio.file.NoSuchFileException: not_existed.txt
> }
> ```

### 9.1.2 应对`“处理异常时抛出的新异常”`场景

问题：在下面场景中，应当捕捉异常A？还是捕捉异常B呢？

> (1) 处理业务逻辑时抛出异常A，导致`try-with-resources`要关闭资源
>
> (2) 在关闭资源时，又抛出新的异常B

`try-with-resources`的处理方法

> 会重新抛出异常A，而异常B则由`try-with-resource`类库来捕获并将其标记为”suppressed“，例如下面的例子1

但是要注意这种机制、只有在异常没有被破坏的前提下才可用

> 例如Scanner，会拦截并捕获两个异常，然后重新抛出一个新异常。例如下面的例子2中，只能捕获Scanner抛出的新异常。例子可以参考下面的”完整代码“

完整代码：[../code/ch9/sec01/TryWithResources.java](../code/ch9/sec01/TryWithResources.java)

例子1

> ```java
> try {
>    	// 测试场景构造
>    	// 构造一个内部类，传给Scanner，来让Scanner处理业务逻辑，以及关闭时都会抛出异常
>    	try (InputStream in = new InputStream() {
>    		public int read() throws IOException {
>    			throw new IOException("read failed");
>    		}
>    		public void close() throws IOException {
>    			throw new IOException("close failed");
>    		}
>    	}) {
>    		System.out.println(in.read());
>    	}
> } catch (Exception ex) {
>    	System.out.println(LOG_PREFIX + "exception thrown by try-with-resources: " + ex);
>    	// 输出
>    	// exception thrown by try-with-resources: java.io.IOException: read failed
> 	Throwable[] secondaryExceptions = ex.getSuppressed();
>    	System.out.println(LOG_PREFIX + "exception suppressed: " + Arrays.toString(secondaryExceptions));
>    	// 输出
>    	// exception suppressed: [java.io.IOException: close failed]
>    }
> ```

### 9.1.3 捕获多个异常：`catch(ExceptionA|ExceptionB e)`

> 可以编写如下代码，让多个异常共享同一个catch分治，来避免代码冗余
>
> ~~~java
> try {
>    	...
> } catch (FileNotFoundException | UnknownHostException ex) {
>    	...
> }
> ~~~

### 9.1.4 简化处理反射方法时的异常：`catch(ReflectiveOperationException e)`

Java 6的时候，调用反射方法要处理多种异常

> 例如`ClassNotFoundException`、`NoSuchMethodException`、`IllegalAccessException`、`InvocationTargetException`

Java 7引入了一个新的父类异常`ReflectiveOperationException`，只需捕捉这一个就可以

> `catch (ReflectiveOperationException e) {...}`

## 9.2 使用文件

### 9.2.1 取代`File`类的`Path`接口

> Path：(1)可能是含有多个目录名称的序列；(2)也可能带着一个文件名
>
> 代码位置：[../code/ch9/sec02/PathDemo.java](../code/ch9/sec02/PathDemo.java)

#### (1) 绝对路径：`Paths.get()`

> ```java
> // [1] 绝对路径，Paths.get()
> // 对于无效路径会抛出InvalidPathException异常
> Path absolute = Paths.get("/", "home", "cay");
> System.out.println(LOG_PREFIX + absolute);
> // 输出：/home/cay
> 
> Path relative = Paths.get("myprog", "conf", "user.properties");
> System.out.println(LOG_PREFIX + relative);
> // 输出：myprog/conf/user.properties
> 
> Path homeDirectory = Paths.get("/home/cay");
> System.out.println(LOG_PREFIX + homeDirectory);
> // 输出：/home/cay
> ```

#### (2) 路径解析：`p.resolve(q)`，`p.resolveSibling(q)`，`p.relativize(q)`，`p.normalize()`

> ```java
> // p.resolve(q)，规则如下：
> // * 如果q是绝对路径，返回${q}
> // * 如果q是相对路劲，返回${p}/${q}
> Path configPath = homeDirectory.resolve("myprog/conf/user.properties");
> System.out.println(LOG_PREFIX + configPath);
> // 输出：/home/cay/myprog/conf/user.properties
> 
> // p.resolveSibling(q)，针对p的父目录进行解析
> Path workPath = Paths.get("/home/cay/myprog/work");
> Path tempPath = workPath.resolveSibling("temp");
> System.out.println(LOG_PREFIX + tempPath);
> // 输出：/home/cay/myprog/temp
> 
> // p.relativize(q)：从路径p到路径q的相对路径
> Path relPath = Paths.get("/home/cay").relativize(Paths.get("/home/fred/myprog"));
> System.out.println(LOG_PREFIX + relPath);
> // 输出：../fred/myprog
> 
> // p.normalize()：去掉冗余成分之后的路径
> Path normalizedPath = Paths.get("/home/cay/../fred/./myprog").normalize();
> System.out.println(normalizedPath);
> // 输出：/home/fred/myprog
> ```

#### (3) 路径拆分：`p.getParent()`，`p.getFileName()`，`p.getRoot()`

> ```java
> // p.getParent()：
> // 如果p是目录，返回的p的上一级目录
> // 如果p是文件，返回的p所在的目录
> Path parent1 = Paths.get("/home/cay/myfile.txt").getParent();
> System.out.println(LOG_PREFIX + parent1);
> // 输出：/home/cay
> Path parent2 = Paths.get("/home/cay/mydir/").getParent();
> System.out.println(LOG_PREFIX + parent2);
> // 输出：/home/cay
> 
> // p.getFileName()：
> // 如果p是文件，返回文件名
> // 如果p是目录，返回最后一级目录的目录名
> Path file1 =  Paths.get("/home/cay/myfile.txt").getFileName(); // the path myprog.properties
> System.out.println(LOG_PREFIX + file1);
> // 输出：myfile.txt
> Path file2 =  Paths.get("/home/cay/mydir/").getFileName(); // the path myprog.properties
> System.out.println(LOG_PREFIX + file2);
> // 输出：myDir
> 
> // p.getRoot()
> // 如果是绝对路径，返回该路径的根目录
> // 如果是相对路径，返回null
> Path root1 = Paths.get("/home/cay/myfile.txt").getRoot(); // the path /
> System.out.println(LOG_PREFIX + root1);
> // 输出：/
> Path root2 = Paths.get("/home/cay/myfile.txt").getFileName().getRoot();
> System.out.println(LOG_PREFIX + root2);
> // 输出：null （单独的文件名部分没有root）
> Path root3 = Paths.get("./code/next/").getRoot();
> System.out.println(LOG_PREFIX + root3);
> // 输出：null （相对路径没有root）
> ```

### 9.2.2 文件操作

> 代码位置：[../code/ch9/sec02/FilesDemo.java](../code/ch9/sec02/FilesDemo.java)

#### (1) 读取和写入小文件

> 对于小文件，可以将文件内容当做字符串或字符串列表来处理
>
> ```java
> // 读取全部内容：Files.readAllBytes(Path)
> byte[] bytes = Files.readAllBytes(filePath("FilesDemo.java"));
> // 将byte[]转换为String（可指定编码）：new String(bytes, Charset)
> String content = new String(bytes, StandardCharsets.UTF_8);
> System.out.println(NEW_LOG_PREFIX + content.substring(0, 100) + "...");
> // 输出
> // import java.io.ByteArrayOutputStream;
> // import java.io.IOException;
> // import java.net.URL;
> // import java.n...
> 
> // 按行读取内容
> List<String> lines = Files.readAllLines(filePath("FilesDemo.java"));
> System.out.println(NEW_LOG_PREFIX + "Last line: " + lines.get(lines.size() - 1));
> // 输出
> // Last line: }
> 
> // 以二进制方式覆盖写入（可指定编码）：Files.write(Path, byte[])
> // 按行覆盖写入：Files.write(Path, List<String>)
> content = content.replaceAll("e", "x");
> Files.write(filePath("FilesDemo1.out"), content.getBytes(StandardCharsets.UTF_8));
> Files.write(filePath("FilesDemo1.out"), lines);
> 
> // 以追加的方式写入：File.write(Path, List<String>, StandardOpenOption.APPEND)
> Collections.reverse(lines);
> Files.write(filePath("FilesDemo2.out"), lines, StandardOpenOption.APPEND);
> 
> // 如果存在则删除文件：Files.deleteIfExists(Path)
> boolean deleted = Files.deleteIfExists(filePath("FilesDemo3.out"));
> System.out.println(NEW_LOG_PREFIX + deleted);
> ```

#### (2) 读取和写入大文件

> 对于大文件，或二进制文件，可以考虑使用`InputStream`/`OutputStream`或者`Reader`/`Writer`
> *   `InputStream in   = Files.newInputStream(path);`
> *   `OutputStream out = Files.newOutputStream(path);`
> *   `Reader reader    = Files.newBufferedReader(path);`
> *   `Writer writer    = Files.newBufferedWriter(path);`
>
> ```java
> // 从InputStream拷贝到Path：Files.copy(InputStream, Path)
> URL url = new URL("http://horstmann.com");
> Files.copy(url.openStream(), filePath("FilesDemo3.out"));
> 
> // 从Path拷贝到OutputStream：Files.copy(Path, OutputStream)
> ByteArrayOutputStream out = new ByteArrayOutputStream();
> Files.copy(filePath("FilesDemo3.out"), out);
> System.out.println(NEW_LOG_PREFIX + out.toString("UTF-8").substring(0, 100) + "...");
> // <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> // <html><head>
> // <title>302 Found</title>
> // </head><bod...
> ```

#### (3) 创建文件和目录

> ```java
> // 创建新的目录: 
> // 上一级目录必须存在，目标目录已经存在时会抛异常： Files.createDirectory(Path)
> // 将缺失的上一级目录一起创建，目标目录已经存在时会抛异常： File.createDirectories(Path)
> Path tmpDir = Files.createDirectory(Paths.get("tmp"));
> System.out.println(NEW_LOG_PREFIX + tmpDir.toAbsolutePath().toString());
> // /Users/fangkun/Dev/git/java8note/tmp
> 
> // 创建空文件：Files.createFile(Path)
> // 文件已经存在时会抛异常
> Path tmpFile = Files.createFile(Paths.get("tmp.txt"));
> System.out.println(NEW_LOG_PREFIX + tmpFile.toAbsolutePath().toString());
> // /Users/fangkun/Dev/git/java8note/tmp.txt
> 
> // 检查文件/目录是否存在: Files.exists(Path)
> System.out.println(NEW_LOG_PREFIX + Files.exists(tmpDir));
> System.out.println(NEW_LOG_PREFIX + Files.exists(tmpFile));
> // true
> // true
> 
> // 删除文件或目录: Files.deleteIfExists(Path)
> Files.deleteIfExists(tmpDir);
> Files.deleteIfExists(tmpFile);
> System.out.println(NEW_LOG_PREFIX + Files.exists(tmpDir));
> System.out.println(NEW_LOG_PREFIX + Files.exists(tmpFile));
> // false
> // false
> ```

#### (4) 创建临时文件和目录

> ```java
> // 创建临时文件
> // Files.createTempFile(dir, prefix, suffix);
> // Files.createTempFile(     prefix, suffix);
> // Files.createTempFile(dir, prefix        );
> // Files.createTempFile(     prefix        );
> 
> Path newPath = Files.createTempFile(null, ".txt");
> System.out.println(NEW_LOG_PREFIX + newPath);
> // /var/folders/nb/n2wl0lms2g57q00_t5qd2nsc0000gn/T/14595181751598492480.txt
> 
> // 创建临时目录
> // Files.createTempDirectory(dir, prefix, suffix);
> // Files.createTempDirectory(     prefix, suffix);
> // Files.createTempDirectory(dir, prefix        );
> // Files.createTempDirectory(     prefix        );
> 
> newPath = Files.createTempDirectory("fred");
> System.out.println(NEW_LOG_PREFIX + newPath);
> // /var/folders/nb/n2wl0lms2g57q00_t5qd2nsc0000gn/T/fred16143100884822648692
> ```

#### (5) 复制、移动、和删除文件

> ```java
> // 从Path拷贝到Path: Files.copy(Path, Path)
> Files.copy(
>         filePath("FilesDemo3.out"), filePath("FilesDemo4.out"));
> 
> // 从Path移动到Path：Files.move(Path, Path)
> Files.move(
>         filePath("FilesDemo4.out"), filePath("FilesDemo5.out"));
> 
> // 拷贝设置（1）覆盖已存在文件StandardCopyOption.REPLACE_EXISTING (2) 拷贝文件属性StandardCopyOption.COPY_ATTRIBUTES
> Files.copy(
>         filePath("FilesDemo3.out"), filePath("FilesDemo5.out"),
>         StandardCopyOption.REPLACE_EXISTING,
>         StandardCopyOption.COPY_ATTRIBUTES);
> 
> // 原子移动文件、要么移动完成、要么源文件仍然存在：StandardCopyOption.ATOMIC_MOVE
> Files.move(
>         filePath("FilesDemo5.out"), filePath("FilesDemo6.out"),
>         StandardCopyOption.ATOMIC_MOVE);
> 
> // 删除文件或空目录：Files.delete(Path)
> Files.delete(filePath("FilesDemo6.out"));
> 
> // 仅在文件或空目录存在时删除：Files.deleteIfExists(Path)
> boolean isDeleted = Files.deleteIfExists(filePath("FilesDemo6.out"));
> System.out.println(NEW_LOG_PREFIX + isDeleted);
> 
> // 对于非空目录的删除，需要参考FileVisitor接口的API文档
> ```

## 9.3 简化`equals`、`hashCode`和`CompareTo`方法的编写

> 代码位置：
>
> * [../code/ch9/sec03/Person.java](../code/ch9/sec03/Person.java)
> * [../code/ch9/sec03/Point.java](../code/ch9/sec03/Point.java)

### 9.3.1 使用`Objects.equals(Object, Object)`简化`equals`方法的编写

> ```java
> public boolean equals(Object otherObject) {
>    	// 先对顶部的对象进行null值判断、类型判断
>    	if (this == otherObject) {
>    		return true;
>    	}
>    	if (otherObject == null || this.getClass() != otherObject.getClass()) {
>    		return false;
>    	}
>    	Person other = (Person) otherObject;
> 
>    	// Java 6的老式写法
>    	/*
>    	boolean isFirstEqual = false;
>    	if (null == this.first) {
>    		isFirstEqual = (null == other.first);
>    	} else {
>    		isFirstEqual = this.first.equals(other.first);
>    	}
>    	boolean isSecondEqual =
>    	...
>    	return isFirstEqual && isSecondEqual;
>    	*/
> 
>    	// Java 7提供Objects.equals方法，来简化上面代码的代码
>    	// 对于Object.equals(a, b)
>    	// * a,b都是null时返回true
>    	// * 只有a是null时返回false
>    	// * 其他情况返回a.equals(b)
>    	return Objects.equals(first, other.first) && Objects.equals(last, other.last);
> }
> ```

### 9.3.2 使用`Objects.hash(Object ...)`简化`hashCode`方法的编写

> ```java
> public int hashCode() {
>    	// Java 7提供方法，
>    	// 替代诸如 31*Object.hashCode(first) + Object.hashCode(second)这样的代码
>    	return Objects.hash(first, last);
> }
> ```

### 9.3.3 使用`Integers.compare(Integer, Integer)`等方法来简化`compareTo`的编写

> ```java
> public int compareTo(Point other) {
>    	// 使用Java 7提供的方法，可以避免直接相减带来的溢出问题
>    	// Integer、Long、Short、Byte、Boolean都提供了各自的静态方法compare
>    	int diff = Integer.compare(x, other.x); // No risk of overflow
>    	if (diff != 0) {
>    		return diff;
>    	}
>    	return Integer.compare(y, other.y);
> }
> ```

## 9.4 安全需要

> Java 7要求运行RIA（富互联网应用程序、Java Applet及Web Start应用程序）需要求商业机构办法的证书进行签名来防止JAR包manifest entry中的`Permissions:sandbox`（或`Permissions:all-permission`）被串改，同时可以增加形如`Codebase: https://www.mycompany.com www.mycompany.com:8080`之类的限制，限定应用程序加载URL，来防止它们被黑客利用。但RIA仍然不是开发首选，只是出于维护旧的应用的需要。

## 9.5 其他改动

代码位置

> * [../code/ch9/sec05/Misc.java](../code/ch9/sec05/Misc.java)：9.5.1 ~ 9.5.3， 9.5.6
> * [../code/ch9/sec05/ProcessDemo.java](../code/ch9/sec05/ProcessDemo.java)：9.5.4
>
> * [../code/ch9/sec05/ClassLoaderDemo.java](../code/ch9/sec05/ClassLoaderDemo.java)：9.5.5

### 9.5.1 修复字符串”+123“转换为数字时的问题

> ```java
> // Java 7修复了形如"+1"的整形数字符串在被parse成整数时的bug
> double   x1 = Double.parseDouble("+1.0");
> int      n1 = Integer.parseInt("+1");
> short    s1 = Short.parseShort("+1");
> byte     b1 = Byte.parseByte("+1");
> BigInteger bi1 = new BigInteger("+1");
> int      n2 = Integer.decode("0x10");
> int      n3 = Integer.decode("010");
> Integer nw1 = Integer.valueOf("+1");
> Long    lw1 = Long.valueOf("+1");
> System.out.printf("%f %d %s %d %s %d %d %d %d\n", x1, n1, s1, b1, bi1, n2, n3, nw1, lw1);
> // 输出： 1.000000 1 1 1 1 16 8 1 1
> ```

### 9.5.2 全局Logger

> Java 8提供了一个简洁又安全的形式来输出全局Logger，形式如下
>
> ```java
> Logger.getGlobal().info("x1=" + 1.0);
> // 输出： 信息: x1=1.0
> ```
>
> 它用来解决老版本Java的如下问题：
>
> * `Logger.global.finest("x=" + x)` （已经deprecated了）需要初始化、并且容易造成静态初始化代码段死锁
> * `Logger.getLogger(Logger.GLOBAL_LOGGER_NAME)`（来自Java6）使用起来比较繁琐

### 9.5.3 null检查

> ```java
> public void process(String directions) {
>    	// directions为null时，会抛出NullPointerException并且可以设置错误提示
>    	// 相比普通的null值检查，代码简洁并且更容易定位错误
>    	this.directions = Objects.requireNonNull(directions, "directions must not be null");
> }
> // 该方法抛出异常时的输出
> // java.lang.NullPointerException: directions must not be null
> // at java.base/java.util.Objects.requireNonNull(Objects.java:233)
> // at Misc.process(Misc.java:45)
> // at Misc.main(Misc.java:25)
> ```

### 9.5.4 替代`Runtime.exec`的`ProcessBuilder`

> 代码：[../code/ch9/sec05/ProcessDemo.java](../code/ch9/sec05/ProcessDemo.java)
>
> 替代Java5的Runtime.exec执行外部命令，可以使用builder模式，设置输入、输出、工作目录等
>
> ```java
> // 例子1
> ProcessBuilder builder1 = new ProcessBuilder("pwd");
> builder1.redirectErrorStream(true);
> builder1.redirectOutput(ProcessBuilder.Redirect.INHERIT);
> Process process1 = builder1.start();
> process1.waitFor(10, TimeUnit.SECONDS);
> // 输出 : /Users/fangkun/Dev/git/java8note
> 
> // 例子2
> ProcessBuilder builder2 = new ProcessBuilder("grep", "[A-Za-z_][A-Za-z_0-9]*", "-o");
> builder2.redirectInput(path("ProcessDemo.java").toFile());
> builder2.redirectOutput(path("identifiers.txt").toFile());
> Process process2 = builder2.start();
> process2.waitFor(1, TimeUnit.MINUTES);
> ```

### 9.5.5 `URLClassLoader`的改进

> 代码：[../code/ch9/sec05/ClassLoaderDemo.java](../code/ch9/sec05/ClassLoaderDemo.java)
>
> Java 7的`URLClassLoader`实现了AutoClosable接口，可以放在try-with-resources语句中，防止资源泄漏
>
> ```java
> try (URLClassLoader loader = new URLClassLoader(urls)) {
>    	Class<?> klass = loader.loadClass("org.junit.runner.JUnitCore");
>    	System.out.println(klass.getMethod("main", String[].class).invoke(null, (Object) args));
> }
> // 输出
> // JUnit version 4.11
> // Time: 0.004
> // OK (0 tests)
> ```
>
> 但是注意：如果仍然需要使用载入的类，就不应当关闭它，否则会抛ClassNotFoundException

### 9.5.6 BitSet

> 一个表示bit序列的集合，计算非常高效
>
> (1) 构造`BitSet`
>
> ```java
> // 用byte[]构造
> byte[] bytes = {(byte) 0b10101100, (byte) 0b00101000};
> BitSet primes = BitSet.valueOf(bytes);
> System.out.println(primes);
> // {2, 3, 5, 7, 11, 13}
> 
> // 用long[]构造
> long[] longs = {0x100010116L, 0x1L, 0x1L, 0L, 0x1L};
> BitSet powersOfTwo = BitSet.valueOf(longs);
> System.out.println(powersOfTwo);
> // {1, 2, 4, 8, 16, 32, 64, 128, 256}
> ```
>
> (2) 转换成`byte[]`,` long[]`,` IntStream`
>
> ~~~java
> // toByteArray()
> for (byte bt : powersOfTwo.toByteArray()) {
>     System.out.print(
>             Integer.toBinaryString(
>                     Byte.toUnsignedInt(bt)));
> }
> System.out.println();
> // 1011011010001000000010000000000000001
> 
> // toLongArray()
> for (long l : powersOfTwo.toLongArray()) {
>     System.out.print(l + ",");
> }
> System.out.println();
> // 4295033110,1,1,0,1,
> 
> // stream()：返回IntStream
> powersOfTwo.stream().forEach(System.out::println);
> // 1
> // 2
> // 4
> // 8
> // 16
> // 32
> // 64
> // 128
> // 256
> ~~~





