##  Java



### 1 基础知识

#### 1.1 java外部基础

##### 1.1.1 JDK，JRE和JVM

> **JDK**

​	jdk (java development kit)Java开发工具包，其包含了JRE和一些java的开发工具，如java.exe、javac.exe、javadoc.exe等，jdk是提供给java开发人员使用的，即有了jdk，就可以编写java程序来运行了。

> **JRE**

​	jre(java runtime environment) java运行环境，其包含了jvm和java的核心类库。jre是用来运行java程序的，不支持java的开发工作。

> **JVM**

​	jvm(java virtual machine) java虚拟机。jvm保障了java可以在任何系统下运行，对于不同的操作系统，有着不同的java虚拟机，其屏蔽了底层运行平台的差异，实现了一次编译，到处运行。

##### 1.1.2 java程序的编译和运行

> **编译**

​	在编写完一个后缀为.java的源文件后，将其通过javac.exe编译成.class的字节码文件，以便计算机识别。

> **运行**

​	通过编译得到.class的字节码文件后，计算机就可以通过java.exe来运行这个字节码文件，执行所编写的程序。

##### 1.1.3 配置环境变量

​	环境配置是为了解决java工具包与一个java程序没在同一个目录下而导致此java程序无法运行的情况，将java工具包配置到环境变量中可以让java程序所在的目录在系统环境中检索到java工具包，进而可以在任何目录下完成java的编译和运行。

​	一般先配置JAVA_HOME，JAVA_HOME指向jdk安装目录，再编辑环境变量path，在其中添加%JAVA_HOME%\bin。在这里%JAVA_HOME%是用来引用JAVA_HOME所指向的位置，然后\bin为JAVA_HOME所指向位置内的bin目录。

​	用%JAVA_HOME%而不是直接用bin所在目录的路径的好处是方便以后修改，如以后需要修改jdk目录了，则只改JAVA_HOME的指向即可，而不用去path内改bin的位置。

##### 1.1.4 路径

路径是指到目标文件夹所途径的文件，比如从

~~~java
C:\Program Files\Java\
~~~

到

~~~java
C:\Users\Public
~~~

其有两种路径，一种是相对路径，一种是绝对路径。

> 相对路径

​	从当前目录开始定位，一路到目标目录所形成的路径，一般要用到..（其含义为返回上一级目录），完成示例的路径如下：

~~~java
..\..\users\public
~~~

> 绝对路径

​	从顶级目录开始定位，一路到目标目录所形成的路径，如果所在目录和目标目录的距离不远，即都在某个子目录下的不同子目录中，则相对路径可能要比绝对路径短；若两目录中间要通过一次顶级目录，则一般绝对路径比相对路径近。绝对路径完成示例如下：

~~~java
C:\users\public
~~~

##### 1.1.5 API文档

​	API是application programming interface（应用程序编程接口）的缩写，是java提供的基本编程接口，即java本身自带的一些类和方法，可以直接用。可以去中文在线文档上看https://www.matools.com。



#### 1.2 java内部基础

##### 1.2.1 程序编写细节

​	1、java源文件以.java为扩展名，源文件的基本组成部分为类（class）；

​	2、java应用程序的执行入口是main方法，其有固定书写格式：

~~~java
public static void main(String[] args){
    
}
~~~

​	3、java严格区分大小写；

​	4、一个源文件中最多只有一个public类，其他类的个数不限；

​	5、源文件的文件名必须与public类的文件名一致，即若有

~~~java
public class a{}
~~~

则此源文件名称应为a.java;

​	6、maim方法可以不再public类之下，但是一定要有一个类下有main方法。



##### 1.2.2 注释

​	注释是写给人看的，而不是写给计算机，故计算机是不会去识别注释内的字（但是如果编译器的字符编码表与计算机的字符编码表不同，哪怕是注释内的字，也会报错，导致无法将源文件编译为字节码文件）。

>**单行注释**

~~~java
//
~~~

​	单行注释用两个斜杠表示，此注释只在这一行管用，回车之后又变回程序部分。

> **多行注释**

~~~java
/*
 
 */
~~~

​	多行注释可以在/*   */范围内任意注释任意行。

> **文档注释**

~~~java
/**
	* @author 作者姓名:chan9he
	* @version 当前程序版本
*/
~~~

​	文档注释的内容可以被jdk中的工具javadoc.exe所解析，生成一套以网页形式体现的此部分程序的说明文档，一般写在类上方。文档注释中，有固定的格式，应按格式写。可以在doc中用javadoc.exe来生成一组网页形式的文档，其使用方法如下

~~~c++
javadoc -d 文件夹名称 -author -version java文件名
~~~



##### 1.2.3 转义字符

> **换行：\n**

​	换行字符可以将打印出来的最终结果换行输出

~~~java
System.out.println("北京\n上海");
~~~

​	其输出结果为：

~~~java
北京
上海
~~~



> **制表：\t**

​	制表字符可以让打印出来的最终结果自动空格对齐（但是若\t前的字符个数不同，其空格长度也不同，若想合理，则要多加\t）

~~~java
 System.out.println("北京\t\t天津\t上海\n黑龙江\t内蒙古\t湖北");
~~~

其输出为

~~~java
北京    天津 上海
黑龙江  内蒙古   湖北
~~~



> **单个\：\\\\**

​	我们在打印时往往需要输出某个目录，而目录中时存在"\\"的，而如果直接在System.out中输入目标路径，如输入

~~~java
System.out.println("C:\Program Files\Java");//错误
~~~

​	则javac会将\p、\J当成非法的转义字符，而无法进行编译，故此时用\\\来代替\就可以了

~~~java
System.out.println("C:\\Program Files\\Java");
~~~

其输出为

~~~java
C:\Program Files\Java
~~~



> **单个"：\\"（单个'同理）**

​	若在打印时想输出某一句带引号的话，如张三：“回家吃饭了。”若把此段话直接放进System.out中，则张三话上的引号会与println()中的引号发生冲突，导致无法进行编译（但是如果用的中文输入法的引号则可以正常编译，此处举例有点狭隘）

~~~java
System.out.println("张三："回家吃饭了"");//错误
~~~

​	正确的输入如下

~~~java
System.out.println("张三：\"回家吃饭了\"");
~~~



> **回车：\r**

​	理论上\r是将光标移动到此行最前方，然后将\r后面的字符依次替换最前方的字符，而IDEA是只输出\r后方的字符

~~~java
System.out.println("北京欢\r迎你");
~~~

理论上输出为

~~~java
迎你欢
~~~

idea输出为

~~~java
迎你
~~~



##### 1.2.4  “+” 的使用

​	“+”的效果是看其左右两边的字符的属性的：

​	1、左右两边都是数值型时，做加法运算；

~~~java
System.out.println(12 + 13);
~~~

其结果为

~~~java
25
~~~

​	

​	2、左右两边只要有一方为字符串时，做拼接运算

~~~java
System.out.println("12" + 13);
System.out.println(12 + 13 + "hello");
System.out.println("hello" + 12 + 13);
~~~

其结果为

~~~java
1213
25hello
hello1213
~~~



当然也可以进阶着理解一下

~~~java
System.out.println(10 + 10 + 10 + "10" + 10 + 10);
~~~

其结果为

~~~java
30101010
~~~

​	因为java是从上至下，从左至右进行运算的，所以前三个10为正常加法运算，到第四个10的时候，此10是字符而不是数字，故进行拼接运算。

​	所以说从第四个10开始，此串数就不能算是纯粹意义上的数值了，而变成了字符，所以之后的10哪怕不是字符而是数字，也只能进行拼接，而无法进行数值运算了。



##### 1.2.5 键盘输入语句

​	在编程中经常需要从键盘输入数据，此时就可以使用键盘输入语句来获取，这个功能由扫描器完成，即Scanner。

​	在使用Scanner时，要先导入该类所在的包 java.util.*，之后创建Scanner对象，最后就可以调用里面的功能了，其使用如下

~~~java
import java.util.Scanner;//表示把java.util下的类Scanner导入
public class input{
    public static void mian(String[] args){
        Scanner myScanner = new scanner(System.in);//myScanner是Scanner类下的对象
        System.out.println("请输入姓名：");
        String name = myScanner.next();
        System.out.println("请输入年龄：");
        int age = myScanner.nextInt();
    }
}
~~~



##### 1.2.6 java内存结构

​	java内存结构由栈、堆、方法区三大部分组成。一下大体介绍一下各个部分的功能，具体细节之后会学习。

​	栈：一般声明各种变量会在栈中为其分配一个地址空间，这个地址空间可以直接存放各种基本数据类型，也可存放另外的指向堆的地址，这种情况一般是该变量是一个引用类型的数据时使用。

​	堆：堆中一般存放数组、对象等。一般引用类型的数据类型会用到堆，比如在定义一个数组后，数组的具体内容会存放在堆中， 而栈中只有该数组的数组名和该数组具体内容的地址。同理对象也是这样。

​	方法区：方法区中包含常量池和类加载信息等，常量池中一般用来存放字符串，类加载信息是调用某个类时使用的，其中包含属性信息和方法信息。



##### 1.2.7  instanceof

​	instanceof是比较操作符，用于判断对象的类型是否为XX类型或XX类型的子类型（instanceof是判断运行类型是否相同的）。如

~~~java
public class run{
  public static void main(String[] args){
    B b = new B();
    System.out.println(b instanceof B);//true，b的运行类型为B，与B相同
    System.out.println(b instanceof A);//true，b的运行类型为B，是A的子类
    
    A a = new B();
    System.out.println(a instanceof A);//true，a的运行类型为B，是A的子类
    System.out.println(a instanceof B);//true，a的运行类型为B，与B相同
  }
}
class A {}
class B extends A {}
~~~



##### 1.2.8 断点调试

​	断点调试是指在程序的某一行设置一个断点，调试时，程序运行到这一行会停住，然后就可以一步一步向下调试，调试过程可以看各个变量的当前的值，如果出错，调试到出错的代码行会显示错误，从而停止程序。



​	要注意，断点调试过程中，程序是在运行状态的，因此是以对象的运行类型为主的。



​	断点调试时，右键程序选Debug即可，其中有几个功能如下

1、step over  逐行执行；

2、step Into  进入方法内；

3、force step into 强制进入方法；

4、step out 跳出方法；

5、resume program 执行到下个断点。

6、stop debug 结束debug。







#### 1.3 数据基础

##### 1.3.1 进制

​	常用的进制为2进制、8进制、10进制、16进制，计算机中常用2进制表示数

​	2进制为满2进1，以0b或0B开头；

​	八进制为满8进1，以0开头；

​	十进制为满十进一，不需添加开头标志；

​	十六进制为满16进一（数字只有0-9，另外6个数用A-F表示，字母不区分大小写），以0x或0X开头；

~~~java
int n1 = 0b1010;//表示10
int n2 = 1010;//表示1010
int n3 = 01010;//表示520
int n4 = 0x1010;//表示4112
~~~



##### 1.3.2 原码、反码、补码

​	原码、反码、补码是针对有符号数的二进制数的（java中全是有符号数），对于有符号数来说，其二进制的最高位（最左边的为）为符号位，为0则表示正，为1则表示负。

​	正数的原码、反码、补码都一样；

​	负数的反码 = 其原码符号位不变，其他位取反；

​	负数的补码 = 其反码 + 1；

​	0 的反码、补码都是0；

​	在计算机运算时，是运算补码的，而我们在观察运行结果时，是看原码的；



#### 1.4 Object 类

​	Object类是所有类的父类，所有对象都可以用Object类的方法。下面简单介绍一些Object类的方法

##### 1.4.1 equals方法

​	equals方法是判断相等的一种方法，其与“==”有相似也有区别，下面对比equals和“==”来看

> **==**

​	 == 是一个比较运算符，其既可以判断基本数据类型，也可以判断引用数据类型。



​	== 用于判断基本数据类型时，判断的事两边的值的大小是否相等，如

```
System.out.println(1 == 1.0);
```

其结果为true



​	==用于判断引用数据类型时，判断的是引用的地址是否相等。如

```
class A {

}
public class run{
	public static void main(String[] args){
		A a = new A();
		A b = a;
		System.out.println(a == b);
		}
}
```

其结果为true。当然，如果进阶一点，当两个对象的编译类型不同时，其结果还是相同的。如

```
class A{}
class B extends A{}
public class run{
	public static void main(String[] args){
		A a = new A();
		B b = a;
		System.out.println(a == b);
		}
}
```

其结果依旧为true。。

> **equals**

equals的使用方法如下

```
XX.equals();
```

​	

equals方法的初写是在Object类下的，其用于判断栈中不同引用的地址是否相同，其源码如下

```
public boolean equals(Object obj) {
        return (this == obj);
    }
```

可以看到，equals方法在Object类下的实现还是比较简单的，this是指XX部分，obj是用到了Object是所有类的父类的性质，然后用多态参数去传入一个任意类的实参，该实参就为括号内的部分，具体案例如下

```java
class A {}
class B {}
public class run{
  public static void main(String[] args){
    A a = new A();
    B b = new B();
    b.equals(a);
    //其中对比源码来看，this就是b，obj就是a。
		//上代码结果为false
    
    A aa = new A();
    B bb = aa;
    bb.equals(aa);
    //由于equals比较的只是引用aa与引用bb在栈中指向的地址是否相同，而该代码把aa指向的地址赋给来bb，故其指向一样，结果为true。
  }
}


```



equals不仅有Object类下的实现，其还在Object的子类中进行了重写，从而有了新的功能。比如Object类的子类，String类下的equals方法源码如下

```java
  public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        //以上部分是判断类的，由于任何类都是Object的子类，所以可以用到多态参数来进行向上转型的传入实参。
        if (anObject instanceof String) {
            String anotherString = (String)anObject;//此处向下转型是为了调用String类的参数，因为若不向下转型，原对象是只能使用编译类型的参数和方法的
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
    //以上部分用于判断String类型的字符串是否相等
        return false;
    }
```

此时该方法就可以额外判断字符串是否相等。



| 名称   | 概念           | 基本数据类型                         | 引用数据类型                                                 |
| ------ | -------------- | ------------------------------------ | ------------------------------------------------------------ |
| ==     | 比较运算符     | 可以用于基本数据类型，判断值是否相等 | 可以用于引用数据类型，判断引用地址是否相同                   |
| equals | Object类的方法 | 不可以用于基本数据类型               | 可以用于引用数据类型，默认为判断引用地址是否相等，而子类往往重写该方法，用于判断对象的属性是否相等 |



#####  1.4.2 hashCode方法

hashCode方法返回哈希值，该方法的效果如下

1、提高具有哈希结构的容器的效率；

2、两个引用，如果指向的是同一个对象，则哈希值一定一样；

3、两个引用，如果指向的对象不同，则哈希值一定不同；

4、哈希值主要根据地址号而得到的，但是不能完全将哈希值等价于地址；

详情之后再将



##### 1.4.3 toString方法

toString方法返回的是一个字符串，该字符串包含该对象的全类名（包名+类名）+ @ + 哈希值的十六进制，该方法的源码如下

```java
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
```

而一般使用toString方法是要重写一遍的，用来返回对象的属性，该方法如get或int一样，可以用command+N来调出来。

而如果直接输出类名，则等价于输出类名.toString。



##### 1.4.4 finalize方法

finalize方法用于对象被回收时，当对象被回收时，系统会自动调用该对象继承Object的finalize方法。子类可以重写该方法。主要用于释放资源。而所谓被回收时，就是当某个对象没有引用时。如

```java
public class run{
  public static void main(String[] args){
    A a = new A("a");//建立A类下的对象，其引用为a；
    a = null;//将引用a指向空，则刚刚建立的A类下的对象没有被任何引用所指向，此时就会被系统回收
  }
}
class A {
  String name;
  public A (String name){
    this.name = name;
  }
}
```

而Object中的finalize方法是空的，即只提供了一个机制，具体内容要自己在子类中重写。要注意，并不是只要对象引用为空，就会执行一下finalize方法。具体回收谁是由系统内部的算法决定的。而我们也可以用System.gc();方法来主动出发垃圾回收机制。具体如下

```java
public class run{
  public static void main(String[] args){
    A a = new A("a");
    a = null;
    System.gc();
    System.out.println("程序退出了");
  }
}
class A {
  String name;
  public A (String name){
    this.name = name;
  }
  protected void finalize() throws Throwable(){
    System.out.println("垃圾回收机制触发")
  }
  
}
```

其结果为

```
程序退出了;//要注意，是先把主程序执行完成，才去执行垃圾回收算法
垃圾回收机制触发
```



### 2 变量

#### 2.1 变量概念

​	变量是程序的基本组成单位，无论哪种高级语言进行编写程序，变量都是其基础。

> **定义变量**

有三个要素：类型 名称 = 值

~~~java
int num1 = 10;
~~~

当然也可以先声明，再赋值

~~~java
int num1;
num1 = 10;
~~~

要特别注意，局部变量定义时必须赋值；而全局变量定义时可以不赋值，有默认值

> **变量存储**

​	在声明一个变量后，计算机会在内存内为此变量分配一片存储空间，即此变量为地址，该地址指向了一个空间。可以理解为，声明了一个门牌号，计算机为这个门牌号安排了一个房子。

​	在声明完变量后为变量赋值，这个过程就是通过变量找到内存空间，然后将此空间内的数据换成当下赋值的数据.

> **注意事项**

​	1、变量类型不同，占用的空间大小不同如int为4个字节（1字节为8比特）

long为8个字节。

​	2、变量必须先声明再使用；

​	3、一个数据类型的变量可以在此类型内不断改变其值，如

~~~java
int num1 = 10;
System.out.println(num1);
num1 = 20;
System.out.println(num1);
~~~

其结果为

~~~java
10
20
~~~

​	4、变量在同一个作用域内不能重名，即可以理解为同一个小区不能有两个相同的门牌号。若想重名，则要分开在不同的作用



#### 2.2 数据类型

​	数据类型分为基本数据类型和引用数据类型，基本数据类型和引用数据类型在数据存放上有着极大的不同，基本数据类型是可以直接存放到变量所指向的地址的，而引用数据类型则需要更多操作。

​	基本数据类型的不同变量在相互赋值时，是拷贝形式的，即两变量互不影响，其分别指向不同的地址，知识不同的地址内的内容一致。而引用数据类型在相互赋值时，会将不同的变量指向同一个地址，即不同的变量共用一个地址，因此若地址内容改变，则各个变量都会变。

​	引用数据类型包括数组、类、接口。这些之后会一一介绍。此处主要说明基本数据类型。

​	基本数据类型包括：

> **整数类型**

​	**byte（字节）**：占1字节即8比特（bit）。它可表示的范围为-128~127即-(2^7)~(2^7)-1（具体为什么之后解释）（bit为最小的存储单元，即1为2进制数）；

​	**short（短整型）**： 占2字节16比特。它可表示范围为-（2^15）~（2^15）-1；

​	**int（整型）**：占4字节32比特。其范围为-（2^31）~（2^31）-1；

​	**long（长整型）**：占8字节。范围为-（2^63）~（2^63）-1；

> **浮点型**

​	**float（单精度浮点型）**：占4字节，其范围为：-3.403E38~3.403E38

​	**double（双精度浮点型）**：占8字节，其范围为：-1.798E308~1.798E308

> **字符型**

​	**char（字符）**：占2字节

> **布尔型**

​	**Boolean（布尔型）**：占1字节



##### 2.2.1 整数类型

​	java的整型常量默认为int型，声明long型常量时其值后应加“L”。如

~~~java
int i = 1;
long l = 1L;
~~~

​	各数据类型直接不可随意转化

~~~java
int i = 1L;//错误
~~~

上示方法会提示long型转到int可能会有损失。



​	一般情况下用int就是足够的了，计算机也是默认int。不默认为long是因为long占的内存太大了，如果装一个不大的数会导致资源浪费。



##### 2.2.2 浮点类型

​	浮点数在计算机中的存放形式为：符号位+指数位+尾数位，其中尾数位有可能丢失，造成精度损失，故小数一般都是近似值。



​	浮点型的默认形式为double型，因此声明float型时，要在其值后面加“F”，如

~~~java
float f1 = 1.1;//错误
float f2 = 1.1F;
double d = 1.1;
~~~

如不写F，会导致计算机进行从float转到double的处理，从而导致错误。但是double型可以装float数，如

~~~java
double d = 1.1F;
~~~

是可以的因为float精度没有double高，故double是装的下float的。



​	浮点型的表示方法1：用10进制表示，若是0.几，则可省略0。如

~~~java
double num1 = 1.2;
double num2 = 1.2F;
double num3 = .2;
~~~

其最终打印结果为

~~~java
num1 = 1.2  num2 = 1.2    num3 = 0.2 
~~~

​	浮点型表示方法2 : 用科学计数法表示如,e2表示为*10^2，E-2表示为\*10^-2（注意大小写）如

~~~java
double num1 = 5.12e2;
double num2 = 5.12E-2;
~~~

其值为

~~~java
num1 = 512.0;
num2 = 0.0512;
~~~

此处a定义为double型，故小数点后会有数。



​	在对小数进行运算时，要注意一个很严重的问题，即计算机进行小数运算时会不知道小数到底有多长，从而导致无法精确的运算，更无法进行精确的比较，如

~~~java
double num1 = 2.7;
double num2 = 8.1/3;
~~~

其结果理论上应该是a = b = 2.7，但是其真正结果为

~~~java
num1 = 2.7
num2 = 2.6999999999999997
~~~

因此在使用浮点型时要注意一个很严重的问题，即对运算结果为小数的两个数进行相等比较判断时，直接用相等判断很可能会出错，如

~~~java
if（num1 == num2）{
    System.out.println("相等");
}else{
    System.out.println("不相等");
}
~~~

其结果会是不相等。故最合理的写法为判断两小数的绝对值之差小于某一个足够小的数则认为其为相等

~~~java
if(Math.abs(num1 - num2) < 0.0001){
    System.out.println("相等");
}else{
    System.out.println("不相等");
}
~~~

则其结果会为相等。但是如果直接将两相等的小数分别赋给两个变量，则这两个变量比较时会得到相等的结果。



##### 2.2.3字符型

​	字符型会输出单引号内引起来的一个字符，该字符可以是数字，可以是汉字，也可是英文字母等等。若是引起来的是多个字符，则为非法的；

~~~java
char a = 'a';
char b = '汉';
char c = '9';
char d = '10';//非法定义
~~~



​	字符型一定是用单引号引起来的，如用双引号，则为string型；

~~~java
char e = "a";//非法
~~~



​	字符型可以用转义字符'\\'来将其后的字符变为特殊字符，如

~~~java
char f = '\n';//\n为换行，即给f赋予了换行的能力
System.out.println("a" + a + b + f + c);
System.out.println(a + b + c + d);//直接相加时会对表把字符改成数字再计算
~~~

其结果为

~~~java
aa汉
9
20571
~~~



​	字符型也可以定义一个不带引号的数，但这个数要能在编码表上与某一个字符对应上才是合法，如

~~~java
char g = 98;
~~~

其输出结果为

~~~java
b
~~~

因为在ASCII表上，98对应字符b。当然，由此原理也完全可以反向输出，如

~~~java
char h = 'b';
System.out.println((int)h);
~~~

其结果为

~~~java
98
~~~



​	char类型是可以运算的，只要其单引号内引起来的字符能由编码表对应为某一个数即可，此事就可将单引号与其内的字符看成是一个数字，进行直接运算，不需要定义

~~~java
System.out.println('a' + 10);
System.out.println('何' + 10);
~~~

其结果为

~~~java
107
20319
~~~



​	如果定义字符型为某个字符加某个数，只要其最终结果对应ASCII上某个数，就是合法的，如

~~~java
char a = 'a' + 1;
System.out.println((int)a);//此行输出a+1后对应的数字
System.out.println(a);//此行输出a+1后对应的数字对应的字符
~~~

其结果为

~~~java
98
b
~~~



##### 2.2.4 布尔型

​	布尔型只取true 和 false 两种值，只占一个字节，一般用于逻辑运算如if语句，while语句等

~~~java
Boolean b1 = true;
boolean b2 = false;
~~~

​	要注意，不能用0或非0的整数来代替false或true。



#### 2.3 数据类型转换

​	数据类型的转换分为自动类型转换和强制类型转换两种

##### 2.3.1 自动转换

> **转换规则**

​	精度（容量）小的类型可以自动转换为精度大的类型，自转有以下两种：

~~~java
char < int < long < float < double;

byte < short < int < long < float < double;    
~~~

由此规则可知

~~~java
int a = 'c'//正确，因为char型精度没有int高，故可以直接转化过去
double b = 80//正确，因为int精度远小于double，故可转
~~~

其输出为

~~~java
a = 99;
b = 80.0;
~~~



> **转换细节**

​	1、当多种类型的数据混合运算的时候，系统会先将所有的数据转成参与计算的类型中容量最大的那种数据类型，然后进行计算。如

~~~java
int a = 10;
float b = a + 1.1;//错误的
~~~

此句错误的原因：a是int 而1.1是double型（系统默认小数是double），故此两种类型相计算时，自动转换为double型，而double型比float型精度高，故double型转到float型会出错。其有以下两种改法

~~~java
int a = 10;
double b = a + 1.1;

int c = 10;
float d = c + 1.1F;
~~~



2、将精度大的数据类型赋值给精度小的数据类型时，会报错，但是反之会自动转换。如

~~~java
int a = 1.1//错误，因为1.1是系统默认的double型，而double比int精度高
double b = 10;//正确
~~~

当然也有特殊情况

在输入整数给byte或short时，会先判断该数的值是否在byte或short的范围内，若在，则可以赋值成功。

~~~java
byte a = 10;//正确的，虽然10默认为int，但是其在-128~127之内，故可以是byte
~~~

若是把一个比byte小的数先赋值给int了，在用这个int赋给byte则不行。即直接用变量赋值则要严格看其数据类型转换是否符合规则。

~~~java
int a = 10;
byte b = a;//错误，
~~~



3、byte与char或short之间不可相互自动转换 （系统规定），但是byte char short直接可以进行计算，他们会都变成int再计算。如

~~~java
byte a = 1;
short b = 1;
char c = 'a';
short d = a + b + c;//错误，因为byte、short、char运算时会转成int，而int比short大，故会转换出错误
int r = a + b + c;//正确
~~~

而且甚至两个byte相加赋值给另一个byte都不行

~~~java
byte a = 1;
byte b = 1;
byte c = a + b;//错误，a + b结果为int型的2，不能给byte
int d = a + b;//正确
~~~



4、Boolean型不参与转换

##### 2.3.2 强制转换

> **转换规则**

​	强制转换是自动转换的逆过程，是将精度大的转换为精度小的数据类型，使用时加上强转符()即可。强转会造成精度的丢失。

~~~java
int a = (int)1.9; 
System.out.println(a);
int b = 1000;
byte c = (byte)b;
System.out.println(c);
~~~

其结果为

~~~java
1
-48//此结果不是为127，而是以某种方式的精度损失
~~~

> **转换细节**

​	强转只对距其最近的数有效，如果想讲一串数强转，则要加括号

~~~java
int a = (int)10.5 * 3.5;//错误，只转了10.5而没转3.5，其还是double型
int b = (int)(10.5 * 3.5);//正确
~~~



##### 2.3.3 常见情况

~~~java
short s = 12;//成立
short s1 = 6 + 6;//成立，此为常量，只要长度不超过short界线就行
short s2 = s - 9;//不成立，因为s - 9是变量运算，会转换成int。
short s3 = (short)(s - 9);//成立

char c = 'a';//成立
int i = 16;//成立
float d = .314F;//成立
double e = c + i + d;//成立，后边运算完后是float，将float赋给double是可以的

~~~



#### 2.4 String类型转换

> **基本转string**

​	一般基本数据类型转字符串只需要加上 + “”即可。

~~~java
int n1 = 1;
String s1 = n1 + "";
System.out.println（s1）;
~~~

其结果为

~~~java
1
~~~



> **String 转 基本**

​	要用到一个方法为Integer.parseInt、double.parsedouble等等

~~~java
String s = "123";
int i = Integer.parseInt(s);
double d = Double.parseDouble(s);
float f = Float.parseFloat(s);
long l = Long.parseLong(s);
byte b = Byte.parseByte(s);
short s1 = Short.parseShort(s);
boolean b1 = Boolean.parseBoolean("true")
~~~

这里是用到的各个基本数据类型对应的包装类中的相应方法来实现的，如int对应的包装类为Integer，double对应包装类为Double。

​	字符串String转字符char时，只能将该字符串的第一个字符提出给char，而且得到的是字符，而不是数字。

​	

​	String型转基本型时，一定要保证字符串内的类型是与基本型相同的，如

~~~java
String s = "hello";
int i = Integer.parseInt(s);
~~~

是不成立的，因为hello无论如何不会变成一个数字。



### 3 运算符

#### 3.1 算数运算符

算数运算符是针对数值的一种运算方式，有+（正）、-（负）、+（加）、-（减）、*（乘）、/（除）、%（余）、++（自增）、--（自减）等等。

> **加减乘的使用**

这部分跟数学里无异，可直接计算

~~~java
int a = 1;
int b = 2;
System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
~~~

其结果为

~~~java
3
-1
2
~~~



> **除法的使用**

使用除法是要注意小数部分的情况，拿10/4举例

~~~java
System.out.println(10 / 4);
System.out.println(10.0 / 4);
double b = 10 / 4;
System.out.println(b);
~~~

上几种输出为

~~~java
2;
2.5;
2.0;
~~~

下面逐步分析原因，第一个输出为2是因为10和4都是int型，其数学上计算出应为2.5，但是计算机中int型为整型，故只保留2；第二个输出为2.5是因为10.0为double型，而当高精度与低精度进行运算时，会自动调整为高精度，故其运算结果为double型，故其结果保留了小数；第三个输出为2.0是因为虽然定义了b为double型，但是10/4仍然是int型，相当于把int赋值给double，是可以成功赋值的，但是其小数部分会先抹除，再补0。



> **取余的使用**

​	取余再java中有一个公示：

~~~java
a % b = a - a / b * b//只对整型有用
~~~

例如

~~~java
System.out.pritnln(10 % 3);
System.out.pritnln(-10 % 3);
System.out.pritnln(10 % -3);
System.out.pritnln(-10 % -3);
~~~

其结果为

~~~java
1;
-1;
1;
-1;
~~~

以上结果直接套公示即可。若是有浮点型参与计算，则有些异议

~~~java
System.out.println(10.0 % 3);
System.out.println(10.0 - 10.0 / 3 * 3);
~~~

其结果为

~~~java
1.0;
0.0
~~~

由此可见，对于浮点型，取余仍是正确的，但是上述公示则不成立了。



> **自增的使用**

​	自增分为i++和++i两种，其中i++为先使用，再自增；++i为先自增后使用

~~~java
int i = 8;
int j = ++i;
int k = i++;
System.out.pritnln(i + " " + j + " " + k);
~~~

其结果为

~~~java
10 9 9
~~~

要注意，虽然有关i的运算是在给j和k赋值的过程中，但是其也对i造成影响，也会使i增加



此处解释一个问题：

~~~java
int i = 1;
i = i++;
System.out.println("i = " + i);
~~~

中间有一个 i = i++ 的过程，其在计算机内分三步实现：

（1）计算机分配一个临时变量temp，将最初i的值赋给temp，即 temp = i； （2）计算机执行 i = i + 1，即i++的过程；（3）将temp的值再给i，i = temp。

其结果为

~~~
i = 1
~~~

若是

~~~
int i = 1;
i = ++i;
System.out.println("i = " + i);
~~~

则其中间i = ++i 的部分执行情况如下：

（2）计算机分配一个临时变量temp，将最初i的值赋给temp，即 temp = i； （1）计算机执行 i = i + 1，即i++的过程；（3）将temp的值再给i，i = temp。

其结果为

~~~
i = 2
~~~



#### 3.2 关系运算符

​	关系运算符也叫做比较运算符，用于对比两个值的关系。其有以下几种：相等于（==）、不等于（！=）、小于（<）、大于（>）、小于等于（<=）、大于等于（>=）等等。关系运算符的运算结果为true或false。其使用如下

~~~java
int a = 8;
int b = 9;
System.out.println(a == b);
System.out.println(a != b);
System.out.println(a > b);
System.out.println(a < b);
System.out.println(a >= b);
System.out.println(a <= b);
boolean flag = a > b;//因为关系运算符运算结果为true或false，故其可赋值给Boolean型变量
System.out.println(flag);
~~~

其结果为：

~~~java
false;
true;
false;
true;
false;
true;
false
~~~



​	有一点要特别注意，当比较两个字符串是否相同是，用equals方法。如

~~~java
String name1 = "我";
String name2 = "你";
if(n1.equals(n2)){
            System.out.println("y");
        }else{
            System.out.println("N");
        }
~~~

其结果为

~~~java
N
~~~



#### 3.3 逻辑运算符

​	逻辑运算符用于连接多个条件，最终的结果为true或false。逻辑运算符有三种，与（&）、或（|）、非（！）、异或（^）。其中与和或还有短路与（&&）、短路或（||）的细分。

> **与运算**

​	与运算是指a与b同时为true时其结果为ture，否则为false。

~~~java
int a = 50;
if(a > 20 & a < 90){
    System.out.println("1");
}
~~~

其结果为

~~~java
1
~~~

​	

​	与传统逻辑与（&）运算而言，有一种更高效的与运算为短路与运算（&&），短路与和逻辑与的结果条件一样，都是当两个同时为true是其结果为true，但是短路与的特点是如果前方的条件已经判断出false了，则不会再继续判断之后的条件，直接输出最终结果false。

~~~java
int a = 4;
int b = 9;
if(a < 1 && b < 11 && b < 10){
    System.out.println("1");
}else{
    System.out.println("2");
}
~~~

其结果为

~~~java
2
~~~

此处因为a<1已经是false了，故之后有关b的两个判断都不再做了，直接输出结果，节省计算时间。

由此可延伸出一个更细节的点，如下

~~~java
int a = 4;
int b = 9;
if (a < 1 & ++b < 15){
    System.out.println("1");
}else{
    System.out.println("2");
}
System.out.println(b)
~~~

其结果为

~~~java
1
10//此处虽然++b是在if的判定中，但是依旧算数，此时计算机给b分配的内存上存储的数已经是10了。
~~~

当然若换成&&就是令一种结果了

~~~java
int a = 4;
int b = 9;
if (a < 1 && ++b < 15){
    System.out.println("1");
}else{
    System.out.println("2");
}
System.out.println(b)
~~~

其结果为

~~~java
1;
9;//由于判断a<1已经可以得出false了，故计算机不会继续往后处理，则++b也就不再处理了
~~~



> **或运算**

​	或运算是指a或b其中只要有一个为true，则其结果为true，只有当a b都是false时其其结果才为false

~~~java
int a = 50;
if(a > 20 | a < 40){
    System.out.println("1");
}
~~~

其结果为

~~~java
1
~~~



短路或与短路与类似，只是判断条件变的完全相反，此处不过多赘述，直接上例子

~~~java
int a = 4;
int b = 9;
if(a > 1 || b > 10 || b > 11){
    System.out.println("1");
}else{
    System.out.println("2");
}
~~~

其结果为

~~~
1
~~~

同理，短路或的延伸跟短路与的延伸一样，不再举例。



> **非运算**

​	非运算也叫取反操作，如果条件本身是true，则非之后为false，反之亦然。

~~~java
System.out.println(6 > 5);
System.out.println(!(6 > 5));
~~~

其结果为

~~~java
true;
false;
~~~



> **异或运算**

​	异或运算为两个条件都同为true或false时，其结果才为false，否则为true。

~~~java
Boolean b1 = (10 > 9) ^ (8 > 7);
Boolean b2 = (10 > 9) ^ (8 < 7);
System.out.println(b1);
System.out.println(b2);
~~~

其结果为

~~~java
false
true
~~~



#### 3.4 赋值运算符

​	赋值运算符分为基本赋值运算符和复合赋值运算符，其中基本赋值运算符就是“ = ”，用来将等号后面的值赋给等号前面的变量。此处重点描述复合赋值运算符。

​	复合赋值运算符分为一下几种： += 、 -= 、*= 、/= 、%= 等等，上述几种赋值运算符都与+=用法一样，故此处只讲述＋=的用法。

> **+=**

​	+=是一种简化的写法，其正常写法如下

~~~java
int a;
a += 1;
a = a + 1;//即a += 1
~~~



> **注意事项**

​	赋值运算符是从右向左运算的，即先运算后赋值；

​	赋值运算符的左边只能是变量，右边可以是变量、表达式、常量

​	复合赋值运算符会进行类型的转换，因为用+=会默认添加一个强制类型转换

~~~java
byte b = 2;
b = b + 3;//不成立，因为3为int型，运算完结果为int，无法赋值给byte。
b += 3;//成立，因为此式子实际上等于b = (byte)(b+2)
~~~



#### 3.5 三元运算符

​	三元运算符的表达式为：

~~~
条件?表达式1:表达式2;
~~~

如果条件为true，则运算表达式1，若条件为false，则运算表达式2。其实质是一个if……else程序。示例如下

~~~java
int a =9;
int b = 99;
int result = a > b ? a : b;
System.out.println(result);
~~~

其结果为

~~~
99
~~~

​	

​	在三元运算中，只会执行其中一个表达式，而另一个表达式不会执行，如下

~~~java
int a =9;
int b = 99;
int result = a > b ? a++ : b++;
System.out.println(result);
System.out.println("a=" + a);
System.out.println("b=" + b);
~~~

其结果为

~~~
99;
9;//由于条件为false，故不执行？后的语句，a不变
100//由于条件为false，故执行：后的语句，b加1
~~~



​	在用三元运算符赋值时，要保证被赋值的数据类型是可以接受表达式1或表达式2类型的类型，如

~~~java
int a = 3;
int b = 4;
int c = a > b? 1.1 : 2.2;//错误
~~~

以上程序就无法编译通过，因为表达式中的数据类型为double，无法转进int中，除非在1.1与2.2前加强转符号。



三元运算符也可以复合运算。如下程序用来输出三个数中最大的数

~~~java
int n1 = 10;
int n2 = 15;
int n3 = 20;
int max1 = n1 > n2 ? n1 : n2;
int max2 = max1 > n3 ? max1 : n3;
System.out.println("max2");
~~~

其复合写法如下

~~~java
int n1 = 10;
int n2 = 15;
int n3 = 20;
int max = (n1 > n2 ? n1 : n2) > n3 ? (n1 > n2 ? n1 : n2) : n3;
System.out.println("max");
~~~



三元运算符是一个整体，其中的数据类型如果不同，要默认转为可转到的最大数据类型。如

```java
int n1 = 1;
double d1 = 2.0;
System.out.println(true? n1 : d1);
```

此处理论上是输出n1，即输出1的，但是由于三元运算符是一个整体，整体内的数据类型要保持一致，故此处会将n1的int型转为double型，最后输出1.0。

#### 3.6 位运算符

​	位运算要用到位运算符，<<（算数左移） 、 >>（算数右移） 、>>>（无符号右移）、<<<（无符号左移）、~2（按位取2的反）、2&3（2按位与3）、2|3（2按位或3）、2^3（2按位异或3）等等。要注意，计算机在运算时，时算各个数字的补码的，而我们看到的结果是计算机算出来的补码反推回的原码。

> **按位与&、按位或|、按位异或^、按位取反~**

​	按位与：两位全为1，结果为1，否则为0；

~~~
2&3:
  	2(补码):00000000 00000000 00000000 00000010
  	3(补码):00000000 00000000 00000000 00000011
   取与得=:00000000 00000000 000000000 00000010
~~~

此时取与后的数为某个数的补码，而这个结果符号位为0，是正数，故补码和原码相同，可知其结果为2；



​	按位或：两位有一个为1，结果为1，否则为0；

​	按位异或：两位不同为1，相同为0；

​	按位取反：1变0,0变1；

~~~
~ -2:
	-2(原码)10000000 00000000 00000000 00000010
	-2(反码)11111111 11111111 11111111 11111101
	-2(补码)11111111 11111111 11111111 11111110
按位取反后得=00000000 00000000 00000000 00000001
运算后的符号位为0，故原码与此补码相同，最终结果为1.
~~~

~~~
~ 2:
	2(原码)00000000 00000000 00000000 00000010
	2(补码)00000000 00000000 00000000 00000010
按位取反得= 11111111 11111111 11111111 11111101
~~~

此结果符号位为1，故该码原码与此补码不同，得进行补码到反码的运算：1）将补码减1得到反码；2）将反码除符号位全部取反得原码

~~~
		11111111 11111111 11111111 11111101
减1后得 =11111111 11111111 11111111 11111100
取原码得=10000000 00000000 00000000 00000011
其结果为 -3
~~~



> **算数左移、算数右移、逻辑右移、逻辑左移**

​	算数右移：若低位溢出，其符号位不变，并用符号位补溢出的高位，如

~~~java
byte a = 1 >> 2;//1右移2位
	1(补码)00000001
 1>>2(补码)00000000 01
        其最终结果为0
~~~

​	右移若干位相当于原数除若干个2；



算数左移：符号位不变，低位补零。如

~~~java
byte a = 1 << 2;//1左移2位
	1(补码)00000001
 1<<2(补码)00000100
        其最终结果为4
~~~

​	左移若干位相当于原数乘乘若干个2；



逻辑移动，也称为无符号移动，即不管符号位，一律视为正常2进制数字，溢出就溢出了。

#### 3.6 运算符的优先级

1）（）、{}、等

2）单目运算符  ++ 、-- 等

3）算数运算符1  * 、 / 、 % 

4）算数运算符2  + 、 - 

5）位移运算符 >> 、 << 等

6）比较运算符1  < 、 >  、 <= 、 >=

7）比较运算符2 ==、！=

8）逻辑运算符 & 、| 、！ 、^等

9）三元运算符 ？ ：

10）赋值运算符 = 、 *= 、 +=等

上述优先级从上到下

有一个表，用的多了就记住了，此处不展开



#### 3.7 标识符

​	当对各种变量、方法、类等命名时所使用的字符都是标识符，或者说凡是自己起名字的地方都成为标识符。如

~~~java
public class a{
    int a;
}
~~~

> **标识符规则**（必须遵守）

​	标识符由26个英文字母的大小写、数字0-9、_或$组成；

​	数字不可作为标识符的开头；

​	不可以使用关键字或保留字，但能包含关键字或保留字（关键字就是java中以有的固定的词语，如class、public等）（保留字是目前java还没使用但是以后可能会使用的一些名词）;

​	标识符严格区分大小写；

​	标识符不能包含空格；

> **标识符规范**（显得更加专业）

​	包名由多个单词组成时所有字母都小写，单词间用点隔开，如

~~~java
apple.bnana
~~~



​	类名、接口名由多单词组成时，所有单词的首字母大写（大驼峰），如

~~~java
AppleBnana
~~~



​	变量名、方法名由多个单词组成时，第一个单词首字母小写，从第二个单词开始首字母大写（小驼峰）。如

~~~java
appleBnana
~~~



​	常量名由多个单词组成时，所有字母都大写，单词间用下划线分开，如

~~~java
APPLE_BNANA
~~~



### 4 控制结构

#### 4.1 顺序控制

​	顺序控制即程序默认的从上到下逐条执行语句，中间没有任何判断或跳转。

​	在顺序控制时要注意，定义的变量一定要向前引用，如

~~~java
int n1 = 1;
int n2 = n1 + 1;
~~~

而不能反过来

~~~java
int n2 = n1 + 1;//错误
int n1 = 1;
~~~



#### 4.2 分支控制

​	分支控制分为if-else控制和Switch控制两种，指当遇到某种情况时执行某个代码。

##### 4.2.1 if -else

if else 分为单分支控制、双分支控制、多分支控制

> **单分支（if）**

if基本语法如下

~~~java
if（条件表达式）{
    执行代码；
}
~~~

如条件满足，则执行if内代码；如条件不满足，则跳过此代码。如判断是否成年

~~~java
import java.util.Scanner;
public class ***{
    public static void main(String[] args){
        Scanner.scanner = new scanner(System.in);
        System.out.println("请输入年龄");
        int age = scanner.nextInt();
        if(age > 18){
            System.out.println("以成年");
        }System.out.println("跳过if内代码继续往下执行");
    }
}
~~~



> **双分支（if...else）**

​	if else 基本语法如下

~~~java
if（条件表达式）{
    执行代码；
}else {
    执行代码；
}
~~~

如条件满足，则执行if部分代码，否则执行else内代码。如上例

~~~java
import java.util.Scanner;
public class ***{
    public static void main(String[] args){
        Scanner.scanner = new scanner(System.in);
        System.out.println("请输入年龄");
        int age = scanner.nextInt();
        if(age >= 18){
            System.out.println("已成年");
        }else{
            System.out.println("未成年")
        }System.out.println("程序继续");
    }
}
~~~



> **多分支（if...else if....else if..）**

​	多分支基本语法如下

~~~java
if(条件表达式){
    执行代码；
}else if(条件表达式){
    执行代码；
}else if（条件表达式）{
    执行代码；
}.....
 else{
     执行代码；
 }

~~~

多分支控制语句是从上到下依次判断的，若上面已经有满足的语句了，则下方的都不进行执行。如判断信用分

~~~java
import java.util.Scanner;
public class ***{
    public static void main(String[] args){
        Scanner.scanner = new scanner(System.in);
        System.out.println("请输入分数");
        int score = scanner.nextInt();
        if(score >= 0 && score <= 100){
        if(score >= 90){
            System.out.println("信用优秀");
        }else if(score > = 75 && score < 90){
            System.out.println("信用良好");
        }else if(score >= 60 && score < 90){
            System.out.println("信用及格");
        }else{
             System.out.println("信用不及格");
        }else{
            System.out.println("输入错误");
        }
        }
        
    }
}
~~~



##### 4.2.2 switch

> **基本语法**

~~~java
switch(表达式){
    case 常量值1 :
        执行代码;
        break;
    case 常量值2:
        执行代码;
        break;
        .....;
        default;
        default执行代码:
        break;
        
}
~~~

​	

> **语法细节**

​	其中switch后表达式为某个数据，且只可以是char、byte、short、int、enum（枚举）这几张数据类型。如

~~~java
switch(a){
    case a:
        System.out.println("a");
        break;
    case b:
        System.out.println("b");
        break;
}
~~~



​	case后的一定是常量，而不能是变量。如

~~~java
char a = 'a';
switch(a){
    case 'a' ://成立，因为'a'为常量
        break;
    case a://不成立，因为a 为自己定义的一个变量
        break;
}
~~~



​	break是直接退出Switch结构，而不单单是退出case；



​	default是当所以case都无法匹配Switch的表达式后执行的部分，Switch后可以没有default。



​	如果某个case后没有break，则程序会去执行这个case后case内的代码，而不去判断这个case后的case是否成立。而如果所以case后都没有break，则程序会在某个case成立后依次执行该case之后的所有程序，最终执行完default后结束。如下

~~~java
import java.util.Scanner;
public class test7 {
    public static void main(String[] args) {
        Scanner myscanner = new Scanner(System.in);
        System.out.println("请输入一个数");
        int n = myscanner.nextInt();
        switch(n){
            case 1 :
                System.out.println("a");
                break;
            case 2:
                System.out.println("b");
            case 3:
                System.out.println("c");

        }

    }
}
~~~

当输入为1，其结果为a。

当输入为2，则其结果为b c。



​	Switch后的表达式中的数据类型应该和case后常量的类型一致，或者是可以自动转换为可以相互比较的类型。如

~~~java
char c = 'a';
switch(c){
    case 'a'://可以成立，因为类型完全一致
        break;
    case 20://可以成立，因为char可以自转为int
        break;
    case "a"://不成立，因为char不可自转为String
        break;
}
~~~



#### 4.3 循环控制

循环控制有for循环，while循环和do while循环。循环控制就是重复执行循环内的代码，直到退出该循环。

##### 4.3.1 for循环

> **基本语法**

~~~java
for（循环变量初始化;循环条件;循环变量迭代）{
    执行代码;
}
~~~

如

~~~java
for(int i = 1; i < 10 ;i++ ){
    System.out.println("i =" + i);
}
~~~

在执行for循环时，先定义完变量后，判断条件，条件成立则执行代码，执行完代码后再进行变量迭代。

> **语法细节**	

​	for循环内一定要有两个分好，分号间可以没内容，但是不能没分号。如

~~~java
int i = 1;
for(;i < 10; i++){
    
}


int j = 1;
for（;i < 10;）{
    i++;
}//效果与上代码一样


for(;;)//此为死循环
~~~



循环变量初始化时可以有很多个变量，但是各个变量的数据类型应该一样，并且中间用逗号隔开；同理，变量迭代也是这样。如

~~~java
for(int i = 0, int j = 0; i < 10; i++ ,j++)
~~~



##### 4.3.2 while 循环

> **基本语法**

~~~java
循环变量初试化;
while(循环条件){
    执行代码;
    循环变量迭代;
}
~~~

其实while循环和for循环思想类似，就是各个要素所在位置不同了而已。

~~~java
int i = 1;
while(i < 10){
    i++;
}
~~~



> **语法细节**

​	循环条件一定是一个布尔型的值，即为true或false。

~~~java
while(true){//此为死循环
    
}
while(false){//不执行此while
    
}
~~~



while循环可以实现实时监听，即一直等待客户输入，否则程序不终止。如

~~~java
import java.util.Scanner;
public class *** {
    public static void main(String[] args) {
        Scanner myscanner = new Scanner(System.in);
        int a = 0;
        while(back != 1){
            System.out.println("请输入1");
            back = myscanner.nextInt();
        }
    }

}
~~~

上程序会一直执行，知道客户端输入了“1”



##### 4.3.3 do while 循环

> **基本语法**

~~~java
循环变量初始化;
do{
    执行代码;
    循环变量迭代;
}while(循环条件);
~~~

do while 与 while不同点就在于do while是一定会先执行一遍之后再判断条件。即do while至少执行一次。



> **语法细节**

与while一样，不再赘述。



##### 4.3.4 多重循环

多重循环是指一个循环嵌套一个循环，在实际编程中常常会用到这种方法。如

~~~java
for(;;){
    while(){
        
    }
}
~~~

但是实际使用时一般不会超过三层嵌套。



若外层循环n次，内层循环m次，则程序会一共执行m*n次。

下面示例为统计3个班级，每个班级5个人的分数情况

~~~java
import java.util.Scanner;
public class **** {
    public static void main(String[] args) {
        Scanner myscanner = new Scanner(System.in);
        int score = 0;
        double sum1 = 0;
        int peoplenum = 0;
        double average1 = 0;
        int passnum = 0;
        int classnum = 0;
        int classpeople = 0;
        System.out.println("请输入共多少班级");
        classnum = myscanner.nextInt();
        for(int i = 1; i <= classnum; i++){
            int sum = 0;
            double average = 0;
            System.out.println("请输入" + i + "班多少人");
            classpeople = myscanner.nextInt();
            System.out.println("请输入" + i + "班中学生的成绩");
            for(int j =1 ; j <= classpeople; j++){
                System.out.println("请输入" + i +"班中学生" + j + "的成绩");
                score = myscanner.nextInt();
                while(score < 0  || score > 100){
                        System.out.println("输入不合法，请重新输入");
                    score = myscanner.nextInt();
                }
                sum += score;
                average = sum/5;
                peoplenum++;
                if(score >= 60){
                    passnum++;
                }
            }
            System.out.println("该班级总成绩为" + sum);
            System.out.println("该班级平均成绩为" + average);
            sum1 += sum;
        }System.out.println("该校平均分为" + sum1/peoplenum);
        System.out.println("该校及格人数为" + passnum);
    }
}
~~~



#### 4.4 跳转控制语句

##### 4.4.1 break

> **基本语法**

​	break语句可以用来终止某个语句块的执行，一般用于Switch、for、while、do while中，其基本代码如下

~~~java
{...
    break;
 ...
    
}
~~~

如

~~~java
for(int i = 0 ; i < 10 ; i++){
    if(i == 3){
        break;
    }
    System.out.println(i);
}
~~~

此处break直接退出了for循环，所以不会再继续打印2以后的数字了。



> **语法细节**

​	break语句在多层嵌套的循环中出现时，可以特地指明要用此break退出某层循环，只要用标签说明一下即可。如

~~~java
lable1:
for(; ;){
   lable2:
    for(; ;){
        if(){
            break lable1;
        }
    }
}
~~~

上程序中break直接退出大循环。

​	在实际开发中，尽量不要使用标签，break默认退出最近的循环体。

​	要注意，当break退出的是大循环内的小循环时，其效果是退出当次大循环的所有小循环，而轮到下次大循环时还是会执行break退出之前的小循环。

~~~java
for(int i = 0 ; i < 3 ; i++){
    for(int j = 0 ;j < 4 ; j++){
        if(j == 2){
            break;
        }
        System.out.println(j)
    }
}

~~~

其结果为

~~~java
0;
1;
0;
1;
0;
1;    
~~~



##### 4.4.2 continue

> **基本语法**

continue用于结束本次循环，进行下一次循环，使用范围和break一致。

~~~java
{...
    continue;
 ...
}
~~~

其使用方法和break一样，但是效果不同

~~~java
for(int i = 0 ; i < 10 ; i++){
    if(i == 3){
        continue;
    }
    System.out.println(i);
}
~~~

在这个循环就与break的循环不同了。其输出为

~~~
0;
1;
2;
4;
...
~~~



~~~java
 for(int i = 0 ; i < 3 ; i++){
            for(int j = 0 ;j < 4 ; j++){
                if(j == 2){
                    continue;
                }
                System.out.println(j);
            }
        }
~~~

这个与break也不同，其输出为

~~~java
0;
1;
3;
0;
1;
3;
0;
1;
3;
~~~



> **语法细节**

与break一样，continue也可以用标签来指明退出某一层的当次循环。不再过多赘述



##### 4.4.3 return

return一般用于方法中，表示跳出所在方法，如果return写在主方法main里，则退出整个程序。在学习方法时详细说明，这里不再介绍。



### 5 数组

#### 5.1 数组

​	数组可以存放多个同一类型的数据，数组也是一种数据类型，是引用类型，因此数组的本质是对象（关于引用类型和对象以后解释）。

​	数组是多个相同类型的数据的组合，便于对这些数据进行统一管理。

​	在说明如何定义变量时用门牌号与房间进行了类比，若如此看，则数组好比某层楼，一层楼中若干个房间。



##### 5.1.1 数组的定义	

​	数组的定义方法有两种，一种是动态初始化，另一种是静态初始化。

> **动态初始化**

​	动态初始化为只规定数组的类型和长度，其内容动态决定。

~~~java
数据类型[] 数组名称 = new 数据类型[长度];
~~~

如

~~~java
int[] array = new int[5]
~~~



也可以先声明一个数组，在对这个数组进行创建。即

~~~java
数据类型[] 数组名称;
数组名称 = new 数据类型[数组长度]
~~~

如

~~~java
int[] array;
array = new int[5];
~~~



> **静态初始化**

静态初试化就是将所有数组的细节一开始全部定义进去的一种方法。

~~~java
数据类型[] 数组名称 = { , , , , ....};
数据类型 数组名称[] = { , , , , ....};//两种都可以
~~~

如

~~~java
int array[] = {1,2,3};
int[] array = {1,2,3};
~~~



> **定义细节**

在定义数组时要注意数组的数据类型和赋予数组的数据要合理，而不能赋予不可自转的数据如

~~~java
int[] arr = {1,2,3};//合理
int[] arr = {1,2,3.1};//不合理，因为3.1为double，无法自转为int
~~~



定义数组而没有赋值，则各个类型的数组有其默认值，如

~~~java
int 默认为 0;
short 默认为 0;
byte 默认为 0;
long 默认为 0;
float 默认为 0.0;
double 默认为0.0;
char 默认为 \u000;
Boolean 默认为 false;
String 默认为 null;
~~~



##### 5.1.2 数组的存取

> **取数**

取数组中某个数用是用下标（位置）来取的，如

~~~java
int[] array = {1,2,3,4,5};
int b = array[4];
System.out.println(b);
~~~

其值为

~~~
5
~~~

表示取该数组中第五个数。

特别要注意，数组的下标是从0开始算的。



遍历一个数组一般用循环实现，如

~~~java
int[] array = {1,2,3,4,5};
for(int i = 0; i < 5; i++){
    System.out.println(array[i]);
}
~~~

在想输出一个数组时，一般都只能用循环实现。



数组的长度可以通过java的一个方法得到

~~~java
数组名.length
~~~

故，在遍历数组时，条件一般为

~~~java
for( ; i < 数组名.length ; ){
    
}
~~~



> **存数**

向数组中存数一般是用Scanner与for循环来实现的。如

~~~java
import java.util.Scanner;
public class *** {
    public static void main(String[] args) {
        Scanner myscanner = new Scanner(System.in);
        int[] array = new int[5];
        for(int i = 0; i < 5; i++){
            System.out.println("请输入数据");
            array[i] = myscanner.nextInt();
        }
        System.out.println(array);
    }
~~~



##### 5.1.3 数组赋值

数组赋值和变量赋值有本质的区别，在各个基本数据类型的变量赋值时，其赋值方式为值拷贝，即值传递，被赋值的变量的变化不会影响原变量，如

~~~java
int n1 = 1;
int n2 = n1;
n2 = 2;
System.out.println(n1);
System.out.println(n2);
~~~

此处n2的改变不会影响n1，其结果为

~~~java
1;
2;
~~~

值拷贝是指，有两个不同的变量，其分别指向两个不同的地址，若将变量1的值赋值给变量2，就是将变量1地址内的数据拷贝一份，直接给到变量2的地址内；



​	但是数组的赋值在默认情况下赋的是地址，是引用传递（地址拷贝），赋值方式是引用赋值。所以被赋值数组的变化会影响赋值数组的变化，如

~~~java
int[] arr1 = {1,1,1};
int[] arr2 = arr1; 
arr2[0]= 2;
System.out.println(arr1[0]);
~~~

其结果会是2，而不是原来的1了。

​	地址拷贝是指，有两个不同的数组，原来其分别指向两个不同的地址，但是将数组1的值赋值给数组2后，是将数组1的地址复制了一份，来替换掉数组2的地址，这样数组1和数组2都指向同一个地址，因此无论从哪一方进行地址内部数据的改变，都会影响到令一方。



若想数组赋值时两数组相互独立，则要用数组拷贝。此时需要定义一个与数组1长度一样的数组，并且数据类型要合理，即数组2的数据类型精度要大于等于数组1。定义完之后对数组1进行遍历，遍历得到数依次赋值给数组2。

~~~java
int[] arr1 = {1, 2, 3};
int[] arr2 = new int[arr1.length];
for (int i = 0; i < arr1.length; i++) {
            arr2[i] = arr1[i];
        }
for(int i = 0; i < arr2.length; i++){
            System.out.print(arr2[i]);
        }
~~~

其结果为

~~~java
1 2 3;
~~~

并且再对arr2修改不会影响arr1。



#### 5.2 二维数组



> **数组定义**

~~~java
arr[i][j];
~~~

​	二维数组可以看成是每个一维数组的元素都是一个一维数组，就组成了一个二维数组。即当一维数组的每个元素不再是数，而是一个数组，就组成了二维数组。

~~~java
arr[i][j]//表示二维数组的第i个一维数组中第j个数
~~~

即每个arr[i]都是一个一维数组，将其整体看为一个一维数组名称，如视arr[i] 为 brr，则arr[i] [j] 就是 brr[j]。

##### 5.2.1 数组定义

> **动态初始化**

​	含义与一维数组一样，都是只定义数据类型和数组长度，不精确到数。

~~~java
数据类型[][] 数组名称 = new 数据类型[长度1][长度2];
~~~

如

~~~java
int arr[][] = new int[2][3];
~~~



也可以用第二种初始化方法

~~~java
数据类型[][] 数组名称;
数组名称 = new 数据类型[长度1][长度2]
~~~



> **静态初始化**

同一维数组一致

~~~ java
数据类型[][] 数组名称 = {{},{} ...}
数据类型 数组名称[][] = {{},{} ...}
数据类型[] 数组名称[] = {{},{} ...}
~~~

由上面第三条就会引出一个易混点

~~~java
int[] x,y[];
~~~

表示

~~~java
int[] x;
int[] y[];
~~~

即x是一个一维数组，而y是一个二维数组的数组

> **定义细节**

二维数组可以先只定义其一维数组的含量，之后再慢慢定义各个一维数组的长度或内容，如

~~~java
int[][] arr = new arr[3][];//只规定此二维数组包含四个一维数组
for(int i = 0; i < arr.length ; i++){//对此二维数组的长度进行循环
    arr[i] = new int[i + 1];//arr[i]是一个一维数组，故适用一维数组的定义方式，用此方式为arr[i]来定义长度
}
for(int j = 0; j < arr[i].length ; j++){//对各个一维数组的长度进行循环
    arr[i][j] = j + 1;//为各个一维数组赋值
}
~~~

​	总之，就是要学会将arr[] [] 中的arr[] 看成一个一维数组的整体。

二维数组可以允许其各个一维数组长度不一，称为列数不确定性。即允许

~~~java
int[][] arr = {{1,2,3,4,5},
               {1,2,3},
               {1,2,3,4}};
~~~



二维数组的遍历需要用双循环

~~~java
int[][] arr = {{1,2,3},{1,2,3,4},{1,2,3,5,7}};
for(int i = 0; i < arr.length; i++){//表示循环二维数组的长度
    for(int j = 0; j < arr[i].length; j++){//表示循环二维数组中每个一维数组的长度
        System.out.println(arr[i][j]);
    }
}
~~~



### 6 面向对象（初级）

#### 6.1 类、对象

##### 6.1.1 关系

​	类实际上是自己定义的一个数据类型，如int、double性质一样，对象就好比数据类型里的具体数据。比如定义一个“猫”类，“猫”类中有一个对象是白猫，其就好比定义一个double类，100.0是double类里的一个具体数据。

​	类是一个泛指，是一种事物的属性、行为等的概括，比如人类、猫类；对象是一个具体的，是类中具体的实例，比如白人、黑人 ， 美短、英短。

类和对象的声明形式如下

~~~java
public class ***{
    public static void mian(String[] args){
        类名 对象名 = new 类名();//new 类名()是为新建的对象分配了一个地址空间，用来存放对象的属性。即实际上有内容的是 new 类名()部分，这部分才是真正的对象，而对象名不过是个名称而已。
        对象名.shuxing1 = *;
        对象名.shuxing2 = *;
    }
}
class 类名 {
    int shuxing1;//属性1（成员变量1）
    double shuxing2;//属性2（成员变量2）
}
~~~

以猫类为例

~~~java
public class ***{//这个是主类，类名与文件名一致即可
    public static void main(String[] args){
        Cat cat1 = new Cat();//由于下面已经创建Cat类了，故这里可以直接用。Cat cat1表示声明一个Cat类的对象，这个对象的名字（用于指代该对象，与对象属性无关）为cat1，new Cat()表示为该对象分配了一个存储空间，该空间内部可以定义此对象的各种属性。
        cat1.age = 1;//表示Cat类中的被cat1所指代的对象年龄为1岁
        cat1.name = "猫猫";//表示Cat类中的被cat1所指代的对象名字为猫猫
    }
}
class Cat {//创建了一个Cat类，下面给Cat类赋予属性
    int age;//Cat类中每个对象（即每个猫）都有年龄这一属性
    String name;//Cat类中每个对象都有名字这一属性
    
}
~~~



##### 6.1.2 属性

在上程序中，属性也叫为成员变量。

属性一般是基本数据类型，也可以是引用类型中的数组或接口、对象。

属性的定义方法和变量的定义方法差不多，就是多了一个访问修饰符，其结构如下

~~~java
访问修饰符 属性类型 属性名;
~~~

​	访问修饰符有四种（public, proctected , 默认 , private），在后面会详细介绍。

​	对象的属性的默认值遵守数组的规则，即

~~~java
int 默认为 0;
short 默认为 0;
byte 默认为 0;
long 默认为 0;
float 默认为 0.0;
double 默认为0.0;
char 默认为 \u000;
Boolean 默认为 false;
String 默认为 null;
~~~



##### 6.1.3 创建对象

创建对象有两种方法，可以先声明再创建，也可以直接创建。以猫类为例

~~~java
Cat cat1 = new Cat();//直接创建，下面为先声明在创建

Cat cat1;//先声明一个Cat类中的对象，系统为其分配门牌号为cat1
cat1 = new Cat()；//为cat1这个门牌号分配房间
~~~

该过程在java内存中的过程如下

​	先在方法区的类信息处加载Cat类信息，查看该类的属性和方法信息；

​	然后在堆中分配空间，进行对象属性的默认初始化，此时完成了对象的创建，对象的各个信息会写在堆中

​	再将堆所在的地址赋给对象cat1所在栈的位置，即让系统为cat1在栈中分配的地址空间的内容中写上该堆地址。

​	为对象的各个属性进行重新定义，相应的其在堆中与方法区里的常量池中的数据会进行对应的改变。

​	

#### 6.2 成员方法

##### 6.2.1 方法定义

​	成员方法（简称方法）与成员变量（属性）都是修饰类用的。拿猫类举例，猫有各种属性，如颜色、年龄等，同时猫也有各种自己的操作（动作），如睡觉、吃饭等，这些操作就是猫类的方法。下面简单举例

~~~java
public class ***{
    public static void main(String[] args){
        Cat cat1 = new Cat();
        cat1.sleep();
    }
}
class Cat{
    String color;
    int age;
    public void sleep(){
        System.out.println("猫会睡觉");
    }
    public void eat(){
        
    }
}
~~~

上程序有好几处要解释一下（针对cat类）

> **public**

​	是一种访问修饰符，public表示方法是公开的；

> **void** 

​	表示方法没有返回值；此处也可以让方法有返回值，比如想返回int型的值，将void变为int，然后再方法内加return即可，如

~~~java
public int sleep(){
    int a = 1;
    return a;
}
~~~

表示将int返回主方法中调用该方法的那行代码，因此要注意在主函数中声明一个int变量来接受该值（接受类型要合理），如

~~~java
public static void mian(String[] args){
	...;
	int a = cat1.sleep();//将方法sleep中的返回值返回到这句话中了，此时cat1.sleep()相当于一个int值。
}
class Cat{
	...;
	public int sleep(){
   	 	int a = 1;
    	return a;
	}
}
~~~



> **sleep()**

​	sleep是方法名，()是形参列表。形参列表中可以声明变量，如（int n1，int n2）表示接受外界输入的两个int值。想使用时只要在调用时的括号内写数就行，如

~~~java
public static void mian(String[] args){
	...;
	cat1.sleep(5,10);
}
class Cat{
	...;
	public void sleep(int n1,int n2){
    	...
	}
}
~~~

表示把5输入进sleep方法中让其计算。



> **{}**

：{}内是方法体，可以写该方法对应的代码，用输出“猫会睡觉”来实现猫类中的睡觉这个方法（拿睡觉吃饭可能有点难理解，如果自己定义一个“加”方法，则大括号内就可以写如何实现这个方法）



> **cat1.sleep（）** 

​	表示在主方法中调用Cat类下的sleep方法，此时运行程序会输出“猫会睡觉”。	方法在创建好之后如果不去调用，则会无事发生。



##### 6.2.2 方法细节

> **访问修饰符**

​	访问修饰符是用来规定方法使用范围的，共有四种修饰符：public protected 默认 priva，细节之后再讲。



> **返回类型**

​	上面说明了如果只返回一个数，则可以在方法创建时把void改成int、double等，单如果想返回若干个数，则基本数据类型就不够用了，因此要用到数组如int[] 、double[]等，如

~~~java
public class ***{
    public static void main(String[] args){
        ...;
        AA a = new AA();
        int[] a1 = a.retruntwo(3,4);//在主方法内接受时，要注意数据类型要与方法返回的数据类型一致。
    }
}

calss AA{
    public int[] returntwo(int n1 , int n2){
        int[] arr = new int[2];
        int n3 = n1 + n2;
        int n4 = n1 - n2;
        arr[0] = n3;
        arr[1] = n4;
        return arr;//此处要保证return的数据类型与void处所在的数据类型兼容
    }
}
~~~

​	返回值的数据类型转变的路径如下：return的变量的数据类型 ——> 方法创建时规定的返回数据类型——> 主方法中用于接受返回值的变量的数据类型。这三者是逐层递增的，要保证其数据类型合理，如

~~~java
public class ***{
    public static void main(String[] args){
        A a = new A();
        double b = a.retrunOne;
    }
}
class A {
    public float returnOne(){
        int n1 = 10;
        return n1;
    }
}
~~~

上述程序的返回值类型是 int ——> float ——> double，是合理的，故可行。



​	返回类型可以是任意数据类型，基本数据类型和引用数据类型都可以。

​	

​	在返回类型为void时，方法中可以没有return语句，若有return，则retrun后不可跟返回值，应只有retrun；，如

~~~java
public void a（）{
...;
...;
return;//此处retrun后不跟值
}
~~~



> **形参列表**

​	注意形参是针对方法的，而属性即成员变量是针对类的，这两个是两个不同概念。

​	一个方法可以有若干个形参，也可以无形参。多个形参时其中间用逗号隔开。

​	参数类型可以是基本数据类型如int、double等，也可以是引用数据类型，如数组等。

​	调用待参数的方法时，要对应着参数列表传入兼容类型的参数。

​	形式参数是指在定义方式时所带的参数、实际参数是指在调用方法时赋值的参数。如

~~~java
public class ***{
    public static void main(String[] args){
        A a1 = new A();
        a1.a(1,2);//此处1,2为实参
    }
}
class A{
    public void a(int a, int b){//此处a , b 是形式参数
        System.out.println(a + b);
    }
}
~~~

相当于形参是指此处可以放数，放啥数实参说了算。实参和形参的类型要兼容，个数和顺序要一致。



> **方法体**

​	方法体即{}内的内容，可以是输入、输出、变量、运算、分支、循环等等，还可以在方法体内调用其他方法，但是不能在方法体内再定义方法。



##### 6.2.3 方法调用

> **同类**

​	同一个类中的方法可以直接调用，如

~~~java
public class ***{
    public static void main(String[] args){
       A a1 = new A();
        a1.useMethod();
    }
}
class A{
    public void print(int a){
        System.out.println("print()方法被调用" + a);
    }
    public void useMethod(){
        print(10);
        System.out.println("ok")
    }
}
~~~

上代码最终结果为

~~~java
print()方法被调用 10
ok
~~~

其程序执行过程为：在主方法内创建一个属于A类的对象---a1，a1调用A类中的方法useMethod，系统查找A类中方法useMethod，发现该方法调用了A类中另外一个方法---print，并将实参10传入print方法，故系统查找并将print方法使用在useMethod方法中，再在主方法中使用useMethod方法。



> **跨类**

​	跨类方法调用，需要通过对象名进行调用，即要在方法内先创建被调用方法所属类的对象，再使用方法，和主方法调用方法一样。如

~~~java
public class ***{
    public static void main(String[] args){
       B b1 = new B();
        b1.b();
    }
}
class A{
    public void print(int a){
        System.out.println("print()方法被调用" + a);
    }
    public void useMethod(){
        print(10);
        System.out.println("ok");
    }
}
class B{
    public void b{
        A a1 = new A();
        a1.useMethod();
    }
}
~~~

其结果为

~~~java
print()方法被调用 10
ok
~~~

​	要注意，跨类的方法调用和方法的访问修饰符有关系，之后细谈。



##### 6.2.5 方法传参

方法的参数可以是基本数据类型如int、double等

~~~java
public void ***(int a){//{doubl a}等都可以
    
}
~~~

也可是引用数据类型，如数组、类等

~~~java
public void **(int[] a){
    
}
~~~

~~~java
class AAA {
    
}
class BBB{
    public void ***(AAA a){//此处参数是AAA类
        
    }
}
~~~

当参数为类时有点抽象，可以类比理解，如当参数为int型时，是int a，即该方法中引入一个int类的实例化对象---a，同理，当参数为类AAA时，是AAA a，即引用的是AAA类中的一个实例化对象 a。

​	只要记住 类是一种数据类型，就好理解了。



> **基本数据类型**

​	对于基本数据类型，参数的传递是值拷贝模式，故在被调用方法内的任意变化都不会影响原方法内的值，如

~~~java
public class ***{
    public static void main(String[] args){
        int a = 1;
        int b = 3;
        A a = new A();
        a.AA(a,b);
        System.out.println(a + " " + b);
    }
}
class A {
    public void AA(int a, int b){//要注意，此处的int a和int b与主方法中的互不想干，就好比两个不同for循环中的int i 一样，各算各的。
        int temp = a;
        a = b;
        b = temp;
    }
}
~~~

此处输出结果为

~~~java
1 3
~~~

会发现a和b的值并没有因为在主方法中调用AA方法（该方法为交换输入两数的值）而改变。



> **引用数据类型**

​	对于引用数据类型，由于其传递是传地址的，故被引用的方法内的变化会影响原方法，如

~~~java
public class ***{
    public static void main(String[] args){
        B b1 = new B();
        int[] arr = {1,2,3}//原数组第一个数字为1
        b1.BB(arr);
         for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i] + " ");
        }//遍历打印原数组
    }
    
}
class B {
    public void BB(int[] arr){
        arr[0] = 2;//此处把传来的数组的第一个数字该为2
        for(int i = 0; i < arr.length; i++){
            System.out.print(arr[i] + " ");
        }//遍历打印该数组
    }
}
~~~

其结果为

~~~java
2 2 3;
2 2 3;
~~~

传递的参数为引用数据类型时，如果方法中的值改变了，则原处的值也会变。

同样的，如果形参为类，也是如此。例如

~~~java
public class ***{
    public static void main(String[] args){
        Person p = new Person();//新建一个person类中的名为p的对象
        p.age = 10;//p对象的属性为 age = 10
        AAA a = new AAA();//新建一个AAA类中的名为a的对象
        a.AA(p);//将在主方法中创建的有属性的p传递给AAA类中的AA方法。
        System.out.println("年龄为" + p.age)
    }
class Person{//该类作为参数被AAA类中AA方法引用
    int age;
}
class AAA{
    public void AA(Person p){//Person p就类比int a、double b等
        p.age = 40;//修改了
    }
}
~~~

其最终结果为

~~~java
40
~~~

有关形参为类，还有以下扩展

~~~java
public class ***{
    public static void main(String[] args){
        person p = new person();
        p.name = "he";
        p.age = 20;
        AAA a = new AAA();
        person p1 = a.AA(p);//此处p1不用再用new person了，因为不需要p1在堆里有自己的空间，只要声明一下p1，让他在栈中有一个空间可以指向某地址即可，然后用方法AA在堆中开辟一个新空间存放p的数据，然后将该方法开辟的空间所在地址赋给p1，这样p1就指向堆中的新空间了，并且新空间的数据是通过方法AA得到的p的数据的拷贝
        System.out.println(p1.name + " " + p1.age);
    }
}
class person {
    String name;
    int age;
}
class AAA {
    public person AA(person p){//此处public 的person就类比void、int、double[]等类，表明该方法返回值是person类的
        person p1 = new person;
        p1.name = p.name;
        p1.age = p.age;
        return p1;
    }//AA方法是用于将传入的person复制一份再传回
}
~~~



##### 6.2.6 方法递归

> **递归概念**

递归可以通俗的理解为在一个方法内重复使用该方法，如

~~~java
public void test(int n){
    if(n > 2){
        test(n - 1);
    }
}
~~~

上述方法就是在test方法内重复使用test方法。递归时，计算机会在栈中重复开若干个test栈（方法），直到该方法结束。最终程序结算时，从最后开的栈依次往前结算。如

~~~java
public class ***{
    Test t = new Test();
    t.test(3);
}
class Test{
    public void test(int n){
        if(n > 2){
            test.(n - 1);//此处属于同类方法调用，可以直接调用
            System.out.println(n);
        }
    }
}
~~~

其最终结果为

~~~java
2;
3;
~~~

上述代码执行流程如下：栈中先有主方法，主方法内调用方法test，并赋值3；在栈中开一个test1栈，将n =3 赋值进去，满足if，执行if内test，再在栈中开一个新test栈，称test2栈，同时将n-1=2赋值给test2,；test2中if不满足，则不执行if内程序，执行输出语句，输出2，然后此栈（test2）销毁，返回test1栈；此时test1栈中，if语句执行完毕（test.(n - 1)执行完毕），继续往下执行，执行输出语句，输出3。执行完毕后此栈销毁；回到主方法栈，t.test(3)语句执行完毕，继续往下执行。



> **递归细节**

​	每执行一个方法时，就创建一个新的栈空间；

​	方法的局部变量如果是独立的，即若是基本数据类型，则各个方法不会相互影响；

​	如果方法内使用的是引用数据类型，如数组、对象等，则各个方法会共享该数据；

​	递归必须向退出递归的条件逼近，如上述程序的if（n > 2）{ test (n - 1)}，就是逐步向退出条件n > 2 逼近。

​	方法执行完毕以后return给调用的语句，当所有因递归而产生的栈退出完毕，则主方法中该递归结束。



##### 6.2.7 方法重载

> **重载概念**

 	方法重载是指可以在同一个类中存在多个同名方法，但是要求这些方法的形参列表不同，如主方法内可以存在若干个system.out.println方法。

~~~java
class A {
    public int a(int n1, int n2){
        return n1 + n2;
    }
    public int a(int n1, int n2,int n3){
        return n1 + n2 + n3;
    }
}
~~~

上述代码是可以成功编译的，因为虽然A类中存在了两个方法a，但是这两个方法a的形参内容不同，因此可以编译，在调用方法时，会根据传入的参数个数，自主选择方法，如

~~~java
public class ***{
    public static void main(String[] args){
        A aa = new A();
        aa.a(1,2);//此处由于传入两个参数，则使用第一个方法a
        aa.a(1,2,3);//同理，这里使用第二个方法a
    }
}
~~~



​	使用方法重载可以简化各个不同方法的命名，也有助于记忆各个同类型方法。



> **重载细节**

​	方法重载的前提是方法名相同，如果方法名都不相同，就无重载的说法了。

​	形参列表必须不同，形参或个数、或数据结构、或顺序要存在不同。要注意

~~~java
public int a(int n1 ,int n2){
    
}
public int a(int a1 , int a2){
    
}
~~~

​	上述两个方法是同一个方法，没有构成方法重载，编译不会通过。因为虽然看似形参列表内存在不同，但是这个不同是形参名称不同而已，形参的个数、数据类型、顺序都相同。如果在主方法中传入两个int型数，计算机会不知道用这两个方法的哪一个。

​	如果在调用方法时存在可以强转和完全符合两种情况同时存在，则用完全符合的方法。如

~~~java
public class ***{
    public static void main(String[] args){
        A a = new A();
        double a = a.aa(20.0,30);//此处传入的是一个double和一个int，如果此时没有第二个方法，是可以直接int强转为double从而使用第一个方法的，而因为第二个方法存在，且完美符合传入的形参类型，故用第二个。
    }
}
class A {
    public double aa(double a , double b){
        
    }
    public double aa(double a , int b){
        
    }
}
~~~

如果让计算机难以判断就会出错，如将上程序改动一下

~~~java
public class ***{
    public static void main(String[] args){
        A a = new A();
        double a = a.aa(20,30);
    }
}
class A {
    public double aa(int a , double b){
        
    }
    public double aa(double a , int b){
        
    }
}
~~~

如果下两个方法只存在一个，则主方法可以成功调用，因为int可以强转double，但是如果两个方法都存在，则主方法部分会报错，因为这时计算机无法判断哪个int来强转double。



​	方法重载对返回值无要求。如

~~~java
public int a(int n1 , int n2){
    
}
public void a(int n1 , int n2){
    
}
~~~

上述两个方法也不构成方法重载，依旧是方法的重复定义，因为虽然两方法的返回类型不一样，但是其形参列表完全相同，故在计算机看来依旧是同一个方法，编译不会通过。



##### 6.2.8 可变参数

> **可变参数概念**

​	java允许将同一个类中的多个同名同功能但是参数个数不同的方法封装成同一个方法。在不知道某个方法要输入多少个参数时可以使用。

​	如要实现求若干个数的和

~~~java
class A {
    public int sum(int n1 ,int n2){
        return n1 + n2;
    }
    public int sum(int n1 ,int n2,int n3){
        return n1 + n2 + n3;
    }
    public int sum(int n1 ,int n2,int n3 , int n4){
        return n1 + n2 + n3 + n4;
    }
    ......
    
}
~~~

​	上方法名称相同，方法思想相同，参数个数不同，则可用可变参数优化如下

~~~java
public int sum(int... nums){
    int res = 0;
    for(int i = 0, i < nums.length ; i++){
        res = res + sum[i];
    }
    return res;
}
~~~

上代码就可实现若干个数相加，下面依次讲解。

​	上代码中，"int..."表示该参数为int类型的可变参数，即可以接受多个int类型的数（0~多个）。

​	nums就是参数名称和int n1中的n1一个概念。但是在可变参数中，nums要当成数组使用，它有数组的属性，因此可以有nums.length，求和时也是遍历数组来求和的。

​	

> **可变参数细节**

​	可变参数的实参可以是数组，即调用该方法时，可以传数组进去。如

~~~java
public class ***{
    public static void main(String[] args){
        int[] n = {1,2,3}
        A AA = new A();
        AA.a(n);
    }
}
class A {
    public void a(int... nums){
        
    }
}
~~~



​	可变参数可以和普通类型的参数一起放在形参列表内，但要保证可变参数放在后面。如

~~~java
public void a(int a , int... b){
    
}
~~~

此时如果有返回值，则一定要找一个最合理的返回类型。



​	一个形参列表中，只能有一个可变参数。

~~~java
public void a(int... a, int... b){
    
}//不合法的写法
~~~



下面举一个实例

~~~java
public class ***{
    public static void main(String[] args){
        AA A = new AA();
       	System.out.println( A.aa("李明", 10,20,30));
    }
    
}
class AA{
    public String aa(String name , double... score){
        double sum;
        for(int i = 0 ; i < score.length ; i++){
            sum += score[i];
        }
        return name + "的总分为" + sum;
    }
}
~~~

其结果为

~~~java
李明的总分为60
~~~



#### 6.3 细节补充

##### 6.3.1 变量作用域

> **概念**

​	在java中，主要的变量分两种，一种是成员变量（成员属性）也称为是全局变量，另一种是局部变量。

​	全局变量的作用域为整个类的整体，而局部变量则一般是指定义在方法中的变量（局部变量也有定义在代码块中的，现在不介绍）。如

~~~java
class Cat{
    int age = 10;//此为全局变量
    public void a(){
        int n = 10;//此为局部变量
    }
}
~~~

​	全局变量可以被整个类中任意一个方法所使用，但是局部变量只能被定义它的方法来使用。



​	全局变量可以不赋值直接使用，因为其有默认值，而局部变量不赋值就无法使用，其没有默认值（默认值看6.1.2的内容）。如

~~~java
class Cat{
    int age = 10;
    int weight;//合法的定义
    public void a(){
        int n;//不合法定义，此处应该赋值来进行变量的初始化
    }
}
~~~



> **细节**

​	局部变量可以和全局变量重名，使用变量时遵从就近原则，或者说在不同的作用域下变量名称可以相同。如

~~~java
class Cat{
    String name = "a";
    public void a(){
        Sting name = "b";
        System.out.println(name);
    }
    public void b(){
        String name = "c";
        System.out.println(name);
    }
}
~~~

其输出为

~~~java
b
c
~~~

​	但是在同一个作用域中无法有重名的变量，如在属性中定义两个变量都叫name或在某个方法中定义两个变量都叫name是不可以的。



​	全局变量可以被本类使用，也可被其他类调用。但是局部变量只可被本类的本方法使用。如

~~~java
class A{ 
    int age = 10;
    public void AA(){
        System.out.println(age);//全局变量被本类使用
    }
}
class B{
    A a = new A();
    System.out.println(a.age);//全局变量跨类使用
}
~~~



​	全局变量可以加修饰符，局部变量不可以加修饰符（修饰符之后学）。



##### 6.3.2 构造器

​	之前再创建对象时，都是先把对象创建好之后再对其属性进行赋值的，如

~~~java
public class {
    public static void main(String[] args){
        A a = new A();//创建对象
    	a.age = 10;//对属性进行赋值
    
    }
   
}
class A {
    int age;
}
~~~

​	而如果想在创建对象的同时就对对象的属性同时进行赋值，就需要用到构造器。构造器是用来完成对象属性初始化的。

> **概念**

​	构造器是一种特殊的方法，在定义构造器时和定义一般方法有些不同，但是规则和一般方法一样。其基本语法为

~~~java
[修饰符] 方法名（形参列表）{
    方法内容;
}
~~~

构造器的修饰符可以是默认；构造器没有返回值；方法名必须和类名一致；参数列表和成员方法规则一样。其使用方法如下

~~~java
public class {
    public static void mian(String[] args){
        A a = new A(10);//此处就可以直接为对象a的属性age赋值为10
    }
}
class A {
    int age;
    public A (int aAge){
        age = aAge;
    }
}
~~~

​	由此可见，当类存在属性时，在类中创建一个构造器会将对象属性初始化的工作量大幅缩短，只需在构造对象时直接定义属性即可

​	

> **细节**

​	构造器也有重载，如

~~~java
class A{
    int age;
    String name;
    public A (int aAge){
        age = aAge;
    }
    public A(String aName){
        name = aName;
    }
}
~~~



​	如果没有定义构造器，则系统会自动给类生成一个默认无参构造器如

~~~java
class A{
	//public A(){}
}
~~~

就为系统自动分配的构造器，在之前学的构造对象时，后面的括号都不加内容，就是调用了这个默认的构造器。

​	一旦自己创建了一个构造器，系统的默认构造器就被覆盖了。如

~~~java
public class ***{
    public static void main(String[] args){
        A a = new A();//编译失败，此为默认构造器时使用的语句，而此时默认构造器已经被覆盖了，因此必须赋值。
        A b = new A(10);//成功编译
    }
}
class A {
    int age;
    public A (int aAge){
        age = aAge;
    }
}
~~~



​	也可以为无参构造器进行语句编写，让所有对象的属性都一样，就是有点显得多此一举。

~~~java
class A {
    int age;
    public A(){
        age = 10;//让所有对象的age都为10，和在定义属性时写int age = 10是一个效果
    }
}
~~~



##### 6.3.3 this关键字

​	在使用构造器时，构造器的局部变量都不能与类的属性一样，因为如果一样相当于没定义，如

~~~java
class A{
    int age ;
    public A(int age){
        age = age;
    }
}
~~~

​	此时无论构对象时传入的age是多少，其age最终都为默认值，即0。因为当局部变量和全局变量重名时，采取就近原则，所以构造器内age = age的两个age都是局部变量定义的age，与全局变量的age毫无关系。

​	所以如果能够将构造器内的局部变量名称定义的与全局变量一样，将极大的增强可读性，此时要用到this。



> **概念**

​	java会给每个对象分配this，代表当前对象，可以通俗的理解为this就是对象的代名词，或者说，this代表本类。用this就可以很好的解决上述问题

~~~java
public class***{
    public static void main(String[] args){
        A a = new A(10);
    }
}
class A{
    int age ;
    public A(int age){
        this.age = age;
    }
}
~~~

此时对象a的age就是10了。

​	this可以理解为是一个指向当前对象的地址的标识符。



> **细节**

​	this关键字可以用来访问本类的属性、方法和构造器。如

~~~java
class A {
    int age;
    public A(int age){
        this.age = age;//this访问属性
    }
    public void test(){
        
    }
    public void t(){
        test();//直接调用本类方法的收到
        this.test();//用this调用本类方法
        //这两种的区别之后再讲
    }
}
~~~

this调用构造器有点特殊，只能在一个构造器中调用另一个构造器。如

~~~java
public class**{
    
}
class A {
    int  age;
    String name;
    public A(int age){
        this.age = age;
    }
    public A (int age , String name){
        this.age = age;
        this.name = name;
    }
    public A(){
        this(10);//此处调用第一个构造器，是由形参列表的匹配与否决定的
        this(10 , "he");//同上理，此处调用第二个构造器
    }
}
~~~

有一个小细节，在调用构造器时，要将this语法放到第一行。



​	this用于区分当前类的属性和局部变量。

​	this只能在类定义的方法中使用。

​	



### 7 面向对象（中级）

#### 7.1 包

​	在之前写程序创建各个类时，会发现不能创建两个相同名字的类，如我建两个A类，是不被允许的，哪怕是在两个不同的.java文件下都不行，这是因为不允许在同一个包下建两个同名类。

​	包可以通俗的理解为文件夹，在同一个文件夹内，不能存在两个名字相同的类。

> **基本语法**

~~~java
package 目录1.目录2;
~~~

​	package是关键字，表示打包；

​	点前方表示上级目录，点后方表示下级目录，若有多个点则依次类推。



在引用两个不同包中相同名称的类时，要在其中一个类引用时声明其包名，如

~~~java
包名.类名 对象名 = new 包名.类名();
~~~



> **命名规范**

​	包名只能包含数字、字母、下划线，不能用数字开头，不能是关键字或保留字。

​	一般是用小写字母来命名各个包（一般用com开头），如

~~~java
com.公司名.项目名.业务模块名;
~~~



> **使用细节**

​	引用包的基本语法为

~~~java
import 包名;
~~~

其也有细分

~~~java
import 包名.类名;
import java.util.Scanner;//表示引入java包下的util包下的Scanner类
~~~

~~~java
import 包名.*;
import java.util.*;//表示引入util包下所有类。
~~~

一般用第一个方法。



​	package的作用是声明当前类所在的包，需要放在类的最上面，一个类最多只有一个package语句。

​	import语句放在package语句与类定义语句之间

~~~java
package 包;
import 包.类;
public class {
    
}
~~~



#### 7.2 访问修饰符

​	java提供了四种访问修饰符，用于控制方法和属性的访问权限

> **访问类别**

公开级别：public， 对外公开（本类、同包、子类、不同包）

受保护级别：protected， 对子类和同一个包中的类公开（本类、同包、子类）

默认级别：没有修饰符，向同一个包的类公开（本类、同包）

私有级别：private，只有类本身可以访问（本类）



> **使用细节**

 	修饰符可以用来修饰类中的属性、方法，但是只有默认修饰符和public修饰符才可以修饰类本身。

​	关于子类部分，学完继承再补充。

​	当修饰符修饰方法时，其规则与修饰属性的规则一样。



#### 7.3 封装

​	封装就是把抽象出来的数据（属性）和对数据的操作（方法）封装在一起，数据（属性）被保护在内部，程序的其他部分只有通过被授权的操作（方法），才能对数据（属性）进行操作。



> **封装步骤**

​	1）首先将属性进行私有化（private），让外部不能直接修改属性；

​	2）提供一个公共（public）set方法，用于对属性判断并赋值，该方法大体流程如下

~~~java
public void setXXX(数据类型 参数名){//XXX为某个属性
    进行逻辑判断，若判断成功，则修改原属性为当前参数名对应的数据
    属性 = 参数名
}
	
~~~

​	3）提供一个公共（public）get方法，用于获取属性的值 

~~~java
public 数据类型 getXXX{
    return xx;
}
~~~

其中set方法和get方法都是官方自带方法，可以自己写，也可以command + N调出。

~~~java
package fengzhuang;

import java.util.Scanner;

public class part1 {
    public static void main(String[] args) {
        person p = new person();
        p.setName("he");
        p.setAge(130);
        p.setIncome(100);
        System.out.println(p.print());
    }
}
class person{
    String name;
    private int  age;
    private double income;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if(age > 1 && age < 120) {
            this.age = age;
        }else {
            this.age = 18;
            System.out.println("输入年龄错误，改为默认18");
        }
    }

    public double getIncome() {
        System.out.println("请输入密码");
        Scanner myscanner = new Scanner(System.in);
        int password = myscanner.nextInt();
        if(password == 123){
            return income;
        }else {
            System.out.println("密码错误，无法查看");
            return 0;
        }
    }

    public void setIncome(double income) {
        this.income = income;
    }
    //以上为get和set

    public String print(){
        return "姓名" + getName() + " " + "年龄" + getAge() + " " + "收入" + getIncome();
    }
}
~~~

其中set方法可以放到构造器内，从而简化代码

~~~java
public person(String name , int age , double income){
        this.setName(name);
        this.setAge(age);
        this.setIncome(income);
    }
~~~



#### 7.4 继承

​	当有很多类的属性和方法有相同，则一般用继承来解决。例如

~~~java
class pupil{
    public String name;
    public int age;
    public double score;
    
    public void testing(){
        System.out.println("小学生" + name + "考小学数学，年龄为" + age + "其成绩为" + score); 
    }
}
~~~

~~~java
class graduate{
    public String name;
    public int age;
    public double score;
    
    public void testing(){
        System.out.println("大学生" + name + "考大学数学，年龄为" + age + "其成绩为" + score); 
    }
}
~~~

上两个代码重复部分极大，因此要用到继承来提高代码复用性。

> **继承概念**

​	继承可解决代码复用问题，当多个类存在相同的属性和方法时，可以从这些类中抽象出父类，在父类中定义这些相同的属性和方法，所有子类不需要重新定义这些属性和方法，只需要通过extends来声明继承父类即可。

​	其格式如下

~~~java
class A extends C{
	A类特有属性;
	A类特有方法;
}
~~~

~~~java
class B extends C{
	B类特有属性；
	B类特有方法；
}
~~~

~~~java
class C {
	A类B类共有属性;
	A类B类共有方法；
}
~~~

其中C类就称为父类，也称基类；A类B类就是C类的子类，也称派生类。其中A类和B类也可以分别拥有自己的子类，即A类B类即当子类，也当父类。



> **继承细节**

​	子类继承父类所有的属性和方法，其中非私有的属性和方法可以在子类中直接访问，但是私有属性和方法不能在子类直接访问，要通过父类提供的公共方法去访问（类比封装中的get方法）



​	子类必须调用父类的构造器，完成父类的初始化。当父类有无参构造器时，默认调用父类的无参构造器，若此时创建一个子类对象，会发现父类的无参构造器被调用了，这是系统默认调用的。

​	若父类中没有提供无参构造器，则必须在子类的构造器中用super（之后学）去指明使用父类的哪个构造器来完成对父类的初始化工作。（如不指明，则在继承时会报错）

​	super（形参列表）可以在子类的某个构造器中使用，用来指定调用父类的与super形参列表匹配的构造器。

​	super在使用时必须放在构造器的第一行。



​	java所有类都是Object的子类。



​	子类最多继承一个父类，若想让一个类继承多个类则要间接继承，即若想a同时继承b和c，可先让a继承b，在让b继承c，则a相当于同时继承b和c

​	

​	不能滥用继承，子类和父类必须满足is~a的逻辑关系，如

~~~
person is a music? No

music extends person//不合理


cat is a animal? Yse

cat extends animal//合理
~~~



​	当某个属性被个各类共有后，在子类中调用该属性，则由近到远查看，即若子类有该属性且可以被访问，则用子类的属性，若子类没有，则依次往上面的类查找，即查看父类有没有，查看“爷爷类”有没有等等，直到查到Object类，若都没有该属性或找到该属性但是属性为私有，会报错。同理，调用方法也是这样。

~~~java
class futher{
    String name = "futher";
    int age = 45;
    private double income = 100;
    String hoby = "1";
}
class son extends futher{
    String name = "son";
    private String hoby  = "2";
}
public class *** {
    public static void main(String[] args){
        son s = new son();
        System.out.println(s.name);//son类本身有name，故输出son类中的name
        System.out.println(s.age);//son类没有age，而futher类有age，故输出futher类age
        System.out.println(s.income);//son类没有income，而futher类的income是私有的，无法直接访问，故会报错。但是son类的对象s是有imcome这个属性的，只是不能直接访问罢了。要想访问，只需在futher类中写一个public的getIncome方法即可
        System.out.println(s.hoby);//由于son类的hoby是私有的，外无法访问，故会报错，而虽然父类的hoby是共有的，但是不会去查找该属性了
    }
}
~~~



#### 7.5 super

​	super代表父类的引用，用于访问父类的属性、方法、构造器。

> **基本语法**

super可以访问父类的属性，但是不能访问父类private属性；super可以访问父类方法，但是不能访问private方法，其访问格式如下

~~~java
super.属性名;
super.方法名（形参列表）
~~~



super可以访问父类构造器，但是只能放在构造器的第一句，其格式为

~~~java
super(参数列表);//根据参数列表不同来选择不同的构造器
~~~

此处就可以发现，在构造器中，super和this不能同时出现，当然也有特殊情况。如

~~~java
public class A {
  String name;
  public A (String name){
    this.name = name;
  }
}
//此为正常使用构造器
~~~

~~~java
public class A {
    String name;
    public draft2(){
    };
    public draft2(String name){
        this.name = name;
    }
}

class d2 extends A{
    int age;
    public d2(){
    }
    public d2(String name,int age){
       // super();
        this();
    }
}
~~~

其结论为：当子类使用父类的无参构造器时,如果不声明，即不写处super()这一语句，则子类的构造器第一行，可以用this(形参列表)来调用子类中自己的构造器。 而如果在子类的构造器中明写了super语句，哪怕写的是默认语句super()，也无法在该构造器内再写this()语句了。

> **使用细节**

​	使用super可以实现父类的属性由父类初始化，子类属性由子类初始化。如

~~~java
class A {

    public A (String name, int age){
        this.name = name;
        this.age = age;
    }
}
class B extends A {
    int income;
    public B (String name , int age , int income){
        super(name,age);
        this.income = income;
    }
}
~~~





​	当子类和父类有成员（属性或方法）重名时，想访问父类的成员，则要用到super，若用this或直接调用则会用到子类的成员。

~~~java
class A {
   
    public void test(){
        System.out.println("A方法")
    }
}
class B extends A{
    int age;
    public void test(){
        System.out.println("B方法")
    }
    public void run_(){
        test();//直接调用test方法，若本类没有，则去父类找，以此类推
        this.test();//this表示调用该方法的对象，依旧是属于本类，故也是从本类开始找test方法
        super.test();//super表示父类的调用，不理睬本类任何方法，直接访问父类、若父类没有再访问爷爷类依次类推到Object类
    }
}

public class ceshi{
    public static void main(String[] args){
        B b = new B();
        b.run_();
        
    }
}
~~~

其结果为

~~~java
B方法;
B方法;
A方法;
~~~



​	super不限于直接父类，也可以是爷爷类等等，super实际上是一个遵循就近原则的向上查找，如子类和爷爷类有重名成员，而父类没有，则用super就访问到爷爷类的成员了。



​	super可以类比this，this是表本类的对象，而super是在子类中访问父类的对象。在调用构造器方面，this和super都只能放在构造器的第一行，故在调用构造器时只能选择本类或父类的其中一个



> **super和this的比较**

| 区别点     | this                                                       | super                                                |
| ---------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| 访问属性   | 访问本类中的属性，如果本类中没有此属性，则从父类中继续查找 | 直接访问父类中的属性，若一级父类没有，则继续向上查找 |
| 调用方法   | 访问本类中的方法，如果本类中没有此属性，则从父类中继续查找 | 直接访问父类中的方法，若一级父类没有，则继续向上查找 |
| 调用构造器 | 调用本类构造器，必须放在构造器的首行                       | 调用父类构造器，必须放在构造器首行                   |



#### 7.6 重写

​	方法重写，简单说就是子类方法和父类方法完全一致（方法名称、返回类型（返回类型可以不同，细节处讲）、形参列表），就称子类的方法重写了父类的方法。 

> **重写细节**

​	要构成重写，要求子类方法的方法名称、形参列表与父类完全一致。

​	关于返回类型，父类的返回类型可以和子类相同，也可是子类返回类型的父类。	

~~~java
public Object getInfo(){
  
}//父类方法
public String getInfo(){
  
}//子类方法
//此处子类方法构成了父类方法的重写，因为String是Object的子类，并且其方法名称和形参列表完全相同
~~~



​	关于访问修饰符，子类方法的访问修饰符不能比父类访问修饰符权限小。

~~~java
protected void run(){
  
}//父类方法
public void run(){
  
}//子类方法
//两方法构成重写，因为子类方法和父类方法三要素完全一致，并且子类方法的访问权限比父类访问权限大
~~~



> **重写和重载**

| 名称             | 发生范围 | 方法名   | 参数列表                       | 返回类型                               | 修饰符                     |
| ---------------- | -------- | -------- | ------------------------------ | -------------------------------------- | -------------------------- |
| 重载（overload） | 本类     | 必须一致 | 类型、个数或顺序至少有一个不同 | 无要求                                 | 无要求                     |
| 重写（override） | 父子类   | 必须一致 | 必须一致                       | 一致或父类返回类型是子类返回类型的父类 | 子类修饰符范围大于等于父类 |



#### 7.7 多态 

​	多态是指方法或对象具有多种形态，多态是建立在封装和继承基础之上的。其中方法的多态实际就是重写和重载所体现的。而多态的重点是对象的多态。

##### 7.7.1 编译类型和运行类型

​	多态主要是对象的各种转型，而转型就要知道编译类型和运行类型

> **编译类型**

~~~java
class Animanl{}
class Cat{}
public class test{
    public static void mian(String[] args){
        Animal a = new Animal();//对象创建
    }
}
~~~

​	看主方法内的对象创建过程，等号左边的Animal是编译类型，a是对象的引用（放在栈中的部分，也即对象的名称），后面new Animal（）部分是对象本体，放在堆中，被a引用。

​	Animal的编译类型决定了再编译器中编程是否可以通过，也即在编译时看对象在Animal类下的属性和功能是否合法，其他细节讲完引用类型再一起说。

> **运行类型**

​	在上代码中，new Animal（）中的Animal是运行类型，它代表了程序在运行时，对象所具有的属性和功能是Animal类下的。



​	上述情况是最简单的情况，即编译类型和运行类型一致了，而java是允许编译类型和运行类型不一致的（前提是类是父子类），这时就会有很多的扩展。如

~~~java
class Animanl{}
class Cat extends Animal{}
public class test{
    public static void mian(String[] args){
        Animal a = new Cat();//对象创建
    }
}
~~~

​	此时编译类型是Animal，但是运行类型变为Cat了。

​	

> **细节**

一个对象的编译类型和运行类型可以不一致；

编译类型载定义对象时就确定了，不可更改；

运行类型可以变化；

编译类型为 “=” 的左边，运行类型为其右边；

当编译类型与运行类型不同时，要求编译类型与运行类型为父子类（或子父类）;



##### 7.7.2 对象多态

​	对象的多态主要是指对象的编译类型和运行类型不同的情况。而这两个类型要满足是父子类的关系。其中转型分为向上转型和向下转型

> **向上转型**

​	多态的向上转型本质上是父类的引用指向了子类的对象（父类在栈里的名称指向了子类在堆里的内容），其语法为：

~~~java
父类 父类引用 = new 子类();
~~~

​	在向上转型时，新建的对象拥有父类的所有属性和方法，但是在调用父类属性或方法时仍要遵守访问权限；

​	向上转型后无法调用子类特有的属性和方法，因为能调用哪些属性或方法是由编译类型决定的，而向上转型的编译类型是父类类型，父类中不包含子类的属性或方法。

​	向上转型后，最终的运行效果主要看子类的内容，如子类有父类的方法重写，则运行该方法时是运行的子类的方法。当某个方法子类没有，只有父类有时，才运行父类的这个方法。



~~~
此部分具体实例看idea中多态部分例子1与2，此处就不再写入了。
~~~



​	

> **向下转型**

由向上转型可以看出一些问题，即向上转型后，无法使用子类特有的属性或方法，而解决这一问题的方法就是向下转型，其本质是将父类对象的地址强制赋值给子类引用，其语法为

~~~java
子类 子类引用 = （子类）父类引用
~~~

由语法可以看出向下转型与向上转型的不同，向上转型是直接将父类的引用直接指向子类的对象，而向下转型是先有一个父类的对象，然后将该对象的地址给子类的引用。



向下转型后编译类型和运行类型就都是子类了。（也不能完全这么说，运行类型在对象创建时就确定好了，向下转型只改变编译类型，而不改变运行类型）



所谓向下转型，可以理解为一个直接创建子类对象的闭环步骤，即

~~~java
父类 父类引用 = new 子类（）;
子类 子类引用 = (子类) 父类引用;
//其约等于
子类 子类引用 = new 子类();

//这两种的区别就是，前者在栈中多了一个父类的引用，而后者只有一个子类的引用。当然，这些引用都指向子类的对象。 
~~~

由此可以看出，向下转型时，要求父类父类引用的指向必须是该子类的对象（即向下转型时，父类再栈中的引用地址是子类再堆中的内容所在的地址）。



> **属性**

多态还会涉及到属性，当父类和子类存在相同属性时，则多态后对象的属性是看编译类型的，此处是与方法不同的。如

~~~java
class A {
  int count = 10;
}
class B extends A {
  int count = 20;
}
class run{
  public static void main(String[] args){
    A a = new B();
    System.out.println(a.count);
  }
}
~~~

其输出为

~~~java
10
~~~



> **动态绑定**

​	动态绑定机制是指，当调用某对象的方法时，该方法会和该对象的运行类型绑定。可以理解为，凡是涉及到方法，都要从运行类型开始找，若运行类型没有，才去找父类。

​	当调用对象属性时，没有动态绑定机制，哪里声明，哪里使用。

具体示例看IDEA。

##### 7.7.3 多态应用

>  **多态数组**

​	多态数组就是类比数组，将若干个对象放进一个数组中，因为类与数组都是引用数据类型，因此其有相似的使用规则。如

~~~java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
  public String say(){
    return name + age;
  }
}

public class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }
    public String say() {
        return super.say() + "\t" + score;
    }
}

public run{
  public static void main(String[] args){
    Person[] p = new Person[2]; 
    p[0] = new Person("a" , 10);
    p[1] = new Student("b", 20 ,30);
  }
  for(int i = 0 ;i < 3 ; i++ ){
    System.out.println(p[i].say());
  }
}
//细节讲解看IDEA多态部分例子3
~~~



>  **多态参数**

多态参数是指在定义一个方法时，令方法的形参列表内为父类类型，然后实际传入参数时传入子类类型，即让形参为父类，实参为子类。

IDEA中多态部分例子1就用到了多态参数。

具体示例看IDEA多态部分例子4。



### 8 面向对象（高级）

#### 8.1 静态

##### 8.1.1 类变量

​	类变量也叫静态变量，是该类所有对象共享的变量。任何一个该类的对象去访问它时，取到的都是相同的值，任何一个该类的对象去修改它时，修改的也都是同一个变量。

> **定义语法**

```java
访问修饰符 static 数据类型 类变量名；
public static int age = 10;//例
```



> **访问方法**

```
类名.类变量名;
A.age;//例，在A类中有一个age的静态变量，就可以直接用类名访问，不需要对象
```

​	当然，也可以用对象来访问静态变量。在访问静态变量的同时，要注意访问区间是与正常变量一样的，要遵循公共、私有等区间。



> **细节**

​	静态变量在加载类时就已经有了，即使没有创建对象，也是已经加载出来了的，故静态变量可以不需要对象来直接访问，静态变量是存放在方法区而不是堆中。而非静态变量则是伴随着对象的创建而加载的，故非静态变量要通过对象访问而不能直接通过类名访问。



##### 8.1.2 类方法

类方法也叫静态方法。

> **定义语法**

```java
访问修饰符 static 数据类型 方法名（）；
public static void run(){}//例
```



> **访问方法**

```
类名.类方法名();
A.run();//例 
```



> **细节**

一般静态方法会大量的应用在工具类，即将工具类的方法设成静态方法，以方便随时调用，提高效率。



类方法中不允许使用和对象有关的内容，如this、super等，也包括非静态变量和非静态方法，而普通方法中则可以有这些。总结一下就是：静态方法中只能有静态方法或静态变量，而不能有非静态方法或非静态变量（指不可直接调用，要通过在静态方法内创建对象再调用），但是非静态方法中都可以有。



类方法和普通方法都是随类加载而加载的，因为方法是存放在方法区中而变量是存放在堆中，故普通变量是随对象加载而加载的，除普通变量外，类变量、类方法、普通方法都是随类加载而加载（注意，方法的加载不等于运行，方法只有在被调用时才运行，方法加载相当于有了但是还不用）



普通方法与对象有关，需要通过对象调用，而不能通过类名调用。而类方法既可以通过对象调用也可以通过类名调用。



##### 8.1.3 main方法

​	从学java到现在，使用 public static void main(String[] args){} 这串字符已经很多遍了，其中的public是访问修饰符、static是静态、void是返回类型、String[] args表示形参列表内部为字符串数组，main为该方法的名称。现在整体说明一下main方法的细节



> **细节**

1。main()方法是被java虚拟机调用的

2。因为要被外部调用，故main方法的访问修饰符要是public的

3。因为调用时为了节省空间提高效率，故而将main方法设成static的静态方法

4。main方法接收String类型的数组参数，该数组中保存执行java命令时传递给所运行的类的参数。其一般不用，具体使用可看P383。



> **使用**

1。在main方法中，可以使用该类的静态成员，因为main方法也是一个静态方法，也正因为如此，mian方法内不可以直接访问本类非静态成员，要先创建对象再调用。



##### 8.1.4 代码块

​	代码块又称为初始化快，属于类中的成员，即是类的一部分。代码块类似于方法，将逻辑语句封装在方法体中，通过{}将其包围起来。

但是其和方法不同的是，其没有方法名，没有返回类型，没有参数，只有方法体，而且不通过对象或类来调用，而是加载类时或创建对象时隐式调用。



> **基本语法**

```
static/空 {代码};
```

其要么是静态的，写static；要么是非静态的，前面就什么都不加，直接写大括号。



> **使用细节**

​	若代码块前加static，则称为静态代码块，其用于对类进行初始化，伴随着类的加载而执行且只执行一次。

​	而由此就要延伸一下类的加载相关知识了：类加载一般分三种情况：首先是创建该类的对象时会加载，或者创建子类对象时子类和父类都会加载(父类先加载，子类后加载)，最后就是使用类的静态成员时会加载类。要注意，在java中，类只会加载一次，因此静态代码块也会随则类的唯一一次加载而进行唯一一次运行。



​	若代码块前无static，则是普通代码块，其在每次创建对象都会执行。即普通代码块是伴随对象的创建而运行的。可以将普通代码块看成时构造器的延伸，他们都在对象创建时才运行。



​	创建对象时，在类中各个不同的成分有调用的先后顺序，下面简单梳理一下：

1、静态属性初始化和调用静态代码块的优先级一样，如果有多个静态代码块和多个静态属性，则按在程序中的先后顺序来调用。（优先级并列第一）

2、普通属性初始化和调用普通代码块的优先级一样，如果有多个普通代码块和多个普通属性，则按在程序中的先后顺序来调用。（优先级次之）

3、调用构造器（优先级最后）

​	再延拓一下，如果两个类存在继承关系，则其各个不同成分的执行顺序如下：

1、父类的静态成分（优先级第一）

2、子类的静态成分（优先级第二）

3、父类的普通成分（优先级第三）

4、父类的构造器（优先级第四）（构造器可以看成是普通成分）

5、子类的普通成分（优先级次之）

6、子类的构造器（优先级最后）







​	之前学过，构造器中默认隐藏了一个super（），即默认调用父类的无参构造器（若无继承则调用Object类的无参构造器），而实际上构造器内还隐藏了一个调用普通代码块，所以在创建对象时才会调用普通代码块。其中super优先级是默认比调用普通代码块高的。而本类中的构造器比代码块优先级低，因此在创建子类对象后，最终的执行顺序为

```
父类普通代码块--->父类构造器---->子类普通代码块---->子类构造器
```

如

```java
public class run{
  
}
class A {
  {
    System.out.println("A普通代码块");
  }
  public A(){
    System.out.println("A构造器");
  }
}
class B extends A{
  {
    System.out.println("B普通代码块");
  }
  public B(){
    System.out.prinln("B构造器");
  }
}
```

其运行结果为

```
A普通代码块;
A构造器;
B普通代码块;
B构造器
```



​	静态代码块只能直接调用静态成员（要通过创建对象来调用），普通代码块可以调用任意成员



总结一下就是：若不创建对象，只加载类，则会加载所有的静态成员（静态属性、静态方法、静态代码块）；若创建了对像，则会加载所有的成员（静态的和非静态的），但是静态成员的优先级大于非静态成员。



##### 8.1.5 单例设计模式

​	设计模式是在大量的实践中总结和理论化后优选的代码结构，编程风格、以及解决问题的思考方式。设计模式中能很好的体现出静态方法和属性的应用。

​	而单例设计模式是指，采取一定的方法保证在整个系统中，对某个类只能存在一个对象实例，并且该类只提供一个取得其对象实例的方法。

​	单例设计模式有两种，饿汉式和懒汉式。

> **饿汉式**

​	实现步骤：

1、构造器私有化，防止用于直接new对象

2、类的内部创建对象

3、向外只提供一个静态的公共方法用于返回类内创建的对象

具体实例看idea中代码single部分



> **懒汉式**

​	实现步骤：

1、构造器私有化

2、类内定义对象引用，不创建对象

3、向外提供创建对象的方法

具体实例看idea中代码single部分



​	懒汉式和饿汉式都是只为外界提供一个对象，但是饿汉式是加载类时直接创建好对象，只等外界引用；懒汉式是只有当外界明确需要创建对象时才会开辟内存来创建对象，空间利用率要比饿汉式高，但是在多线程时懒汉式可能会出问题，以后会细讲。



#### 8.2 final关键字

> **基本介绍**

fianl可用来修饰类、属性、方法和局部变量，其常用有一下几个情况：

1、当不希望类被继承时，即想让某个类为最后一个（final字面意思）类时，可以用final修饰

2、当不希望父类的某个方法被子类重写时，可以用final修饰

3、当不希望类的某个基本数据类型被修改时，可以用final修饰

4、当不希望局部变量被修改时，可以用final修饰

5、当不希望某个引用数据类型的地址改变时，可以用final修饰



> **基本语法**

```
访问修饰符 final ***
```



> **细节**

​	final修饰的属性又称常量（普通的属性是变量），一般用大些字母来命名；



​	final修饰的属性在定义时，必须赋初值，如果不赋值会报错，并且以后不能再修改，赋值可以选在定义时、构造器中、代码块中。如

```java
class A {
	final int I = 10//定义时直接赋值
	{
 	 	I = 10;//若定义时没赋值，则可以在代码块中赋值（一定要先声明再在代码块中赋值）
	}
	public A (){
    I = 10;//常量也可在构造器中赋值
  }
```



​	如果final修饰的属性是静态的，则该属性初始化的位置只能是定义时或者静态代码块中。如

```java
public static final int i = 10;//在定义时赋值
static {
i = 10;//也可在静态代码块中赋值
}
```



​	final类只是不能被继承，但是可以创建其对象。



​	若final类中的某个方法是final的，则该方法虽然不能被重写，但是子类是可以继承该方法来使用的。



​	一般来说，如果一个类已经是final类了，就没有必要再给其方法设置成final方法了。因为该类已经不能有子类了，所以也不会存在方法被重写的情况



​	final不能修饰构造器



​	final和static一起使用在某些情况下不会使类加载，从而节省内存。如

```java
public class A {
	public static void main(String[] args){
		System.out.println(B.i);
		System.out.println(B.j);
	}
}
public class B {
	public final static int i = 10;
	public static int j = 20;
	static {
		System.out.println("B静态代码块")
	}
}
```

其结果为

```
10;
20；
B静态代码块；
```

​	可见，在输出被final修饰的i时，其并不会加载B类，从而导致B类的静态代码块没被加载出来，直到输出没被final修饰的j，才加载B类。因为final加static在一起相当于把某个常量放在了某个类中，而无其他操作，故可以只把常量拿出来而不加载类。



当final修饰引用数据类型时，则该对象的引用地址就不会再改变了，它只能指向该地址，但是地址内的内容是可以变化的。此处对象包括数组，即一个final的数组，数组内容是可以改变的。

#### 8.3 抽象类

​	当父类的一些方法不能确定该如何执行时，比如动物类中有eat方法，但是由于不确定是食草动物还是食肉动物，故无法明确eat的内容。此时就可以用抽象（abstract）来修饰该方法，同时若类中有抽象方法，则该类也要变为抽象类。

> **基本语法**

```java
访问修饰符 abstract 类名{}//用于修饰类
访问修饰符 abstrcat 返回类型 方法名（） ;//用于修饰方法，此时方法无方法体，有形参列表
```

其使用类似于final。



> **细节**

​	抽象类不能被被实例化，即不能创建抽象类的对象。但是虽然抽象类不能被实例化，但是其本质还是类，它可以有正常类所拥有的所有内部结构。



​	抽象类不一定要包括abstract方法，即可以只有类抽象而无方法抽象，但是不能只有方法抽象而类不抽象。



​	abstract只能修饰类和方法



​	如果一个类继承了抽象类，则它必须实现抽象类的所有抽象方法，除非它自己也是一个抽象类。



​	抽象方法是为了被子类重写的，因此，抽象方法不能被private、final、static修饰。其中，private是将方法私有化使其子类无法调用该方法，故而无法重写；final的意义就是将方法设为最终方法，故子类无法重写。

​	关于static修饰方法不能被重写详细说明一下。学完面向对象（中级）可以知道，重写实际上是多态的一种特点，而多态是于对象密切相关的，可以说没有对象就没有多态，而没有多态则重写也无意义。故static这一与类相联系的概念是无法用于override这一于对象相连的操作的。当然子类也可以写一个与父类的某一个static方法一模一样的方法，但这不构成方法重写，而是将父类的方法隐藏了。



##### 看一下p401



#### 8.4 接口

接口就是给出一些没有方法体的方法或属性，封装到一起，当某个类要使用时，在根据具体情况把这些方法写出来

> **使用方法**

```
interface 接口名{}//用于创建接口
class 类名 inplements 接口名{}//用于继承接口
```



> **细节**

1、接口不能被实例化，即不能new一个接口。



2、接口中所有方法都是public的，并且默认隐藏了abstract。如

```java
void run();
```

其实质上是

```java
public abstract void run();
```

但是要注意，在实现该接口的类中，要明确写出访问修饰符public，如果什么都不写，在一般类中会认为是默认，则访问范围变小了，故实现不了。



3、一个普通类实现接口，就要把接口中的所有抽象方法都实现（可以用alt + enter来直接调用 ）。



4、抽象类实现接口，可以不实现接口方法。



5、一个类可以同时实现多个接口，不同接口直接用逗号隔开。



6、接口中的属性只能是final的，而且是静态的。如

```java
int n1 = 10;
```

实际上是

```java
public static final int n1 = 10;
```

由于属性是final的，故定义时必须初始化一个值。



7、接口不能继承其他类，但是可以继承其他多个接口。如

```java
interface A extends B,C{

}
```



8、接口只能用public或默认修饰符来修饰，这点和类的修饰规则一样。



> **接口 VS 继承**

​	如果A类继承了B类，则A类中的对象天生就有B类的成员变量，就拿人来做比喻，儿子继承父亲，则儿子天生就有两条腿，两只手。

​	而接口是对类单继承机制的一种补充，比如父亲不会游泳，故儿子没办法从父亲那里继承来，这时可以用接口来使儿子学会游泳。同理，也可以学会开飞机开汽车等父类不包含的方法。

```java
class A extends B implements C,D
```



继承需要满足 is ——a 的关系，而接口只需满足like——a的关系即可，即接口更加灵活。



> **接口的多态性**

​	凡是实现了接口的类，则该类下的对象都可以传入形参列表为接口的地方去，如example1中的USB接口接收了Mouse对象。即接口的引用可以指向实现了该接口的类的对象。如

```java
public class A {
  public void work(B b){
    b.run();
  }
  pubilc static void main(String[] args){
    C c = new C();
    work(c);//此处可以把C类中的对象c直接传入形参味B接口的方法中
  }
}

interface B{
  void run();
}

class C implements B{
  public void run(){
  }
}
```

以上代码更直接点，则如

```java
B b = new C();
```

也是成立的



同理，多态数组也可以使用

```java
public class run {
    public static void main(String[] args) {
        Usb[] u = new Usb[2];
        u[0] = new Phone();
        u[1] = new Camera();
    }
}

interface Usb{

}

class Phone implements Usb{

}
class Camera implements Usb{

}
```



#### 8.5 内部类

当一个类的内部又完整的嵌套了另一个类结构，则被嵌套的类称为内部类（inner class）、嵌套类的类称为外部类（outer class）。

内部类的最大特点是可以直接访问私有属性，并且体现类与列类直接的包含关系。



> **基本语法**

```java
class Outer{//外部类
	class Inner{//内部类
	
	}
}

class Other{//其他类

}
```



> **内部类的分类**

内部类大分分两种、细分分四种

1、定义在外部类的局部位置上（如方法体内）

​	1）局部内部类（有类名）

​	2）匿名内部类（无类名）

2、定义在外部类的成员位置上

​	1）成员内部类（无static修饰）

​	2）静态内部类（有static修饰）







##### 8.5.1 局部内部类

​	局部内部类一般定义在外部类的方法体内，有时也定义在代码块中，有类名。

> **基本语法**

```java
class Outer{
  {
    class Inner//定义在代码块中
  }
  public void run(){
    class Inner1//定义在方法内
  }
}
```



> **使用细节**

1、局部内部类可以直接访问外部类的所有成员，包括私有成员



2、不能添加访问修饰符，因为局部内部类的地位就是一个局部变量（如与int n1 = 1；地位相同），局部变量不能有访问修饰符，它的使用范围仅仅在定义它的方法或代码块中。



3、局部内部类可以被final修饰。如果用final修饰，则该类不会再被继承了。



4、外部类用局部内部类的成员，需要创建一个内部类的对象，然后再调用。要注意，这个对象要在创建内部类的方法内创建。因为局部内部类相当于是该方法内的一个局部变量，出了该方法，变量就失效了，所以操作要在方法内操作（那为什么局部内部类可以被继承？）



5、如果外部类和内部类存在同名的成员，则遵循就近原则。如果想访问外部类的成员，则使用形式如下

```
外部类名.this.成员
```

其中外部类.this 相当于外部类的对象，谁调用就是谁



6、局部内部类不能有静态成员。



##### 8.5.2 匿名内部类

​	匿名内部类本质是一个自带类体的对象，其定义在方法体或代码块内，有时也用在方法的形参列表内，该类没有名字（实际上是系统自动分配名字），匿名内部类同时还是一个对象。

> **基本语法**

```java
class Outer{
  {//定义在代码块内
    new 类或接口（形参列表）{
      类体
    }
  }
  
  public void run(){//定义在方法内
    new 类或接口（形参列表）{
      类体
    }
  }
  
  public void m1(new 类或接口(){
    
  })
}//定义在形参列表里（前提是该方法原来的形参列表接收的是类）
```



> **使用细节**

1、要注意，匿名内部类自己就是一个对象，其要么继承了一个父类，要么实现了一个接口。如

```java
class A {
  public void m1(){
    B b = new B(){
      //该匿名内部类为一个继承了B的类
      //在计算机内部自动实现了这样一句话：class A$1 extends B
    };
    
    C c = new C(){
      //该匿名内部类为实现了C的类
      //计算机内部自动实现这样一句话：class A$2 implements C
    };
  }
}

class B{
  
}
interface C{
  
}
```



2、观察可以发现，匿名内部类与正常的对象创建十分相似

```java
B b = new B();//此为创建对象
B b = new B(){};//此为创建匿名内部类
```

实际上，匿名内部类是可以直接当对象使用的，如

```java
class A {
	public void m1(){
    new B(){
      public void run(){
        System.out.println("run");
      }
    }.run();//这里可以像对象调用方法一样，直接用点方法来调用，而不需要创建一个引用来调用方法。
  }
}
class B{
  public void run(){
    
  }
}
```



3、由于匿名内部类没有类名，故其把实例化的任务完全交给父类了，自己没有构造器。而局部内部类是可以有构造器的。



4、匿名内部类可以直接访问外部类的所有成员，包括私有的成员。



5、匿名内部类不可有访问修饰符，其地位也是相当于一个局部变量。同理，其作用域也是只有在创建该内部类的方法体或代码块中。



6、每个匿名内部类只有在创建时会加载一次，之后自动就没了，但是由该匿名类创建的对象可以一直使用。



7、如果外部类和内部类存在同名的成员，则遵循就近原则。如果想访问外部类的成员，则使用形式如下

```
外部类名.this.成员
```

其中外部类.this 相当于外部类的对象，谁调用就是谁



8、匿名内部类说白了，就是一个自带类体的对象，该对象的编译类型为new 后面的类型，运行类型为自带的类，在运行时，根据动态绑定机制，一般都是运行自带类体里面的成员。



9、总结来说，匿名内部类，就是在另一个地方创建的一个继承了某个类的子类的实例化。



##### 8.5.3 成员内部类

成员内部类定义在外部类的成员位置（如写属性的地方可以直接写成员内部类，即可以直接写在类的内部供整个类使用，而不需要写在方法体内部仅仅供某个方法使用了），并且没有static修饰。

> **基本语法**

```java
class Outer {
	class Inner{

	}
}
```



> **使用细节**

1、成员内部类可以添加任意的访问修饰符，因为它的地位是一个成员，而不是局部变量了。



2、外部类访问成员内部类，要在外部类里创建一个内部类的对象，再使用内部类的成员，外部类可以访问内部类的成员，包括私有成员。



3、内部类访问外部类可直接访问，包括私有。



4、外部其他类也可访问内部类，有两种方法

```java
class A {
  class B{
    
  }
  public B getB(){
    return new B();
  }
}

class C {
  //第一种方法，先创建一个外部类对象，然后用对象.new 内部类（）来完成内部类的实例化
  A a = new A();
  A.B b = a.new B();
  
  //第二种方法是在外部类内创建一个方法返回内部类对象
 A a1 = new A();
 A.B b1 = a1.getB();
}
```



5、如果内部类的成员和外部类的成员重名，则遵循就近原则。如果想在内部类访问外部类同名成员，则用

```
外部类名.this.成员
```





##### 8.5.4 静态内部类

静态内部类也是定义在外部类成员的位置，其有static修饰

> **基本语法**

```java
class A {
  static class B{
    
  }
}
```



> **使用细节**

1、静态内部类可以直接访问外部类的静态成员，包含私有，但是不能访非静态成员



2、静态内部类可以添加访问修饰，因为其相当于一个类下的成员，其作用范围为整个类。



3、外部类访问静态内部类要先创建内部类对象，在用静态内部类对象去访问内部类成员。



4、外部其他类访问内部静态类相比于访问成员内部类要简单一点，因为静态内部类可以直接通过类名来访问，故而省去了创建对象的步骤（前提是静态内部类的访问修饰权限够大，若是private则无法访问），当然，也可在外部类内写方法来返回内部类对象（此处可以直接写静态方法）

```java
class A {
  static class B{
    
  }
  
  public static B getB(){
    return new B();
  }
}

class C {
  A.B b = A.new B();
  A.B b1 = A.getB();
}
```



5、如果内部类的成员和外部类的成员重名，则遵循就近原则。如果想在内部类访问外部类同名成员，则用

```
外部类名.成员
```

要注意，此处跟其他的类不一样，这里没有.this，是因为静态内部类是静态的，其只能访问外部类的静态成员，而静态成员可以直接用类名访问，故省去this。还有一个原因就是，this是跟对象相关的，而静态成员是无法触及到对象的，故静态内部类不用也不能用this来访问外部类成员。





### 9 枚举、注解

#### 9.1 枚举

枚举，顾名思义，一个一个举例举出来。枚举类一般应用于某些对象是固定的时候。

##### 9.1.1自定义枚举类

所谓自定义枚举类，就是单独写一个类，此类满足以下几个条件

1、不提供seting方法，因为枚举对象只读不改

2、对枚举对象/属性通常使用final+static来修饰

3、枚举对象的命名通常全部大写

4、枚举对象根据需求可以有多个属性

5、枚举类的构造器私有化，避免再次创建对象



##### 9.1.2 关键字实现枚举

所谓关键字实现枚举，就是将类（class）换成枚举（enum），之后进行操作

```
class A {}
enum A {}
```



关键字enum实现枚举类有以下几个点要注意

1、使用enum创建的枚举类会默认继承Enum类（但是与class定义的类都会默认继承Object类不一样，enum类是有且只能有一个父类为Enum，不可再继承其他类了）。但是enum仍然是个类，故其可以实现接口



2、enum类默认是个final类。



3、传统的对象创建变成简单的对象创建

```java
class A {
	public static final A a = new A();//传统对象创建
}

enum A {
  a();//enum对象创建，直接对象名加实参列表（列表内是选构造器用的）
  b;//如果调用午餐构造器，可以直接写对象名，而省略实参列表
}
```

要注意的就是构造器要用对。



4、当有多个枚举对象时，对象间用逗号隔开。枚举对象要定义在枚举类的第一行。



5、调用enum的对象直接用类名.对象名即可



6、调用enum的方法可以用 类名.对象名.方法名



##### 9.1.3 Enum类中的常用方法

由于Enum是所有枚举类的父类，故对其中的常用方法应该有一个基本的了解

> **name**

Enum中提供的name方法是用来返回枚举对象名称的方法

```java
public class A{
  public static void main(String[] args){
    System.out.println(b.name());//此处.name方法返回的是b，b为枚举类中的对象名
  }
}
enum B{
  b();
}
```



其余的在idea中enum3包中补充了

#### 9.2 注解

​	注解（Annotation）也被称为元数据，用于解释 包、类、方法、属性、构造器、局部变量等信息。注解和注释一样，不影响程序的逻辑，但是注解可以被编译或运行，相当于镶嵌在代码中的补充信息。

​	在javaSE中，注解的使用目的比较简单，例如标记过时功能，忽略警告等。在javaEE中注解占据了更重要的角色，例如来配置应用程序等任何切面等。

​	在使用注解时，前面要加@符号，并且应该把注解当成一个修饰符使用，用于修饰它支持的程序元素。注解有以下三个基本用法

1、@Override：限定某个方法，是重写父类方法，该注解只能用于方法

2、@Deprecated：用于表示某个程序元素已过时

3、@SuppressWarnings：抑制编译器警告

​	

​	还有一种修饰注解的注解称为元注解



##### 9.2.1 Override

@Override表示指定该方法为重写的父类方法，在程序编译时，编译器会检查其是否真的重写了，如果没有重写，则会报错

```java
class A {
  public void m1(){
    
  }
}

class B extends A{
  @Override
  public void m2(){}//此处由于m2方法与m1方法方法名不同，故不构成重写，而上面又有重写符号，则编译器会报错
  
  public void m1(){
    System.out.println("m1")
  }//此处虽然没有Override，但是其仍构成父类的m1方法重写。
}
```



​	如果没有写Override注解，但是子类重写了父类方法，则也算是构成重写。即@Override只是去检查某个方法是否构成重写，而不是去令某个方法变成重写方法，是否重写还是看方法本身。



Override只能修饰方法，不能修饰包、类、属性等



##### 9.2.2 Deprecated

​	Deprecated用于表示某个程序元素（类、方法等）已经过时，不再推荐使用。但是过时的元素依旧可以使用，在使用时，该元素上会有一个删除线。

​	Deprecated可以修饰方法、属性、构造器、类、包等参数



##### 9.2.3 SuppressWarnings

​	SuppressWarnings是抑制警告用的，所谓警告就是程序中标黄的位置，其影响比错误（标红的位置）小的多，很多时候可以不用理睬，如果嫌这些警告碍事，就可以用SuppressWarnings来消除



SuppressWarnings是有方法体的，具体想抑制的警告要写在方法内，其内部可以填如下信息：

all ： 抑制 所有警告、 boxing: 抑制与封装/拆封有关的警告 、cast：抑制与强转型有关的警告 等等

```
@SuppressWarnings({"此处写具体消除的部分"})
```



SuppressWarnings的使用范围与放置位置有关，比如将该注解放在方法上，则其会抑制该方法内所有警告、如果放在属性上，则会抑制该属性的警告、如果放在类上，则会抑制该类下的所有警告等等



### 10 异常

#### 10.1 异常概念

​	java中，将程序执行中发生的不正常情况称为异常（语法异常不包括在内，逻辑错误也不算异常）。

​	在程序执行的过程中，发生的异常可以分为两类

1、error：java虚拟机无法解决的严重问题，如jvm系统内部出现错误，资源耗尽等情况。error是严重错误，程序会崩溃



2、exception：该异常是由于其他编程错误或者偶然的外在因素影响而导致的一般性问题，可以使用try-catch方法来进行异常处理。



异常分为两类，一种是运行时异常，一种是编译时异常

​	所谓编译异常，就是指从java源代码时用javac.exe将其编译成class文件时会出现的异常

​	运行异常就是指从.class文件用java.exe将其运行时出现的异常



​	运行时异常编译器不要求强制处理（编译器检查不出来），该异常一般是逻辑错误（如计算2/0是无法计算的，但是编译器无法识别，只有运行时才会知道错误），这类异常很普遍，如果全部处理则程序的效率会很低。但是对于编译时异常，则必须要处理。

​	也就是说，运行时异常可以通过try-catch来测试出来，而编译时异常会直接在编程时标红，要当场该掉。所以重点看运行时异常



#### 10.2 异常导图

|                                   |                       |                         |                                             |
| --------------------------------- | --------------------- | ----------------------- | :------------------------------------------ |
|                                   |                       |                         | StackOverflowError(栈溢出错误)（Error子类） |
|                                   |                       | **Error（错误异常类）** |                                             |
| Serializable(Throwable实现的接口) |                       |                         | OutOfMemoryError(内存不足错误)（Error子类） |
|                                   | Throwable（异常根类） |                         |                                             |
| Object(Throwable继承的类)         |                       |                         | **RuntimeException(Exception子类)**         |
|                                   |                       | Exception（特例异常类） |                                             |
|                                   |                       |                         | FileNotFoundException(Exception子类)        |
|                                   |                       |                         |                                             |

其中黑体：Error、RuntimeException是运行时异常，其他异常为编译时异常。

#### 10.3 常见的运行时异常

以下这些运行时异常都是RuntimeException的子类

> **NullPointerException(空指针异常)**

当应用程序试图在需要数据的地方使用null时，会抛出该异常。如

```java
class A {
  public void m1(){
    String name = null;
    System.out.println(name.length());//此处需要name的长度，而name定义为空，故会抛出空指针异常
  }
}
```



> **AirthmeticException(数学运算异常)**

当出现异常的运算条件时，会抛出该异常。如

```java
class A {
  public void m1(){
    int n1 = 10;
    int n2 = 0;
    int res = n1/n2;//此处由于0不能当除数，故会抛出数学运算异常
  }
}
```



> **ArrayIndexOutOfBoundException(数组下标越界异常)**

用非法索引访问数组时抛出的异常，所谓非法索引，是指索引为负或者大于等于数组大小。如

```java
class A {
  int [] arr = {1,2,3};
  for(int i = 0 ;i <= 3, i++){//此处索引会达到3，当索引为3时其指向的实际上是数组的第四个数，而数组的长度正好为3，故会有数组下标越界异常抛出
   System.out.prinln(arr[i]);
  }
}
```



> **ClassCastException(类型转换异常)**

当试图将对象强转为不是实例的子类时，会抛出该异常。如

```java
class A {
  public static void main(String[] args){
    B b = new C();
    C c = (C)b;//这两句为正常的向上转型后再向下转型的过程
    
    D d = (c)b;//这句是非法的，因为向上转型时并没有引用并没有指向D，故此处会抛出类型转换异常
  }
}
class B {}
class C extends B{}
class D extends B{}
```



> **NumberFormatException(数字格式不正确异常）**

当程序时图将字符串转换成一种数值类型，但该字符串不能转换为适当格式，抛出该异常。如

```java
class A {
	public static void main(String[] args){
    String name = "123";
    int num = Integer.parseInt(name);//此为正常将字符串转为int型数据
    
    String name1 = "何";
    int num1 = integer.parseInt(name1);//此处无法正常转为int，因为此String为汉字。
  }
}
```



#### 10.4 常见编译时异常

编译异常就是指在编译期间就必须处理的异常，否则代码不能通过编译。

1、SQLException : 操作数据库时，查询表可能发生异常

2、IOException: 操作文件时，发生的异常

3、FileNotFOundException:当操作一个不存在的文件时，发生的异常

4、ClassNotFoundException：加载不存在的类时发生的异常

5、EOFException：操作文件，到文件尾部发生异常



#### 10.5 异常处理

异常处理就是当异常发生时，对异常处理的方式，一般分两种：

> **try-catch-finally**

​	程序员在代码内主动捕获异常，然后自行处理。

其程序逻辑如下

```java
try{
  //有可能有异常的代码块
}catch(Exception e){
  //若无异常，则catch代码块不执行
  //当异常发生时，系统将该异常封装成Exception类下的对象e传入catch
  //得到异常对象后，程序员可以把对该异常的处理写在这里
}finally{
  //不管try代码块是否有异常发生，始终要执行finally代码块
  //通常finally里通常写释放资源的代码（关闭程序等等）
}
```



> **throws**

​	将发生的异常抛出，交给调用者来处理。

其处理如下

```
JVM -----> main方法 ------> 被main方法调用的f1方法 ----> 被f1方法调用的f2方法
```

若上方法中的f2方法出现异常了，其可以选择用try-catch-fianlly自己处理，也可以选择用throws抛给f1看f1如何处理。当异常抛给f1后，f1也可以有以上两种选择，若f1也是通过throws抛该main方法，则main方法依旧是两种处理方式二选一，若其最终选择抛异常给JVM机，则JVM不能在抛异常了，JVM机会直接输出异常信息，然后退出程序。



##### 10.5.1 try - catch

​	t-c的基本语法在上面已经介绍了，此处补充一些细节。

> **细节**

1、try-catch方法中可以不包括finally部分



2、如果try内的代码块异常发生了，则异常后面的代码块不会再继续执行，而是直接跳到catch中。在catch执行后，程序会继续执行。但是如果没有catch，则程序会直接结束



3、如果异常没有发生，则会正常执行完try内的代码，并且不再执行catch内的代码，转而继续执行其之后的代码。



4、finally代码块无论是否有异常，程序都会执行



5、可以有多个catch语句，捕获不同的异常，进行不同的业务处理。这个要求子类异常的捕捉写在前，父类异常的捕捉在后。如

```java
public class example02 {
    public static void main(String[] args) {

        try {
            e021 e = new e021();
            e = null;
            System.out.println(e.getName());//此处异常为空指针异常（NullPointerException）

            int n1 = 1;
            int n2 = 0;
            int res = n1 / n2;//此处异常为数学运算异常
            /*
             此处Exception类是空指针异常类和数学运算异常类的父类，故这两个异常都可以捕获到此catch中（多态）
             当然，该catch只能捕第一个异常，因为try内只要发现异常就中断执行转而执行catch了。
             如果想单独捕获两个异常，则可以再分别写catch代码块，将其形参列表改为异常的类
             有一个要注意的点是，子类异常的捕获代码要写再父类异常的捕获代码前面，此处空指针异常和算数异常
            写在了Exception的前面
             */
        } catch(NullPointerException e1){
            System.out.println("空指针异常" + e1.getMessage());
        }catch(ArithmeticException e2){
            System.out.println("算数异常" + e2.getMessage());
        }catch (Exception ex) {
            System.out.println(ex.getMessage());
        }
    }
}

class e021{
    private String name ="j";

    public String getName(){
        return name;
    }
}
```



6、可以直接使用try-finally来运行，这样相当于没有捕获异常去处理该异常，因此程序会直接退出掉。其应用场景为执行一块代码，无论其是否发生异常，都要执行某个业务逻辑。如

```java
public class example03 {
    public static void main(String[] args) {

        try {
            int n1 = 2;
            int n2 = 0;
            int res = n1 / n2;//此处有算数错误
        } finally {
            System.out.println("执行finally");//无论是否发生错误，程序都会执行finally，故会输出此句
        }
        System.out.println("程序结束");//由于存在异常，而且没有用catch来捕捉处理该异常，故程序会直接在执行完finally后中断，不会输出此句

    }
}

```





##### 10.5.2 throws

​	如果一个方法中可能会产生某种异常，但是不能确定如何处理该异常，则由throws来声明该方法并不对这个异常进行处理，而是将该异常交给该方法的调用者。

​	在方法声明中用throws可以声明该方法会抛出多个异常，throws后面的异常类型可以是方法中产生的异常类型，也可以是异常的父类。如

```java
public void m1() throws Exception {
  
}
```



所有程序都必须有异常处理，如果没有声明是t-c，则必是throws。



对于运行异常，程序是有默认处理机制的，即不用声明抛出异常或者抓取，系统会默认将该运行异常抛给JVM，然后JVM通过将程序崩溃来解决该异常。

但是对于编译异常，就必须明确指出是要将异常抛给上级或者在本方法内抓取处理



子类重写父类的方法时，对抛出的异常的规定为：子类重写的方法，所抛出的异常类型要么与父类抛出的异常类型一致，要么为父类抛出异常类型的子类型



如果throws过程中，方法用到了try-catch异常处理，则会用try-catch。



#### 10.6 自定义异常

当程序中出现了某些错误是Throwable的本类或子类中所没有的，这时候就可以自己设计异常类，用于描述错误信息。

> **自定义异常步骤**

1、定义类：自定义异常的类名，该类继承Exception或RuntimeException。

2、如果继承Exception，该自定义异常属于编译异常

3、如果继承RuntimeException，则该自定义异常属于运行时异常（一般来说，继承RuntimeException，因为系统对于运行时异常有默认处理）

```java
class 自定义异常类名 extends RuntimeException{}
```



#### 10.7 throw和throws

| 名称   | 意义                                           | 位置             | 后面接的部分      |
| ------ | ---------------------------------------------- | ---------------- | ----------------- |
| throws | 异常处理的方式（抛出）                         | 方法的方法名后面 | 异常名称          |
| throw  | 手动生成异常对象的关键字（throw new 异常名称） | 方法体内         | new出来的异常对象 |



### 11 常用类

#### 11.1 包装类

包装类是针对八种基本数据类型的，其对应关系如下

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| boolean      | Boolean   |
| char         | Character |
| byte         | Byte      |
| short        | Short     |
| int          | Integer   |
| long         | Long      |
| Float        | Float     |
| double       | Double    |

在知道了这些类之后，调用这些类中的各种方法就变得清晰了。

其中后六个类是继承的Number大类

> **包装类与基本数据类型的转换**

基本数据类型和包装类的相互转换实际上就是指装箱和拆箱。装箱：基本数据类型--->包装类，拆箱相反。

装箱实际上是由基本数据类型到引用数据类型的转换（从int到实例化包装类后的对象）；

同理，拆箱就是将对象变为基本数据类型

​	在jdk5以前，还需要手动装箱和手动拆箱，其步骤如下

```java
int n1 = 10;
        //手动装箱：两种方法
        //方法1：创建对象，将已定义的数据类型放入包装类对象的形参列表中。
        Integer integer = new Integer(n1);
        //方法2：调用包装类的静态方法来创建对象
        Integer integer1 = Integer.valueOf(n1);
 //手动拆箱用包装类的对象调用其方法来拆箱
        int i = integer.intValue();
```



在jdk5以后，就可以自动装箱和拆箱了，其过程更加简单方便

```java
int n2 = 100;
        //在jdk5以后就可以自动装箱
        //其装箱方法就是直接令对象等于基本数据类型。但是其底层使用的仍然是.valueOf()这一方法
        Integer integer2 = n2;

        //也可以自动拆箱
        //直接将对象给数据类型，其底层也是用的.intValue()方法。
        int n3 = integer2;
```

此处只拿integer举例了，其他的包装类也是一样的过程、一样的方法。

实际上平时定义变量都可以用自动装箱理解（但实际上不是这么回事，用包装类的话会在堆中有地址空间，而不用的话只在栈中有空间）

```java
int i = 100;
//其可以理解为将基本数据类型100装箱给int类下的对象i
//Integer i = 100;
//Integer.valueOf(100)
```

！！！有必要看一下valueOf()的源码。



要注意，自动装箱和一直以来用的数据类型定义不是同种关系。如

```java
Double d1 = 1.0;//此为自动装箱，创建的d1是一个Double类的对象，用于接收数据
double d2 = 1.0;//此为正常的数据类型的初始化，d2是一个数据类型为double的数
```

其中d1可以通过Double类中的方法进行拆箱从对象变为一个数

```java
double d = d1.valueOf(1.0);
```



> **包装类与String类型转换**

之前在学变量的时候，已经知道了基本数据类型和String类型的相互转换，现在要介绍的是包装类与String类型的转换。

包装类转String有三种方法，String类转包装类有两种办法

```java
public class example02 {
    public static void main(String[] args) {
        //此处为包装类转string。
        Integer i = 10;//自动装箱

        //此处只是将i和分号变成了一个整体，使这个整体是string类型的。i本身是没有变的，依旧可以输出i
        String str1 = i + "";
        System.out.println(i);
        System.out.println(str1);
        //上方法是包装类转string的第一种方法，下面是第二种方法

        Integer i1 = 10;
        //直接用包装类中的toString方法来转string
        String str2 = i.toString();

        //还可以通过String类中的拆包来转,这个方法实际上也是在方法内部调用类了toString方法
        Integer i2 = 10;
        String str3 = String.valueOf(i2);


      //*********************************************************************************************//
        //此处为String转包装类
        //可以直接通过Integer类的构造器来new一个Integer对象,如果字符串类型不能转int，则会有类型转换错误的异常
        String s1 = "123";
        Integer integer1 = new Integer(s1);
        System.out.println(integer1);


        //也可以通过自动装箱来转换，Interger.parseInt()返回的是基本数据类型int，之后将基本数据类型放入包装类中实现自动装箱
        String s2 = "321";
        Integer integer2 = Integer.parseInt(s2);

    }
}
```

```
疑问：对象是如何与数相比价的？见p464
```



#### 11.2 String类

##### 11.2.1 String类的结构剖析

1、String对象用于保存字符串，其本质是一组字符序列，通常用双引号括起字符序列。字符串使用的是Unicode编码，一个字符占两个字节。

2、之前定义包装类的时候会发现一个现象---以前定义变量时用的是小写（如int i = 1里的int是小写的），故而此时还不是创建对象的过程。但是以前在定义字符串时就已经是大写的了（如String s = "jack"），这实际上就是创建了个String对象。而既然根对象有关，那必然也根构造器有关。String类有很多构造器。

3、String类实现了Serializable接口，实现这个接口就代表String实现了串行化（可以在网络中传输）。

4、String类实现了Comparable接口，实现这个接口代表String实例化后的对象可以进行大小比较。

5、String类是final类，不可被继承。

6、 String类有一个属性是 'private final char value[]'，此为一个数组，该属性就表明了String对象实际上就是一个char字符的集合。于此同时还要注意一个重点，该数组是final的，而可变类型的final就代表了其地址不会再变了（不代表数组内容不变）。即数组value在栈中的地址永远不变，但是在堆中的内容是可变的。 



##### 11.2.2 String类创建剖析

String类实现有两种方式

```java
String s = "jack";//一直以来用的是这种
String s = new String("jack")//通过正常创建对象的流程来实现String
```

这两种方式有本质的区别，第一种方式是不创建对象的，s的值直接从常量池里寻找，若常量池中没有“jack”，则创建一个“jack”进常量池。也就是第一种过程只有栈区和方法区里的常量池两部分。

第二种方式则是先创建对象进堆区，然后用String类中的属性value（上一节中的value）来存放字符。虽然过程不同，但是字符的位置都是在常量池中寻找，不过一个地址直接给栈区，一个地址给堆区罢了。

举例深入说明一下：

```java
public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "abc";
        System.out.println(s1.equals(s2));
        //此输出为True，String类重写类equals方法，是用于比较内容是否相同的，而s1与s2内容都是abc，故True
        System.out.println(s1 == s2);
        //此输出也为True，"=="是用于判断地址是否相等的。首先这两种方法都是不通过堆区，直接在方法区内创建字符的。
        //第一步是s1检查方法区内有无"abc"，发现没有，则在方法区内创建一个字符串"abc"并在栈中将地址指向该方法区
        //第二步由s2检查方法区，发现依据存在"abc"，则直接将该"abc"的地址放如s2的引用中。

        String s3 = new String("def");
        String s4 = new String("def");
        System.out.println(s3.equals(s4));
        //此为True，原理如上equal
        System.out.println(s3 == s4);
        //此为false，因为此时s3与s4指向的地址是堆区的对象了，而这两个对象都是new出来的，故其地址不同。
        //但是，该对象的value[]属性所指向的地址应该是相同的，都指向方法区内的"def"所在地址
        System.out.println();
    }
```



##### 11.2.3 String类的特性

该节主要是一些例题，看IDEA中的例子即可



##### 11.2.4 String类的常用方法

> equals

equals方法区分大小写，用来判断数据内容是否相等



> equalsIgnoreCase

该方法是不关心大小写的方法，也是用来判断内容是否相等的



> length

获取字符串的长度（字符的个数）



> indexOf

获得字符在字符串中第一次出现的的索引、索引从零开始，若找不到，则返回-1



> lastIndexOf

获取字符在字符串中最后一次出现的索引，索引从零开始，若找不到则返回-1



> substring

截取指定范围的字符串



> trim

去除前后空格



> charAt

获取某索引处的字符。众所周知，字符串是不能通过str[0]这种方式来获取该字符串中某个位置的字符的，要用charAt来获取。

```java
string s = "abc";
s[0]; //该方法不对
s.charAt(0) //得这样取
```



以上具体代码看IDEA。IDEA内还有其他方法补充



##### 11.2.5 StringBuffer类

众所周知，String字符串的内容是无法进行修改的，这在使用时又时会有些限制。那么怎么办才能优化这个问题呢？用StringBuffer就行，StringBuffer也是字符串，但是它是可以更改的字符串。

我们可以对StringBuffer进行增删改查。

StringBuffer类实现了Serializble接口，可以进行串行化。

StringBUffer类的父类中定义了成员属性 char[] value，用来存放StringBuffer定义的字符串。该属性和String类中的属性不同，该属性不是final的，代表StringBuffer定义的字符串可以进行改变。

StringBuffer定义的字符串存放在堆中，而不是像String创建的字符串存放在常量池中。

```java
StringBuffer str = new StringBuffer("hello");
```



> String和StringBuffer对比

String保存的是字符串常量，存放在常量池中，每次String引用的更新实际上是新开辟地址来存放新数据，效率低，其内容实际上保存在了private final char[] value中，final决定了该变量是常量的性质。

StringBuffer保存的是字符串数组变量，存放在堆中，每次对StringBuffer引用的改变都是改变堆中相应地址内的内容，节省空间，效率高。其内容存放在char[] value中，其性质是变量。

```java
String str = "hello";
str = "world" //该过程实际上是在常量池新开辟了一个空间，该空间内部存放world，然后str放弃引用hello，转而引用world。
  
StringBuffer str = new StringBuffer("hello");
str = "world" //该过程首先在堆中开辟一个char数组空间存放"hello"，然后将该空间内的hello改为worl d。引用自始至终都不变。
```



> StringBuffer构造器

```java
StringBuffer str = new StringBuffer();//默认构造器，会构造一个数组长度为16的char数组用来存放字符串
StringBuffer str = new StringBuffer(100);//指定构造器1，用来自定义数组长度
StringBuffer str = new StringBuffer("hello");//指定构造器2，构造一个实参长度+16的数组，并将实参传入该数组内
```



> StringBuffer与String的相互转化

```java
//1、str转strbf
String str = "hello";
//用构造器直接转换
StringBuffer sbf = new StringBuffer(str);//用构造器2直接转换
//用append方法转换
StringBuffer sbf = new StringBuffer();
sbf = sbf.append(str);
  
//2、strbf转string
StringBuffer sbf = new StringBuffer("hello");
//用toString方法
String str = sbf.toString();
//是呀String构造器来转换
String str = new String(sbf);

```





> StringBuffer的增删改查

```java
StringBuffer str = new StringBuffer("hello");
        // 增,增是直接在字符串结尾添加内容（数字或字符或字符串都行）
        str.append("he");
        str.append('l');
        System.out.println(str);

        // 删，删是选择一个指定区间，将区间内内容删除，区间访问规则为顾头不顾尾
        str.delete(0,2);
        System.out.println(str);

        //改，改也是确定一个区间，将区间内内容替换为想改内容，只能改为字符串类型的内容，用双引号。访问规则同上。
        str.replace(0,1,"a");
        System.out.println(str);

        //查，查是查找该字符串中某个或某节元素第一次出现的位置，若没该元素则返回-1
        System.out.println(str.indexOf("he"));

        //插，插是选一个指定位置，将指定字符串插入进去，然后将指定位置之后的字符串向后平移，插可插字符也可插字符串
        str.insert(3,"ab");
        str.insert(3,'a');
        System.out.println(str);
```



##### 11.2.6 StringBuilder类

StringBuilder类是可以笼统的理解为StringBuffer类的简易化，它运行起来要比StringBuffer类更快，但是只能在单线程中运行。



StringBuilder类继承 AbstractStringBuilder类、实现了Serializable，该类的对象实例可以进行串行化（在网络中传输、可保存在文件中）



StringBuiler类是final的，不可被继承

StringBuiler类的对象字符也是保存在AbstractStringBuilder类中的char value中，这点与StringBuffer类似。因此字符序列是存放在堆中的。



StringBuiler类的方法与StringBuffer类几乎一样，但是Builder中一般只用append



> String三个类的比较

StringBuiler和StringBuffer类非常相似，均代表可变的字符序列，而且其方法使用也一样。



String是不可变的字符序列，效率低，但是复用率高

StringBuffer是可变字符序列、效率高，线程安全（可多线程）

StringBuilder是可变字符序列，效率最好，线程不安全(不可多线程)



对于String的使用说明：若用String s = "a"来创建一个字符串，则当对s进行修改时，如s += "b"，则是将原来的“a”丢弃，再产生一个新字符串"ab"，这会导致大量副本字符串再内存中残留，降低效率。故若要经常对字符串进行修改，则不宜使用String类





#### 11.3 Math类

Math类包含用于执行基本数学运算的方法，如初等指数、对数、平方根、三角函数等。

建议啥时候用啥时候查，不再细说。



#### 11.4 Arrays类

Arrays类里面包含一系列静态方法，用于管理或操作数组（如排序或搜索）



> toString

toString方法用来返回数组的字符串形式，或者简单理解为遍历数组

```java
int[] intger = {1,2,3,4,5};
//常用的for循环遍历数组
for(int i = 0; i < intger.length;i++){
  System.out.println(intger[i]);
}

//直接用toString方法
System.out.println(Arrays.toString(intger));
//该方法是将数组里内容逐个保存为字符串形式放入StringBuffer中进行返回。
```





> sort

sort方法用于排序，将数组从小到大排一遍。由于数组是引用数据类型，故通过sort方法排序后，会反馈给原数组。

```java
int [] arr = {-1,0,56,12,27};
//正常的冒泡排序（通过双循环，找出最大的往后放）
for(int i = 0 , i < arr.length - 1 , i++){
  for(int j = 0, j < arr.length - i - 1 ,j++){
    int tem = 0;
    if(arr[j] > arr[j+1]);
    tem = arr[j+1];
    arr[j + 1] = arr[j];
    arr[j] = tem;
  }
}
//通过sort来进行排序
Arrays.sort(arr);
```

上面这个sort是最基础的，还有高级的定制排序

```java
Arrays.sort(arr,new Comparator(){
  @Override
  public int compare(Object o1, Object o2){
    Integer i1 = (Integer)o1;
    Integer i2 = (Integer)o2;
    return i1 - i2
  }
})
//此处就不做解释了，用到了匿名内部类实现的Comparator接口，之后就是往上跳回父类看源码，挺复杂，但是核心就是此处重写的compare方法。
```

这里写一个详细的运行过程

```java
public class sort{
  public static void main(String[] args){
    int arr[] = {-1,-3,0,13,5};
    
    bubble(arr,new Comparator c(){
      @Override
      public int compare(Object o1 , Object o2){
        int i1 = (Integer)o1;
        int i2 = (Integer)o2;
        return i1 - i2
      }
    })
    System.out.println(arr);
    
  }
  
  public static void bubble(int[] arr, Comparataor c){
    int temp = 0;
    for(int i = 0 , i < arr.length - 1 , i++){
  		for(int j = 0, j < arr.length - i - 1 ,j++){
    		if(c.conpare(arr[j],arr[j+1])>0){
    			tem = arr[j+1];
    			arr[j + 1] = arr[j];
    			arr[j] = tem;
        }
  		}
		}
	}
}
```

实际上该过程又称为定制排序，即排序的具体内容可以在匿名内部类中自己定义，很方便

> binarySearch

该方法是有序数列的二叉查找方法，即给定一个有序数列，查找某个数据的索引

```java
int arr[] = {1,2,5,8,12};
int index = arr.binarySearch(arr,8);
System.out.println(index);
//输出为3
```



> copyOf

将一个数组从头开始指定长度复制到新数组中

```java
int arr01[] = {1,4,7,9,14};
int arr02[] = Arrays.copyOf(arr01,arr01.length);//将整个数组复制给新数组
int arr03[] = Arrays.copyOf(arr01,arr01.length - 1);//将arr01中除了最后一个数复制给新数组
int arr04[] = Arrays.copyOf(arr01,arr01.length + 1);//将arr01中全部数复制给新数组，之后在最后补一个0
System.out.println(Arrays.toString(arr02));
System.out.println(Arrays.toString(arr03));
System.out.println(Arrays.toString(arr04));
```



还有几个其他的方法就不再一一列举了



#### 11.5本章作业还没写，看p494到p497



### 12 集合

前面我们保存多个数据都是使用的数组，但是数组也是有其自己的不便的。如

数组的长度开始时必须指定，指定后不可更改；保存的必须为同一类型的元素；使用数组进行增加或删除元素的代码较为复杂。而集合可以很好的结局这个问题



#### 12.1 集合框架体系

集合可以动态保存任意多个对象，使用起来极为方便。并且提供了一系列方便的操作对象的方法。

![image-20230306213852629](/Users/changhe/Library/Application Support/typora-user-images/image-20230306213852629.png)

![994798BEB3721DF55F3255D0DCE22D61](/Users/changhe/Library/Containers/com.tencent.qq/Data/Library/Caches/Images/994798BEB3721DF55F3255D0DCE22D61.jpg)



Collection有两个重要的子接口，List和Set，他们的实现子类都是单列集合（单列集合简单理解为传入实参个数为1）

Map接口实现的子类是双列集合，存放key和value（双列集合简单理解为实参个数为2）

要将上两个图熟记。





#### 12.2 Collection

##### 12.2.1集合常用方法

```java
Collection list = new ArrayList();//向上转型

        //add方法，实现添加
        list.add("jack");//装入一个String str = new String("jack")，实际上jack是一个在堆中指向常量池堆对象
        list.add(10);//同上理，Integer int = new Integer(10)，实际上是一个自动装箱的过程，10是一个堆中堆对象
        list.add(true);//同理

				//集合有其自己的toString方法，可以直接打印
        System.out.println(list);

        //remove方法，实现删除
        list.remove(0);//删除第一个元素
        list.remove(true);//删除指定元素true；
        System.out.println(list);//集合中重写了toString方法，可以直接打印

        //contains，查找元素是否存在
        boolean b = list.contains(10);
        System.out.println(b);

        //size，获取list中元素的个数
        System.out.println(list.size());

        //isEmpty，判断list是否为空
        System.out.println(list.isEmpty());

        //clear,清空list
        list.clear();
        System.out.println(list);

        //addAll，添加多个元素，通过另一个集合来添加
        List list2 = new ArrayList();
        list2.add("tom");
        list2.add('a');
        list2.add(3);
        list.addAll(list2);
        System.out.println(list);

        //containsAll,判断多个元素是否都存在，也是通过另一个集合判断，即判断该集合内是否包含另一个集合的全部元素
        list.add(87);
        System.out.println(list.containsAll(list2));

        //removeAll，删除多个元素，通过传入另一个集合，将该集合内与传入集合内容相同的部分删除
        list.removeAll(list2);
        System.out.println(list);

```



##### 12.2.2 集合遍历

由于集合不是数组，它不能通过普通的for循环来取数据，如

```java
int[] i = {1,2,3,4,5};
for(int i = 0; i < i.length, i++){
  System.out.print;n(i[i]);
}
//普通数组可以用简单的for循环来遍历

Collection col = new ArrayList();
col.add(1);
col.add(2);
col.add(3);

col[0];
col[1];
col[2];
//这三个都是错误的语法，因为col是一个对象，它不能用索引来取值
```





那我们怎么在集合中遍历取值呢？



> 迭代器遍历

Collection接口遍历元素的方式是使用迭代器（Iterator）

迭代器是一个接口，即存在接口Iterator，实现了该接口的对象就称为迭代器。

所有实现了Collection接口的集合类都有一个iterator()方法，用来返回一个实现了Iterator接口的对象，即返回一个迭代器。

Iterator仅用于遍历集合，其本身并不实例化对象。

Iterator可以理解成指针，用next来向下一个元素指向。

```java
public class _02_Iterator {
    public static void main(String[] args) {
        Collection col = new ArrayList();
        col.add(new Book("红楼梦",30));
        col.add(new Book("三国演义",50));
        col.add(new Book("西游记",60));


        //使用的iterator()方法是个范型，要有对象来接收它，具体等范型再讲
        Iterator iterator = col.iterator();


        //先判断iterator.hasNext()是否为True，即判断该元素是否还有下一个元素，若有才往下进行，否则列表遍历结束。
        while (iterator.hasNext()) {

            //.next用来返回指向的对象，将对象返回到最大的类Object中，以防止有些对象可能不太同一个小类而报错
            Object next =  iterator.next();

            //print的时候默认调用toString方法，由于多态存在，故虽然next的编译类型是Object，但是
            //它还是用运行类型Book中的方法，此处再由动态绑定机制，来运行Book中的toString方法
            System.out.println(next);

        }
      
      //当循环结束后，此时指针即iterator，指向的是列表中最后一个元素，若想再次进行循环列表，则需要将iterator重制
        iterator = col.iterator();

        while (iterator.hasNext()) {
            Object next =  iterator.next();
            
        }


    }
}

class Book{
    String name;
    int price;

    public Book(String name, int price) {
        this.name = name;
        this.price = price;
    }

    @Override
    public String toString() {
        return "Book{" +
                "name='" + name + '\'' +
                ", price=" + price +
                '}';
    }
}

```





> 增强for循环

集合也可以通过增强for循环来遍历，增强for的语法可能看起来稍微简单点，但是其底层还是迭代器。



其语法如下

```java
for(Object obj : 集合){
  
}
```

如例

```java
public static void main(String[] args) {
        Collection col = new ArrayList();
        col.add(new Book("红楼梦",30));
        col.add(new Book("三国演义",50));
        col.add(new Book("西游记",60));
  
  for(Object book : col){
    System.out.println(book);
  }
```





#### 12.3 List

##### 12.3.1List接口基本介绍

List接口是Collection接口的重要子接口

> 性质

实现了List接口的类（此处特指Vector、ArrayList、LinkedList这三个类），其内部元素是有序的（添加顺序和取出顺序一致，即先入先出的队列），且内容可重复。

```java
 List list = new ArrayList();
        list.add("jack");
        list.add("tom");
        list.add("nancy");
        list.add("tom");//内容可重复
        list.add(100);
        list.add('a');
        System.out.println(list);
```



list集合中每个元素都有系统为其分配的索引，可以直接靠索引取出，用.get(int index)方法做到（这点集合Collection做不到）。

```java
System.out.println(list.get(3));
```





> 方法

之前介绍了集合（Collection）的常用方法，现在再介绍一下List的常用方法

```java
package _02_List._01_method;

import java.util.ArrayList;
import java.util.List;

public class example02 {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("jack");
        list.add("tom");
        list.add("mary");
        list.add("john");


        //add方法，与集合有不同，此处可以指定索引，若不指定也行，则默认加到最后。list可以加入null
        list.add(2,"jery");

        //addAll，用法与集合一样，但是也是多了一个索引可指定插入位置
        List list2 = new ArrayList();
        list2.add("h");
        list.addAll(1,list2);


        //indexOf方法，与集合完全一致，
        System.out.println(list.indexOf("jery"));

        //get方法，与集合一致,get方法返回的是obj对象
        System.out.println(list.get(3));

        //还有些小方法也与集合差不多
        //有一个list特有多set方法，用于替换
        list.set(1,"xiaoming");
        System.out.println(list);





    }

}

```



> 集合遍历

List可以用三种方式来循环，详情看下面代码

```java
package _02_List._2_ergodic;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

/**
 *list的三种循环遍历方式，
 * 1、迭代器
 * 2、增强for
 * 3、普通for（集合不能）
 */
public class test {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("jack");
        list.add("tom");
        list.add("xiaoming");

        //1、迭代器
        Iterator iterator = list.iterator();

        while (iterator.hasNext()){
            Object obj = iterator.next();
            System.out.println(obj);
        }


        //2、增强for
        for(Object obj : list){
            System.out.println(obj);
        }

        //3、普通for
        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}

```



> 排序

用list排序时，可以通过set方法来更改两个对象的位置，而不需要建立中间变量来临时存放搭桥了。

```java
package _02_List._homework;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.Iterator;
import java.util.List;

public class test {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add(new Book("红楼梦","曹雪芹",100));
        list.add(new Book("三国演义","罗贯中",10));
        list.add(new Book("水浒传","施耐庵",1000));
        list.add(new Book("西游记","吴承恩",10000));

        for(Object obj : list){
            System.out.println(obj);
        }

        sort(list, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                Book book1 = (Book) o1;
                Book book2 = (Book) o2;
                return book1.price - book2.price;
            }
        });

        Iterator iterator = list.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println(next);

        }

    }

    public static void sort(List list, Comparator c){
        int listSize = list.size();
        for (int i = 0; i < listSize - 1; i++) {
            for (int j = 0; j < listSize - i - 1; j++) {
                Book book1 = (Book)list.get(j);
                Book book2 = (Book)list.get(j + 1);
                if(c.compare(book1,book2)>0){
                    list.set(j,book2);
                    list.set(j+1,book1);
                }


            }
        }

    }
}


class Book{
    String name;
    String author;
    int price;

    public Book(String name, String author, int price) {
        this.name = name;
        this.author = author;
        this.price = price;

    }

    @Override
    public String toString() {
        return "Book{" +
                "name='" + name + '\'' +
                ", author='" + author + '\'' +
                ", price=" + price +
                '}';
    }
}

```



##### 12.3.2 ArrayList

ArrayList是一个实现了List接口的类，之前将List的时候，都是用ArrayList来实现的，故基本情况介绍的差不多了已经。简单说点注意事项就行



> 注意事项

1、ArrayList可以加入null（空）

2、ArrayList是由数组来实现数据存储的。

3、ArrayList基本等同于Vector（另一个实现了List接口的类），但是ArrayList是线程不安全的（无synchronized修饰），在多线程的时候不宜用ArrayList



4、ArrayList中维护了一个Object类型的数组--elementData，用来存放存入ArrayList中的数据，其创建为

```java
transient Object[] elementData;//transient单词的意思是瞬间，在java中修饰是用来表示一个成员不会被序列化（序列化指保存到硬盘？）
```



5、ArrayListy有两个常用的构造器，一个是无参构造器，一个是指定长度的构造器

```java
ArrayList()；
ArrayList(int)
```

若使用无参构造器，则初始elementData容量为0、第一次超过当前容量时，则扩容elementData至10、若再次超过，则每次扩容1.5倍；

若使用指定大小的构造器，则初始elementData大小为指定大小，若扩容，则扩容至1.5倍



> 源码分析

1、构造器调用过程：

```java
ArrayList list = new ArrayList();//调用无参构造器，跳转
```

```java
public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}//无参构造器跳转到这里，发现其elementData是由DEFAULTCAPACITY_EMPTY_ELEMENTDATA确定，再跳进这串字母中
```

```java
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};//发现就是一个空的{}，故至此，无参构器的ArrayList
//调用完毕，创建了一个空{}。
```



2、向ArrayList中加入数据进而扩容的过程

```java
list.add(1)；//向ArrayList中加入整型--1，跳进add方法。
```

```java
public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }//发现程序并没有急着将列表扩容，而是先将int装箱成Integer，从数据变成对象，以便存放进ArrayList中
```

```java
public boolean add(E e) {
        ensureCapacityInternal(size + 1);  
        elementData[size++] = e;
        return true;
    }//当装箱完毕后，进入真正的add部分，add接收一个对象，然后先进行ensureCapacityInternal判断，看其是否可以进行扩容，跳进去看看
//当判断完ensure后，进行数组的数据添加，将size+1，并在+1前的size位置添加要添加的数据，至此，添加数据完成。主要看上面的扩容机制
```

​		ensureCapacityInternal部分	

```java
private void ensureCapacityInternal(int minCapacity) {
  if(elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA){//判断是否为第一次扩容
     minCapacity = Math.max(DEFAULT_CAPACITY，minCapacity)//扩容为10
  }
  ensureExplicitCapacity(minCapacity)
}//ensureCapacityInternal接受一个minCapacity，其为size+1，当前size为0（因为无参构造器的数组长度是0），minCapacity为1.
		//	然后进行elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA比较，看当前数组是否为初始空数组，发现是，则进而进行minCapacity的赋值，将其赋为（DEFAULT_CAPACITY（其值为10），minCapacity（此时为1））中最大的一个，故而此时minCapacity为10；
//最后进行ensureExplicitCapacity方法，跳进去看看
```

​					ensureExplicitCapacity部分

```java
private void ensureExplicitCapacity(int minCapacity) {
        modCount++;//记录当前集合被修改的次数（用于多线程判断的，不用太在意）

        if (minCapacity - elementData.length > 0)//用当前minCapacity减去当前数组长度，若minCapacity大于数组长度，则进行扩容，即判断若添加数据之后，长度是否溢出，溢出才扩容，不溢出不阔。
            grow(minCapacity);//真正的扩容代码，跳进去看看
    }
```

​									grow部分

```java
private void grow(int minCapacity) {//此时minCapacity为10
        // overflow-conscious code
        int oldCapacity = elementData.length;//将当前数组长度放到变量（老容量）中
        int newCapacity = oldCapacity + (oldCapacity >> 1);//定义新容量= 老容量+老容量/2（>>表示右移，二进制右移一位，则其大小除2（先这么记）），即扩容至1.5倍。但是如果老容量大小为0，则新容量永远为0，这该怎么办呢？用下面的if判断
        if (newCapacity - minCapacity < 0)//若新容量小于min，则将新容量=min，实际上就是第一次扩容时将大小扩容为10
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)//若新容量大于2147483639，则用hugeCapacity处理，就是说容量也不能无限制增加，此处hugeCapacity就不看了
            newCapacity = hugeCapacity(minCapacity);
       
        elementData = Arrays.copyOf(elementData, newCapacity);//将数组内容复制，并将容量变为newCapacity这么大，第一次newCapacity=10,之后就是逐次加1.5倍
    }
```

至此，ArrayList的扩容机制就说明完毕了，此处用的是无参构造器的扩容。若指定构造器，其过程也是一摸一样的，就是不需要进行初次扩容了。也不需要将minCapycity变成10。



##### 12.3.3 Vector

前面说ArrayList时也说了，Vector跟ArrayList基本一样，就是一个线程安全一个线程不安全。

> 注意事项

1、Vector底层也是一个数组对象

```java
protected Object[] elementData;
```



2、Vector是线程同步的，即线程安全，因为其操作有synchronized修饰，如

```java
public synchronized E get(int index){
	...
}
```



3、实际开发中，需要线程安全时，一般用vector。



> 对比

|           | 底层结构                                   | 版本   | 线程与效率     |                                                              |
| --------- | ------------------------------------------ | ------ | -------------- | ------------------------------------------------------------ |
| ArrayList | 可变数组(transient Object[] elementData)   | jdk1.2 | 不安全，效率高 | 如果用有参构造器，则扩容时每次扩容1.5倍；如果是无参构造器，则扩容时先扩容至10，再扩容至1.5倍 |
| Vector    | 可变数组（protected Object[] elementData） | jdk1.0 | 安全，效率低   | 如果是无参构造器，则默认长度为10（与ArrayList不同，Arr中默认为0），每次扩容至2倍；如果是有参构造器，则每次扩容至2倍。 |





##### 12.3.4 LinkedList

> 概念

LinkedList的底层实现了双向链表。其可以添加任意元素（元素可重复）、包括null。LinkedList线程不安全



LinkedList底层维护了一个双向链表。其含三个主要属性：first（Node）、last（Node）、size（int）。其中first和last都属于Node类，是一个对象，first是链表的头节点、last是链表的尾节点，size是一个int属性的数据，记录链表的长度



有关Node类，链表内的每个节点都是个Node对象，Node中有三个属性：item、next、prev。其中next和prev都是Node类下的对象，分别用来指向下一个节点和前一个节点。item是数据本身。



总结一下就是，链表内包含若干个节点，每个节点内有三个属性：前节点信息、本节点数据、后节点信息。



> 简单的双向链表实现

```java
package _03_LinkedList;

public class _01_easy_linkedList {
    public static void main(String[] args) {
        Node first;
        Node last;
        int size;//双向链表的三个属性
        
        Node temp = new Node(); //临时节点，用来临时存放first或last，方便遍历后重制头尾。

        //创建三个节点
        Node jack = new Node("jack");
        Node tom = new Node("tom");
        Node mary = new Node("mary");

        //将三个节点链接起来(是双向链表而不是循环链表，只要保证前后对应即可)
        jack.next = tom;
        tom.next = mary;

        mary.prev = tom;
        tom.prev = jack;

        //将头尾指向节点
        first = jack;
        last = mary;


        //遍历节点
            //从头到尾
        temp = first; //先将first赋值给临时节点
        while (true){
            if(first == null){
                break;
            }
            System.out.println(first);
            first = first.next;
        }
        first = temp; //由于first在循环中移动了，故要在此将first的值重新取回。

            //从尾到头

        temp = last;
        while (true){
            if(last == null){
                break;
            }
            System.out.println(last);
            last = last.prev;
        }
        last = temp;

        //插入节点进某个位置
        //1、先创建节点
        Node smith = new Node("smith");
        //2、将smith插入时，只要将其前后节点的指向改变一下就行


        smith.prev = jack;
        smith.next = tom;

        jack.next = smith;
        tom.prev = smith;


        
        temp = last;
        while (true){
            if(last == null){
                break;
            }
            System.out.println(last);
            last = last.prev;
        }
        last = temp;



    }
}

class Node{ //节点类，定义节点内都应该有什么
    public Object item;
    public Node next;
    public Node prev;//节点的三个属性


    public Node(){}

    public Node(Object o){
        this.item = o;
    }

    public String toString(){
        return "此Node为" + item;
    }
}

```





> 源码分析

主要分析LinkedList的增删改查（主要讲增删）

1、构造器调用

```java
LinkedList list = new LinkedList(); //调用无参构造器，跳转
```

```java
public LinkedList() {}//LinkedList类的无参构造器中什么都没有，故三个属性：size、first、last都是默认值。至此，链表创立完毕
```



2、添加

添加有两种常用的，一种是只指定添加什么数据，默认添加到表尾（下面讲这种）

另一种是既指定添加什么数据，也指定添加到哪个位置，稍微复杂。

```java
list.add(1);//向刚创立的链表对象内部加入int 1。开始跳转
```

```java
public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }//先对int类型进行装箱，装为Integer型对象。再进行下一步
```

```java
public boolean add(E e) { //此处e为Integer型的“1”
        linkLast(e); //此e同样是
        return true;
    }//进入add方法，输入一个参数，返回一个boolean型来确实是否添加成功。add内部调用的是linkLast方法，将add中输入的参数输入进去。跳进linkLast
```

```java
void linkLast(E e) {//尾插法
        final Node<E> l = last;//先将链表中的last赋值给临时尾节点l。
        final Node<E> newNode = new Node<>(l, e, null); // Node(Node<E> prev, E element, Node<E> next)，此为该构造器的三个形参，由此可知，该新节点为：前一个节点是l，内部数据是Integer的“1”，尾节点为空。

        last = newNode;//将该新节点赋值给链表尾部last，即此时链表的last已经时新节点了
        if (l == null)//如果l ==null，即若是空链表
            first = newNode; //则将头节点也指向新节点，即向空链表中添加第一个节点时，头节点和尾节点都是该节点
        else
            l.next = newNode;//若不是空链表，则将l的next设为新节点，而l目前是老链表的尾节点，将尾节点的下一个节点赋值后，该尾节点就变成了倒数第二个节点，新节点变成了尾节点。
        size++;//添加成功链表长度加一
        modCount++;
    }
```

总结一下该算法的精妙之处：在链表内添加新节点，该新节点在构造时，就将老链表的尾节点置为该添加节点的前节点，这样省心点。然后判断是否为空链表，若为空链表，则只将头节点指向该新节点即可；若不为空链表，则不用管头节点了（因为此时头节点一定指向了第一个添加的节点上），只用将老链表的尾节点的后节点指向新节点即可。

3、再次添加

过程和第一次添加一样，就是最后if判断的时候走下面的过程。

```java
list.add(1);
```



4、删除节点

删除节点有三种：默认删除队头节点、指定删除某个位置的节点、指定删除某个元素的节点。此处讲默认

```java
list.remove();//跳进remove方法
```

```java
public E remove() {
        return removeFirst();
    }//返回删掉的节点是哪个，调用removeFirst方法，跳入该方法
```

```java
public E removeFirst() {
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return unlinkFirst(f);
    }//将头节点赋值给一个临时节点，然后判断是否为空表，若空则无法删除，抛出异常、若不空则执行unlinkFirst方法，并将头节点传入。跳入该方法
```

```java
private E unlinkFirst(Node<E> f) {
        // assert f == first && f != null;
        final E element = f.item; //将头节点数据取出
        final Node<E> next = f.next;//将头节点的next取出赋值给next，
        f.item = null;
        f.next = null; //取出之后将f节点置空，此处不用置prev信息，因为头节点的prev已经是空了。
        first = next;//将链表的first指向头节点的next，此时该next为新的头节点
        if (next == null)//若新头节点为空
            last = null;//则意思是将老链表的头节点取出后链表就空了，故将last也置空
        else
            next.prev = null;//若头节点后还有节点，则将新头节点的前节点置空，（因为链表头节点前面就是没节点的）
        size--;//将链表大小减一
        modCount++;
        return element;//将老头节点的数据部分返回
    }
```





> Ar rayList和LinkedList的比较

|            | 底层结构 | 增删效率           | 改查效率                                 |
| ---------- | -------- | ------------------ | ---------------------------------------- |
| ArrayList  | 可变数组 | 较低、通过数组扩容 | 较高、通过索引直接定位                   |
| LinkedList | 双向链表 | 较高、通过链表追加 | 较低、得到索引后需要遍历才能得到指定节点 |

总结：增删用LinkedList，改查用ArrayList。





#### 12.4 Set

##### 12.4.1 Set接口基本介绍

set接口是实现了Collection接口的另一重要接口。

set接口是无序的，添加或取出元素的顺序是不一致的，且无索引

set接口不允许添加重复元素，可以添加null，但由于不可重复，故只能有一个null

由于set接口也实现了Collection，故其常用方法与Collection一致，有增删改查等等。

set接口的遍历也是可以用迭代器或增强for来遍历，但是不能用普通for加索引来遍历，这是list特有的遍历方式。



> 性质

实现了set方法的类有两个：treeSet和HashSet，下面用HashSet实现Set接口来说明一下set接口的方法（总要有类来实现接口，要不无法查看接口方法）

```java
package _04_Set._01_method;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class method {
    public static void main(String[] args) {

        //以Set接口的实现类：HashSet类来实例化对象讲解Set方法
        //Set接口的实现类的对象（简称Set接口的对象，此处指HashSet类的对象），
        // 不能存放重复元素（可以放，但是不存），可以添加null，并且添加顺序与取出顺序不一致
        //但是要注意，Set的取出顺序虽然与添加顺序不一致，但是取出数据不是随机的，而是固定的，即每次取出都以这种顺序取出


        Set set = new HashSet();
        set.add("john");
        set.add("jack");
        set.add("tom");
        set.add("john");//重复
        set.add(null);
        set.add(null);//重复

        System.out.println(set);

        //遍历
        //1、迭代器
        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            Object o = iterator.next();
            System.out.println(o);
        }

        //2、增强for
        for(Object o : set){
            System.out.println(o);
        }
    }
}

```





##### 12.4.2 HashSet

HashSet实现了Set接口，Set的方法HashSet都能用。



HashSet的底层是HashMap，可看其构造器源码：

```java
Set HashSet = new HashSet(); //调用HashSet构造器
```

```java
public HashSet(){  //构造器具体内容
  map = new HashMap<>();//实际上new了一个HashMap
}
```



HashSet可以存放null，但是只能放一个null（可以写的时候放很多，但是只会保存一个），其他元素也一样，只能放一个。



HashSet接口是无序的，添加或取出元素的顺序是不一致的，且无索引。但是取出数据不是随机的，而是固定的，即每次取出都以这种顺序取出。



> HashSet的底层说明

HashSet的底层是HashMap，而HashMap的底层是：数组+链表+红黑树（有一个固定长的数组，数组中的每一个位置都存放条链表(由结点组成)，当链表和数组到达一定值时，将链表存为数的形状）

这样处理数据的原因是，该结构的存储效率高。



元素添加规则如下：

1、在添加元素时，会先通过内部算法得到一个hash值，再将这个hash值转换为一个索引值；

2、找到数组表的索引位置，看该位置是否有其他元素，若没有则直接放入；

3、若有元素，则调用equals方法（可以重写）进行比较，若元素相同，则放弃添加（决定了HashSet接口无法添加相同的元素）；若不相同，则对该链表之后的全部节点进行比较，若有相同元素，则放弃添加，若无相同元素，则添加到链表结尾。



在java8中，若链表长度=8，并且数组长度>=64，则将链表转化为红黑树。每次链表到8时都会判断数组长度到没到64，若没到则会将数组进行2倍扩容。





> 源码分析

1、构造器调用

```java
HashSet set = new HashSer();//创建对象，调用构造器
```

```java
public HashSet(){
  map = new HashMap<>();//构造器内部实际上是一个HashMap对象
}
```



2、添加元素

```java
set.add("tom");//调用add方法
```

```java
public boolean add(E e) {//传入一个元素
        return map.put(e, PRESENT)==null;//使用map.put方法，跳入。还有一个PRESENT属性，其实际上是HashSet类内的一个静态Object对象，无实际意义，就是个占位作用，表示这得输入一个东西。最终返回的是哈希值是否==null，若不等，则代表添加新元素了，返回true
    }
```

​		PRESENT部分

```java
private static final Object PRESENT = new Object();
```





```java
public V put(K key, V value) {//输入key、value，返回value。此处key是add的输入元素，为“tom”，value是PRESENT。
    return putVal(hash(key), key, value, false, true);//此处有个方法的嵌套，putVal()方法和hash()方法，先看hash()方法
}
```

​			hash()

```java
static final int hash(Object key) {//返回一个int类型，返回的是一个hashcode，即哈希值。且返回的是key的hash值，此处为"tom"的hash值
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);//可以发现这里并不纯粹是哈希值，而是通过了点计算
    }
```

​			putVal()

```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        
  Node<K,V>[] tab; Node<K,V> p; int n, i;//定义一些辅助变量
  
  			
  //此if用来判断数组长度是否为0，若为0则进行第一次扩容至16   
  if ((tab = table) == null || (n = tab.length) == 0)//此处table就是hashMap内部定义的存放链表头节点的数组（上面讲的数组），若此时数组为空（刚定义数组，还没放数），则执行下条语句
            n = (tab = resize()).length;//此处使用resize（）方法，调整数组容量。resize（）方法看下面单独讲解。resize返回一个newtab，其长度为16.故此时n=16

  
  //此if用来判断传入的实参是否与该表内的其他数据相同，若不相同，则将传入的数据加入数组     
  					if ((p = tab[i = (n - 1) & hash]) == null)//此时tab是resize后的tab，容量为16.根据key得到的hash值去计算key应该存放的table的哪个索引位置，并把该key的节点同时赋值给p。若p为空，则表示该索引处还没放节点，则执行下语句
            tab[i] = newNode(hash, key, value, null);//创建一个新node，将其放入tab指定索引处。该节点保存hash值、数据本体、value、和下一个节点（null）。
        
  //若新传入实参的hash值对应索引位置有人了，则进行下面的else判断
  					else {
            Node<K,V> e; K k;//定义一个临时节点变量、一个临时元素变量
    
    				//该if判断：若索引处节点的hash与准备加入节点的hash相同，且两者节点内容也相同，则不进行添加
            if (p.hash == hash &&//此时p是数组中与该新实参哈希值一致的索引位置的节点。
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
    
    			//该if判断p是不是一个红黑树，若是红黑树，则直接往树里添加，不展开讲了
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
    
    				//若上俩个条件都不满足，则进行该else。即当准备加入的节点与头节点hash值不同，但是通过tab[i = (n - 1) & hash]计算后发现还是要添加进该节点所在链表处，则对该链表的全部值进行一遍循环，判断准备加入的节点数据是否与链表内数据有重复，若都无重复才加入，否则不加入。
            else {
              //进行一次无限循环，退出该循环有两种方式：1、新加入的节点与之前全部节点的元素都不相同，则添加该节点到链表结尾，break；2、如果中间有一个节点与该节点一致，则不进行添加，break；
                for (int binCount = 0; ; ++binCount) {
                  //情况1
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                      	//若添加元素够该链表长度为8，则对当前链表进行红黑树化判断（链表长度等于8；数组长度大于64）
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                  //情况2
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { //此处决定替换，存在value时才用（比如之后要讲的Map部分）
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)//若当前size已经大于临界值了
            resize();//进行reshize扩容
        afterNodeInsertion(evict);//此方法在HashMap定义的空方法，用于让HashMap的子类来重写该方法
        return null;//返回空，代表添加成功。（因为最开始的比较为map.put(e, PRESENT)==null），只有返回的是null才为true
    }
```

​			

​						resize（）

```java
final Node<K,V>[] resize() {//返回一个节点型的数组
        Node<K,V>[] oldTab = table;//先将hashmap底层定义的table赋值给老数组
        int oldCap = (oldTab == null) ? 0 : oldTab.length;//记录老数组的容量
        int oldThr = threshold;//定义一个容量临界值，若此时数组长度已经到临界值位置，则进行扩容，而不是等到数组长度慢了再扩
        int newCap, newThr = 0;//定义新数组的容量和临界值
        if (oldCap > 0) {//若老数组长度>0
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {//若老数组长度等于零
            newCap = DEFAULT_INITIAL_CAPACITY;//将新数组长度定义为16（该常量大小为16）
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);//将临界值大小定义为0.75*16
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;//记录一下临界值12
        @SuppressWarnings({"rawtypes","unchecked"})
            Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];//新建一个Node型的数组，将其长度定义为newCap即16
        table = newTab;//将新数组赋值给底层真正使用的数组。此时table是长度为16，内容为null的数组
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
//要注意，resize方法扩容数组是通过临界点来判断的，临界点是数组长度的0.75倍。但是并不是说数组的16个索引中放入了12个值才扩容，而是说只要数组加入了数据就算size++，哪怕只占用了一个索引，但是索引后的链表加了16个数也进行数组扩容。
```





##### 12.4.3 LinkedHashSet

linkedHashSet其他与HashSet都差不多，就是其内部是一个双向链表来维护的。就是除了数组内部维护的单链表外，各个元素之间还用双链表维护。



打个比方：A添加进[0]，B添加进[1]。A除了包含next节点用来指向[0]的后续节点外，还有after和before节点，这两个节点独立于next节点，用来指向A之后添加的节点，无论该节点是否加入[0]的位置。故此时A.next = null（因为[0]后没加节点）；A.after = B，因为B在A之后添加，同时B.before = A。之后若添加C进[0]，则此时ABC的关系为：A.next = C、A.after = B、A.before = null；B.next = null、B.after = C、B.before = A；C.next = null、C.after = null；C.before = B 。



LinkedHashSet差不多就这个意思，就不再展开讲了。



##### 12.4.4 TreeSet

TreeSet与HashSet的最大区别就是，TreeSet是可排序的，而hashSet是无序的。

> 源码分析

1、TreeSet底层是TreeMap

2、TreeMap类在构建时，有一个compatator属性，即

```java
private final Comparator<? super K> comparator
```

该属性是用于比较排序的（往后看就懂了）

3、TreeSet常用两个构造器，第一个是无参构造器，另一个是接收实现了Comparator接口的对象的构造器

```java
public TreeSet() {//无参构造器
    this(new TreeMap<E,Object>());//底层实际上是构造了一个Treemap
}

public TreeSet(Comparator<? super E> comparator) {//有参构造器，接收一个实现了Comaprator接口的对象
    this(new TreeMap<>(comparator));//构造一个TreeMap，将comaprator对象传入
}
```

此处主要讲有参构造器部分，再将comparator传入TreeMap时，TreeMap实现了下一步

```java
public TreeMap(Comparator<? super K> comparator) {
    this.comparator = comparator;//将第二条中TreeMap定义的属性设为comparator对象
}
```

也就是说，若调用TreeSet的无参构造器，则TreeMap的comaprator属性是null；若调用的是有参构造器，则该属性就是有参构造器接收的comparator。而之所以调用实现了comparator接口的有参构造器，是为了重写Comparator中的compare方法，进行TreeSet有序化

下面举个实例

```java
TreeSet treeset = new TreeSet(new Comparator(){//调用有参构造器，使用匿名内部类实现Comparator接口
  public int compare(Object o1 ,Object o2){//重写Compatator接口的compare方法
    return null;
  }
} );
```

对treeset进行添加

```java
treeset.add("jack");//调用add方法，跳入
```

```java
public boolean add(E e) {
    return m.put(e, PRESENT)==null;
}//发现TreeSet类内定义的add方法，接收一个元素e，内部使用的是put方法，将e当作key传入put方法中。跳入put方法
```

```java
public V put(K key, V value) {
        Entry<K,V> t = root;
        if (t == null) {
            compare(key, key); 

            root = new Entry<>(key, value, null);
            size = 1;
            modCount++;
            return null;
        }
        int cmp;
        Entry<K,V> parent;
        
        Comparator<? super K> cpr = comparator;//主要是这里，将Comparator类型的cpr=构造器定义的comparator
        if (cpr != null) {//此时cpr必然不为0
            do {
                parent = t;//将添加数据的前一个数据设为parent
                cmp = cpr.compare(key, t.key);//通过重写的方法比较当前数据与当前欲插入的数据，返回int型
                if (cmp < 0)//若返回值小于零
                    t = t.left;//则将t移动一位以便继续比较
                else if (cmp > 0)//同理
                    t = t.right;
                else//如果前后俩个值判定后返回0（某方面想等的情况下），则不进行添加
                    return t.setValue(value);
            } while (t != null);//直到t移出整个set，否则循环进行比较
        }
        else {
            if (key == null)
                throw new NullPointerException();
            @SuppressWarnings("unchecked")
                Comparable<? super K> k = (Comparable<? super K>) key;
            do {
                parent = t;
                cmp = k.compareTo(t.key);
                if (cmp < 0)
                    t = t.left;
                else if (cmp > 0)
                    t = t.right;
                else
                    return t.setValue(value);
            } while (t != null);
        }
        Entry<K,V> e = new Entry<>(key, value, parent);
        if (cmp < 0)
            parent.left = e;
        else
            parent.right = e;
        fixAfterInsertion(e);
        size++;
        modCount++;
        return null;
    }
```















































#### 12.5 Map

之前讲过，Collection（Set和List接口）是单列接口，而Map是双列接口，且Map传入的参数是key和value。实际上真要说的话，Set和List也都是双列接口，它们接收的key就是元素本体，而接受的value则是一个常量的Object对象--PRESENT（在追HastSet的源码时遇到过），其没具体意义，只是用来占位而已。但是Map则将vlaue的值变得有意义了。

map传入的是（key，value），而Collection传入的是（key）



（个人感觉，Map可以理解为python中的字典，[key,value]）



##### 12.5.1 Map接口的特点

1、Map接口与Collection接口是同级别的，两者并无相互指向的联系。

2、Map接口用于保存具有映射关系的数据：key-value。

3、Map中的key和Value可以是任何类型的数据，因为接收形参是Objcet类的。并且key和value会封装到HashMap$Node（HashMap的内部类）对象中。（之前跑HashSet源码也见过： tab[i] = newNode(hash, key, value, null)，此处newNode就是HashMap&Node）

4、Map中的key不允许重复，原因与HashSet的元素不允许重复类似。但是HashSet中元素重复则后放的元素放不进去，而Map中则是后放的元素替换掉之前的元素

5、Map中的value可以重复。

6、Map中的value和key都可以为空，但是key只能存在一个空，而value则不限

7、Map中的key通常用String来形容。如map.put("第一个人的年龄",18)；map.put("第二个人的年龄",20)。但是不代表所有的key都得用string表示。

8、key和value的关系是一对一的，不会存在一对多的情况。因为在Map中的各个key都是唯一且不同的，故每个key都对应一个其所属的value。用get（key）来取出value的情况。



> 底层分析



![12761C9FB216AECCA6562EC4836922E9](/Users/changhe/Library/Containers/com.tencent.qq/Data/Library/Caches/Images/12761C9FB216AECCA6562EC4836922E9.jpg)

（EntrySet结构如上图右边，key放入的是个set集合、values放入的是collection集合，两者又一起组成了一个entry放入entryset中，entryset也是个set类型的集合。

）

Map存放的数据[key,value]是存放在HashMap类的内部类---HashMap$Node中的，该内部类定义了一个链表节点该有的各种属性。而且HashMap$Node也实现了一个Entry接口。会形成一个EntrySet集合，该集合是Entry数据类型的，用来存放HashMap$Node中key和value的索引，key和value的具体内容还是在HashMap$Node中。



有关entrySet这里说明一下，entrySet本是Map接口中提供的方法：Set<Map.Entry<K, V>> entrySet()，后来被HashMap重写了：public Set<Map.Entry<K,V>> entrySet() ，但是无论如何重写，该方法返回的类型依旧是Set<Map.Entry<K, V>>（<>内的先不管，总之是一个Set型，即集合）。而在HashMap中又定义了一个HashMap$EntrySet内部类，entrySet集合的运行类型就是HashMap$EntrySet。

再看Set<Map.Entry<K, V>> entrySet()这部分，可知Entry是一个只接收key和value的接口，故而entrySet集合装的是Entry对象，所以entrySet也是只接收key和value。



刚刚提到entrySet的运行类型为HashMap$EntrySet，那entrySet内部存放的数据的运行类型是什么呢？是HashMap$Node，因为在HashMap类的内部类HashMap$Node的定义时，该Node就实现了Entry：static class Node<K,V> implements Map.Entry<K,V> 。



entrySet集合主要是方便Map的遍历，因为Map.Entry接口提供了两个重要的方法--getKey和getValue



总结一下：1、Map接口定义了一个Entry接口，该接口存放key和value以及各种关于这两个属性的方法；2、Map接口中定义了一个entrySet方法，该方法返回一个Set集合，该集合是Entry接口型的；3、HashMap类重写了entrySet方法，内容先不论，返回的还是一个Entry型的集合；4、HashMap类中定义的内部类Node类，也实现了Entry接口。5、HashMap类还定义了一个EntrySet内部类。

整个过程就是，将HashMap$Node中的Node对象向上转型成Entry对象，再将Entry对象存放在EntrySet集合中。



知道以上内容后，看以下代码就简单了

```java
Map map = new HashMap();//用HashMap类来实例化Map接口（因为接口不能直接实例化，故得找一个实现了该接口的类来变相实例化接口）
map.put("no.1","a");//在HashMap中加入数据，具体数据是一个Node型的

Set set = map.entrySet();//调用entrySet方法来构造一个Set集合。将map中存放数据的key和value的索引放入set中

set.getClass();//set集合的运行类型是HashMap$EntrySet。原因是多态，变量map的编译类型是Map，但是其运行类型是HashMap，故调用map.entrySet方法时，用的是HashMap类中的方法，而HashMap中的entrySet方法构造的是HashMap定义的EntrySet内部类，故set的编译类型是Set，运行类型是hashMap$EntrySet
for(Object o : set){
  o.getClass();//set集合中的数据的运行类型是HashMap$Node型的。道理也是多态。我们知道，在定义entrySet的返回类型时，要求的set是set<Entry<k,v>>，即返回的是一个Entry的接口，所以理应set内的元素是Entry型的，但是由于HashMap内的内部类Node也实现了Entry接口，故由多态可知，Node实例化的对象也是可以放进set集合中的，而此处Node就是("no.1","a")，将它放入了set中，故set内部元素实际上是一个HashMap$Node型，所以其运行类型是HashMap$Node
}
//整个过程可以成是：HashMap$EntrySet装着HashMap$Node
```



##### 12.5.2 Map接口常用方法 

> 常见方法

```java
package _05_Map;

import java.util.HashMap;
import java.util.Map;

public class _03_MapMethod {
    public static void main(String[] args) {
        Map map = new HashMap();//HashMap来实现Map接口

        //1、添加，put
        map.put("no.1",100);
        map.put("no.2",true);
        map.put("no.3",10.3);
        map.put("no.4","jack");
        map.put("no.5",new Book("a",100));//以上五个成功添加
        map.put("no.1",200);//替换no.1
        map.put("no.6",10.3);//value重复无影响
        System.out.println(map);

        //2、删除 remove，一般用根据key删除
        map.remove("no.2");
        System.out.println(map);
        
        //3、取值，get，根据key进行索引
        System.out.println(map.get("no.5"));


        //5、长度，size
        System.out.println(map.size());

        //6、判空，isEmpty
        System.out.println(map.isEmpty());

        //7、查找某key是否存在，containKey。若用get来找一个空key会返回null，而map中是可以将value设成null的，会引起歧义。
        System.out.println(map.containsKey("ad"));

    }
}

class Book{
    String name;
    int age;

    public Book(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

```



> 遍历方法
>

在介绍Map底层时说过，其细数的话有三个集合---存放key的keyset、存放value的collection、将key和value视为整体作为entry对象存放的entryset。这三个集合都是可以遍历的。

```java
package _05_Map;

import java.util.*;

public class _04_MapFor {
    //遍历Map的方法
    public static void main(String[] args) {
        Map map = new HashMap();


        map.put("no.1","jack");
        map.put("no.2","tom");
        map.put("no.3","john");
        map.put("no.4","lucy");
        map.put("no.5",100);

        //遍历一：先取出所有的key，然后通过key取出对应的value。用keySet
        Set keyset = map.keySet();//keySet取出的是key，而key是装在Set中的，故可用Set类接收

            //有了key后就可以用迭代器或者增强for来循环Map了
        for(Object o : keyset){
            System.out.println(o + "_" + map.get(o));//用get方法来取出map特定key对应的value
        }

        Iterator iterator = keyset.iterator();//要注意是keyset的迭代器，一来是map接口没有迭代器，二来是要通过迭代key来取value的值
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println(next + "_" + map.get(next));

        }


        //遍历二，先取出所有的value，然后遍历value及其对应的key
        Collection values = map.values(); //同样，map的value是存放在collection中的，要用Collection接收

            //有了collection集合后就可以用collection的遍历方式开始遍历
        for(Object o : values){
            System.out.println(o);//由于map没提供根据value找key的方法，故只能单输出value了
        }

        Iterator iterator1 = values.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println(next);
        }


        //遍历三，取出entryset集合，然后遍历
        Set entrySet = map.entrySet();

        for(Object o : entrySet){
            Map.Entry m = (Map.Entry) o; //由于调用map的运行类型是HashMap，故调用entrySet时用的是HashMap中的该方法
                                        //而该方法得到的是Entry的是HashMap中的entry，无法用Map中的遍历方法，故要转型成Map的Entry。
            System.out.println(m.getKey() + "_" + m.getValue());
        }

        Iterator iterator2 = entrySet.iterator();
        while (iterator2.hasNext()){
            Object o = iterator2.next();
            System.out.println(o.getClass());
            Map.Entry m = (Map.Entry) o;
            System.out.println(m.getKey() + "_" + m.getValue());

        }


    }


}

```





#### 12.6 HashMap

讲Map时就是用HashMap实现的，此处讲点其他细节

##### 12.6.1 底层剖析

> 扩容机制

扩容机制与HashSet完全相同

1、HashMap底层维护了一个table数组，该数组存放的数据类型是Node型，默认为null；

2、创建对象时，将加载因子(loadfactor)初始化为0.75；

3、添加k-v时，通过key的哈希值得到该k-v在table中的索引。然后判断该索引处是否有元素，若无元素，则直接添加进table的该索引处，若有元素，则继续判断该元素的key是否和本地元素的key相同。若相同，则替换v；若不同，则判断该头节点所处位置是链表还是树，作出相应的处理。若发现添加时容量不够，则进行扩容

4、第一次添加，将table扩容至16，临界值(threshold)为12

5、以后再扩容，则将table容量扩为两倍，临界值也为原来的2倍。

6、若链表的元素个数超过8，且同时table大小大于等于64，则对链表进行树化。



流程如下

1、创建HashMap对象

```java
HashMap map = new HashMap();//创建一个HashMap对象，跳入进构造器
```

```java
public HashMap() {
    this.loadFactor = DEFAULT_LOAD_FACTOR; //无参构造器默认会讲加载因子设成0.75（DEFAULT_LOAD_FACTOR该常量为0.75）
}//此时HashMap维护的table为空：HashMap$Node[] table = null;
```



2、添加

```java
map.put("no.1",10);//添加k="no.1"，v=10的Node。跳入put方法
```

```java
public V put(K key, V value) {//key="no.1",value = 10
    return putVal(hash(key), key, value, false, true);//调用hash方法计算key的哈希值，传入其他实参进入putVal方法
}
```

```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;//定义一个Node型的tab，一个Node型的p，两个int遍历
  
    if ((tab = table) == null || (n = tab.length) == 0)//令tab=table（构造时说过，table此时等于null），判断tab是否为空或者令n为tab的长度，看长度是否为0.
        n = (tab = resize()).length;//若if成立，则tab进行resize（即扩容），n等于扩容后的长度
  
    if ((p = tab[i = (n - 1) & hash]) == null)//判断完是否需要扩容后就开始判断是否添加数据了。令p为tab数组中对应哈希值索引上的结点，判断p是否为空。
        tab[i] = newNode(hash, key, value, null);//若该结点为空，则将该节点放入要添加的结点。将欲添加节点的信息通过newNode方法构造一个新结点放入tab中
  
    else {//若p所代表的结点不为null
        Node<K,V> e; K k;//构造临时变量：Node型的e，key型的k
      
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))//如果p的哈希值与欲添加节点的哈希值一样，并且两者的key的内容也一样。
            e = p;//则将临时变量e等于tab中的结点p。
      
        else if (p instanceof TreeNode)//若p所带领的一众结点不是链表而是树
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);//则进行某些操作，不用管
      
        else {//若欲添加节点既和p不一样，p所处位置也不是树而是链表，则将欲添加节点与链表之后的所有节点进行比较
            for (int binCount = 0; ; ++binCount) {//进行一次无限循环
              
                if ((e = p.next) == null) {//将p的下一节点赋值给e，若e为空
                    p.next = newNode(hash, key, value, null);//则代表链表遍历结束，将p的下一个节点，即尾节点设为欲添加节点（此时先别急为啥p明明是链表头节点，但是p的下一个节点就是尾节点了，这个后几行代码会解释）
                  
                    if (binCount >= TREEIFY_THRESHOLD - 1) //树化操作，不管
                        treeifyBin(tab, hash);
                    break;//若成功将尾节点构造成欲添加的节点，则推出无限循环
                }
              
                if (e.hash == hash &&//若刚刚的p的下一个节点e不是等于null
                    ((k = e.key) == key || (key != null && key.equals(k))))//则将欲添加节点和e进行key的各个比对（和比对p时一样）。
                    break;//若各个条件一致，则直接退出循环，不进行添加。（此时代表，欲添加节点和链表中的某个节点的key一样了）
              
                p = e;//若前两个操作都没有退出循环，即p的下一个节点不是尾节点，且欲添加节点与p的下一个节点key也不同。则将p=p.next，将链表往后遍历一步，再进行新一轮判断。即最后要么某时候欲添加节点与链表中节点撞衫了，要么就是p指向尾节点了。而e要么是null，要么是一个与欲添加节点撞衫的节点。
            }
        }
      
        if (e != null) { //经过了刚刚的遍历，若e不是空，则代表e不是链表尾的后一位置，而是一个正好与欲添加节点的key一致的一个节点，要开始进行value的替换了
            V oldValue = e.value;//将e的value赋给临时遍历OldValue
            if (!onlyIfAbsent || oldValue == null)//onlyIfAbsent是传入的实参，设置的是false，故!onlyIfAbsent永远是true，则只判断oldvalue是否为null即可。但是由于是｜｜，故无论oldvalue是否为空，都进行value替换。也就是说，只要欲添加结点的key和e一致了，那就必然将e的value置为新value。
                e.value = value;//将e的value等于欲添加节点的value
                afterNodeAccess(e);//一个空方法，具体怎么用看程序员怎么重写了，此处暂无意义
                return oldValue;//将整个putVal方法返回，返回链表中原value值
            }
        }
  
  //若刚刚的if无返回，代表欲添加节点与链表中所有节点都不一致，此时e=null，也成功将欲添加节点加入了链表尾部
    ++modCount;//计数加1，没啥意义
    if (++size > threshold)//判断是否需要扩容
        resize();
    afterNodeInsertion(evict);//待重写的方法，无意义
    return null;//进行些操作后返回putVal方法，返回值为null
}
```





#### 12.7 Hashtable

##### 12.7.1 基本介绍

1、Hashtable是Map接口下的一个实现类，和HashMap是同级别的类。

2、Hashtable存放的也是一对值：key-value

3、Hashtable的键与值都不能是null，否则会抛出异常NullPointerException;

4、hashtable的方法和HashMap大差不差

5、Hashtable是线程安全的（有synchronized修饰），但是HashMap是线程不安全的



##### 12.7.2 底层机制

1、Hashtable底层维护的也是一个table数组，该数组是Hashtable$Entry型的，即Hashtable$Entry[] table;，该数组初始化大小是11

2、table数组也有一个临界值与加载因子，加载因子还是0.75，则临界值=11*0.75 = 8；

3、扩容时，将老容量*2之后再+1。



##### 12.7.3 HashMap与hashtable对比

|           | 版本 | 线程安全 | 效率 | null   |
| --------- | ---- | -------- | ---- | ------ |
| HashMap   | 1.2  | 不安全   | 高   | 可以   |
| Hashtable | 1.0  | 安全     | 较低 | 不可以 |



要注意Hashtable底层不再有Node节点了，它是将key-value直接存放到Entry接口中的，然后将Entry直接存放在Hashtable表中。而HashMap是将Key-value存放到Node对象中，再将Node对象向上转型成Entry接口中，存放进EntrySet表内。





#### 12.8 集合选型

在实际开发中，选择什么集合实现类，主要取决于业务操作特点，然后根据集合实现类特性进行选择。



先判断存储的类型（单列（一组对象）还是双列（一组键值对））

若是单列，则选择Collection接口的子类，即LInkedLiset、ArrayList、HashSet、TreeSet中选一个。若数据允许重复，则选择List接口中的实现类、若不允许重复，则选择Set接口的实现类。

若是双列，则选择Map接口的子类等等。具体看下图![FC36BBC3AAC1C6FF8AAEE6829BC14930](/Users/changhe/Library/Containers/com.tencent.qq/Data/Library/Caches/Images/FC36BBC3AAC1C6FF8AAEE6829BC14930.jpg)

​	

#### 12.9 Collections工具类

该类中定义了好多好用的用于集合的方法。







### 13 泛型

泛型是指"<>"部分。

泛型可以理解为类的形参列表，决定这个类是什么数据类型的。即可以视泛型为一个赖子，可以是任何类型，这些类型在对象创建时指定一下就行。

总的来说，泛型是一个可以接收数据类型的数据类型。

简单举个例

```java
class dog{
  String s;//通常在dog类中定义属性时就这样定义，但是如果s不想当String类型了，而想当Int型怎么办呢？此时只能再建一个参数
  int i;//独立建一个int型的参数
}

class dog<E>{//<E>就可看成是类的形参列表，决定这个类中某个属性的数据类型
  E s;//在创建dog类对象时，指定一个类型，则s就是该类型的数据。该E可以是任何类型，在定义对象时指定。
}
```





总的来说，泛型可以在类声明时通过一个标示，来表示类中某个属性的类型、某个方法的返回类型或参数类型

```java
class dog<E>{
  E e;
  
  public E mathon(){
    return e;
  }
  
  public dog(E e){
    this.e = e;
  }
}

class run{
  public static void main(Stirng[] args){
    dog<String> d = new dog<String>("h");
    //此时相当于
    //class dog{
    	//String e;
    
    	//public String mathon(){
    		//return e;
  		//}
    	//public dog(String e){
    		//this.e = e;
  		//}
  	//}
    
    dog<Integer> d1 = new dog(Integer)(1);
    //同上理
  }
}
```

也就是说，该dog类的每个对象，都可以有其各自的类型。泛型是在编译时就确定类型了的。



#### 13.1 泛型类

接口和类都可以有泛型

> 语法

```java
class 类名<E>{}//此处E可以是任何字母，知道是泛型就行
```



> 细节

普通成员可以使用泛型（属性、方法）；

使用泛型的数组，不能初始化

静态方法不能使用泛型

泛型类的类型是在创建对象的时候确定的

若在创建对象时没有指定泛型，那么泛型默认是Object



普通类内也可有泛型方法



> 展示

举例说明一下

```java
class Tiger<T,R,M>{//由于Tiger类后有<>，故Tiger是有泛型的，该泛型有三个指标：T，R，M
  String name;//正常属性
  T t;
  M m;//使用泛型的属性
  
  R[] r;//使用泛型的数组不能初始化，因为还不知道这个数组是什么类型的数组，故无法在内存中开辟空间，只能先定义了，等确定了类型才开辟空间
  
  public Tiger(String name,T t,R r,M m){//使用了泛型的构造器
    this.name = name;
    this.t = t;
    this.m = m;
    this.r = r;
  }
  
  public T getT(){//使用泛型的方法。返回类型可以是泛型
    return t;
  }
  
  public void m1(M m){//泛型使用方法
    
  }
  
  public static void m2(M m){//报错，静态方法无法使用泛型，因为静态方法是加载类时就加载了，而泛型要等到对象创建时才能确定。
    
  }
}

```





#### 13.2 泛型接口

> 语法

```java
interface 接口名<E>{
  
}
```



> 细节

接口中，静态成员也不能使用泛型（道理和泛型类一样）。而接口中的属性默认都是静态的，故接口中一般不会出现泛型属性。

泛型接口的类型，在继承接口或实现接口时确定

没有指定泛型接口的类型时，默认为Object





> 展示

```java
Interface IUsb<U,R>{
  int i;//可以，普通属性
  U u;//不可以，接口属性是静态的，无法成为泛型。
  
  U get(U u);//返回泛型的使用了泛型的方法
  
  void hi(R r);//无返回值的泛型方法
  
  void run(R r1,R r2,U u1,U u2);//无返回值的泛型方法
  
  
}

class A implements IUsb<String,Double>{}//实现接口时可以直接指定接口的泛型
Interface B extends IUsb<Integer,String>{}//继承接口时直接指定接口的泛型
```





#### 13.3 范型方法

> 语法

```java
修饰符<E,,,> 返回类型 方法名（形参）{}
```



> 细节

1、泛型方法可以定义在普通类中，也可定义在泛型类中

2、当泛型方法被调用时，泛型的类型会确定下来

3、若修饰符后无泛型，而只要形参列表里有泛型，则该方法不是泛型方法，只是使用了泛型的方法（前面有些说成泛型方法说错了）





#### 13.4 泛型通配符

1、范型不具备继承性：

```java
List<Object> list = new ArrayList<String>();//虽然String是Object的子类，但是不能这么写，后面只能是Object
```



2、<?>表示支持任意泛型类型；<? extends A>表示支持A类与A的子类；<? super A>表示支持A类与A的父类





### 14 线程

#### 14.1 相关概念

> 程序

程序是完成特定任务、用某种语言编写的一组指令集合，简单说就是IDEA中写的代码



> 进程

进程是指运行中的程序，比如使用typora写笔记的时候，typora就是一个进程。系统会为进程分配内存空间。

进程是程序的一次执行过程，是动态的过程。进程有自己的产生、存在和消亡过程。



> 线程

线程由进程创建，是进程的一个任务。如启动下载软件是启动了一个进程，在下载软件中下载一个任务，则启动了一个线程，若同时下载另一个任务，则就又启动了一个线程。



#### 14.2 线程相关概念

##### 14.2.2 线程

线程可以分为单线程和多线程

> 单线程

在同一时刻只允许执行一个线程



> 多线程

在同一时刻可以执行多个线程，如qq进程可以同时与多个人聊天等



##### 14.2.2 并发并行

> 并发

并发是指同一时刻，多个任务快速交替执行，造成一种“貌似”同时多错觉，简单来说，单核cpu实现的多任务就是并发。

如单核cpu开启了两个任务：qq和微信，则虽然看似同时执行了qq和微信，但是这只是cpu的执行切换速度很快，其实同一时刻只有其中一个被执行了。



> 并行

并行指同一时刻有多个任务同时执行，多核cpu可以实现并行。



并发和并行是可以共存的。比如4核cpu执行五个任务，则每个任务先分配一个不同的cpu，然后多余的那个任务找一个cpu去并发。



#### 14.3 线程使用

java中的线程使用有两种方法：继承Thread类并重写其中的run方法；实现Runnable接口并重写run方法。

Thread类也实现了Runnable接口，说到底，实现线程还是用的Runnable接口中的run方法。

当一个类继承或实现上两种方法后，该类就变成了一个线程类，可以重写run方法来确定该线程要执行什么操作。

```java
public void run() {
        if (target != null) {
            target.run();
        }
    }//此为Thread重写的Runnable的run方法
```



而上述run方法只是表面线程中要执行什么操作，真正启动线程是start方法

```java
public synchronized void start() {
        /**
         * This method is not invoked for the main method thread or "system"
         * group threads created/set up by the VM. Any new functionality added
         * to this method in the future may have to also be added to the VM.
         *
         * A zero status value corresponds to state "NEW".
         */
        if (threadStatus != 0)
            throw new IllegalThreadStateException();

        /* Notify the group that this thread is about to be started
         * so that it can be added to the group's list of threads
         * and the group's unstarted count can be decremented. */
        group.add(this);

        boolean started = false;
        try {
            start0();
            started = true;
        } finally {
            try {
                if (!started) {
                    group.threadStartFailed(this);
                }
            } catch (Throwable ignore) {
                /* do nothing. If start0 threw a Throwable then
                  it will be passed up the call stack */
            }
        }
    }
```

start方法中核心是调用start0方法

```java
private native void start0();//该方法是本地方法（native方法），由JVM机调用（底层由c++实现）
```

run方法是由start0来调用，而具体什么时候实现run方法要看系统分配。

具体流程如下：主线程中调用start方法--->start方法开启start0方法---->start0方法被JVM机调用并重写的run方法，实现多线程。





当我们在IDEA中run程序时，相当于开启了一个进程。开启程序的进程后，会先找到主方法，开启第一个线程--主线程。之前学的时候主线程里没有其他线程了，就单线程就结束了，但是如果主线程里有新（线程.start），则又开启了一个新线程，就变成多线程的进程了。

要注意，当主线程执行到开启新线程的语句后，主线程并不会阻塞，会继续往后执行。而且主线程结束也不代表子线程就不执行了，这两个线程的运行是独立的。而只要有线程在进行，进程就不会结束。



#### 14.4 线程的7大状态

![96a498f26bae50647762ab2d0ef6f67c](/Users/changhe/Library/Containers/com.tencent.qq/Data/Library/Application Support/QQ/nt_qq_20a8d2bc7cad483944f4c07642609169/nt_data/Pic/2023-05/Ori/96a498f26bae50647762ab2d0ef6f67c.png)

![image-20230730223253985](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230730223253985.png)

1、NEW，尚未启动的进程，但是已经建好了
2、Runnable，在java虚拟机中的线程。即start后的线程。该状态又可分两种细状态：ready状态和running状态，ready是在虚拟机中不运行的状态，run是开始运行的状态
3、Blocked，被阻塞等待监视器锁定的线程
4、Watting，等待另一个线程执行完毕后再执行该状态，即被join插队后的线程处于watting
5、Timed_Watting，等待一个指定时间后再开始运行的线程，即sleep后的线程处于该状态
6、terminated，已经退出的线程处于该状态





#### 14.4 线程同步

在一些程序中，有些数据因为安全需要不应该允许被多个线程访问，此时就要使用同步访问的技术，保证数据在任何时刻，最多只有一个线程访问，以保证数据的完整性。

线程同步可以理解为：当有一个线程在对内存进行操作时，其他线程都不可对该内存地址进行操作直到该线程完成操作。该线程完成操作后，其他线程才可对该地址进行操作



#### 14.5 互斥锁

在java语言中，引入了对象互斥锁的概念，来保证共享数据的完整性

每个对象都对应于一个可称为“互斥锁”的标记，这个标记用来保证在任一时刻，只能有一个线程访问该对象。

关键字synchronize来与对象的互斥锁联系，当某个对象用synchronize修饰时，表明该对象在任一时刻只能由一个线程访问，从而实现同步。



同步的局限性：导致程序的执行效率低



锁是通过同步方法来实现的，同步方法分静态的非静态的。静态的同步方法代表整个类都是同步的（带锁的），非静态同步方法代表某个对象是同步的（带锁的）

其具体的加锁位置如下（在以下位置都可以加上static表示静态）

```java
synchronized(this){
  
}//代码块上加锁

public synchronized void main(){}//方法上加锁
```



有几点需要注意，当使用代码块加锁时，不同线程调用该代码块的this对象必须是同一个this（this可以不是当前类实例的对象，可以是其他对象，但是要保证不同线程访问该锁时必须是同一个对象）。目前可以简单的理解为，必须得是一个线程类实例化出一个对象，再放入若干个thread类中开启若干个线程

这个机制就注定了，若想新建一个可以实现了锁的线程类，则该类必须得是通过Thread方法来实现start方法，而不能通过该类的实例化对象实现start方法

```java
class A implements Runnable{
  synchronized(this){}
}

class main{
  public static void main(String[] args){
    A a = new A();
    Thread t1 = new Thread(a);
    Thread t2 = new Thread(a);  //此时t1和t2两个线程内部都是a对象，可以放心的调用a内的锁
  }
}
```



如果是静态方法在调用synchronized代码块时，则后面的this要变成.class，因为静态方法不能包含对象，其是类的方法

```java
class A extends Thread{
  synchronized (A.class){}
}

```



### 15 IO流



#### 15.1 IO原理与分类

##### 15.1.1 文件

> 基本概念

1、文件：文件是用来存放数据的

2、流：数据在数据源（文件）与程序（内存）之间经历的路径

3、输入流：文件--->内存

4、输出流：内存--->文件

5、在java中，目录会被视为一种特殊的文件，如“/Volumes/common/Code/JavaCode/chapter15”，这个路径虽然是个目录，但是其在java中也被当为文件对待



> 相关操作

1、创建文件

创建文件有三种方式：

```java
File file = new File(String pathname)//根据欲创建文件的绝对路径创建一个File类的对象
File file = new File(File parent,String child)//根据父目录文件对象+欲创建的文件名称构建File类对象
File file = new File(String parent,String child)//根据父目录路径+欲创建的文件名称构建File类对象

file.creatNewFile();//这一步是真正把File对象创建成了一个可以看见的文件
```



2、获取文件信息

获取文件信息常用方法有以下几种：

```java
System.out.println(file.getName());//获取文件名称
System.out.println(file.getAbsolutePath());//获取绝对路径
System.out.println(file.getParent());//获取文件所处目录
System.out.println(file.length());//获取文件大小（字节为单位）
System.out.println(file.exists());//文件是否存在
System.out.println(file.isFile());//该路径是否为文件
System.out.println(file.isDirectory());//该文件是否为目录
```



##### 15.1.2 io的基本概念

1、i/o时input/output的缩写，用于数据传输、读写文件、网络通讯等

2、java中，对于数据的输入输出操作往往以”流（Stream）“的形式进行。可以把流理解为运输信息的工具，如果将信息理解为外卖，则流就可以理解为外卖员来专门进行运输外卖。每个流对象会绑定一个信息来专门运输这个信息。

3、java.io包下提供了各种”流“类和接口，用以获取不同种类的数据，并通过方法输入或输出数据。

4、java的输入流是从磁盘、光盘等存储设备中将数据读入到程序中；输出流是将程序中的结果保存到外部



> 流的分类

按数据流的流向不同分为：输入流、输出流。

输入流用来讲数据从存储写入内存、输出流是用来将内存的数据写入存储



按流的角色不同分为：节点流、处理流/包装流

处理节点流的类有：FileReader、FIleWriter等；处理包装流的类有：BUfferedReader、BufferedWriter等

|        | 节点流                       | 包装流                                |
| ------ | ---------------------------- | ------------------------------------- |
| 输入流 | FileinputStream / FileReader | BufferedInputStream / BufferedReader  |
| 输出流 | FileOutputStream /FileWriter | BufferedOutputStream / BufferedWriter |
|        |                              |                                       |

节点流可以从一个特定的数据源读写数据、包装流是存在于在已经存在的流之上，为程序提供更为强大的读写功能。









按操作数据单位的不同可分为：字节流（8bit），字符流（根据字符情况看）

|        | 字节流         | 字符流   |
| ------ | -------------- | -------- |
| 输入流 | inputStream类  | Reader类 |
| 输出流 | OutputStream类 | Writer类 |





这里类里重要的子类如下

|                | 字节流              |                      | 字符流             |                   |
| -------------- | ------------------- | -------------------- | ------------------ | ----------------- |
|                | **inputStream**     | **OutputStream**     | **Reader**         | **Writer**        |
| **节点流**     | fileInputStream     | FileOutputStream     | FileReader         | FileWeriter       |
| **处理流**     | BufferedInputStream | BufferedOutputStream | BufferedReader     | BufferedWriter    |
| **对象处理流** | ObjectInputStream   | ObjectOutputStream   |                    |                   |
| **转换流**     | OutputStreamWriter  | InputStreamReader    | OutputStreamWriter | InputStreamReader |

转换流是将字节流转为字符流用的。

字节流和字符流都各自有输入和输出流，上表说明了这四种流的顶级父类。这几个父类都是抽象类，无法直接实例化，要通过其子类来创建对象。

第十五章主要针对上面12种类来详细讲解。



#### 15.2 节点流



##### 15.2.1 fileInputStream

字节输入流，主要功能是将某个文件中的内容以字节的形式提取进程序内，该类的主要方法就一个——read（）。

该方法有两种重载，一种是无实参的read方法，一种是接受字符数组的read方法

```java
public void readFile01(){
        String path = "src/_09_IO/Resources/example1.txt";
        FileInputStream fileInputStream = null;
        int temp = 0;

        try {//用try来环绕下面的语句，不然会有编译异常
            fileInputStream = new FileInputStream(path); //创建一个FileInputStream对象，将该对象与path路径下的文件绑定，即外卖小哥取了特定的餐

            //1、read方法，遍历读取FileInputStream对象的内容（即与该对象绑定的文件内容），读取出来的结果是int的，最后可以转成byte来接受，因为byte和int可以互转。若读取完毕，则返回-1，若本来就无内容，则会异常。
            temp = fileInputStream.read(); //如果文件里面的内容是以多字节为单位的，如汉字这种一个字符占两三个字节的，那么用字节输入流就只能将每个汉字的若干个字节挨个独自读取，最后肯定乱码。这种字符得用字符流读取
            

                //其常见用法如下，用于while循环的条件判断
            while ((temp = fileInputStream.read()) != -1){ //在使用时，要把read方法放到循环里才能遍历赋值，要不只会将文件里第一个值赋进去
                System.out.println((char)temp);
            }

        } catch (IOException e) {
            e.printStackTrace();


        }finally {//在finally里关闭文件流，防止资源浪费
            try {
                fileInputStream.close(); //用这句话来关闭流
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

```



```java
public void readFile02(){
        String path = "src/_09_IO/Resources/example1.txt";
        FileInputStream fileInputStream = null;
        int readLen = 0;
        byte[] bytes = new byte[8];//定义一个字节数组，用于read方法里。该字节数组的长度就是一口气读入，字节数组用来存放read（byte[] bytes）所读取的具体字节数据

        try {
            fileInputStream = new FileInputStream(path);

            while ((readLen = fileInputStream.read(bytes))!= -1){
                System.out.print(new String(bytes,0,readLen));//此处输出不能挨个字节输出了，要以字符串的形式输出
            }


        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }
```



##### 15.2.2 FileOutputStream

字节输出流，主要是将程序内生成的数据内容以字节的形式写入外部文件中。其常用方法为writh方法

```java
    public void WrtieFile(){
        String path = "src/_09_IO/Resources/example_02_02.txt";
        FileOutputStream fileOutputStream = null;

        try {
            fileOutputStream = new FileOutputStream(path); //实例化一个output对象

            //写入一个字节
            fileOutputStream.write('a');

            //成批写入字节
            String str = "helloworld";//先写一个字符串，但是该字符串是不能直接通过字节输出流写入文件的，要转成字节
            byte[] bytes = str.getBytes();//通过字符串的getBytes方法来将字符串里的内容转成字节数组
            fileOutputStream.write(bytes);//然后就可以通过字节输出流将字节数组写入文件

            //writh方法有一个重载方法——write（byte[] b , int off , int len），三个形参分别为字节数组、起始索引、写入字节长度。即从字节数组中的第off个索引开始，写入len个字节
            //该方法可以直接处理字符串，但其底层实际上还是刚刚的将字符串变为字节数组的方法
            fileOutputStream.write(str.getBytes(), 0 , str.length());




        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileOutputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }
```



在用字节输出流时有个细节，每次重新运行写入方法时会覆盖掉原文件中的内容再写入当次写入的内容。

有一个方法可以不进行覆盖而转成追加写入内容，其变换在与

```java
FileOutPutStream fileoutputstream = new FileOutputStream(path);//构造字节输出流实例对象的第一种方法
FileOutPutStream fileoutputstream = new FileOutputStream(path,true);//构造实例对象的第二种方法，用该方法来创建的字节输入流对象是进行内容追加而不是内容覆盖。
```



##### 15.2.3FileReader



实际上fileReader的使用方法和fileInput Stream的使用方法差不多，主要方法都是read方法，也都有一个read的重写方法。区别就是，FileReader是以字符为单位进行操作的，而fileinputStream是以字节为单位操作的。



> 无实参的read方法

```java
public void fileReader01(){
        String path = "src/_09_IO/Resources/example_03_01.txt";
        FileReader fileReader = null;
        int temp = 0; //做一个临时int来接受read到的内容，read返回的值是int类型的，最后可以用char来接受，因为int可以自动转char

        try {
            fileReader = new FileReader(path);

            //循环读取
            while ((temp = fileReader.read()) != -1){
                System.out.print((char) temp);
            }


        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileReader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
```



> 有实参的read方法

```java
public void FileRead02(){
        String path = "src/_09_IO/Resources/example_03_01.txt";

        FileReader fileReader = null;
        int temp = 0; 
        char[] chars = new char[3]; //这里多加了一行

        try {
            fileReader = new FileReader(path);

            //循环读取
            while ((temp = fileReader.read(chars)) != -1){
                System.out.print(new String(chars,0,temp)); //这里打印是通过String来打印
            }


        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileReader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }
//除了上面做注释的两处变了，其他地方都一样
```



##### 15.2.4 FileWriter

同filereader与fileinputstream类似一样，filewriter与fileoutputStream也非常类似，其主要方法也是write方法。也是一个针对字节操作、一个针对字符操作。

要说多了点不同，就是filewriter的write方法重载了五个，而fileoutputStream只重载了两个。

```java
public void FileWriter(){

        try {
            fileWriter = new FileWriter(path); //实例化filewriter对象。若不想以覆盖形式写信息而想以追加方式写信息，则和上面一样，在后面加true

            fileWriter.write('H');//写入单个字符
            fileWriter.write("e"); //写入只含有一个字符的字符串
            char[] chars = {'l', 'l', 'o'};
            fileWriter.write(chars);//写入一个字符数组

            char[] chars1 = {',','w','o','x','x'};
            fileWriter.write(chars1,0,3);//从char1的索引0开始写，写三个字符进去

            String s = "rl";
            fileWriter.write(s);//写入整个字符串

            String s1 = "dxxx";
            fileWriter.write(s1,0,1);//同理，写入字符串的某部分

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fileWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```



要注意，这点非常重要。filewriter对象使用完后，一定要进行close或者flush（刷新），否则其写的内容会一直保存在内存中，写入不到文件里。这一步看源码可以发现，close里才定义了讲字符写入文件的方法，而不调close方法就无法将内容从内存写入存储。



#### 15.3 处理流

Buffered系列是包装流（处理流）的分支，它是建立在其他流之上的。简单理解就是强化一下其他类，让其有更强大的功能。

这里的其他流包括了大类下的所有流，如BufferedReader可以强化Reader类下的所有类、BufferedWriter可以强化Writer类下的所有类。

处理流在关闭时只需要关闭外层流就可以了，buffered会在关闭外层流后自动关闭底层流。

在包装时，字节流的包装流包装字节流的底层流、字符流的包装流包装字符流的底层流。（BufferedWriter包装FileWriter而不包装FileOutputStream）





> 节点流和处理流的异同

1、节点流是底层的流，直接跟数据源相连接

2、处理流用来包装节点流，既可以消除不同节点流之间的实现差异，也可以提供更方便的方法来完成输入输出

3、处理流对节点流进行包装，使用了修饰器设计模式，不会直接与数据源相连接（该原理看idea里面）



该设计模式结构如下（以reader为例）

（小tips）BufferedReader的构造器是接受一个Reader类的对象，这也很符合Buffered类的特性，它是强化某个Reader对象用的。

```java
new BufferedReader(Reader r)
```

具体实例如下：

```java
public abstract class _01_Reader {

    public void readFile(){}
    public void readString(){}

}

public class _02_FileReader extends _01_Reader{

    public void readFile(){
        System.out.println("对文件进行读取");
    }
}


public class _03_StringReader extends _01_Reader{

    public void readString(){
        System.out.println("读取字符串");
    }
}

public class _04_BufferedReader extends _01_Reader{

    private _01_Reader reader;

    public _04_BufferedReader(_01_Reader reader){
        this.reader = reader;
    }

    //强化之前的文件读取方法，这里让读取文件能进行多次读取
    public void readFiles(int num){
        for (int i = 0; i < num; i++) {
            reader.readFile();
        }
    }

    //强化之前的字符串读取方法，这里让读字符串能进行多次读取
    public void readStrings(int num){
        for (int i = 0; i < num; i++) {
            reader.readString();
        }
    }


}

public class _05_run {
    public static void main(String[] args) {

        _04_BufferedReader bufferedReader = new _04_BufferedReader(new _02_FileReader());
        bufferedReader.readFiles(10);
        bufferedReader.readStrings(1); //这里根据多态，是没有内容输出的。因为fileReader类只重写了readFile方法，readString方法还是Read类里的，只有一个外壳，内容还是空的

        _04_BufferedReader bufferedReader1 = new _04_BufferedReader(new _03_StringReader());
        bufferedReader1.readStrings(10);
    }
}
```



##### 15.3.1 BufferedReader

这些应用实际上和前面的几乎一样，都是做一个对象来进行read或者write。下面就简单看下实例应用就行。

```java
public static void main(String[] args) throws Exception{

        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_04_01.txt";
        FileReader fileReader = new FileReader(path); //先做一个底层流的对象
        BufferedReader bufferedReader = new BufferedReader(fileReader);//将该底层流放入bufferedreader种（或者说将bufferedreader包装上底层流）

        //bufferedreader的方法（相比普通的FileReader要高阶一点）
        //按行读取文件readLine()方法。当返回为null时表示文件读取完毕。
        String temp;
        while ((temp = bufferedReader.readLine()) != null){
            System.out.println(temp);
        }

        bufferedReader.close();//关闭流时只需要关闭外层流就行，即只关闭包装流，包装流会自动关闭节点流

    }
```



##### 15.3.2 BufferedWriter

```java
    public static void main(String[] args) throws Exception{
        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_04_02.txt";
        FileWriter fileWriter = new FileWriter(path);
        BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);

        //写入信息
        bufferedWriter.write("hello");
        bufferedWriter.newLine();//插入一个换行符
        bufferedWriter.write("world");

        bufferedWriter.close();//关闭流
    }
```

 

##### 15.3.3 BufferedInputStream

```java
    public static void main(String[] args) throws Exception{
        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_04_01.txt";
        FileInputStream fileInputStream = new FileInputStream(path);
        BufferedInputStream bufferedInputStream = new BufferedInputStream(fileInputStream);

        //方法:read()，读取文件种的字节，将字节转换为int，若文件读取完毕则返回-1
        int temp = 0;
        while ((temp = bufferedInputStream.read()) != -1){
            System.out.print((char)temp);
        }

        bufferedInputStream.close();

    }
```



##### 15.3.4 BufferedOutputStream

```java
    public static void main(String[] args) throws Exception{
        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_04_03.txt";
        FileOutputStream fileOutputStream = new FileOutputStream(path);
        BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(fileOutputStream);

        //方法:read()，读取文件种的字节，将字节转换为int，若文件读取完毕则返回-1

        bufferedOutputStream.write('h');

        bufferedOutputStream.close();

    }
```



#### 15.4 对象流

ObjectXXX为对象流，其也是处理流，构造器接受一个流对象。在保存一个数据时，比如保存100，如何知道这个100是什么数据类型的呢？文件中只能看到100这个阿拉伯数字，但是无法知道它是int型还是char还是String进去的100。这样可能会对以后的数据恢复造成麻烦，故在保存数据时，将数据的数据类型也一起保存起来是有必要的。



连带数据类型进行保存数据的过程和恢复数据的过程实际上有个专有名词——序列化和反序列化。

序列化就是在保存数据时，保存数据的数据类型和数据值；反序列化就是在恢复数据时恢复数据的数据类型和数据值。

某个对象想要支持序列化机制，则这个对象所在的类必须是可序列化的，而让类可序列化就需要让类实现以下接口之一：Serializable、Externalizable。



##### 15.4.1 ObjectOutputStream

序列化过程如下

```java
public class _01_ObjectOutputStream {
    public static void main(String[] args) throws Exception{

        //此处演示序列化的过程，虽然path的文件此时是个txt文件，但是序列化后的文件是按其特有的方式存储的，不是txt了
        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_0401.txt";
        FileOutputStream fileOutputStream = new FileOutputStream(path);
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);


        //序列化数据到path中
        objectOutputStream.write(100);//此处将int类型的100进行序列化，此处int型会自动装箱成Integer类型，而Integer类型又实现了Serializable接口，故可以被序列化
        objectOutputStream.writeBoolean(true);//将布尔型通过自动装箱后进行序列化
        //其他基本数据类型也可通过自动装箱后进行序列化

        //将dog对象序列化
        objectOutputStream.writeObject(new Dog("大黄"));



    }
}

class Dog implements Serializable{ //实现可串行化的接口后可以进行序列化
    String name;
    public Dog(String name){
        this.name = name;
    }
}
```

在序列化完成后，打开存储的txt文件，会发现其全是乱码，因为序列化后的文件不是txt格式的，但是该文件可以用来进行反序列化。



##### 15.4.2 ObjectInputStream

反序列化在反自定义的对象时有些细节

```java
public static void main(String[] args) throws Exception {
        //加载需要反序列化的文件
        String path = "D:\\Code\\JavaCode\\Study\\src\\_09_IO\\Resources\\example_0401.txt";
        FileInputStream fileInputStream = new FileInputStream(path);
        ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);

        //反序列化的顺序要和序列化的顺序一致
        System.out.println(objectInputStream.readInt());
        System.out.println(objectInputStream.readBoolean());

        //此处将序列化的对象取出，取进object类中，然后打印。Object dog = objectInputStream.readObject();
        // 将序列化中的狗对象取出但想使用dog类下的run方法该怎么办呢？此处dog的编译类型是Object类，而Object类下并没有定义run方法，故需要向下转型。
        //但是向下转型又需要该包下又Dog类，故在反序列化时若想用序列化对象的信息，需要将那个类原封不动的拿到这个class下
        //上面是按理说。但是由于此处_02_ObjectInputStream类和_01_ObjectOutputStream类都在同一个包下，故其共享dog类，可以直接用。
        //若是不同包下，一定要把dog类拿到新包中（且一般情况要将dog类公有化）

        Object dog = objectInputStream.readObject();
        System.out.println(dog);
        Dog dog1 = (Dog)dog;
        dog1.run();



        objectInputStream.close();

    }
```



> 细节

1、反序列化的顺序要 和序列化的顺序一致

2、序列化和反序列化的对象要实现了Serializable接口

3、序列化的类中可以添加一个long类型的final static 私有属性serialVersionUID ，让其值等于1L来提高版本兼容性

```java
Private static final long serialVersionUID = 1L;
```

4、序列化对象时，默认将里面所有属性都进行序列化，但static或transient修饰的成员不会进行序列化，相当于这些属性不会被保存进文本

5、序列化对象时，要求对象的属性也时实现了序列化的属性。如上面dog类的属性String是字符串类型实现了Serializable接口，故dog可以序列化。但是若dog里还有一个其他自定义的对象，而该对象所在的类没有实现序列化接口，则在序列化dog时会报错。

6、序列化有可继承性，若某个类实现了序列化，则其子类也默认实现序列化



#### 15.5 转换流

在进行文件读取时，默认的文件编码形式时utf-8，是可以正常读取的。但要是文件的编码格式改变了，将文件读取进java程序中就会发生乱码。

此时使用转换流来指定字节流的编码，然后将字节流转换为字符流来处理乱码问题。



##### 15.5.1 InputStreamReader

顾名思义，将InputStream转为Reader的流，字符输入转换流。

字符输入转换流，其构造器为

```java
InputStreamReader(InputStream , Charset)
```

通过此构造器可以看出，字符输入转换流接受一个任意字节输入流对象，再接受一个编码格式。作用为将该输入流对象的编码改为指定的编码，并将该字节流改为字符流



##### 15.5.2 OutputStreamWriter

同字符收入转换流的原理一样。



#### 15.6 配置流

在有些时候，我们常常将一个程序所需要参数单独拿出来放到一个文件中，这个文件叫配置文件（类似python里的option文件）

此时我们就需要用一种流将这种文件读取进程序中。



配置流的父类是Hashtable，实际上是一个集合类



使用配置流时，对配置文件有一定的格式要求，其要求文件

```
键1=值1
键2=值2
```

其中等号两端不加空格，键值上不带引号。



> 常见方法

load：加载配置文件的键值对到Properties对象

list：将数据显示到指定设备

getProperty（key）：根据键获取值

getProperty（key，value）设置键值对到properties对象

store：将properties中的键值对存储到配置文件中，若配置文件内有中文，则会存储为Unicode码



### 16 正则

正则表达式，Regular Expression又常简写为RegExp，是一种专门处理字符串匹配问题的方法，常用于处理文本信息。

一个正则表达式就是用某种模式去匹配所给文本的公式。

#### 16.1 底层实现

先举一个例子

```java
public class run {
    public static void main(String[] args) {
        String txt = "现在有一个文本，该文本中记录了各种信息，其中有很多数字信息，而现在要想办法将该文本中的4连的数字信息全部提取出来，给出数字信息如下" 						+ "123，1245，1451，345，12，5125。常规提取要遍历字符串，判断每个字符是否等于那10个阿拉伯数字，如果用正则就会简单很多";

        //1、确定匹配的目标：匹配数字
        String regExpStr = "\\d\\d\\d\\d";//这里每个\\d表示任意一个数字，四个\\d连在一起表示取出4连数字

        //2、应用正则规则
        Pattern pattern = Pattern.compile(regExpStr);//创建一个正则表达式对象。相当于将指定的正则规则应用上


        //3、根据规则创建匹配器
        Matcher matcher = pattern.matcher(txt);//创建一个匹配器matcher，按照正则表达式的规则去匹配txt字符串

        //4、开始循环匹配
        while (matcher.find()){
            System.out.println("找到：" + matcher.group(0));
        }


    }

}
```

其中需要了解mathcer.find()的工作原理、matcher.group()的工作原理



先看find（）部分：

根据指定的正则规则去给定字符串中去匹配满足规则的字符串，比如目前找到了第一个满足规则的子字符串：1245

然后会将该子字符串的开始索引记录到matcher对象中的属性： int[] groups数组中，并将开始索引记为groups[0]，然后将该子字符串的结尾索引+1记录到groups[1]中。如1245中，1在整个字符串中的索引为69,则group[0] = 69，而gruop[1] = 73。（之所以结尾索引要加1，是因为截取字符串的方法subString是顾头不顾腚的）

同时记录matcher中属性：int oldlast的值为刚刚查找完的子字符串结束的索引值+1，即此时oldlast=73。

然后下次find执行时，从索引73开始向后搜索。并且再有与正则方法相匹配的字符后，会将其索引依旧记录再groups[0]与groups[1]上



再看group（）的部分

group（）方法的核心是一个返回：return getSubSequence(groups[group*2],groups[group *2 +1]).toString。这里groups是刚刚通过find记录上的groups数组，group是该group方法接受的实参。getSubSequence是切割字符串的方法

上方示例传入的实参是0，故相当于SubSequence了groups[0]到groups[1]之间的字符（在整个文本中，相当于截取了索引为69到73之间的字符），并将其toString了之后return回去



再由此引出一个问题，为什么group方法要传入的实参是0呢？可不可以是其他值呢？可以是其他值，实参是零的时候一般是最简单的正则用的，若使用到分组的情况，则group方法就要传入其他实参了。示例如下

```java
String regExpStr = "(\\d\\d)(\\d\\d");//这里将每两个\\d之间用括号分开，表示进行分组，第一个括号表示将这四个数的前两个数分为第一组、第二个括号表示第二组

...
    ...
    while(matcher.find()){
            matcher.group(0);//之后经过中间相同的操作来到find方法和group方法部分
    }
  
```

现在再来看find方法发生了什么：

首先先找到符合未分组情况下的匹配的字符串位置，还是会找到1245，还是将groups[0]=69(1所在的索引)、groups[1]=73(5所在索引数+1)。之后find方法还会将分组后的情况记录下来，先记录第一组，将groups[2]=69(1所在的索引)、groups[3]=71(2所在索引+1)；之后记录第二组groups[4]=71(4所在索引)、groups[5]=73(5所在索引+1)。

然后group方法就可以传入其他实参了

如果想查看未分组的情况，则依旧传入0，得到的return是getSubSequence(groups[0 * 2 = 0 ], groups[0 *2 +1 = 1]).toString，即取出的是69~73之间的字符（顾头不顾腚形式）；若想查看第一组，则直接传入1，得到return为getSubSequence(groups[1 * 2 = 2 ], groups[1 *2 +1 = 3]).toString，取出的是69~71之间的字符。同理，查看第二组则传入2即可。



#### 16.2 语法

正则表达式有各种字符，可以大体分为六类：限定符、选择匹配符、分组组合和反向引用符、特殊字符、字符匹配符、定位符。

但是在说明这些字符前，要强调一下转义字符在正则中的使用情况。



##### 16.2.1 转义字符

如果现在有一个字符串为：“abc%(”，现在想匹配到"("，是不能直接用"("当正则的，要用上转义字符

```java
public static void main(String[] args) {
        String txt = "abc%(";

 
        String regExpStr = "(";//这里只写一个括号会编译错误，正确写法应该如下
    	String regExpStr = "//("//前面用两个反斜杠当转义字符用

        Pattern pattern = Pattern.compile(regExpStr);//创建一个正则表达式对象。相当于将指定的正则规则应用上


        Matcher matcher = pattern.matcher(txt);//创建一个匹配器matcher，按照正则表达式的规则去匹配txt字符串

        while (matcher.find()){
            System.out.println("找到：" + matcher.group(0));
        }
```

两个反斜杠当转义字符是java中正则特有的，其他语言要看其他语言怎么规定的。



需要用到转义字符的字符有：`.` `*`  `+` `()` `$` `/`  `\` `?` `[]` `^` `{}` 



> 字符匹配符

| 符合 | 符号含义                                         | 示例    | 解释                                                   |
| ---- | ------------------------------------------------ | ------- | ------------------------------------------------------ |
| [ ]  | 可接收的字符列表                                 | [abcd]  | 匹配a、b、c、d中任意一个字符                           |
| [^]  | 不接受的字符列表                                 | [^abcd] | 匹配除a、b、c、d外其他的一个字符（包括数字和特殊符号） |
| -    | 连字符                                           | [A-Z]   | 匹配任意A-Z之间的一个字符                              |
| .    | 匹配除\n以外的任何字符（\n为换行符）             | a..b    | 匹配以a开头、b为结尾的任意长度为4的字符                |
| \\\d | 匹配单个数字字符（相当于[0-9]）                  | \\\d{3} | 匹配长度为3的数字字符串                                |
| \\\D | 匹配单个非数字字符（相当于[^ 0-9\]）             | \\\D{4} | 匹配长度为4的不包含数字的字符串                        |
| \\\w | 匹配单个数字、大小写字母（相当于[0-9a-zA-Z]）    | \\\w{5} | 匹配长度为5的字符串（不包含特殊字符）                  |
| \\\W | 匹配单个特殊字符                                 | \\\W{2} | 匹配长度为2的特殊字符串                                |
| {}   | 表数量的字符                                     | \\\d{3} | 表示匹配三个字符                                       |
| \\\s | 匹配任何空白字符（空格、指标等）                 | \\\s{2} | 匹配长度为2的空白字符                                  |
|      | 也可不加符号的进行匹配，就匹配完全符合要求的字符 | abc6    | 匹配字符串中所有的“abc6”                               |



上面是基本操作，有一些进阶操作，它们也可以进行不同的排列组合

进阶操作如不区分大小写：

(?i)ab 表示匹配字符串中所有“ab”，不区分大小写，匹配结果可能为：ab、aB、Ab、AB

a((?i)b)c表示匹配字符串中所有abc，其中b不区分大小写，匹配结果可能为：abc、aBc

a(?i)bc表示匹配字符串中所有abc，其中bc不区分大小写，匹配结果可能为abc、aBc、abC、aBC

想不区分大小写，也可以在pattern对象构造时，传入构造器为

Pattern pattern =  Pattern.compile(regStr, Pattern.CASE_INSENSITIVE)，表示对大小写不敏感



> 选择匹配符

用于指定多个匹配结果，比如既想匹配这个又想匹配那个，就可以用选择匹配符

| 符号 | 符号含义                   | 示例   | 解释                                                         |
| ---- | -------------------------- | ------ | ------------------------------------------------------------ |
| \|   | 匹配“\|”之前与之后的表达式 | ab\|cd | 匹配ab与匹配cd（有ab就匹配ab、有cd就匹配cd，两者都有就两者都匹配） |





> 限定符

用于指定前面的字符和组合项连续出现多少次(放在后面)

要注意，不能将两个限定符放在同一个字符匹配符后面，如不能：[abc]*{3}。即每个字符匹配符后面只能跟一个限定符

| 符号  | 含义                          | 示例   | 解释                                 |
| ----- | ----------------------------- | ------ | ------------------------------------ |
| *     | 指定字符重复n次（可以是0次）  | (abc)* | 匹配仅包含任意个abc的字符串          |
| +     | 指定字符串重复1次到n次        | a+b    | 匹配以至少一个a开头，后面是b的字符串 |
|       |                               | a+     | 匹配只包含任意个a的字符串            |
| ?     | 指定字符重复0次或1次          | a?b    | 匹配b\ab                             |
| {n}   | 指定匹配后的字符串长度为n     | a{3}   | 匹配长度为3的仅包含a的字符串         |
| {n,}  | 指定匹配后的字符串长度至少为n | a{3,}  | 匹配长度至少为3的只包含a的字符串     |
| {n,m} | 指定匹配字符串长度为n~m之间   | a{3,5} | 匹配长度为3、4、5的只包含a的字符串   |



> 定位符

规定要匹配的字符串出现的位置

| 符号            | 含义                 | 示例           | 解释                                                         |
| --------------- | -------------------- | -------------- | ------------------------------------------------------------ |
| ^(放在最前面)   | 表示匹配的字符的开头 | ^[0-9]+[a-z]*  | 以任意长度（长度不能是0）的数字开头，后接任意长度（可以是0）的小写字母 |
| $（放在最后面） | 表示匹配的字符的结尾 | ^[0-9]+[a-z]+$ | 以任意长度的数字开头，并以至少一个小写字母结尾               |
| \\\b            | 匹配结尾             | jack\\\b       | 以jack结尾的字符串                                           |
| \\\B            | 匹配开始             | jack\\\B       | 以jack开始的字符串                                           |



#### 16.3 关键类

正则表达式有三个关键的类：Pattern类、Matcher类和PatternSyntaxException三个类。

pattern类是一个正则表达式的类，其没有public的构造方法，要创建pattern对象需要调用其公共的静态方法来创建。该方法接受一个正则表达式作为它的第一个参数：Pattern pattern = Pattern.compile(pattern);



matcher对象是对输入字符串进行解释和匹配的引擎，与pattern类一样，matcher也没有公共的构造方法，需要使用pattern对象中的matcher方法来构造matcher对象。



### 17 网络

#### 17.1 网络基础

> 网络通信

1、概念：两台设备之间通过网络实现数据传输

2、网络通信：将数据通过网络从一台设备传输到另一台设备

3、java.net包下提供了一系列类或接口，供程序员使用，完成网络通信



根据网络的覆盖范围大小不同，可以对网络分为三类：局域网（覆盖范围小，覆盖一个教师或者一个机房）、城域网（覆盖范围大，覆盖一座城市）、广域网（覆盖范围巨大，覆盖一个国家甚至全球）



> IP地址

1、概念：用于唯一标识网络中每台计算机

2、查看ip地址的方法：cmd-->ipconfig

3、ip地址的表现形式：点分十进制。

ipv4是由四个字节来表示的，而每个字节有8位，故一共有32位来表示，且每个字节的表示范围位0~255。ip地址是分为两部分的：网络地址+主机地址，具体网络地址占几个字节、主机地址占几个字节，要由该ip地址是ABC三个类中的哪个类来决定，若是A类，则第一个字节表示网络地址，后三个字节表示主机地址；若是C类，则前三个字节表示网络地址，最后一个字节表示主机地址

ipv6，由于ipv4不够用了，故提出了ipv6的概念，极大的提高了可用的网络资源地址。ipv6由16进制来表示，每两位表示一个字节。



4、ipv4的类别：ABC三个类的情况刚刚介绍了，现在说一下细节。A类表示的范围为：0.0.0.0~127.255.255.255;B类表示的范围为：128.0.0.0~191.255.255.255；C类的范围为：192.0.0.0~223.255.255.255。其中127.0.0.1 表示本机地址



5、在进行网络通信时，一定要知道通信对方的ip地址才行，否则信息无法准确的找到该去的位置



> 域名

域名是ip地址的另一种表达方式，实际上是ip地址的映射。如百度的ipv4地址为192.168.168.1（随便写的），但是这个ip地址还是难记的，则用www.baidu.com来作为该ip地址的映射，输入该域名则代表输入该ip。该映射是通过HTTP协议来映射的。



> 端口号

1、概念：用来标识计算机上各个软件。每个电脑都有一个各自的ip地址，而每个电脑上的每个软件又有一个各自的端口号，如qq的端口号可能是1001，那么从另一台电脑的qq发送到本机qq时，就要即匹配到本机的ip地址，又匹配到本机的qq的端口。

2、表示方式：端口的表示形式为整数形式，其表示范围为0~65535(2^12 - 1)。

3、有一点要注意，在进行软件开发时，尽量不要用0~1024端口，因为这些端口大部分已经被知名的软件占用了。



#### 17.2 网络协议

先做一个类比：人与人之间要进行交流

人和人通信：依靠 语言[中文、英文、日语...]

程序和程序通信：依靠 数据[各种形式的数据]

这里，中文、英文等语言就相当于人与人之间通信的协议；而各种形式的数据则表示网络协议。

网络协议一般使用tcp/ip协议



> TCP/IP

Transmisson Control Protocol / Internet Protocol（传输控制协议/因特网协议），这个协议是互联网最基本的协议，也是最重要的协议。

该协议的大概过程如下

应用程序-->TCP层 -->ip层 -->网络。

在这个过程中，会将原始数据通过应用程序层后在数据前加入一个app帧、然后进入tcp层，加入一个tcp帧，之后通过ip层，加入一个ip帧，最后进入 网络传入，在首部和尾部分别加入一帧，进而在网络中传输。

在用户接受到一个网络中传入过来的信息后，再经过一遍上面的反过程，就可以将信息准确送到该送的程序位置了。



TCP/ip协议实际上就是5层网络中的传输层和网络层，在java编程时，主要关注传输层的情况





> 传输层

传输层有两个最重要的协议：TCP、UDP



TCP

传输控制协议，使用TCP前必须先建立tcp连接，形成数据传输通道。

传输前，使用“三次握手”方式来保证通道可靠

TCP协议进行通信的两个应用进程为：客户端、服务端

在连接中可进行大数据的传输

传输完毕后会释放已建立的连接

因为需要建立连接释放连接等步骤，故效率低，但是由于通过了连接通道的可靠性认证，故安全性高



UDP

将数据、源、目的地封装成数据报，不需要建立连接

将每个数据报大小限制在64k之内

发送数据结束时无需释放资源

由于没有连接，故不是可靠的，但是由于无连接，不需释放资源，故速度是快的。



下面进行编程时，主要围绕tcp编程和udp编程



#### 17.3 InetAddress



#### 17.4 Socket

Socket，嵌套字。常用来开发网络应用程序。

通信两端都要有socket才行，这是两台机器通信的端点。网络通信其实就是socket间的通信

socket允许程序把网络连接当成一个流，数据在两个socket间通过io传输，即socket对象使用input流或者output流来操作，如

客户端通过socket.getOutputStream()方法来向服务端发送信息流，服务端通过socket.getInputStream方法来得到客户端发送的流。

其流程如下

服务端：监听(ServerSocket（int port）)---->收到连接请求(socket accept()) ----->收到客户端输出流（socket.getInputStream）---->向客户端发送(socket.getOutputStream) ---->关闭socket

客户端：                                                             发送连接请求(Socket(InetAddress address , int port)) ---> 发送输出流(socket.getOutputStream) --->收到服务端输出流(Socket.getInputStream) ---->关闭socket



#### 17.5 TCP/UDP 编程

TCP编程和UDP编程都是依赖于Socket的。



##### 17.5.1 TCP

下面直接展示tcp的使用方法

```java
public class _Client {
    public static void main(String[] args) throws IOException {

        //1、连接服务器
        //使用Socket构造器中的有参构造器来构造，传入一个存有想连接主机的ip信息的InetAddress对象与想连接的主机的端口号。由于服务端也是本机，故服务器的ip地址就用getLocalHost()方法就能得到了
        Socket Clinetsocket = new Socket(InetAddress.getLocalHost(), 9999);
        //相当于用该构造器生成socket对象的同时，也完成了对服务端的连接。此时既连接上了服务端，也可通过socket来进行数据传输。

        //2、发送信息给服务端
        OutputStream outputStream = Clinetsocket.getOutputStream();//通过socket创建一个输出流对象
        outputStream.write("helloworld".getBytes());//通过输出流对象确定要输出的信息并进行输出

        Clinetsocket.shutdownOutput();//这里添加一个写入结束标志

        //3，读取服务端的信息
        InputStream inputStream = Clinetsocket.getInputStream();
        byte[] buf = new byte[6];
        int tem = 0;
        while ((tem = inputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,tem));
        }


        //3、关闭资源
        inputStream.close();
        outputStream.close();
        Clinetsocket.close();





    }
}
```



```java
public class _Server {
    public static void main(String[] args) throws IOException {

        //1、做一个ServerSocket对象，该对象负责监听客户端的连接请求，形参传入该服务器的监听端口（相当于服务器的端口）
        ServerSocket ListenSocket = new ServerSocket(9999);//在本机9999端口监听（在本机9999端口没有其他服务的情况下）
        System.out.println("服务端在端口9999监听，等待连接");
        //该程序会一直阻塞在这里（类似键盘输入Scanner监听键盘，若键盘没输入东西，则程序不往下运行，直到键盘监听到了输入）

        //2、若有客户端的连接请求出现，则ListenSocket通过accept方法生成一个Serversocket对象，该对象来执行各种信息流的读取发送
        Socket Serversocket = ListenSocket.accept();

        //3、读取客户端输入的信息
        InputStream inputStream = Serversocket.getInputStream();
        int tem = 0;
        byte[] buf = new byte[5];
        while ((tem = inputStream.read(buf)) != -1){
            System.out.println(new String(buf,0,tem));
        }

        /**
         * 在进行第一次客户端信息读取时没有任何问题，但是下面的向客户端发送信息就需要添加其他操作了，因为如果只是单纯的使用output流，会导致服务端不知道什么
         * 时候开始发送（相当于不知道什么时候写入结束），进而导致程序一直卡在这里，因此要设置一个写入结束标记。
         * 要保持一个良好的习惯，无论在客户端还是服务端，每次完成写入操作都要进行一次结束标记
         */

        //4、向客户端发送信息
        OutputStream outputStream = Serversocket.getOutputStream();
        outputStream.write("i copy that".getBytes());

        Serversocket.shutdownOutput();//要再设置一个写入结束的标记，来告诉程序说，已经写完要向客户端传输的信息了，可用进行发送了

        //关闭流
        inputStream.close();
        Serversocket.close();
        outputStream.close();
        ListenSocket.close();
    }
}
```



以下是一些注意事项：

socket提供的流读写方法是字节流的方法，若想使用字符流，则需要将字节流用转换流来转成字符流。

每次使用完OutPutStream，一定要记得进行shutdownOutput()来结束该次写入。

下面再展示一下字符流的写入操作

```java
OutputStream out = socket.getOutputStream();
BufferedWriter bufferedwriter = new BufferedWriter(new OutputStreamWriter(out));//通过转换流将字节流转为字符流后装入包装流（也可不装）
bufferedwriter.write("helloworld");//写入信息

//下面三个是重点

bufferedwriter.newLine();//语句的意思是写入一个换行符，在tcp通信中，相当于字符流写入结束，相当于结束标记。
//同时要求读取方使用readLine()来读取该行

bufferedwriter.flush();//使用字符流时，要进行手动刷新，确保字符流写入进了数据通道。

```

字符流的读取操作

```java
InputStream int = socket.getInputStream();
BufferedReader bufferedreader = new BufferedReader(new OutputStreamReader(int));

String s = bufferedreader.readLine();//使用readLine方法来读取输入流的信息
sout(s);
```





##### 17.5.2 UDP

了解就行





### 18 反射

#### 18.1 概念

反射机制允许程序在执行期间借助Reflection API 取得任何类的内部信息（成员变量、成员方法等），并能操作对象的属性及方法。反射常用在框架中

加载完类之后，在堆中就产生了一个Class类型的对象（一个类只会产生一个Class对象），这个对象包含了类的完整结构信息。反射机制就是通过这个对象来得到该类的完整结构的。这个对象就像一面镜子，通过这个镜子可用看到类的结构，因此该机制称为：反射



这里再完善一下java编程的整理流程，整体可以分为三个阶段：编译阶段、类加载阶段、运行阶段

编译阶段：编写java程序（定义类、成员方法、成员变量等等），并通过javac来将该程序编译成`.class`文件。

类加载阶段：当运行阶段加载类时（如new一个对象），类加载阶段就会在堆中创建一个该类的class对象，该对象保存了类的完整结构。那么是如何得到这个class对象的呢？实际上是`.class`文件通过一个类加载器（classLoader）得到的。此过程（由.class文件通过类加载器得到class对象）实际上就已经是反射的过程了。在class对象里，它会将每个成员都当成一个对象（方法也视为对象、构造器也视为对象、属性也视为对象等等）

运行阶段：开始实例化对象，运行方法等。重要的是实例化对象，比如实例化了一个编辑阶段定义的类的对象，那么该对象内部是与类加载阶段的class对象有关联的，即该对象知道自己与堆中的哪个class对象想关联，故而是可以通过运行类型中的实例化对象得到类加载阶段中的class对象。然后class对象就可以调用Class类中定义的各种方法和属性了



总结来说，反射机制可以：

1、在运行时判断任意一个对象所属的类

2、在运行时构造任意一个类的对象

3、在运行时得到任意一个类所具有的成员变量和方法

4、在运行时调用任意一个对象的成员方法和变量

5、生成动态代理



反射相关的主要类有四个：

java.lang.Class 代表一个类，Class对象表示某个类加载后在堆中的对象

java.lang.reflect.Method 代表类的方法

java.lang.reflect.Field 代表类的成员变量

java.lang.reflect.Constructor 代表类的构造器



#### 18.2 优化

虽然反射机制有很好的实用性，但是其加载过程会相对于之间从运行过程中加载慢一些

反射中，Method类、Field类、Constructor类都提供了一个方法叫setAccessible方法

该方法是启动和禁用访问安全检查的开关，当其参数为true时，表示反射的对象在使用时取消安全访问检查，提高反射效率；反之进行检查



#### 18.3 Class类详解

1、Class类也是类，因此也继承Object类。

2、Class类对象不是new出来的，而是系统创建的。系统通过classLoader方法将一个类的结构以class类对象的形式保存在堆中

3、对于某个类的Class类对象，在内存中只有一份，因为类只加载一次。也就是说，不管实例化多少个目标类的对象，该类的Class对象只会在堆中存在一份。

4、每个类的实例都会记得自己是由哪个Class实例所生成的

5、通过Class对象可以完整的得到一个类的完整结构（通过Class类中提供的各种方法得到）

6、Class对象是存放在堆的。

7、类的字节码二进制数据存放在方法区，有的地方称为类的元数据



8、Class内包含以下几个主要的变量

```java
Class class{
    Field[] fields;//用来存放与Class关联的类的属性
    Constructor[] cons;//用来存放与Class关联的类的构造器
    Method[] ms;//用来存放于Class关联的类的方法
}
//如假设现在Class类是dog类的Class，Dog类下有属性：姓名、年龄；构造器：无参一个、有参一个；方法：叫、跑
Field[0] = "name";
Field[1] = "age";//Field数组里存放Dog类的属性名称，这些属性要通过class类中提供的getField方法得到
Cons[0] = 无参构造器;
ms[1] = run;//也类似
```



##### 18.3.1Class类的方法



##### 18.3.2 Class对象的获取

1、在已知类的全名和路径的情况下，可以通过Class类的静态方法forName来获取

```java
Class cls = Class.forName("类名");
```

多用于配置文件

此为在编译阶段获取Class类    



2、已知具体类，通过类名,Class获取该类对应的Class对象





#### 18.4 类加载



##### 18.4.1 动态加载

在学反射之前，所有的类的加载都是静态的，如最常见的Cat cat = new Cat()；这种加载会在程序编译时就进行加载，无论运行时用没用到。

而通过反射用Class来创建一个对应的对象，则是动态加载类。若是运行时并没有用到该类，则不会进行加载。

下面举个例子：

```java
public class run{
    Sacnner scanner = new Scanner(System.in);
    String key = scanner.next();
    
    switch(key){
            case"1":
            	Dog dog = new Dog();//静态加载一个dog对象，但是假设并没有dog类存在
            case"2":
            	Class cls = Class.forName("Dog");
            	Dog o = (Dog)cls.newInstance();//通过反射创建一个Dog对象
    }
}
```

上述代码在编译时，case1会报错，因为Dog类是不存在的；而case2不会报错，因为此时并没有运行，即使运行了也没有从键盘输入2进去。只有真正从键盘输入2了，才会开始报错。

这就是动态加载和静态加载的区别



以下再总结以下类的加载的时机：1、创建对象时（new一个对象 ） 2、当子类被加载时 ；3、调用类中静态方法时；4、通过反射加载时。前三个时静态加载，通过反射是动态加载



##### 18.4.2 加载过程

类加载可细分为3个步骤：加载（loading）、连接（Linking）、初始化（initialization）

看看p720









