# 新人报道--Kotlin(HelloWorld)

本人大三，是新人，需要大神们多多指教哈！


今天是我第一次发blog,，也是java的生日,先祝我们的CafeBaby 生日快乐。

    
- **Kotlin--Hello World!**
- **与Java相比**
- **运行所加载的类**
- **加载额外的类**
- **查看类的结构**
- **用java反编译器查看**


-------------------

## Kotlin--Hello World!

     当单一的Java开发已经无法满足当前软件的复杂需求时，越来越多基于Java虚拟机的语言开发被应用到软件项目中，Java平台上的多语言混合编程正成为主流，每种语言都可以针对自己擅长的方面更好地解决问题。
昨天刚接触了下一门运行在jvm上的语言---kotlin，他的语法与java相比下，简单易懂。
所以做了个简单测试HelloWorld，我是使用eclipse，用习惯了。

``` python
fun main(args: Array<String>) {
	println("HelloWorld!")	
}

```
 这个结构与public static void main(String args[]){….}有点相似。
 
输出结果必然是“HelloWorld!”。

## 与Java相比

>Kotlin与java语言都是运行在jvm上的语言，既然运行在jvm之上运行，那必须符合jvm的排序规则，编译加载.class文件（关于类加载机制过程就不详细讲解了，过段时间专门写一个关于这样的专题）。

我就很好奇它的加载过程，我就做了个测试，代码很简单。
Kotlin:
``` python
fun main(args: Array<String>) {
	println("HelloWorld!")	
}

``` 
Java:
``` python
public static void main(String[] args) {
		System.out.println("Hello World");
	}

``` 
代码很简单

### 运行所加载的类

Kotlin:
![这里写图片描述](http://img.blog.csdn.net/20170523180541096?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
Java:
![这里写图片描述](http://img.blog.csdn.net/20170523180649073?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
前面加载的一模一样，但是往后看就会发现不同。



### 加载额外的类

java:
![这里写图片描述](http://img.blog.csdn.net/20170523180716833?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
到此加载完毕后输出结果

Kotlin:
![这里写图片描述](http://img.blog.csdn.net/20170523180754245?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


![这里写图片描述](http://img.blog.csdn.net/20170523180842621?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
它加载并没有结束，还通过sun.misc.URLClassPath$JarLoader去加载额外的jar包

``` python
[Loaded sun.security.util.SignatureFileVerifier from C:\Program Files\Java\jre1.8.0_101\lib\rt.jar]
[Loaded sun.security.util.ManifestEntryVerifier from C:\Program Files\Java\jre1.8.0_101\lib\rt.jar]
[Loaded kotlin.jvm.internal.Intrinsics from file:/F:/eclipse/configuration/org.eclipse.osgi/1310/0/.cp/lib/kotlin-runtime.jar]
[Loaded kotlin.KotlinNullPointerException from file:/F:/eclipse/configuration/org.eclipse.osgi/1310/0/.cp/lib/kotlin-runtime.jar]
``` 
加载了kotlin.jvm.internal.Intrinsics这个类从kotlin-runtime.jar里。

    我那时候发现[Loaded kotlin.jvm.internal.Intrinsics…，这个是kotlin中的一个类，但是很好奇的是代码中没有出现或者说没有去声明。

### 查看类的结构
我比较好奇这个类为什么会被加载，我拿出Kotlin编译好的class文件，看了下他的结构：

![这里写图片描述](http://img.blog.csdn.net/20170523180054450?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

很惊奇的发现这个类确实被加载进来引用
![这里写图片描述](http://img.blog.csdn.net/20170523180210717?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

也发现了Helloworld这个类是被final修饰的，我还想查看个究竟，通过反编译查看这个代码。

###用java反编译器查看
![这里写图片描述](http://img.blog.csdn.net/20170523180337900?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg3MjQyOTU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
  
    后来发现这个类是在运行时检查参数是否为空值。
    在应用上来看，kotlin的语法的确比较简单易用（本人目前来看），但是我相信每种语言都可以针对自己擅长的方面更好地解决问题。
关于kotlin的一些知识或者我个人对他的一些看法会持续更新喔，欢迎大家来多多提意见哈！


由于这是本人第一次写博客，需要大家多多指教。有啥意见问题多留言哈！

