#  JavaWeb

javaweb，以网页为主进行学习。网页主要分为三部分：HTML、CSS、JavaScript。

HTML是网页的内容信息。

CSS是网页的样式布局。

JavaScript是网页的行为效果

## 一 、基础

### 1、HTML

#### 1.1 基本概念

HTML（HyperText Mark-up Language），超文本标签语言。顾名思义，可以展示远远不止文本的内容标签

HTML 文本是由 HTML 标签组成的文本，可以包括文字、图形、动画、声音、表格、链接等。

HTML 的结构包括头部（Head）、主体（Body）两大部分，其中头部描述浏览器所需的信息，而主体则包含所要说明的具体内容。



> 基本结构

HTML文件由以下几部分组成

1、文档类型说明；

2、文档的语言地区

3、页面的头部信息

4、页面的主体信息

```html
<!--html文件说明：html文件是由浏览器进行解析的，即写好html文件，然后直接用浏览器打开（谁家浏览器都行），然后浏览器会判断所写的html文件是否由错误-->

<!--表示该文件是html型的-->
<!DOCTYPE html>

<!--该行表示语言的地区，默认为en（英国）-->
<html lang="en">

<!--网页的头部-->
<head>
    <!--网页的字符集类型，默认为UTF-8-->
    <meta charset="UTF-8">
    <!--网页的标题，会在网页名称那里显示-->
    <title>test</title>
</head>

<!--网页的主体部分-->
<body>
helloworld
</body>


</html>
```



#### 2  标签

##### 2.1 基本介绍

> 结构

1、HTML文件的标签都由两个尖括号括起来`<>`

2、HTML 标签一般是双标签，如`<b>`和`</b>` 前一个标签是起始标签, 后一个标签为结束标签

3、两个标签之间的文本是 html 元素的内容

4、某些标签称为"单标签",因为它只需单独使用就能完整地表达意思,如`<br/>` `<hr/>`

5、html的注释写法为`<!--XXX--> `



```html
<!--单标签情况-->
<hr/>
hello<br/>
world
```

解释以下，`<hr/>`表示画一条横线，`<br/>`表示换行



> 细节

1、标签不能交叉使用

```html
<body>
    
<div><span>jack</span></div> //正确，这里标签是成对出现的，类似各种括号的用法，左边和右边匹配
<div><span>jack</div></span> //错误，这里就标签交叉使用了
    
</body>
```



2、标签必须正确关闭，即在双标签的情况下，有起始标签则一定要有结束标签与之匹配



3、注释不能嵌套

```html
<!--外部注释<!--内部注释-->--> //错误使用，注释嵌套了，系统会将最左边的左括号与最左边的右括号匹配到一块，然后最右边的右括号就无法解析了
```



最重要的一个细节，html的语法并不是百分百严谨的，有时html语言标签没有闭合、属性（如字体型号、颜色等等）没带引号也不会报错。



##### 2.2 标签分类

> 字体标签

字体标签，font标签，标注网页里字的字体、颜色、大小。

其中color标注颜色、face标注字体、size标注大小。

```html
<body>
    
<font color=blue face="微软雅黑" size=30px>
    helloworld
</font>
    
</body>
```



> 字符实体

有时需要将一些标签显示在网页中，如在网页中显示`<hr/>`，而不让浏览器将其解析为横线。类似java中将转义字符输出。

此时使用字符实体的方法。该方法用`&lt;`来表示左包围、`&gt;`来表示右包围，中间包围起来的就是可以打印出的标签

```html
<body>
    helloworld
    &lt;hr/&gt;
    <hr/>
</body>
```



> 标题标签

标题标签，h标签，用来确定网页中内容各个标题的大小

```html
<!-- 标题标签的属性
h1 - h6 都是标题标签 h1 : 最大 h6 : 最小
align: 属性是对齐属性
left: 左对齐(默认)
center :居中
right : 右对齐
-->
<body>
    <h1>he</h1>
    <h2>ll</h2>
    <h3>ow</h3>
    <h4>or</h4>
    <h5>ld</h5>
    <h6>~</h6>
</body>
```





> 超链接标签

超链接是指从一个网页指向一个目标的链接关系，这个目标可以是另一个网页，也可以是相同网页上的不同位置，还可以是一个图片，一个电子邮件地址，一个文件，甚至是一个应用程序。

```html
<!--
老韩说明:
a 标签是 超链接
href 属性设置连接的地址
target 属性设置哪个目标进行跳转
	_self : 表示当前页面(默认值)
	_blank : 表示打开新页面来进行跳转
-->
<body>
<a href="http://www.sohu.com">搜狐</a><br/>
<a href="http://www.sohu.com" target="_blank">搜狐 2</a><br/> 
</body>
```



> 无序列表

无序列表：ul/li操作。其基本语法为

```html
<ul type="属性值">
    <li>列表内容</li>
</ul>
```

type有三种：disc:符号位实心圆点；cricle：空心圆；square：矩形



实例

```html
<body>
<!--
ul : 表示无序列表
li : 列表项
type 属性：指定列表项前的符号
-->
<h1>员工</h1>
<ul type="circle">
	<li>jack</li>
	<li>tom</li>
	<li>smith</li>
	<li>mary</li>
	<li>milan</li>
</ul>
</body>
```



> 有序列表

有序列表，ol/li操作，与无序列表对应，有序列表会将列表的内容进行自主编号。

基本语法

```html
<ol type="属性值" start=起始值>
    <li>
        列表内容
    </li>
</ol>
```

type属性分为`1、a、A、i、I`，其含义分别为阿拉伯数字、小写字母、大写字母、小写罗马数字、大写罗马数字。确定一个作为属性后，会以选择的属性当作前标进行排序

start属性，确定从第几个数开始排，如start=3，则第一个列表内容的序号就是3（或者c、C、Ⅲ、iii）



实例

```html
<body>
<h1>员工</h1>
	<ol type="I" start="3">
		<li>jack</li>
		<li>tom</li>
		<li>smith</li>
		<li>mary</li>
		<li>milan</li>
	</ol>
</body>
```



> 图像标签

图像标签，img标签，可以在页面上显示图片。

其语法如下

```html
<img src="path(图像的地址)" width="宽度"(此时高度会自动调整),high="高度" border="图像边框大小" alt="若无图片则使用这串文字代替图片" >
```

img是单标签，不需要结束标签，上面这行就直接显示图片了



这里说一下web中的路径信息，web中也分相对路径和绝对路径。

相对路径：` .` 表示当前文件所在的目录；`..` 表示当前文件所在的上一级目录
文件名 : 表示当前文件所在目录的文件,相当于 ./文件名 ./ 可以省略

绝对路径: 正确格式是:` http://IP地址:port/资源路径`。如http://localhost:14124/JavaCode/_01_JavaBase/_09_IO/Resources/test.png，该连接可以直接打开
错误格式是: 盘符:/目录/文件名(传统的相对路径在web中没法用)



> 表格标签

表格标签，table标签。

基本语法为

```html
<!-- 表格标签的各种属性：
table： 标签是表格标签 
border： 设置表格边框大小
width： 设置表格宽度 
height： 设置表格高度
align： 设置表格相对于页面的对齐方式
cellspacing： 设置单元格间距
tr ：是行
th ：是表头
td ：是单元格
align： 设置单元格文本对齐方式 
b ：是加粗标签
-->
<body>
<table width="500" border="1" >
    <tr>
        <td>第一行第一列</td>
        <td>第一行第二列</td>
        <td>第一行第三列</td>
    </tr>
    
    <tr>
        <td>第二行第一列</td>
        <td>第二行第二列</td>
        <td>第二行第三列</td>
    </tr>

</table>
</body>
```



表格标签有进阶的用法，如跨行跨列的使用

需要知道以下属性

```html
<!--
合并列 : colspan="列数"
合并行 : rowspan="行数"
cellspacing : 指定单元格间的空隙大小,0 表示没有空隙
bordercolor: 指定表格边框的演示
border: 表格边框
width： 表格的宽度
-->

```

```html
<body>  
<table border="1" height="250" bordercolor="#E87EFA"  cellspacing="0" width="500"> 
	<tr> 
  		<!--合并了 3 列-->
  		<td align="center" colspan="3">第 1 行第 1 列</td>
  	</tr>
  	<tr>
		<!-- 合并行，跨行 row 行-->
		<td rowspan="2">第 2 行第 1 列</td> 
		<td>第 2 行第 2 列</td>
		<td>第 2 行第 3 列</td>
	</tr>
	<tr>
		<td>第 3 行第 2 列</td>
		<td>第 3 行第 3 列</td>
	</tr>
	<tr>
		<!--合并行，跨行 row 行-->
		<td rowspan="2">第 4 行第 1 列</td>
		<td>第 4 行第 2 列</td>
		<td>第 4 行第 3 列</td>
	</tr>
	<tr>
		<td> 第 5 行 第 2 列 <img src="imgs/2.png" width="100"></td>
		<td>第 5 行第 3 列</td>
	</tr> 
</table> 
</body> 

```



> 表单标签

表单标签，form。

其语法为

```html
<form acation="url" method="">
```

 url 表示定位一个 web 资源的路径, method 主要有两种 get ,post 。它还有input的相关方法，主要是定义表单的界面



拿一个简单的登录界面例子来看，假设现在界面是一个需要输入账号密码的登录界面，则

```html
<!--
1. form 表示表单
2. action: 提交到哪个页面，即输入账号密码后，跳转到action定位的url上
3. method： 提交方式 ,常用 get 和 post 
4. input type=text 输入框
5. input type=password 密码框
6. input type=submit 提交按钮
7. input type=reset 重置按钮
-->
<body>
    
<h1>登录系统</h1>
<form action="_08_table.html" method="get">
	用户名:<input type="text" name="username"><br/>
	密 码:<input type="password" name="username"><br/>
    <input type="submit" value=" 登 录 "> <input type="reset" value="重新填写">
</form>
    
</body>
```

实际上这个表单标签就好比java中的Swing包，都是定义界面用的，不过标签表单的用法稍微有点局限，多用于跳转部分。

有一点要注意，一定要给input设置name属性，否则提交不到服务器



下面对input标签进行一下举例说明。

```html
<!-- 
form 标签就是表单 
input type=text : 是文件输入框 value 设置默认显示内容 
input type=password 是密码输入框 value 设置默认显示内容 
input type=radio 是单选框 name 属性可以对其进行分组 
checked="checked"表示默认选中 input
 type=checkbox 是复选框 checked="checked"表示默认选中
 input type=reset 是重置按钮 value 属性修改按钮上的文本
 input type=submit 是提交按钮 value 属性修改按钮上的文本
 input type=button 是按钮 value 属性修改按钮上的文本
 input type=file 是文件上传域
 input type=hidden 是隐藏域
 当我们要发送某些信息，而这些信息，不需要用户参与，就可以使用隐藏域（提
 交的
 时候同时发送给服务器）
 select 标签是下拉列表框
 option 标签是下拉列表框中的选项
 selected="selected"设置默认选中
textarea 表示多行文本输入框 （起始标签和结束标签中的内容是默认值）
rows 属性设置可以显示几行的高度
cols 属性设置每行可以显示几个字符宽度
-->
```



实例使用如下

```html
<body>

<!--提交后跳转到08table中-->
<form action="_08_table.html">
    用户注册信息<br/>
    <!--text属性是文本属性，输入可见的字符-->
    用户名称: <input type="text" name="username"><br/>

    <!--password属性是隐藏的文本属性，输入的是不可见的字符-->
    用户密码: <input type="password" name="pwd"><br/>
    确认密码: <input type="password" name="pwd1"><br/>

    选择运动项目:<br/>
    <!--checkbox属性是复选属性，同一组复选要保证checkbox的name是一致的。
    checkbox里面有一个属性是value，该属性为真正提交到浏览器去解析的属性-->
    <input type="checkbox" name="sport" value="basketball">篮球<br/>
    <input type="checkbox" name="sport" value="football">足球<br/>

    选择性别:<br/>
    <!--radio属性是单选属性，给出多个选项但只能同时选中其中一个。同一组单选要保证其name一致-->
    <input type="radio" name="gender" value="man">男<br/>
    <input type="radio" name="gender" value="woman">女<br/>

    选择城市:<br/>
    <!--选择框用select来加载-->
    <select name="city">
        <!--这里”选择“没有value属性，故到时候生成页面后，哪怕选择的是”选择“，也不会生效-->
        <option>--选择--</option>
        <option value="bj">北京</option>
        <option value="tj">天津</option>
    </select><br/>

    自我介绍:<br/>
    <!--文本输入框用textarea属性来定义-->
    <textarea rows="6" cols="20"></textarea>

    附件:<br/>
    <!--上传文件用input中的file类型-->
    <input type="file" name="file" value="upFile"><br/>

    <!--提交和重置的定义分别用input中的submit类型和reset类型-->
    <input type="submit" value="提交">     <input type="reset" value="重置">

</form>

</body>
<!--表单注意事项
1. action 表示将 form 表单的数据提交给哪个 url,即服务器的哪个资源(servlet)   
2. method 表示提交的方式 主要是 get / post, 默认是 get
3. 如果 form 表单的元素，没有写 name 属性，则数据不会提交  
4. 对应 select checkbox radio 标签，提交的数据是 value 指定的值 
5. 对应 checkbox 复选框，可以提交多个字，但是 name 是统一的，都是 sport  sprot=xx&sport=yy 
6. 提交的数据，一定要放在 form 标签内，否则数据不会提交 
-->
```

这种方式写出来的页面看起来会有点乱，可以将该表单放进一个没有边框的表格中。



下面介绍一个action和method的含义

action表示将表单提交后，提交到哪个url地址，即服务器在表单提交后打开哪个界面

method属性里分为get和post两种，其中get是不安全的，因为get会将用户的账号密码都显示在网页的url地址里。而post方法则在url地址栏中只显示action属性，相对get会安全。



#### 3 特殊标签

##### 3.1 div标签

div标签可以将文档分割为独立的、不同的部分；div是一个块级元素、它的内容自动地在一个新行显示而不需要使用`<br/>`来换行。

```html
<body>

helloworld
<div>
    <h1>这里是h1级别的标题</h1>
    <a href="http://www.baidu.com">跳转百度</a>
</div>

</body>
```



##### 3.2 p标签

p标签会自动在其前后创建一些空白，表示文本的自然段。即每个p标签之间会有一些空行来表示这是俩不同的自然段（p标签不是指的在文本开头空两个字的空）

```html
<body>
helloworld
<p></p>aaaaaaaaaaaaaaaaaaaaaa</p>

<p>bbbbbbbbbbbbbbbbbbbbbbb</p>

</body>
```



##### 3.3 span标签

span标签是内联元素，其没有换行效果。span是专门用来强调某个信息的，使用span标签时，一定要规定span标签的属性（颜色、字体等等），否则span标签不起作用。

```html
<body>
helloworld有
<span style="color:blue">
    10
</span>
个字母

</body>
```

如这里强调10





### 2 CSS

CSS，Cascading Style Sheet，层叠样式表。

在之前的html里，想要修改某个元素的样式需要在每个元素定义时就将其属性定义上，会相对费力。css可以解决这个问题，css可以让页面的内容和样式进行分离，更方便的控制界面。



#### 2.1 基本语法

css的基本语法分为两部分：选择器和声明；其中选择器就是html里所讲的标签(但是标签选择器只是选择器的一部分)；声名由属性和值组成，多个声明之间由分号分隔。

```css
<sytle type="text/css">
选择器{
    声明1；
    声名2；
    声名3；
    ...
}
<style>

具体例子如
<head>
	<style type="text/css">
    	h1{
            color:red;
        }
    </style>
</head>

<body>
<h1>
    	helloworld
</h1>

</body>
```

 css是写在head标签内的，其用` <style type="text/css">XXX</style>  `来将css语句包起来。

从上面可以看出css的作用，它是将body里要使用的各种标签的格式直接在head里定义好了，然后body就可以直接写内容而不需要自己搞样式了





有一点要注意以下，css的注释写法和html注释写法不一样`/*XXX*/`



#### 2.2 常用样式

##### 2.2.1 字体样式

字体样式一般有：颜色、大小、边框、背景颜色、字体类型等组成

下面将这些属性定义在一个css中

颜色使用color定义，可以写颜色名比如 `green`，也可以写 rgb 值 比如` rgb(200,200,200)`和十六进制表示值 比如 `#708090`。

字体大小使用`font-size`来定义，单位为px；

边框由`border`来定义，border后面可以指定边框的厚度、边框样式和边框的颜色，前面也可也用wight、hight来定义边框的长和宽

背景颜色由`background-color`来定义，后面跟想要的颜色

字体类型由font-family来定义。

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        div{
            color:red;
            font-size: 20px;
            width: 200px;
            height: 200px;
            border: 2px solid red;
            background-color: blue;
            font-weight: bold;
            font-family: 新宋体;
        }
    </style>
</head>
<body>
<div>
    helloworld
</div>

</body>
</html>
```



有时我们也需要将某部分进行居中显示，此时用`margin-lift`和`margin-right`来调整某个模块的左右间距。若想居中，则让这两个值等于auto就行。

而让某部分里的文本进行居中，则使用`text-align:center`。来使文本相对于边框居中（若是没有定义边框，则让文本相对于页面居中）

```css
    <style type="text/css">
        div{
            color:red;
            font-size: 20px;
            width: 200px;
            height: 200px;
            border: 2px solid red;
            background-color: blue;
            font-weight: bold;
            font-family: 新宋体;
            margin:auto;/*这里直接让margin：auto就代表左右都是auto*/
            text-align:center;
                
        }
    </style>
```



##### 2.2.2 超链接相关

超链接主要是将超链接下划线去掉

使用`text-decoration:none`来去掉

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        a{
            color:red;
            font-size: 20px;
            width: 200px;
            height: 200px;
            text-decoration: none;
        }
    </style>
</head>
<body>
<a href="http://www.baidu.com">
    百度
</a>

</body>
</html>
```

但是这里为什么无法让超链接居中呢？（把那些居中的属性写上也没用）



##### 2.2.3 列表相关

众所周知，列表会将里面的信息按行排列，然后在没行前面加一个标记，有时需要去掉这个标记

```css
<style type="text/css">
	ul {
		/*说明:list-style:none 表示去掉默认的修饰*/ 
		list-style: none;
	}
</style>
```



#### 2.3 css使用方式

之前所使用的css，是一种使用方式，另一种是单独写一个`.css`文件，然后在html文件里使用link标签将该css文件的路径引入就行。

```css
div{
    width:400px;
    height:100px;
    background-color: red;
}

span{
    border: 2px dashed blue;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <link rel="stylesheet" type="text/css" href="./csstable.css">
</head>
<body>
<div>
    helloworld
</div>
<span>
    dlrowolleh
</span>
</body>
</html>
```

rel：关联的意思

href：表示要引入的css文件的位置，可以是相对路径也可是绝对路径

type可以写也可也不写

一般用这种引包的方式用的多，但是学习中就用最初学的那种比较方便



#### 2.4 选择器

##### 2.4.1 元素选择器

最常见的选择器就是元素选择器，之前学的那些常用样式都是用的元素选择器，主要是关联html中的某个标签，定义该标签的样式。



##### 2.4.2 id选择器

id选择器可以为标有特定id的html元素指定特定的样式

id选择器以`#`来定义。

id选择器常用在多个标签想个性化的时候用，如刚刚使用元素选择器将div标签的格式定义了，但是我突然有一个div标签的样式不想用统一定义的样式了，就可以用id选择器来单独定义该div的样式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            color: red;
        }
        #css1{/*做一个id选择器，定义该选择器下的属性*/
            color: blue;
        }
    </style>
</head>
<body>
<div>
    helloworld
</div>

<div id="css1"><!--在这里指定想用的样式的id-->
    helloworld
</div>

</body>
</html>
```

  要注意，id选择器在使用时，只能被一个标签使用，如head里定义了一个css1，则body里只能由一个标签用这个css1，不能多个标签同时用该选择器

##### 2.4.3 类选择器

类选择器是通过class属性去选择某个样式，其使用方法类似id选择器，id用`#`修饰，类用`.`修饰

刚刚的id选择器是在元素选择器下找一个标新立异的，class则可以理解为在元素选择器的定义下，找多个标新立异的（但是这几个是同一个类型）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .css1{
            color: red;
        }
        div{
            color: blue;
        }
    </style>
</head>

<body>
<div>
    helloworld
</div>

<div class="css1">
    helloworld
</div>

<div class="css1">
    hello
</div>

</body>
</html>
```



##### 2.4.4 组合选择器

组合选择器就是让多个选择器共用同一种样式。

```css
.class01,#id02,div{
    color:red;
}

```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .css01,#id01,div{
            color: blue;
        }
    </style>
</head>
<body>
<div>
    hello
</div>

<div class="css01">
    world
</div>

<div id="id01">
    id
</div>

</body>
</html>
```



##### 2.4.5 选择器的优先级

在有多个选择器时，选择器的优先级如下：行内样式 > ID 选择器 > class 选择器 > 元素选择器

也就是说，在body内定义的时候规定样式的优先级是最高的，然后是单体定义样式、再然后是批量定义样式、最后是整体定义样式。

可以看出，优先级是随着定位越精确而越高的。





### 3 javaScript

JavaScript 能改变HTML内容，能改变HTML属性，能改变HTML样式 (CSS)，能完成页面的数据验证。

#### 3.1 特点

1、JavaScript是写在head中的，其语句部分用`<script type="text/javascript">XXX</script>`包围。（也可通过导包进去，和css如出一辙）。不过js语言有时候会出现在body里面，但是一般都在head里。

2、JavaScript是一种解释型的脚本语言，C、C++等语言先编译后执行，而JavaScript是在程序的运行过程中逐行进行解释。

3、JavaScript 是一种基于对象的脚本语言，可以创建对象，也能使用现有的对象(有对象)。

4、JavaScript 是弱类型的，对变量的数据类型不做严格的要求，变量的数据类型在运行过程可以变化。

```javascript
<script type="text/javascript">
    var name = "hello";
	name = 100;
</script>
```

此处就体现出了变量的弱类型，name变量最初是string类型，后面也可也直接变成number类型（js里的数据类型）



#### 3.2 变量

js中，变量的相关属性相当松散，定义时可以像python一样不声明就直接创建，也可也象征性的写一个var来当前缀

```javascript
a = "name";
a = 10;
var a = true;
```



> 变量类型

js中变量的类型有以下几种：

数值类型： number
字符串类型： string
对象类型: object
布尔类型： boolean
函数类型： function

注：String字符串可以用单引号引起来也可用双引号引起来



js中还有三个特殊的变量值：

undefined ：变量未赋初始值时，默认 undefined
null ：空值
NaN ：Not a Number 非数值

```javascript
var a;//此时若调用a则a的值就是undefined
var b = null;//直接给变量b赋值null
var c = abc;//由于不知道abc是啥，故c此时是NaN
```



#### 3.3 运算符



js中的运算符（加减乘除、赋值、等于、大于等于、与或非、）都和java一模一样，唯一有不同的就是，js中有一个符号是全等`===`表示三等号左右两边的值和数据类型都相等。

```javascript
a = 5;
b = "5";
a == b;//true，因为a和b的值都是5
a === b;//false，因为a的类型是number、b的类型是string
```



> 细节

1、js中，所有变量都可以作为一个boolean类型的变量去使用，其中0、null、undefined、“”（空字符串）、NaN都是false，其他为true

2、js中，与或的运算默认就是短路与和短路或



#### 3.4 数组

js中数组定义有4种方式。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //定义数组时就直接将数据定义进去
        var cars1 = ["a", "b"]
        console.log(cars1)
        console.log(cars1[0])
        console.log(typeof cars1)//数组类型的数据跟java中性质一样，都是引用数据类型，是对象形式的

        //先定义空数组，再往里装东西
        var cars2 = [];
        cars2[0] = 10;
        cars2[1] = "10";
        cars2[2] = true;
        console.log(cars2)
        console.log(typeof cars2)

        //通过数组的构造器创建数组，并将数据定义进构造器中
        var cars3 = new Array("10", 10 ,true);
        console.log(cars3)
        console.log(typeof cars3)

        //创建空对象，再往对象里面加数据
        var cars4 = new Array();
        cars4[0] = 1;
        cars4[2] = "1";
        cars4[4] = 19;//若是隔一个直接赋值的话，cars[3]会是undefine
        console.log(cars4)

    </script>

</head>
<body>

hello
</body>
</html>

```

js中的数组，扩容非常简单，直接在想要的索引下添加数值就行，然后数组自动扩容到目标索引下，若该索引前面的索引没有赋值，则这些都是没赋值的索引都是undefined。



> 数组遍历

js中的数组遍历类似java，都是用for循环开始遍历

```javascript
for (i = 0; i < cars4.length; i++) {
    console.log(cars4[i]);
}
```



#### 3.5 函数

函数的创建方式很简单，直接function加函数名就行。

js中的函数要调用才能实现，调用方式有两种：直接通过函数名调用、通过事件调用。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        function hi(){
            alert("hi~")//alert用来做出弹窗，然后这个弹窗写的是hi~
        }

        hi();//调用函数
    </script>
</head>
<body>
//通过事件触发函数
<button onclick="hi()">
    点击触发事件
</button>

</body>
</html>
```



> 高级部分

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //1、定义没有返回值的函数
        function function1(){
            alert("function1");
        }

        //2、定义有形参的函数
        //这里形参不指定数据类型，类似python，传啥就是啥类型（比python还宽松）
        function function2(need){
            alert(need)
        }

        //3、定义一个有返回类型的有参函数
        //此时返回值的类型是根据最后计算结果来看的
        function function3(n1,n2){
            return n1+n2;
        }

        function1();
        function2("string");
        a = function3(10+true);
        alert(typeof a);


    </script>
</head>
<body>


</body>
</html>
```



函数还有一种创建方式

```javascript
var 函数名 = function(形参列表){函数体}
```

此时就可以通过函数名来调用函数了（相当于把之前写在function后的函数名提到前面）

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript">
        var f1 = function (n1, n2){
            alert(n1 + n2);
            return n1 + n2;

        }

        a = f1(1,"1")
        alert(typeof a)

    </script>
</head>
<body>

</body>
</html>
```



> 细节

1、JS 中函数的重载会覆盖掉上一次的定义

2、函数的 arguments 隐形参数（作用域在 function 函数内）

​		(1) 隐形参数: 在 function 函数中不需要定义，可以直接用来获取所有参数的变量

​		(2) 隐形参数特别像 java 的可变参数一样。 public void fun( int ... args ）

​		(3) js 中的隐形参数跟 java 的可变参数一样。操作类似数组

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //1、js中函数的重载会覆盖掉上一次的定义，只有后定义的函数气作用
        function f1(){
            alert("hi!")
        }
        function f1(n1){
            alert("nohi")
        }
        f1();//此时调用f1，输出的会是nohi。虽然此处形参列表内没传参数，按java的理论是调用无参的f1方法，但是js中由于已经有了两个f1方法，故只能用第二个f1方法


        //2、js中的每个函数的形参列表中，都有一个arguments的隐藏参数，即便方法定义是形参列表为空，但是调用该方法时也可以传入参数。
        //argument是一个数组，里面存放任意数值
        function f2(){
            for (i = 0; i < arguments.length; i++) {
                alert(arguments[i])
            }
        }
        f2(1,"10",true);//此处虽然f2定义时没有形参列表，但是由于其内部包含argument数组，故还是可以传入参数传进去。

        //3、若传入的实参比函数要求的实参多，则会先把函数要求的实参传入相应的位置，其他的实参则存在arugment中。
        //反之，若形参个数大于实参个数，则最后没被传值的形参会是undifend
        function f3(n1){
            alert(n1)
        }
        f3(1,2,3,4)
    </script>
</head>
<body>

</body>
</html>
```



#### 3.6 对象

js中没有类的概念，对象直接定义

```
定义方法1
var 对象名 = new object();//创建一个空对象
对象名.属性 = 值;//初始化对象的属性
对象名.函数 = function(){}//初始化对象的函数
```

```javascript
定义方法2
var 对象名 ={
    属性1名:值,
    属性2名:值,
    函数1名:function(){},
    函数2名:function(){}
};
```



成员调用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var object1 = new Object();//创建空对象
        object1.name = "小明";//初始化一个对象的属性
        object1.run = function (){//初始化一个对象的方法
            console.log("run");
        }

        console.log(object1.name);//调用object1的属性
        object1.run();//调用object1的方法

        var object2 = {
            name:"小李",
            say:function (){
                console.log("say~")
            }
        }
        console.log(object2.name);
        object2.say();

    </script>
</head>
<body>

</body>
</html>
```

若调用了一个对象没有定义的属性，则该属性的值为undefined



#### 3.7 事件

事件也就是页面的具体某些操作了

事件在使用前，要先进行注册，即当事件响应（触发）与某个函数绑定在一块。

事件的注册有两种方式静态注册和动态注册。

静态注册：通过 html 标签的事件属性直接赋于事件响应后的代码。

```html
<buttun onclinck=""></buttun>;//这里onclinck就是buttun提供的一种静态注册方法，直接将某个函数放在onclinck里面，就代表了按下buttun按钮后会执行这个函数。
```

动态注册：通过 js 代码得到标签的 dom 对象，然后再通过 dom 对象.事件名 = function(){} 。也就是说，dom对象里定义了很多已经有了的事件，然后对dom里的某个事件绑定上某个函数。比如dom对象定义了一个页面加载完毕的事件，然后可以将该事件绑定一个函数进行页面加载完毕后弹窗

其过程为：1、获取标签对应的dom 对象；2、dom 对象.事件名 = fucntion(){}**（这里能直接调用已经定义好的方法，调用了只加载那个方法一次，然后就绑定不上了，为什么？）**

```javascript
window.onload = function(){alert("over~")};
//这里，window是一个js中内置的dom对象可以直接用，onload是dom对象定义的一个事件（当页面加载完毕后触发该事件），然后后面的function是与该事件绑定的一个函数，也就是说，当页面加载完毕后，弹一个窗，该弹窗上写着over~
```

后面在实用动态注册时，一般都需要等界面加载完毕才开始绑定，故都会用到window.onload事件



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    
    <style type="text/css">
        button{
            color: red;
        }
        #cs1{
            color:blue;
        }
    </style>

    <script type="text/javascript">
        function sayok1(){
            alert("ok");
        }
        function sayhi(){
            alert("hi~")
        }

        window.onload = function (){
            var elementById = document.getElementById("cs1");
            elementById.onclick = sayhi()//sayhi不行，只调用一次sayhi后就不与button1绑定了
            elementById.onclick = function (){//得用这个
                alert("hi~");
            }
        }
    </script>

</head>

<body>
<button onclick="sayok1()">button</button>
<button id="cs1">button1</button><!--这里cs1是该button的标签，与css中的cs1通用，即该button既实用了css中的id，又在js中作为标识创建dom用

</body>


</html>
```



> 表单提交事件

当一个按钮被点击后，提交表单（提交该界面）。如注册账号，若用户名、密码等部分符合规范，则提交成功、否则提交失败。

```html
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/html">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //静态注册
        function register(){
            var username = document.getElementById("username");
            var pwd = document.getElementById("password");
            //判断是否有空
            if("" == username.value || "" == pwd.value){
                alert("不能有空")
                return false;//若有空，则返回false
            }
            return true;
        }

        //动态注册
        window.onload = function (){
            var fm = document.getElementById("form2");
            fm.onsubmit = function (){
                if(fm.username2.value == "" || fm.password2.value == ""){
                    alert("不可空");
                    return false;
                }
                return true;
            }
        }
    </script>
</head>


<body>
<h1>注册账号(静态绑定)</h1>
<form action="_01_onclick.html" onsubmit="return register()"><!--实用静态注册绑定函数，这里要注意，这里也要return一次，否则即使函数返回false也会提交成功-->
    用户名:<input type="text" id="username" name="username"></br>
      密码:<input type="password" id="password" name="pwd"></br>
    <input type="submit" value="注册">
</form>
<h1>注册账号(动态绑定)</h1>
<form action="_01_onclick.html" id="form2"><!--实用动态注册绑定函数，这里不需要return了，因为刚刚是直接return到onsubmit的-->
    用户名:<input type="text" id="username2" name="username"></br>
    密码:<input type="password" id="password2" name="pwd"></br>
    <input type="submit" value="注册">
</form>

</body>
</html>
```



#### 3.8 Dom

Dom全称是Document Object Model，文档对象模型，就是将文档（如html文件、css文件都可视为文档）中的标签、属性、文本等内容转换成对象来管理。



> 基本使用

 document 它管理了所有的 HTML 文档内容；document 它是一种树结构的文档；有层级关系 在 dom 中把所有的标签 都 对象化 （得到这个 html 标签的<--->对象--> 操作）；通过 document 可以访问所有的标签对象

Document对象的操作思路大概如下：通过标签的id获取该标签的document对象，再通过该document对象来定义各自操作（如点击等）对应的表现（由函数控制），其实例如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //动态注册
        window.onload = function (){
                var h1 = document.getElementById("myH1");
                h1.onclick = function (){
                    alert(h1.innerText)
                }
        }

        function getValue(){
            var h2 = document.getElementById("myH2");
            alert(h2.innerText)
        }
    </script>

</head>
<body>
<h1 id="myH1" ><div>test1</div></h1>
<p>Click on the header to alert its value</p>

<h1 id="myH2" onclick="getValue()"><div>test2</div></h1>
<p>Click on the header to alert its value</p>
</body>
</html>
```

上面的标签情况比较简单，就是一个简单的标题标签，只需要将其id与document对象进行绑定。

若是遇到情况比较多的标签，如选择标签等等，就要将其name与document绑定了，如下

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script type="text/javascript">

        //静态
        function selectAll(){
            var sports = document.getElementsByName("sport");//此时sport对象是一个集合类型的对象
            //alert(sports);//类型是Object Nodelist，由于是集合，故可以通过遍历来获取所有的sport内容，并操作这些内容
            for (var i = 0; i < sports.length; i++) {
                sports[i].checked = true;
            }
        }


        function selectNone(){
            var sports = document.getElementsByName("sport");
            for (var i = 0; i < sports.length; i++) {
                sports[i].checked = false;
            }
        }



        //动态
        window.onload = function (){
            var button1 = document.getElementById("button1");//通过按钮的id先绑定上按钮的点击操作
            button1.onclick = function (){
                var sport1 = document.getElementsByName("sport");//在按钮的点击操作里绑定上各个sport的操作，此时用name绑定
                for (var i = 0; i < sport1.length; i++) {
                    sport1[i].checked = true;
                }
            }

            var button2 = document.getElementById("button2");
            button2.onclick = function (){
                var sport2 = document.getElementsByName("sport");
                for (var i = 0; i < sport2.length; i++) {
                    sport2[i].checked = false;
                }
            }
        }

    </script>
</head>
<body>
你会的运动项目：
<input type="checkbox" name="sport" value="zq" checked="checked">足球
<input type="checkbox" name="sport" value="tq">台球
<input type="checkbox" name="sport" value="ppq">乒乓球 <br/><br/>
<button onclick="selectAll()">全选</button>
<button onclick="selectNone()">全不选</button><br/>


<button id = "button1">全选</button>
<button id = "button2">全不选</button>

</body>
</html>
```



> 细节使用

在 HTML DOM （文档对象模型）中，每个部分都是节点：文档本身是文档节点；所有 HTML 元素是元素节点；所有 HTML 属性是属性节点；HTML 元素内的文本是文本节点；注释是注释节点。

DOM常用的方法有： childNodes 属性，获取当前节点的所有子节点；firstChild 属性，获取当前节点的第一个子节点；lastChild 属性，获取当前节点的最后一个子节点；parentNode 属性，获取当前节点的父节点；nextSibling 属性，获取当前节点的下一个节点 (后一个)；previousSibling 属性，获取当前节点的上一个节点 (前一个)；className 用于获取或设置标签的 class 属性值；innerHTML 属性，表示获取/设置起始标签和结束标签中的内容；innerText 属性，表示获取/设置起始标签和结束标签中的文本

其大概用例如下

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" type="text/css" href="css.css">

    <script type="text/javascript">
        window.onload = function (){
            var btn01 = document.getElementById("btn01");
            btn01.onclick = function (){
                var Java = document.getElementById("java");
                alert(Java.innerText);
            }

            var btn02 = document.getElementById("btn02");
            btn02.onclick = function (){
                var option = document.getElementsByTagName("option");
                for (var i = 0; i < option.length; i++) {
                    alert(option[i].innerText);
                }
            }

            var btn03 = document.getElementById("btn03");
            btn03.onclick = function (){
                var sports = document.getElementsByName("sport");
                for (var i = 0; i < sports.length; i++) {
                    if(sports[i].checked){
                        alert(sports[i].value);
                    }

                }
            }

            var btn04 = document.getElementById("btn04");
            btn04.onclick = function (){
                var li = document.getElementById("language").getElementsByTagName("li");
                for (let i = 0; i < li.length; i++) {
                    alert(li[i].innerText);
                }
            }

            var btn05 = document.getElementById("btn05");
            btn05.onclick = function (){
                // var sel = document.getElementById("sel01");
                // for (var i = 0; i < sel.length; i++) {
                //     alert(sel[i].innerText)
                // }
                var opt = document.getElementById("sel01").getElementsByTagName("option");
                for (var i = 0; i < opt.length; i++) {
                    alert(opt[i].innerText)
                }

            }

            var btn06 = document.getElementById("btn06");
            btn06.onclick = function (){
                var sel01 = document.getElementById("sel01");
                alert(sel01.firstChild);//将换行符也视为其中一个节点，此时会得到换行符
                alert(sel01[0].value);//此时得到的是有内容的节点
            }

            var btn07 = document.getElementById("btn07");
            btn07.onclick = function (){
                var c = document.getElementById("C++");
                var cpc = c.parentNode.childNodes;
                for (var i = 0; i < cpc.length; i++) {
                    alert(cpc[i].innerText)
                }
            }




        }

    </script>

</head>
<body>
<div id="total">
    <div class="inner">
        <P>
            你会的运动项目：
        </P>
        <input type="checkbox" name="sport" value="zq">足球
        <input type="checkbox" name="sport" value="tq">台球
        <input type="checkbox" name="sport" value="ppq">乒乓球 <br/>
        <hr/>
        <P>
            你认识谁：
        </P>
        <select id="sel01">
            <option>---option---</option>
            <option>艳红</option>
            <option id="ct" value="春桃菇凉">春桃</option>
            <option>春花</option>
            <option>桃红</option>
        </select>
        <hr/>
        <p>
            你的编程语言?
        </p>
        <ul id="language">
            <li id="java">Java</li>
            <li>PHP</li>
            <li id="C++">C++</li>
            <li>Python</li>
        </ul>
        <br>
        <br>
        <hr/>
        <p>
            个人介绍:
        </p>
        <textarea name="person" id="person">个人介绍</textarea>
    </div>
</div>
<div id="btnList">
    <div>
        <button id="btn01">查找 id=java 节点</button>
    </div>
    <div>
        <button id="btn02">查找所有 option 节点</button>
    </div>
    <div>
        <button id="btn03">查找 name=sport 的节点</button>
    </div>
    <div>
        <button id="btn04">查找 id=language 下所有 li 节点</button>
    </div>
    <div>
        <button id="btn05">返回 id=sel01 的所有子节点</button>
    </div>
    <div>
        <button id="btn06">返回 id=sel01 的第一个子节点</button>
    </div>
    <div>
        <button id="btn07">返回 id=java 的父节点</button>
    </div>

</div>

</body>
</html>
```





### 4 xml

 xml 可以做配置文件
xml 文件做配置文件可以说非常的普遍，比如我们的 tomcat 服务器的 server.xml ，web.xml
xml 可以充当小型的数据库 => 程序自己的数据格式存放
xml 文件做小型数据库，也是不错的选择，我们程序中可能用到的数据，如果放在数据库中读取不合适(因为你要增加维护数据库工作)，可以考虑直接用 xm 来做小型数据库 ，而且直接读取文件显然要比读取数据库快



#### 4.1 语法

> 标签（元素）

每个XML文档必须有且只有一个根元素。  

根元素是一个完全包括文档中其他所有元素的元素。  

根元素的起始标记要放在所有其他元素的起始标记之前。 

根元素的结束标记要放在所有其他元素的结束标记之后。  



区分大小写，例如，<P>和<p>是两个不同的标记。

不能以数字开头。

不能包含空格。

名称中间不能包含冒号（:）。

如果标签单词需要间隔，建议使用下划线 比如 <book_title>hello</book_title>

```xml
<students>
    
	<student id="100">
		<name>jack</name> 
		<age>10</age>
		<gender>男</gender> 
	</student>
    
	<student id="200">
		<name>mary</name> 
		<age>18</age>
		<gender>女</gender> 
	</student>
    
	<school>清华大学</school> 
    
	<city/>
    
</students>
```

xml中，标签是可以随意自定义的，只要符合定义的规范就行。



> 属性

1.属性值用双引号（"）或单引号（'）分隔（如果属性值中有'，用"分隔；有"，
用'分隔）

2.一个元素可以有多个属性，它的基本格式为：<元素名 属性名="属性值">

3.特定的属性名称在同一个元素标记中只能出现一次

4.属性值不能包括& 字符

```xml
<students id="01">

</students>
```

这里id就是属性



> CDATA节

有些内容不想让解析引擎执行，而是当作原始内容处理(即当做普通文本)，可以使用 CDATA 包括起来，CDATA 节中的所有字符都会被当作简单文本，而不是 XML 标记。

其语法为

```xml
<![CDATA[XXX]]>
```

其内部可以输入任意字符（除`]]>`外）



#### 4.2 dom4j

不管是 html 文件还是 xml 文件它们都是标记型文档，都可以使用 w3c 组织制定的dom 技术来解析。

 document 对象表示的是整个文档（可以是 html 文档，也可以是 xml 文档）



Dom4j 是一个简单、灵活的开放源代码的库(用于解析/处理 XML 文件)。Dom4j 是由早期开发 JDOM 的人分离出来而后独立开发的。

与 JDOM 不同的是，dom4j 使用接口和抽象基类，虽然 Dom4j 的 API 相对要复杂一些，但它提供了比 JDOM 更好的灵活性。

Dom4j 是个非常优秀的 Java XML API，具有性能优异、功能强大和极易使用的特点。现在很多软件采用的 Dom4j。

使用 Dom4j 开发，需下载 dom4j 相应的 jar 文件（相当于导入第三方的库）



##### 4.2.1 获取document对象

有三种方法：

1、读取 XML 文件,获得 document 对象

```java
SAXReader reader = new SAXReader(); //创建一个解析器
Document document = reader.read(new File("src/input.xml"));//XML Document
```



2、解析xml文本，得到document对象

```java
String text = "<members></members>";
Document document = DocumentHelper.parseText(text);
```



3、主动创建document对象

```java
Document document = DocumentHelper.createDocument(); //创建根节点
Element root = document.addElement("members");
```

主要用的是第一种方法

##### 4.2.2 应用实例

以增删改查为例看dom4j的实用

首先有一个xml的配置文件如下

```xml
<students>
    <student id="01">
        <name>jack</name>
        <age>18</age>
    </student>

    <student id="02">
        <name>mack</name>
        <age>20</age>
    </student>
</students>
```

然后是将该文件视为dom文件来进行操作

```java
public class Dom4j_ {
     public void loadXML() throws DocumentException {
         //得到一个解析器
         SAXReader reader = new SAXReader();
         Document document = reader.read(new File("src/students.xml")); //将刚刚的xml文件进行解析
         
         //1、实现查找
         //1.1. 得到 rootElement，gen元素是students
    	 Element rootElement = document.getRootElement();
         
         //1.2、得到根元素的子元素，该子元素是student
         List<Element> students = rootElement.elements("student");
         
         //1.3、遍历子元素得到该子元素的所有子元素，完成查找操作
         for (Element student : students) {//element 就是 Student 元素/节点  
       	 	//获取 Student 元素 的 name Element
         	Element name = student.element("name");
            Element age = student.element("age");
         }
         
         //2、实现增
         //2.1 添加一个新子元素
         Element newStu = DocumentHelper.createElement("student");
         
         //2.2创建子元素的子元素
         Element newStu_name = DocumentHelper.createElement("name");
         Element newStu_age = DocumentHelper.createElement("age"); 
         newStu_name.setText("宋江");
         newStu_age.setText("23");
         
         //2.3 将子元素的子元素添加进子元素种
         newStu.add(newStu_name);   
		 newStu.add(newStu_age);
         //2.4 再将子元素添加到根元素种
         document.getRootElement().add(newStu);
    
         
         //3、实现删除
         //让父节点删除子节点
         Element stu = (Element)document.getRootElement().elements("student").get(2);
         stu.getParent().remove(stu);
         
         //4、修改
         List<Element> students = document.getRootElement().elements("student");  
		//遍历, 所有的学生元素的 age+3 
		for (Element student : students) { 
			//取出年龄 
			Element age = student.element("age"); 
			age.setText((Integer.parseInt(age.getText()) + 3) + ""); 
		} 
         
         //将上述操作写回xml文件中
         XMLWriter writer = new XMLWriter(new FileOutputStream(new File("src/students.xml")), output); 
   		 writer.write(document);
   		 writer.close();
         
 			 
     }
}
```



## 二、 Web服务

本节主要讲解当从浏览器输入一个url的访问请求时，该url对应的服务器是如何处理该请求的。也就是说浏览器访问主机时，主机的服务器是如何搭载工作的。

先理清一下思路。浏览器向主机发送请求，主机通过服务器处理该请求，然后返回一个响应给浏览器，浏览器接受该响应展示响应对应的界面。

此处核心在于主机处理请求和返回响应的部分，此部分就是主机的服务器。



能满足上述条件的服务器有很多，此处学tomcat。



### 1 tomcat

#### 1.1 介绍

WEB，在英语中 web 表示网/网络资源(页面,图片,css,js)意思，它用于表示 WEB 服务器(主机)供浏览器访问的资源。

WEB 服务器(主机)上供外界访问的 Web 资源分为：1、静态 web 资源（如 html 页面），指 web 页面中供人们浏览的数据始终是不变；2、动态 web 资源，比如 Servlet(java)、PHP 等。

静态 web 资源开发技术Html、CSS、js 等；动态 web 资源开发技术Servlet、SpringBoot、SpringMVC、PHP、ASP.NET 等。



#### 1.2 BS/CS开发的概念

B： browser(浏览器, 种类太多  chrome, ie, edge等等)

C: Client(客户端)

S：Server(服务端, 考虑很多)





 兼容性，因为浏览器的种类很多，发现你写的程序，在某个浏览器会出现问题，其它浏览器正常

 安全性，通常情况下，BS 安全性不如 CS 好控制，因为bs里b（浏览器）部分是别人写的，自己只能被动用。而cs里c（客户端）也是自己写的，故更好调整

易用性，BS 好于 CS，因为谁家电脑都有浏览器，拿来就能用

扩展性，BS 相对统一，只需要写 Server，浏览器端不用管



#### 1.3 javaweb服务器软件

学习 JavaWeb 开发，需要先安装 JavaWeb 服务软件【我们把安装了 JavaWeb 服务软件主机称为 Web 服务器/JavaWeb 服务器】，然后在 web 服务器中开发相应的 web 资源。

而tomcat就类似于该类型的软件，tomcat是一个java程序，该程序可以处理http请求。

tomcat相当于在本机做了一个服务器，可以从浏览器去输入本机ip与端口得到想要的浏览器服务。开启一个tomcat就相当于开启了一个本机服务器。



#### 1.4  简单web服务器

下面搭建一个简单的服务器，其理论也就是tomcat的理论（仅限于理论了，细节差太多）。

```java
package _02_servelLike;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

/**
 * 自己写的web服务，可以接受浏览器的连接请求（http://localhost:9999），并返回helloworld.html文件给浏览器
 * 测试的时候，先运行该程序，然后去浏览器发送连接请求
 */
public class myTomcat {
    public static void main(String[] args) throws IOException {
//1.在 9999 端口监听
        ServerSocket serverSocket = new ServerSocket(9997);
        //如果 serverSocket 没有关闭，就等待连接, 不停的等待
        while (!serverSocket.isClosed()) {
            System.out.println("=====我的 web 服务在 9999 端口监听=====");
            //2. 等待浏览器/客户端连接, 得到 socket
            // 该 socket 用于通信
            Socket socket = serverSocket.accept();
            //3. 通过 socket 得到 输出流，[]
            OutputStream outputStream = socket.getOutputStream();
            // 返回给浏览器/客户端
            //4. 读取 hello.html 文件返回即可=> 如何读取文件内容
            // 得到文件输入流(字符输入流), 和 src/hello.html
            BufferedReader bufferedReader =new BufferedReader(new FileReader("D:\\Code\\JavaCode\\_02_JavaWeb\\src\\_02_tomcat\\_01_open\\helloworld.html"));
            String buf = "";
// 循环读取 hello.html
            while ((buf = bufferedReader.readLine())!=null) {
                outputStream.write(buf.getBytes());
            }
            outputStream.close();
            socket.close();
        }
        serverSocket.close();
    }
}
```

实际上和学网络时在本机搭载的服务端几乎一样，不同的是这里是BS编程，从浏览器到服务端，当时是CS，从客户端到服务端。



然而从上述介绍来看，tomcat不过是完成了浏览器与主机的网络链接，那么浏览器的请求与返回的响应是怎么操作的呢？

此时就要引出tomcat的核心部件——Servlet





### 2 Servlet

#### 2.1 概览

Servlet 在开发动态 WEB 工程中，得到广泛的应用，掌握好 Servlet 非常重要了, Servlet(基石)是 SpringMVC 的基础。

Servlet(是一个java服务器小程序)，它的特点:

他是由服务器端调用和执行的(一句话：是Tomcat解析和执行)，可以将tomcat当作装Servlet的容器。

他是用java语言编写的, 本质就是Java类

他是按照Servlet规范开发的，Servlet实际上是一个接口（类比JDBC来理解）

功能强大，可以完成几乎所有的网站功能(在以前，我们老程员，使用Servlet开发网站) 技术栈要求高

简而言之，Servlet才是BS直接的核心。



先看看Servlet和tomcat之间的关系

tomcat服务器内，维护了一个哈希表`hashmap<id,Servlet>`，当浏览器需要服务器进行响应时，tomcat就用该哈希表里的Servlet来完成需要的操作。



#### 2.2 方法

刚刚说了，Servlet是一个接口，那么下面看看该接口的方法

```java
import javax.servlet.*;
import java.io.IOException;

public class ServletOpen implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

可以看到，Servlet接口的方法只有五个。下面一一介绍一下：

第一个方法，init。是Servlet初始化时的方法，也就是当tomcat需要生成一个Servlet来处理请求了，就会调用一次该方法来生成一个Servlet对象。但是要注意，该方法只会调用一次，只生成一个Servlet对象（大部分情况），也就是说，tomcat虽然维护了一个哈希表，但是该表里通常只有一个对象。



第二个方法，getServletConfig。是获取Servlet配置文件的方法，将有关的配置加载进来



第三个方法，service。核心方法，请求和响应都是在这个方法上处理。该方法接受两个对象。用来处理浏览器的请求，浏览器每次请求servlet时都会调用该方法。当tomcat调用该方法时，会把http请求的数据封装成实现了ServletRequest接口的对象，将该对象传入service方法。该方法还可以接受响应。



第四个方法，getServletInfo。返回servlet信息，实用不多。



第五个方法，destroy。用来关闭Servlet，从哈希表里将该Servlet对象消除。



虽然看着Servlet接口的方法不多，但是该接口不是最常用的接口，常用的是一个实现了Servlet接口的类——httpServlet类，该类除了实现了此接口外，还实现了另外两个接口并继承了一个类，使得httpServlet类的功能变的强大许多，这个到后面再将了。



#### 2.3 完整流程

下面看一套完整的BS流程是如何操作的（使用tomcat和Servlet）。

首先先配置好tomcat，并将ServletAPI导入该项目中。



1、首先写一个实现了Servlet接口的类，该类写在项目的src包下

```java
import javax.servlet.*;
import java.io.IOException;

public class _01_helloServlet implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("servlet创建");

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

        System.out.println("service方法被调用");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}

```

该类简单实现一些Servlet接口。



2、然后再配置好Web/Web-INF包下的web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
   
    <servlet>
        <servlet-name>_01_helloServlet</servlet-name>
        <servlet-class>_01_helloServlet</servlet-class>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>_01_helloServlet</servlet-name>
        <url-pattern>/_01_helloServlet</url-pattern>
    </servlet-mapping>
    
    
</web-app>


```

这里在原文件的基础上补充了`<servlet></servlet>`部分和`<servlet-mapping></servlet-mapping>`部分。

其中第一部分是给tomcat配置servlet代码内容、第二部分是给tomcat配置servlet代码的访问地址。

第一个属性`<servlet-name>_01_helloServlet</servlet-name>`是表示该servlet程序的名字，理论上随便起，但是一般和类名一致

第二个属性`<servlet-class>_01_helloServlet</servlet-class>`是该servlet的在src包下的地址，要由该地址通过反射机制得到该servlet的对象。

第三个属性`<servlet-name>_01_helloServlet</servlet-name>`是告诉服务器使用的servlet对象的名称，跟第一个属性要保持一致

第四个属性`<url-pattern>/_01_helloServlet</url-pattern>`是在浏览器中需要输入的url地址，一般为`http://localhost:8080/项目名称/_01_helloServlet`，来向本机服务器发送一个请求



服务器会首先读取url，此时进入`<servlet-mapping>`部分，然后通过该url得到与该url关联的`servlet-name`，再通过此`servlet-name`进入`<servlet>`的`servlet-name`部分，再通过与`<servlet>`的`servlet-name`关联的`servlet-class`来通过反射生成一个servlet对象。



3、最后写一个html，进行浏览器的操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>注册</h1>
<form action="http://localhost:8080/_02_servletUse/_01_helloServlet" method="get">
    u: <input type="text" name="username"/><br><br>
    <input type="submit" value="注册用户"/>
</form>
</body>
</html>
```

此时一旦点击注册，就会向本机发送请求，然后本机就会通过tomcat创建一个Servlet对象来处理请求。



![image-20230710221738824](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230710221738824.png)

其具体流程如上图。



#### 2.4 生命周期

Servlet主要又三个阶段：

init()初始化阶段；service()处理浏览器请求阶段；destroy()终止阶段。

1、初始化阶段：Servlet 容器(比如: Tomcat)加载 Servlet，加载完成后，Servlet 容器会创建一个 Servlet 实例并调用 init()方法，init()方法只会调用一次。

2、处理请求阶段：每收到一个 http 请求，服务器就会产生一个新的线程去处理[线程]，之后会创建一个用于封装 HTTP 请求消息的 ServletRequest 对象和一个代表 HTTP 响应消息的ServletResponse 对象，然后调用 Servlet 的 service()方法并将请求和响应对象作为参数传递进去。

3、终止阶段：当web 应用被终止，或者Servlet 容器终止运行，或者Servlet 类重新装载时，会调用 destroy() 方法。

![image-20230711151053103](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230711151053103.png)





#### 2.4 get和post

> Servlet处理

浏览器最常用的标签之一就是表单标签，而表单标签里会定义属性get和post。那么服务器该如何对get和post进行回应呢？

```java
import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

/**
 * get和post方法一般是跟表单标签绑定使用的，做表单时form后面会跟一个method属性，该属性的值可为post、get等等，然后就可以在servlet对象中的service方法里
 * 定义post和get可以分别对应什么细节
 */
public class _02_getpost implements Servlet {
    public static void main(String[] args) {

    }

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;//先将接受的servletRequest对象向下转型到ServletRequest的子接口上（因为得到表单的method属性值的方法在该子接口上）
        String method = httpServletRequest.getMethod();//通过转来的子接口得到表单的method属性的值
        if("GET".equals(method)){
            get();
        }else if(method.equals("POST")){
            post();
        }
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }

    public void get(){
        System.out.println("get方法被调用");
    }
    public void post(){
        System.out.println("post方法被调用");
    }
}

```

```xml
    <servlet>
        <servlet-name>_02_getpost</servlet-name>
        <servlet-class>_02_getpost</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>_02_getpost</servlet-name>
        <url-pattern>/_02_getpost</url-pattern>
    </servlet-mapping>
    
```



> httpServlet

除了可以通过实现Servlet接口来完成get和post操作，还可以通过继承httpServlet类来重写该类下的toGet和toPost来实现操作。

httpServlet结构如下

![image-20230711151608085](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230711151608085.png)

其实现过程如下

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class _03_httpservlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("doget调用");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("dopost调用");
    }
}

```

```xml
<servlet>
        <servlet-name>_03_httpservlet</servlet-name>
        <servlet-class>_03_httpservlet</servlet-class>
</servlet>

<servlet-mapping>
        <servlet-name>_03_httpservlet</servlet-name>
        <url-pattern>/_03_httpservlet</url-pattern>
</servlet-mapping>
```



### 3 http协议

超文本传输协议(HTTP，HyperText Transfer Protocol)是互联网上应用广泛的一种网络协议。是工作在 tcp/ip 协议基础上的,所有的 WWW 文件都遵守这个标准。

http 是 TCP/IP 协议的一个应用层协议,http 也是 web 开发的基础



### 4 ServletConfig

 ServletConfig 类是为 Servlet 程序的配置信息的类；Servlet 程序和 ServletConfig 对象都是由 Tomcat 负责创建；Servlet 程序默认是第 1 次访问的时候创建，ServletConfig 在 Servlet 程序创建时，就创建一个对应的 ServletConfig 对 象



### 5 ServletContext

ServletContext 是一个接口，它表示 Servlet 上下文对象；一个 web 工程，只有一个 ServletContext 对象实例； ServletContext 对象 是在 web 工程启动的时候创建，在 web 工程停止的时销毁。

ServletContext 对象可以通过 ServletConfig.getServletContext 方法获得对 ServletContext对象的引用，也可以通过 this.getServletContext()来获得其对象的引用。由于一个 WEB 应用中的所有 Servlet 共享同一个 ServletContext 对象，因此 Servlet 对象之间可以通过 ServletContext 对象来实现多个 Servlet 间通讯。ServletContext 对象通常也被称之为域对象。

这种相互通讯不是说两个对象直接进行信息沟通，而是Servlet对象1将数据存放在ServletContext里，然后Servlet对象2从ServletContext里取。



> 功能

1、获取 web.xml 中配置的上下文参数 context-param （信息和整个 web 应用相关，而不是属于某个 Servlet）

2、获取当前的工程路径，格式: /工程路径 ，比如 /servlet

3、获取工程部署后在服务器硬盘上的绝对路径 ( 比 如 : D:\hspedu_javaweb\servlet\out\artifacts\servlet_war_exploded)

4、像 Map 一样存取数据, 多个 Servlet 共享数据

其实现如下

```java

```





### 6 HttpServletRequset

该类已经接触很多次了，在Servlet接口中的service方法里接受的两个形参对象中，就有一个对象时HttpServletRequset类型的。

HttpServletRequest 对象代表客户端的请求；当客户端/浏览器通过 HTTP 协议访问服务器时，HTTP 请求头中的所有信息都封装在这个对象中； 通过这个对象的方法，可以获得客户端这些信息。



#### 6.1 具体使用

> 常用方法

getRequestURI() 获取请求的资源路径

getRequestURL() 获 取 请 求 的 统 一 资 源 定 位 符 （ 绝 对 路 径 ）

getRemoteHost() 获取客户端的 主机

getRemoteAddr()获取客户端的IP地址

getHeader() 获取请求头

getParameter() 获取请求的参数

getParameterValues() 获取请求的参数（多个值的时候使用） , 比如 checkbox, 返回的数组

getMethod() 获取请求的方式 GET 或 POST

setAttribute(key, value); 设置域数据

 getAttribute(key); 获取域数据

getRequestDispatcher() 获取请求转发对象, 请求转发的核心对象



> 实例说明





#### 6.2 请求转发

目前我们学习的都是一次请求，对应一个 Servlet， 但是在实际开发中，往往业务比较复杂，需要在一次请求中，使用到多个 Servlet 完成。此时需要用到请求转发。

实现请求转发：请求转发指一个 web 资源收到客户端请求后，通知服务器去调用另外一个 web 资源进行处理。HttpServletRequest 对象(也叫 Request 对象)提供了一个 getRequestDispatcher 方法，该方法返回一个 RequestDispatcher 对象，调用这个对象的 forward 方法可以实现请求转发。request 对象同时也是一个域对象，开发人员通过 request 对象在实现转发时，把数据通过 request 对象带给其它 web 资源处理

![image-20230712110004776](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230712110004776.png)



> 实例说明



> 细节

浏览器地址不会变化(地址会保留在第 1 个 servlet 的 url)

在同一次 HTTP 请求中，进行多次转发，仍然是一次 HTTP 请求

在同一次 HTTP 请求中，进行多次转发，多个 Servlet 可以共享 request 域/对象的数据(因为始终是同一个 request 对象)

可以转发到 WEB-INF 目录下(后面做项目使用)

不能访问当前 WEB 工程外的资源

因为浏览器地址栏会停止在第一个 servlet ,如果刷新页面，会再次发出请求(并且会带数据), 所以在支付页面情况下，不要使用请求转发，否则会造成重复支付



#### 6.3 重定向



### 7 HttpServletResponse



## 三、手动实现Web服务

先看下思路

![image-20230714105612295](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230714105612295.png)

分三个阶段实现整体过程。（http响应是从第三阶段返回给浏览器的，不是第一阶段，图画错了）

具体流程如下：

本机服务器开启Socket监听——>浏览器发送连接请求——>本机服务器产生socket对象并通过socket对象开启线程——>在线程中创建servlet对象——>使用doget方法将信息返回给浏览器



### 4.1 网络部分

该部分主要实现服务器监听浏览器的连接请求并启动线程，也是整个服务器启动的入口

```java
public class Run {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("在8080监听");
        Container.init();//启动容器，后面解释

        while (!serverSocket.isClosed()){
            Socket socket = serverSocket.accept();//获取socket

            //将获取的socket放入线程中，然后在线程中进行后面的操作
            SelfThread selfThread = new SelfThread(socket);//这里selfThread是自己写的线程类，后面解释
            Thread thread = new Thread(selfThread);
            thread.start();

            serverSocket.close();

        }
    }
}
```

这部分只负责进行浏览器到服务器的连接，连接完了之后所有的事交给后面的模块做。



### 4.2 线程部分

服务器每接收一个浏览器的连接请求，就会产生一个线程，然后在线程里面开启servlet来对浏览器进行反馈。

```java
package tomcat;

import tomcat.http.SelfHttpRequset;
import tomcat.http.SelfHttpResponse;
import tomcat.servlet.SelfHttpServlet;
import tomcat.servlet.SelfUseServlet;

import java.io.*;
import java.net.Socket;

public class SelfThread implements Runnable{

    private Socket socket = null;//将构造该线程的socket保存在这里，以便提取输入输出流使用

    public SelfThread(Socket socket) {//通过socket来构造线程，服务器每接收一个连接请求，就会产生一个socket，然后每个socket都来生成一个各自的线程
        this.socket = socket;
    }

    @Override
    public void run() {
        try {


            SelfHttpRequset selfHttpRequset = new SelfHttpRequset(socket.getInputStream());//通过socket的输入流构造requset

            SelfHttpResponse selfHttpResponse = new SelfHttpResponse(socket.getOutputStream());//通过socket的输出流构造response


//            SelfUseServlet servlet = new SelfUseServlet();
//            servlet.doGet(selfHttpRequset,selfHttpResponse);
            //这里只能硬实例化servlet，局限性很大，下面使用容器反射来实例化servlet。

            //这里是通过容器模拟对web.xml文件里面的数据进行操作
            String url = selfHttpRequset.getUri();//读取url
            String ServletName = Container.ServletUrlMapping.get(url);//通过容器得到该url对应的类名

            SelfHttpServlet selfHttpServlet = Container.ServletMapping.get(ServletName);//通过刚刚提取的类名得到该类对应对象

            selfHttpServlet.service(selfHttpRequset,selfHttpResponse);//调用service方法


            System.out.println("当前线程为" + java.lang.Thread.currentThread().getName());//显示当前是第几个线程



        } catch (IOException e) {
            e.printStackTrace();
        }finally {

            //确保socket关闭成功
            if(socket != null){
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

在这一步出现了很多需要自定义的东西：SelfHttpRequest、SelfHttpResponce、Container。他们分别模拟的是servlet-api里的HttpServletRequest、HttpServletResponce和容器。下面先把这三个讲清楚



### 4.3 servlet-api包的模拟

首先看看http部分的内容，由之前学的可知，使用doget或者dopost方法，需要向里面传入两个实参：HttpServletRequest和HttpServletResponce对象。

其中HttpServletRequest主要负责解析http请求的请求头，将主要信息提取出来，以便后续使用；HttpServletResponce主要用来完成向浏览器返回信息的准备工作。



> HttpServletRequest

```java
package tomcat.http;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.UnsupportedEncodingException;
import java.util.HashMap;

/**
 * 模拟HttpServletRequset类（在Service方法里接收的第一个参数），
 * 该类中，将http请求的数据：（方法、uri、参数列表）进行封装
 * 如Get /_02_ServletUse/_01_helloServlet?num1=10&num2=20这一常见的请求头中
 * get是方法、后面地址是uri，num1=10&num2=20是参数列表
 *
 */
public class SelfHttpRequset {
    private InputStream inputStream = null;//存放Socket传进来的InputStream

    //接收方法和uri
    private String method;
    private String uri;
    //接收参数列表时，由于不知道会有多少个参数，故用一个hashmap来存放，参数名--参数值组成键值对
    private HashMap<String,String> parametersMapping = new HashMap<>();

    
    //构造器，接收的是读取到的浏览器的请求，即与socket有关的inputstream。取出该请求头中的三部分信息：方法、uri、参数
    public SelfHttpRequset(InputStream inputStream){
        this.inputStream = inputStream;

        try {
            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream,"utf-8"));//将字节流转为字符流

            //虽然请求有好多行，但是HttpRequset只关心第一行的信息，故只取第一行信息
            //第一行结构为：Get(或Post) 资源地址?参数
            //假设第一行长这样Get /_02_ServletUse/_01_helloServlet?num1=10&num2=20
            String requsetLine = bufferedReader.readLine();//得到请求体的第一行


            method = requsetLine.split(" ")[0];//将第一行信息按空格切分，method是请求头的第一个元素，也就是get或post

            int index = requsetLine.split(" ")[1].indexOf("?");//得到？所在的索引
            if(index == -1) uri = requsetLine.split(" ")[1];//若没参数，则uri直接等于空格后半段
            else uri = requsetLine.split(" ")[1].substring(0,index);//按空格切分后取后半部分，再从0取到问号所在索引作为uri

            String parameters = requsetLine.split(" ")[1].substring(index+1);//将？后半部分先取出来
            String[] parameterPair = parameters.split("&");//将各种参数按&分开，先将k-v一起存
            //parameterPair里是["num1=10","num2=20"]
            //然后再将k-v按“=”分开，存进hashmap中
            for(String s : parameterPair){
                //此时s1里应该是["num1","10"]
                String[] s1 = s.split("=");
                //做一个保险一点的判断，若s1的长度确实是2，再进行存放
                if (s1.length == 2){
                    parametersMapping.put(s1[0],s1[1]);//将信息put进hashmap中
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //提供一个获取参数的方法
    public String getParameter(String name){
        if (parametersMapping.containsKey(name)){
            return parametersMapping.get(name);
        }//判断hashmap里是否有想要的参数，若有则直接返回
        else {
            return null;//没该参数则返回null
        }
    }

    public String getMethod() {
        return method;
    }

    public String getUri() {
        return uri;
    }
}

```

可见，HttpServletRequest只需要完成分析http请求头的任务即可。



> HttpServletResponce

```java
package tomcat.http;

import java.io.OutputStream;

/**
 * 模拟HttpServletResponse（Service第二个参数）。
 * 将需要返回给浏览器的信息通过该对象封装起来一起发过去
 *
 */
public class SelfHttpResponse {

    private OutputStream outputStream = null;//做好输出流的存放，到时候好返回给Socket用

    public static final String respHeader = "HTTP/1.1 200 OK\r\n" +
            "Content-Type: text/html;charset=utf-8\r\n\r\n";//将响应头做成静态final属性，因为这个一直不变了

    public SelfHttpResponse(OutputStream outputStream){
        this.outputStream = outputStream;
    }

    public OutputStream getOutputStream(){
        return outputStream;
    }

}

```

HttpServletResponce的任务就更简单了，只需要将响应头的部分封装到该类里面，从而使响应时可以少打几个字。



> 容器

容器有点门道，在使用tomcat时可以发现，只需要在web.xml里设置好想要使用的servlet的配置，到时候直接在浏览器中输入对应的url就能直接调用该servlet了。这个过程主要是容器在支撑。

```java
package tomcat;

//容器类要是有dom4j来对web.xml文件进行解析
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;
import tomcat.servlet.SelfHttpServlet;

import java.util.HashMap;
import java.util.List;
//容器类提供的hashmap
import java.util.concurrent.ConcurrentHashMap;

public class Container {
    //首先做两个hashmap，一个存放web.xml里<servlet></servlet>中的信息（servletname、servlet-class），另一个存放<serlvet-mapping>中的信息（servlet-name、servlet-url）。由于一个web.xml里很可能不只包含一组servlet，故使用集合来存放信息。
    public static ConcurrentHashMap<String, SelfHttpServlet> ServletMapping = new ConcurrentHashMap<>();//存放<servlet></servlet>中的信息，其中servlet的名字就用string来存放，servlet本体则要用SelfHttpServlet类型存放（后面讲该类）
    public static ConcurrentHashMap<String, String> ServletUrlMapping = new ConcurrentHashMap<>();//存放<serlvet-mapping>，其中name和url都用string存放就行

    
    //构造两个hashmap的方法
    public static void init(){
        String path = Container.class.getResource("/").getPath();//得到当前项目的工作路径（工作路径会指out文件夹下的路径）


        SAXReader saxReader = new SAXReader();//构造一个dom4j解析器
        try {
            Document doc = saxReader.read(path + "web.xml");//将工作路径下的web.xml文件做成dom对象

            Element rootElement = doc.getRootElement();//得到该对象根元素--> <web-app>，所有xml文件的根元素都是这个

            List<Element> elements = rootElement.elements();//将该根元素的子元素保存在集合中，此时集合里有<display-name>、<servlet>、<servlet-mapping>三个部分，其中有用的是后两个，故要遍历集合将后两个信息取出来
            for(Element e : elements){
                if ("servlet".equals(e.getName())){//得到servlet元素，将该元素下的两个属性存放到ServletMapping（第一个hashmap中）
                    Element servletName = e.element("servlet-name");
                    Element servletClass = e.element("servlet-class");
                    ServletMapping.put(servletName.getText(),//使用getText方法来得到标签中间的信息，若不用该方法，则得到的是整个标签：`<servlet-name>SelfUseServlet</servlet-name>`
                            (SelfHttpServlet) Class.forName(servletClass.getText()).newInstance());//这里通过类的地址映射出该类的对象，然后将该对象转型为SelfHttpServlet。
                }else if("servlet-mapping".equals(e.getName())){//同理，构造好第二个hashmap
                    Element servletName = e.element("servlet-name");
                    Element servleturl = e.element("url-pattern");
                    ServletUrlMapping.put(servleturl.getText(), servletName.getText());

                }
            }


        } catch (Exception e) {
            e.printStackTrace();
        }

    }


}

```



在看上面三个部分的代码时，可以看到SelfHttpServlet不止一次出现，这也就引出了该过程最后一个步骤，servlet的实现。



### 4.4 servlet部分

servlet，也就是实现浏览器服务器交互内容的主要部分了。下面全面模拟一下servlet。

众所周知，servlet在tomcat里面用时，有三个大部分：

servlet接口（提供5个方法，核心方法是service方法）

HttpServlet抽象类，实现servlet接口，主要是判断使用doget方法还是dopost方法

自己写的servlet类，继承HttpServlet类，重写doGet和doPost方法。



> SelfServlet

```java
package tomcat.servlet;

import tomcat.http.SelfHttpRequset;
import tomcat.http.SelfHttpResponse;

import javax.servlet.ServletException;
import java.io.IOException;

/**
 * 模拟Servlet接口，简化一下，五个方法里面选三个核心的方法
 * 主要提供service方法供HttpServlet重写
 */
public interface SelfServlet {
    void init() throws Exception;

    void service(SelfHttpRequset requset, SelfHttpResponse response) throws IOException;

    void distroy();


}
```

该类也就是提供一个规范，并没有什么实质内容



> SelfHttpServlet

```java
package tomcat.servlet;

import tomcat.http.SelfHttpRequset;
import tomcat.http.SelfHttpResponse;

import java.io.IOException;

/**
 * 模拟HttpServlet
 * 重写service方法（调用doGet和doPost），并提供doGet方法和doPost方法供Servlet重写
 */
public abstract class SelfHttpServlet implements SelfServlet{

    @Override
    public void service(SelfHttpRequset requset, SelfHttpResponse response) throws IOException {//实现SelfServlet的service方法
        if ("GET".equals(requset.getMethod())) this.doGet(requset,response);
        if ("POST".equals(requset.getMethod())) this.doPost(requset,response);
        //通过SelfHttpRequse中提供的getmethod方法，得到浏览器的请求头中的方法是什么，从而确定使用doget还是dopost

    }

    
    //提供抽象方法doget和dopost，以供继承该类的类重写
    public abstract void doGet(SelfHttpRequset requset , SelfHttpResponse response);

    public abstract void doPost(SelfHttpRequset requset, SelfHttpResponse response);


}

```

该类提供了doget和dopost的规范，并通过实现的service方法来读取http请求中的请求头的方法部分，来确定调用哪个doget和dopost中的哪个方法



> SelfUseServlet

```java
package tomcat.servlet;

import tomcat.http.SelfHttpRequset;
import tomcat.http.SelfHttpResponse;
import tomcat.utils.WebUtils;

import java.io.IOException;
import java.io.OutputStream;

/**
 * 真正使用的Servlet,前两个servlet是模拟的servlet-api中提供的，这里是模拟的tomcat自己的
 * 将doGet和doPost重写，然后会影响到HttpServlet的Service方法，进而相当于影响了Servlet接口的Service方法
 */
public class SelfUseServlet extends SelfHttpServlet{//继承SelfHttpServlet，重写doget和dopost
    @Override
    public void doGet(SelfHttpRequset requset, SelfHttpResponse response) {
        int num1 = WebUtils.SelfparseInt(requset.getParameter("num1"),-1);//将requset得到的参数转为数字
        int num2 = WebUtils.SelfparseInt(requset.getParameter("num2"),-1);//同理
        int sum = num1 + num2; 

        //返回计算结果给浏览器
        OutputStream outputStream = response.getOutputStream();
        String respMes = SelfHttpResponse.respHeader + "<h1>" +"计算结果为" +  sum + "</h1>";


        try {
            outputStream.write(respMes.getBytes());
            outputStream.flush();
            outputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void doPost(SelfHttpRequset requset, SelfHttpResponse response) {
        this.doGet(requset,response);

    }

    @Override
    public void init() throws Exception {

    }

    @Override
    public void distroy() {

    }
}

```



### 4.5 总结

这一套完整的流程还是挺明确的，之前tomcat将绝大多数内容都封装了起来，使用的时候只需要在SelfUseServlet类中重写一下doget和dopost就行了，但是如果只知道怎么用tomcat，肯定是不行的，要深入了解一下tomcat的机制才行。

这里就知道了doget和dopost是重写的Httservlet的方法；也知道了tomcat开启服务器后，是通过开启一个线程来完成对浏览器的对接，并在线程里调用service方法来判断使用doget还是dopost方法，一套下来一气呵成。



## 四、工程路径





## 五、会话

### 5.1 Cookie

#### 5.1.1 概念

Cookie是客户端技术，服务器把每个用户的数据以 cookie 的形式写给用户各自的浏览器。当用户使用浏览器再去访问服务器中的 web 资源时，就会带着各自的数据去。这样，web 资源处理的就是用户各自的数据了。 Cookie 是服务器在客户端保存用户的信息，比如登录名，浏览历史等, 就可以以 cookie方式保存。



浏览器会根据不同的访问地址来加载对应该地址的cookie，如浏览器访问百度则会加载在www.baidu.com上存储的cookie，如果访问本机tomcat，则会加载http://localhost:8080上存储的cookie。不会访问一个服务区时把所有的cookie一股脑加载进去的。



> 思路

cookie从无到有的过程是如何的呢？

要明确一点，cookie是服务端定义的数据保存在浏览器的，因此cookie的出生地应该是服务端。

首先浏览器与服务器设置cookie的servlet建立http连接，假设该servlet还没有进行cookie的设置，则此时请求体（若浏览器本来就存有其他cookie信息，则请求体中也会有cookie）和响应体内都没有cookie的具体内容。

若servlet设置了cookie并将该cookie通过`response.addCookie()`方法保存到浏览器了，则此时再次调用该servlet，会发现请求头和响应头都有该cookie的具体信息。其中响应头中cookie相关语句是将cookie保存到浏览器的；请求头中的cookie语句是用来告诉服务器该浏览器都保存了哪些cookie信息，以方便服务器`getcookie`来调用的。其流程图如下

![image-20230719161639560](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230719161639560.png)



观察该图可以发现，在调用`addCookie`方法后，响应体中会出现对应的cookie信息；在调用`getCookie`方法时，服务器会从请求体中的cookie信息里取出各个cookie。



#### 5.1.2 方法

> 创建

Cookie是一个类，该类中维护了一张map，key和Value都是String类型的，分别用来存放Cookie的名称和对应的值。Cookie创建及保存的具体使用看下例

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        response.setContentType("text/html;charset=utf-8");

        //创建一个cookie
        Cookie cookie = new Cookie("username","tom");//构造器构造cookie时，传入该cookie对象的key和value。这里key为username；value为tom

        response.addCookie(cookie);//将该cookie传给浏览器


        PrintWriter writer = response.getWriter();
        writer.println("<h1>cookie传入成功<h1>");
        writer.flush();
        writer.close();


    }
```

就很简单，直接new一个cookie就行，然后通过response去将cookie存入浏览器。



> 读取

Cookie的读取则使用request来读取

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //读取浏览器的cookie信息
        Cookie[] cookies = request.getCookies();//通过request的getcookies方法得到浏览器中保存的所有cookie，记录为Cookie数组形式
        //遍历该cookie数组
        for(Cookie c : cookies){//每个c都是个cookie的对象，第一讲构造cookie时可知，cookie对象都有一个name属性（对应key）和value属性，下面逐个取出这两个属性
            System.out.println(c.getName());
            System.out.println(c.getValue());
        }

        response.setContentType("text/html;charset=utf-8");
        PrintWriter writer = response.getWriter();
        writer.println("<h1>cookie读取成功<h1>");
        writer.flush();
        writer.close();



    }
```



> 生命周期

既然cookie是保存在浏览器中的信息，那么我们希望某个信息在浏览器保存多久呢？1分钟？1年？还是永久。这就涉及到了cookie的生命周期。

Cookie生命周期是人为设定的将该cookie存放在浏览器中的时间，一旦cookie的存在超过了这个时间，则浏览器就不会将该cookie信息放在请求头里了（浏览器内存中删不删除该cookie分情况，有的删有的不删）

Cookie的生命周期分为三种：正数生命、负数生命、0生命。其效果看下例

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        Cookie cookie  = new Cookie("job","java");

        //设置cookie的生命周期
        cookie.setMaxAge(60);//给cookie生命设置成60秒
        //浏览器根据创建的时间，计时60秒，如果时间超过了60秒，则浏览器在发出http请求后，就不再携带该cookie信息了（但是cookie还会存在与浏览器的存储中(有的浏览器不保存，分浏览器的)，只是请求头中没有cookie了）
        response.addCookie(cookie);


        //若将生命周期设置成负数，则表示将浏览器关闭后自动删除该cookie，若不设置生命周期，则默认生命周期为-1，即默认关了浏览器后cookie自动删除
        cookie.setMaxAge(-1);
        response.addCookie(cookie);


        //删除cookie的操作与生命周期也有关，将cookie的生命周期设置成0后再add一下,浏览器就会解析成将该cookie删除
        cookie.setMaxAge(0);
        response.addCookie(cookie);



    }
```





> 保存账号密码

下面看一个案例，来在浏览器中保存账号密码一天

```java
package homework;

import UtilForCookie._00_util_readcookieByName;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class User extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter writer = response.getWriter();

        String name = null;
        String pwd = null;

        //读取从浏览器输入的cookie
        Cookie[] cookies = request.getCookies();
        Cookie usernamecookie = _00_util_readcookieByName.readcookieByName("username", cookies);
        Cookie userpwd = _00_util_readcookieByName.readcookieByName("pwd",cookies);
        if(usernamecookie != null && userpwd != null){
            name = usernamecookie.getValue();//得到username
            pwd = userpwd.getValue();
            System.out.println(pwd + "!");
        }

        //输出原表
        writer.println("<!DOCTYPE html>\n" +
                "<html lang=\"en\">\n" +
                "<head>\n" +
                "    <meta charset=\"UTF-8\">\n" +
                "    <title>Title</title>\n" +
                "</head>\n" +
                "<body>\n" +
                "<h1>用户登录界面</h1>\n" +
                "<form action=\"http://localhost:8080/Cookie/login\" method=\"get\">\n" +
                "    u:<input type=\"text\" value = \"" + name + "\" name=\"username\"><br/>\n" +
                "    p:<input type=\"password\" value = \"" + pwd + "\" name=\"pwd\"><br/>\n" +
                "    <input type=\"submit\" value=\"登录\">\n" +
                "</form>\n" +
                "\n" +
                "</body>\n" +
                "</html>");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        doGet(request,response);
    }
}

```

首先是一个登录servlet，该servlet会输出一个html文件，该文件解析后就是一个简单的登录界面，但是不同与以往的登录界面，此登录界面会自动输入从请求头中读取的cookie信息（即账号密码），若没有则不输入（具体看writer.println里的文本，可以看出跟之前不一样的）。

当点击登录后，会跳转到登录功能的Servlet上，如下

```java
package homework;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class login extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter writer = response.getWriter();

        //1、接收表单提交的参数：账号密码
        String username1 = request.getParameter("username");
        String pwd1 = request.getParameter("pwd");
        


        //2、判断是否为为正确账号密码
        if ("manager".equals(username1) && "123456".equals(pwd1)){
            //如果登录成功，则将账号密码以cookie保存到浏览器中
            Cookie loginuser = new Cookie("username",username1);
            loginuser.setMaxAge(3600 * 24);//保存一天，保证一天内可以不输入账号密码
            Cookie loginpwd = new Cookie("pwd",pwd1);
            loginpwd.setMaxAge(3600 * 24);

            response.addCookie(loginuser);
            response.addCookie(loginpwd);
            writer.println("登录成功");
        }else {
            writer.println("登录失败");
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        doGet(request,response);
    }
}

```

该界面会返回登录是否成功的提示，当然也不限于此。它在判断登录成功与否的同时，还会同时将正确的账号密码保存到浏览器中保存一天。

上面就是一个简单的自动保存账号密码的案例了。



### 5.2 Session

在之前学Cookie时，会发现浏览器里的Cookie信息中，偶尔有一个叫做Jsessionid的信息保存在cookie中，而这个就与Session息息相关了。先介绍下session。

#### 5.2.1 概念

考虑一个问题，浏览器发送连接请求后，服务器是如何确保无论该浏览器访问服务器的哪个界面，服务器都能识别出该浏览器是同一个人访问的呢？或者说如何保证A在访问自己购物车的时候不会突然出错访问到B的购物车呢？就用session来判断。

session是保存在服务器中的数据（cookie是保存在浏览器的，要分清），服务器会为每个浏览器分配其独有的sessionid（保存在cookie中），每个sessionid对应一个session对象，session对象中维护了一个map，由key和value组成，key为String类型，是value对应的名字，value则为Object类型，是可以存放对象的。

> 思路

![image-20230719165517430](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230719165517430.png)

具体流程如上，浏览器在与服务器进行http连接后，服务器当然会解析一下请求体，此时若服务器使用了`requset.getSession()`方法的话，则会解析一下浏览器中cookie里是否保存了Jsessionid这个信息，若没有该cookie，则getSession方法会转而创建一个session对象，并为该session对象分配一个jsesessionid保存到浏览器的cookie中。

如果携带了jsessionid，但是该jsessionid在服务器内并没有能与之对上号的session对象，则也会创建一个新的session对象并分配新id返回覆盖调浏览器中的原携带的jsessionid。

若是浏览器携带的jsessionid可以与服务器内的session对象匹配上，则可以直接进行后续的操作了。



上面是session的内部细节，session的综合流程如下（以访问购物车举例）

![image-20230719170426358](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230719170426358.png)

众所周知Cookie可以存放一些小的信息，但是虽然账号密码这种信息占用空间不大，但是十分重要，故一般不存放再cookie中，都用session进行验证。

假设此时浏览器A和浏览器B都还没有id。servlet1的功能就是验证或创建session并赋予session对象相应的内容（如用户账号密码等等）、servlet2则是根据session里的信息进行对号入座的操作。

浏览器A首先去servlet1获取一个session，假设此session的id为111，则该id通过cookie存放在浏览器A中，该session则直接保存在服务器中。之后浏览器A再去访问servlet2，servlet2发展浏览器A带的sessionid在服务器内有对应的session，则直接对该session进行读写操作，比如读出session中保存的账号密码进行验证，然后让浏览器A显示出该账号密码对应的购物车内容。

同理，浏览器B也去servlet1拿到浏览器B的sessionid，之后拿着这个这个id去servlet2中进行浏览器B的购物车显示。

上面说的浏览器A和浏览器B实际上是由人来操作的也是，再概括就是，用户A将自己的账号密码保存在session中，之后通过该session验证身份后获得自己的购物车信息；用户B也是一样的流程，不过用户A对应的session是111，只属于A自己，用户B对应的session是222，也只属于B自己。



#### 5.2.2 方法

> 创建和读取session对象

session对象是HttpSession类构建的。session的创建和读取都是通过get方法来的，若服务器中没有对应的session，则创建；若有对应的session，则读取。

```java
public class CreateSession extends HttpServlet {
	protected void doPost(HttpServletRequest request, HttpServletResponse response)throws ServletException, IOException {
		doGet(request, response);
	}
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		HttpSession session = request.getSession();//直接完成创建或读取操作，requset里带的cookie信息里面有Jsessionid，然后getSession方法自动将该id拿走去服务器里找对应的session，故不需要对方法里面进行传参。
		response.getWriter().write("<h1>向 Session 对象 保存属性 key1</h1>");
	}
}	
```



> 写入和读取session对象里的信息

写入信息使用`setAttribute("key","value")`方法；读取使用`getAttribute("key")`方法，得到该key对应的value

```java
HttpSession session = request.getSession();  
session.setAttribut("name","tom");//向session对象里存入一组信息，name对应的值为tom
Object sessionMsg = session.getAttribut("name");//取出session对象中name对应的对象，由于session中维护的map的value列是Object类型，故接收时也要用Object来接收，或者转型后接收。
```

还有删除某个属性从session.removeAttribute(String name);看api就知道怎么用了，不展示了



> 生命周期

Session也有生命周期，不同于cookie的生命周期是从cookie被创建那一刻开始计时，session的生命周期是从上次访问该session开始计时的。比如00：00创建了一个生命周期为30分钟的session，理论上该session的生命到00：30。但如果00：20访问过一次这个session，则该session的生命就到了00：50。

Cookie信息的生命周期是浏览器判断创建时间到生命周期的时间后进行删除信息就行，session这边麻烦点，服务器里一般都会将sessionid和session对象作为map保存在一个线程中，然后该线程不停的循环遍历这个map，看看哪个session信息上次访问后超过生命周期没访问了，就把这条id和对象删掉。



`public void setMaxInactiveInterval(int interval) `设置 Session 的超时时间（以秒为单位），超过指定的时长，Session 就会被销毁；

值为正数的时候，设定 Session 的超时时长。负数表示永不超时；

`public int getMaxInactiveInterval()`获取 Session 的超时时间；

`public void invalidate() `让当前 Session 会话立即无效；

如果没有调用 setMaxInactiveInterval() 来指定 Session 的生命时长，Tomcat 会以 Session 默认时长为准，Session 默认的超时为 30 分钟， 可以tomcat 的 web.xml 设置





## 六、JSP

JSP（Java Server Pages）是一种基于servlet的工具，其内核还是servlet，但是其代码是写在html文件下的。（相当于有浏览器界面的servlet，jsp也通过url进行访问）

在使用jsp时，需要去tomcat工具包里找到jsp-api引入到项目中（类似servlet的引包）。

第 1 次访问 jsp 页面的时候，Tomcat 服务器会把 jsp 页面解析成为一个 java 源文件。并且对它进行编译成为`.class` 字节码程序

### 6.1 语法使用

#### 6.1.1 声明语法

声明语法是用来定义jsp所需要的属性、方法、内部类、代码块的（类的五大属性里，除了构造器之外的四个属性jsp都能定义）。

其语法为：

```jsp
<%! 具体内容 %>
```



其实例如下

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>  
<html>  
<head>  
<title>jsp 声明脚本应用实例</title>  
</head>  
<body>  
<h1>jsp 声明脚本应用实例</h1>  
<%!  
//声明属性
  private Integer id;
  private String name = "老韩同学";
  private String job;
  private static String company;
  private Double sal;
//静态代码块
  static {
    company = "字节跳动";
  }
//声明方法
  public String getName() {
    return name;
  }
%>
<hr/>
</body>
</html>
```



#### 6.1.2 表达式语法

表达式语法是定义直接在浏览器中显示出来的信息。

其语法为：

```jsp
<%=具体内容%>
```



其实例如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>jsp 表达式脚本</title>
</head>
<body>
    <h1>jsp 表达式脚本应用实例</h1>
<%!
  String name = "韩顺平教育";
%>
<hr/>
<h1>个人信息</h1>
用户名= <%=name%><br/>
工作是: <%="java 工程师"%><br/>
得到参数= <%=request.getParameter("sex")%>
</body>
</html>
```



要注意表达式脚本中的表达式不能以分号结束。



#### 6.1.3 代码语法

代码语法就相当于正常写java语句的部分了，在jsp中编写所需要的功能。

其语法为：

```jsp
<% 具体内容 %>
```



其实例如下：

```java
public class Monster {
	private Integer id; 
	private String name; 
	private String skill;
	public Monster(Integer id, String name, String skill) {
		this.id = id;
		this.name = name; 
		this.skill = skill;
	}
//先定义一个类，在类里定义一些属性
```

```jsp
<%@ page import="java.util.ArrayList" %> 
<%@ page import="com.hspedu.jsp.entity.Monster" %>
<!-- 上面两行是在jsp中完成导包 --!>

<%@ page contentType="text/html;charset=UTF-8" language="java" %> 
<html>
<head>
<title>计算结果</title>
</head>
<body>
<h1>计算结果</h1>
<%
  ArrayList<Monster> list = new ArrayList<>();
  list.add(new Monster(1, "牛魔王", "芭蕉扇"));
  list.add(new Monster(2, "蜘蛛精", "吐口水"));
  //编写正常的java代码即可
%>
<table bgcolor="#f0f8ff" border="1px" width="500px">
<tr>
<td>id</td>
<td>name</td> 
<td>skill</td> 
</tr>
<%
  for (int i = 0; i < list.size(); i++) {
  Monster monster = list.get(i);
%>
<tr>
<td>
<%=monster.getId()%></td>
<td>
<%=monster.getName()%></td>
<td><%=monster.getSkill()%></td> 
</tr>
</table> 
</body> 
</html>
```



### 6.2 内置对象

我们知道，jsp是servlet的扩展，而jsp的设计者为了更方便的使用jsp，其为jsp默认构建了九大对象，这些对象已经是实例化好的，可以直接拿来使用。

#### 6.2.1 对象

> request

jsp中的request与servlet中的request是同源的，都是HttpSrvletRequest类的实例。



> response

同request，response也是与servlet中的response同源，是HttpServletResponse的实例



> out

jsp中，out是JSPWriter的实例；servlet中则使用的是PrintWriter的实例。但是JSPWriter和PrintWriter都是继承的Writer类，所以out也可以约等于是servlet的输出实例



> session

jsp的session和servlet的session都是HttpSession的实例



> application

jsp中的application则与servlet中的servletContext是同性质，都是用来处理servlet维护的通用空间的。



> exception

jsp中的异常对象，用的不多



> pageContext

表示jsp本身的对象，类比this的性质



> config

与servlet的servletConfig对应



简单举例使用：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>内置对象</title>
</head>
<body>
<%
  //jsp 中可以使用的内置对象:不用创建,直接使用
  out.println("out 对象..");
  String age = request.getParameter("age");
  response.sendRedirect("http://www.baidu.com");
  session.setAttribute("name", "jack");
  //application 等价 servlet 的 servletContext
  application.setAttribute("company", "北京韩顺平教育"); 
  //本页面有效 
  pageContext.setAttribute("num1", 900); 
  //page 
  out.println("page= " + page); 
  //使用 config
  String pwd = config.getInitParameter("pwd");
 %>
 </body>
 <h1>jsp 内置对象</h1>
 num1: <%=pageContext.getAttribute("num1")%>
 </html>
```



#### 6.2.2 域对象

上面介绍了九大内置对象，这九个对象中，有四个是有使用范围的，称为四大域对象。

> pageContext

pageContext存放的对象只能在当前服务中使用（或者说当前servlet中使用，如果跳到其他servlet则无法读取此数据）

![image-20230820172653811](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230820172653811.png)



> request

request存放的数据在仅一次 request 请求有效。

![image-20230820172759866](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230820172759866.png)



> session

session存放的数据在一次会话中都有效

![image-20230820172927153](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230820172927153.png)



> application

application存放的数据在整个 web 应用运行期间有效。

![image-20230820173011497](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230820173011497.png)



域对象是可以像Map一样存取数据的对象。四个域对象功能一样，不同的是它们对数据的存储范围。

从存储范围(作用域范围看) pageContext < request < session < application



### 6.3 jsp实用

需求分析: 使用 jsp 完成一个简单的计算器
1) 要求在前端页面对输入的 num1 和 num2 进行校验, 必须是整数
2) 验证成功, 提交数据给服务器, 能够显示结果。
3) 点击超链接, 可以返回界面。



其思路如图：

![image-20230820173331885](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230820173331885.png)



解决过程

1、创建ui界面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>jsp 版 计算器</title>
<script type="text/javascript">
function check(){
    //得到用户输入的第一个数和第二个数
	var num1=document.getElementById("num1").value;
	var num2=document.getElementById("num2").value;
	//这里我们再去验证是不是一个数
	var reg=/^(([1-9]\d*)|(0))$/;
	if(!reg.test(num1)){
		window.alert("num1 不是一个整数");
		return false;
	}
	if(!reg.test(num2)){
		window.alert("num2 不是一个整数");
		return false;
	}
}
</script>
</head>
<body>
<h1>jsp 版本-计算器</h1>
<form action="<%=request.getContextPath()%>/calCLServlet" method="post" onsubmit="return check()">
num1：<input type="text" id="num1" name="num1"/><br/><br/>
num2：<input type="text" id="num2" name="num2"/><br/><br/>
    
运算符号:
<select name="operator">
<option value="+">+</option>
<option value="-">-</option>
<option value="*">*</option>
<option value="/">/</option>
</select><br/><br/>
<input type="submit" value="计算">
</form>
</body>
</html>
```



2、创建servlet内核

```java
public class CalCLServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
		doGet(request, response); 
	} 
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
		//获取 num1
 		String num1 = request.getParameter("num1");
 		String num2 = request.getParameter("num2");
 		String operator = request.getParameter("operator");
 		//转换数据
 		int i = Integer.parseInt(num1);
 		int j = Integer.parseInt(num2);
 		double res = 0;
 		if ("+".equals(operator)) {
 			res = i + j;
 		} else if ("-".equals(operator)) {
 			res = i - j;
 		} else if ("*".equals(operator)) {
 			res = i * j;
 		} else {
    		 res = i / j;
		}
	String resInfo = i + " " + operator + " " + j + " = " + res;
	request.getSession().setAttribute("resInfo",resInfo);
	request.getRequestDispatcher("/cal/showRes.jsp").
	forward(request, response);
	}
}
```



3、创建计算完毕的界面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>计算结果</title>
</head>
<body>
<h1>计算结果</h1>
<%=session.getAttribute("resInfo")%><br/><br/>
<a href="<%=request.getContextPath()%>/cal/calUI.jsp">返回再来玩一次</a>
</body>
</html>
```



## 七、监听器 过滤器

监听器（Listener）和过滤器（Filter）是JavaWeb三大组件中的后两件（第一件是servlet）。

### 7.1 监听器

监听器的作用是监听某种变化，监听到了之后触发某种事件。在学java基础时也曾用到过监听器来监听键盘的输入，但是此处的Listener监听的内容要相对抽象一点，其监听的一般是信息的变换（如属性的创建、销毁；对象的创建销毁等），当监听到某个信息出现修改后，进而触发某些活动。



监听器要在web.tml里配置好，配置上哪些监听器则服务器就默认同时使用哪些监听器，在服务器开始的一瞬间，监听器就开始工作。



#### 7.1.1 七大监听器

javaweb里的监听器常见的有7个，常用的就两个，其都是接口形式。现在分别介绍一下这两个监听器。在介绍之前，先提前将这两个监听器在web.xml配置好

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--配置监听器-->
    <listener>
        <listener-class>_01_ServletContextLintener</listener-class>
    </listener>

    <listener>
        <listener-class>_02_ServletContextAttributeLintener</listener-class>
    </listener>

    <listener>
        <listener-class>_03_HttpSessionListener</listener-class>
    </listener>



    <!-- 配置servlet -->
    <servlet>
        <servlet-name>_0_testServlet</servlet-name>
        <servlet-class>_0_testServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>_0_testServlet</servlet-name>
        <url-pattern>/test</url-pattern>
    </servlet-mapping>

</web-app>
```

再写一个testServlet用来测试这些监听器的情况

```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class _0_testServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        ServletContext servletContext = request.getServletContext();
        servletContext.setAttribute("1","11");
        servletContext.setAttribute("2","22");
        servletContext.removeAttribute("2");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        doGet(request, response);
    }
}

```



> ServletContextListener

此监听器是最常用的监听器，用来监听ServletContext是否创建。之前学过，ServletContext是随着Web项目创建而创建的一个容器，一般用来实现项目内的信息共享。因此监听ServletContext相当于是监听项目的开始与结束。其实例如下：

```java
import javax.servlet.ServletContext;
import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

/**
 * 当一个类实现了某个监听功能的接口，这个类就是该功能的监听器
 * 一个类可以实现多个监听接口，但是实现多个接口会显得有点乱
 * 此处监听ServletContext事件，监听ServletContext的创建或销毁
 */


public class _01_ServletContextLintener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {
//随着服务器的启动，context也被同时创建出来，context监听器监听到了context被创建，会调用contextInitialized方法
        ServletContext context = servletContextEvent.getServletContext();
        System.out.println("监听到context被创建");



    }

    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {
        //随着服务器的关闭，context被销毁，context监听器监听到了context被销毁，调用contextDestroyed方法
        ServletContext context = servletContextEvent.getServletContext();
        System.out.println("context被销毁");


    }
}

```

ServletContextLintener提供了两个方法，contextInitialized方法在ServletContext被创建后被调用、contextDestroyed方法在ServletContext被销毁时被调用。



> ServletContextAttributeListener

该监听器是用来监听ServletContext里属性变换情况的，当ServletContext里的信息发生了变换，则该监听器里对应的方法就开始执行。如

```java
import javax.servlet.ServletContextAttributeEvent;
import javax.servlet.ServletContextAttributeListener;

/**
 * 该监听器用来监听context内部存储信息的变化
 */
public class _02_ServletContextAttributeLintener implements ServletContextAttributeListener {
    @Override
    public void attributeAdded(ServletContextAttributeEvent servletContextAttributeEvent) {
        System.out.println("监听到context被加入数据");
        String s = servletContextAttributeEvent.getName();
        Object o = servletContextAttributeEvent.getValue();
        System.out.println(s);
        System.out.println((String) o);
    }

    @Override
    public void attributeRemoved(ServletContextAttributeEvent servletContextAttributeEvent) {
        System.out.println("监听到context内部被移除数据");
        String s = servletContextAttributeEvent.getName();
        Object o = servletContextAttributeEvent.getValue();
        System.out.println(s);
        System.out.println((String) o);

    }

    @Override
    public void attributeReplaced(ServletContextAttributeEvent servletContextAttributeEvent) {

    }
}

```

ServletContextAttributeListener提供了三个方法，attributeAdded方法在ServletContext里被添加新属性后被调用、attributeRemoved方法在ServletContext里的属性被删除后被调用、attributeReplaced方法在ServletContext里的属性被修改后被调用。



> 其他监听器

其他还有一些监听器，用的不多，但是使用方法和上面两个监听器的使用方法一致。

1、HttpSessionListener，用来监听Session的创建与销毁，可以监听到用户是否上线。

2、HttpSessionAttributeListener，用来监听Session属性的修改情况。

3、ServletRequestListener，用来监听Request的创建与销毁。

4、ServletRequestAttributeListener，用来监听Request的属性修改情况。

5、HttpSessionBindingListener 感知监听器



### 7.2 过滤器

想象一个应用场景，我有一个后台界面，该界面理论上来说需要通过验证账号密码后进入某个servlet再通过转发给该界面的jsp从而进行访问，但是如果有人直接知道了后台jsp的url，那就可以绕过账号密码验证从而直接访问后台，系统就出现了大漏洞。

Filter就可以做到一层拦截的作用，当服务器启动，则某个项目下的所有界面都需要通过一个Filter验证，只有验证通过了，才可以访问该项目下的信息。

#### 7.2.1FilterUse

直接从实例出发：

> 界面

首先创建界面jsp，一个是登录界面、一个是后台界面。登录界面需要输入账号密码，账号密码去servlet里验证成功后才能进入后台界面。

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>
<h1>管理后台登录</h1>
<form action="<%=request.getContextPath() %>/login" method="post"><!--这里”<%=request.getContextPath() %>/login“的意思是跳转到url为login的地方（前缀与该jsp前缀一致）-->
    u：<input type="text" name="username"/> <br/><br/>
    p：<input type="password" name="password"/> <br/><br/>
    <input type="submit" value="用户登录"/></form>
</body>
</html>
```



```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>

<head>
    <title>后台管理</title>
</head>

<body>
<h1>后台管理</h1>
</body>
</html>

```



> 后台

再做出验证信息的servlet

```java
package _01_filterOut;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class _01_loginCheck extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取用户名和密码
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        if ("123456".equals(password)) {
            //若密码为123456则正确，进行请求转发，转发给admin.jsp，同时分配session
            request.getRequestDispatcher("/FilterOut/_01_admin.jsp").forward(request, response);
            HttpSession session = request.getSession();
            session.setAttribute("username",username);
        }

        else
            //不合法，返回登录界面
            request.getRequestDispatcher("/FilterOut/_01_login.jsp").forward(request,response);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        doGet(request, response);
    }
}

```



> 过滤

在做好基本流程后，添加一个Filter，来进行一层过滤。

```java
package _01_filterOut;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpSession;
import java.io.IOException;

/**
 * 创建filter监听
 */
public class _02_filter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当服务器创建filter后，调用该方法，进行初始化
        System.out.println("filter被创建");

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        //每次调用filter时，都会执行该方法
        //如果不进行放行，则在浏览器里面输入任何url地址都是空白，因为过滤器卡住它了，可以通filterChain.doFilter(servletRequest,servletResponse)来进行放行
        //如果直接放行，则过滤器的意义就没了，所以应该在过滤器设卡，进行账号合法性的判断
        System.out.println("filter被调用");

        //这里设一个判断是否登录过了的卡，效果如下:如果已经登陆过了，则会得到一个服务器分配的session，之后就可以在规定时间内免除登录了，如果没登录过，就先老老实实登录，如果连账号密码都是错的，那必得不到session，则会一直卡在登录界面
        //filter是优先于所有服务器操作的，故浏览器发送请求后，会先找过滤器
        HttpSession session = ((HttpServletRequest)servletRequest).getSession();
        if(session.getAttribute("username") != null){
            filterChain.doFilter(servletRequest,servletResponse);
        }else {
            servletRequest.getRequestDispatcher("/FilterOut/_01_login.jsp").forward(servletRequest,servletResponse);
        }


    }

    @Override
    public void destroy() {
        //销毁filter时调用该方法
        System.out.println("filter被销毁");

    }
}

```



> 配置

下面说明一下配置

先看看上面几个内容该如何配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--filter的配置-->
    <!--filter的配置和servlet的配置大差不差，最大的区别就在于mapping配置的最后一个，url-mapping，表示当发送请求的url只要和url-mapping里的地址一致时，就触发该filter-->
    <!--url-mapping里，"/"表示工程路径，在此处即"http://localhost:8080/_07_Filter"。要是想加入限制，则在/后面加入具体地址即可，表示不是该工程下的所以url都可以触发filter，而是指定路径下的才行-->
    <filter>
        <filter-name>_01_filter</filter-name>
        <filter-class>_01_filterOut._02_filter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>_01_filter</filter-name>
        <url-pattern>/FilterOut/*</url-pattern>
    </filter-mapping>

   
    <servlet>
        <servlet-name>_01_loginCheck</servlet-name>
        <servlet-class>_01_filterOut._01_loginCheck</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>_01_loginCheck</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>


</web-app>
```



> 细节

1、filter在web项目启动时，由tomcat创建filter实例，只会创建一次

2、创建filter实例时，会调用filter的默认无参构造器，同时调用init方法，只会调用一次

3、在创建filter实例时，同时创建一个filterconfig对象，并通过init传入

4、通过filterconfig对象，使用者可以获取该filter的相关配置

5、当一个http请求和filter的url-patter匹配时，就会调用dofilter方法

6、在调用dofilter方法时，tomcat会同时创建servletRequset、servletResponse、FilterChain对象，并作为实参传入进doFilter方法

7、如果后面的请求目标资源（jsp、servlet）需要使用request、response，则filter会将servletRequset、servletResponse向其传入（servletRequset、servletResponse与servlet中使用的request、response是同一个对象）

8、监听器和过滤器的存储方式类似servlet，都是存放在容器中，其会在容器内实例化对象来存放监听器和过滤器的url配置信息，使用时取出。

9、过滤器不会卡请求转发的情况，只在直接访问的时候设卡。



#### 7.2.2 过滤链

过滤链的运行理念和方法嵌套的理念一致，都是一层套一层，最里层的会最先运行结束。

从一个实例看起：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>hi</title>
</head>
<body>
<h1>FilterChain 目录下的 hi.jsp</h1>
<h1>后台管理</h1>
<a href="#">用户列表</a>||<a href="#">添加用户</a>||<a href="#">删除用户</a>
<hr/>
</body>
</html>

```

```java
public class AFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        System.out.println("A前置代码");
        filterChain.doFilter(servletRequest, servletResponse);
        System.out.println("A后置代码");
    }

    @Override
    public void destroy() {

    }
}
```

```java
public class BFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        System.out.println("B前置");
        filterChain.doFilter(servletRequest, servletResponse);
        System.out.println("B后置");
    }

    @Override
    public void destroy() {

    }
}

```



上面定义了一个界面和两个过滤器，从内容上看A过滤器与B过滤器完全没有呼应，因为他们的嵌套是在配置里进行的。下面看看配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
 
    <filter>
        <filter-name>AFilter</filter-name>
        <filter-class>_02_filterChain.AFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>AFilter</filter-name>
        <url-pattern>/FilterChain/*</url-pattern>
    </filter-mapping>
    <filter>
        <filter-name>BFilter</filter-name>
        <filter-class>_02_filterChain.BFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>BFilter</filter-name>
        <url-pattern>/FilterChain/*</url-pattern>
    </filter-mapping>

    <servlet>
        <servlet-name>_01_loginCheck</servlet-name>
        <servlet-class>_01_filterOut._01_loginCheck</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>_01_loginCheck</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>


</web-app>
```

在配置文件里，把A写在了B的前面，则表示B被嵌套在A的里面了，当A运行到` filterChain.doFilter(servletRequest, servletResponse);`时，会进入B，当B运行完后，会再运行A放行语句后面的部分。故最后的输出结果为：

```
A前置；
B前置；
B后置；
A后置；
```



> 细节

1、多个 filter 和目标资源在一次 http 请求，在同一个线程中。

2、当一个请求 url 和 filter 的 url-pattern 匹配时, 才会被执行, 如果有多个匹配上，就会顺序执行，形成一个 filter 调用链。

3、多个 filter 共同执行时,因为是一次 http 请求, 使用同一个 request 对象。

4、多个 filter 执行顺序，和 web.xml 配置顺序保持一致。

5、filterChain.doFilter(req, resp)方法 将执行下一个过滤器的 doFilter 方法, 如果后面没有过滤器，则执行目标资源。

6、注意执行过滤器链时, 顺序是(用前面的案例分析) Http请求 -> A 过滤器 dofilter() -> A 过滤器前置代码 -> A 过滤器 chain.doFilter() -> B 过滤器 dofilter() -> B 过滤器前置代码 -> B过滤器 chain.doFilter() -> 目标文件 -> B过滤器后置代码 -> A过滤器后置代码 -> 返回给浏览器页面/数据。



## 八、Jquery

Jquery是一种将javaScript进行了包装的技术库，其优点在10年之前相当显著，因为Jquery实现了不同浏览器直接的代码兼容问题。

由于Jquery也是一个库，故得从外部下载下来该库然后通过js引入。



### 8.1 事件与对象

Jquery是javaScript的包装，所以Jquery也是写在JavaScript下的，并且javaScript特有的对象这一性质Jquery也有，但是Jquery的对象定义方法与JS差别很大。

> 事件

js和jq绑定事件的思路是一样的，但是语法不同。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery 快速入门</title>
    <!-- 引入 jquery 库-->
    <script type="text/javascript" src="JqueryLib/code.jquery.com_jquery-3.7.0.min.js"></script>
    <script type="text/javascript">
        /**
         * 使用 dom 编程
         * 1. 代码比较麻烦
         * 2. document.getElementById("btn01") 返回的是 dom 对象
         */
        //使用原生 js+dom 完成
        //(1) 当页面加载完毕后，就执行 function
        window.onload = function () {
            //1. 得到 id=btn01 的 dom 对象
            var btn01 = document.getElementById("btn01");
            //2. 绑定点击事件
            btn01.onclick = function () {
                alert("hello, js");
            }
        }
        /**
         * 1. 初次使用 jquery , 会觉得语法比较奇怪，其实 jquery 的底层仍然是 js,只是做了封装
         * 2. $(function () {}) 等价 window.onload = function () {}
         * 3. $() 可以理解成是一个函数 [可以定义 function $(id) {} ...]
         * 3. $("#btn01") 底层: document.getElementById("btn01")
         * 4. 注意 $("#btn01") 不能写成 $("btn01")
         * 5. 通过$("#btn01") 返回的对象就是 jquery 对象(即进行了封装)，而不是原生的 dom 对象
         */

        //使用 jquery
        //1. 引入 jquery 库文件
        //2. $(function(){}) 等价原生的 js 的, 当页面加载完毕就会执行 function(){}
        /*window.onload= function(){}*/

            //1.得到 btn01 这个对象->jquery 对象
            // $btn01 是一个 jquery 对象 其实就是对 dom 对象的包装.
            // 这时我们就可以使用 jquery 对象的方法，事件等待
            // 通过 debug 我们发现 jquery 对象是数组对象.
            //2. jquery 中，获取对象的方法是 $("#id"), 必须在 id 前有#
            //3. 编程中，规定 jquery 对象的命名以$开头.(不是必须，但是约定)
        $(function (){
            var $btn01 = $("#btn02");
            //2.绑定事件
            $btn01.click(function (){
                alert("hello,jquery...~~~")
            })
        });
    </script>
</head>
<body>
<button id="btn01">按钮 1</button>
<button id="btn02">按钮 2</button>
</body>
</html>
```

Jquery的语法相对Js来说几乎就是全新的语法了。



> 对象

刚刚在使用事件时，就已经分别定义过Jquery的dom对象和JS的对象了，

```javascript
var jsDom = document.getElementbyId("XXX");//js对象的定义方式，XXX为某个标签的id
var $JqDom = $("#XXX");//jq的对象定义方式，XXX为某个标签的id
```

而JQ又是JS的包装，所以两者对象直接是能相互转换的



JavaScript转Jquery

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dom对象转换成jquery对象</title>
    <script type="text/javascript" src="JqueryLib/code.jquery.com_jquery-3.7.0.min.js"></script>
    <script type="text/javascript">
        window.onload = function (){
            //先做一个dom对象
            var username = document.getElementById("username");
            alert("username=" + username.value);

            //上节我们知道，jquery对象定义的话应该是:$("#username")
            //但是这里是将已经有的dom对象转成jquery对象，故直接用$(dom对象)即可
            var $username = $(username);
            alert("$username=" + $username.val());
        }
    </script>


</head>
<body>
用户名 <input type="text" id="username" name="username" value="1"/>

</body>
</html>
```



Jquery转Javascript

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Jquery对象转Dom对象</title>
    <script type="text/javascript" src="JqueryLib/code.jquery.com_jquery-3.7.0.min.js"></script>
    <script type="text/javascript">
        window.onload = function (){
            //得到jquery对象
            var $username = $("#username");
            alert("$username=" + $username);

            //jquery对象转Dom方式1
            //jquery对象实际上是一个数组，其内部封装了若干个dom对象（一般只封装一个），可以通过索引来得到具体dom（若只封装了一个dom，则索引用0即可）
            var username = $username[0];
            alert("username=" + username)

            //jquery对象转Dom方式2
            //通过jquery库里的get方式得到具体索引下的对象
            var username1 = $username.get(0);
            alert("username1" + username1)
        }
    </script>
</head>
<body>
用户名 <input type="text" id="username" name="username" value="1"/>
</body>
</html>
```

jQuery转JavaScript的时候有个知识点要注意了，jquery对象是一个数组对象，里面包含若干个dom对象，但是一般只封装一个。



### 8.2 选择器

与js一样，jq也会对各种标签进行选择，选择方式也多种多样，但是都是些见到知道是干啥就行的内容，不用单独记忆，用到就查就行。



### 8.3 标签操作

jq定义好各个标签的对象后，是可以对各个标签进行某种操作的。

#### 8.3.1 修改属性

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="../JqueryLib/code.jquery.com_jquery-3.7.0.min.js"></script>
    <script type="text/javascript">
        $(function(){
            $("#bt1").click(function (){
                //绑定到id=bt1的标签，然后将该标签的value属性内容改为”change“
                $("#bt1").attr("value","change")
            })
        })
    </script>
</head>
<body>
<input type="button" value="更改属性" id="bt1">
</body>
</html>
```



#### 8.3.2 创建标签

jq甚至可以将对象定义在一个待建标签上，然后对该待建标签做各种操作。

```javascript
var $jqDom = $("<div id=\"cq\" name=\"chongqing\">标签内容</div>");
```

这样就相当于做了一个新标签绑定到了jqDom对象上，然后就可以对该标签的位置信息进行定义了，也就引出了下面的插入标签



#### 8.3.3 插入标签

jq里插入标签分为外插和内插。内插的标签会变为被插标签的子标签；外插的标签则与被插的标签同级。实例举例就是：

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        div, span {
            width: 140px;
            height: 140px;
            margin: 20px;
            background: #9999CC;
            border: #000 1px solid;
            float: left;
            font-size: 17px;
            font-family: Roman;
        }
        div.mini {
            width: 30px;
            height: 30px;
            background: #CC66FF;
            border: #000 1px solid;
            font-size: 12px;
            font-family: Roman;
        }
    </style>
    <script type="text/javascript" src="../JqueryLib/code.jquery.com_jquery-3.7.0.min.js"></script>
    <script type="text/javascript">
        $(function () {
            //传统Dom方法
            $("#b1").click(function () {
                //1、创建li标签
                var cq = document.createElement("li");
                //2、给li标签定义属性
                cq.setAttribute("id","cq");
                cq.setAttribute("name","chongqing");
                cq.innerText = "重庆";
                //3、把重庆添加到指定元素后面--以上海为例
                document.getElementById("sh").append(cq);
            })

            //jquery方法
            $("#b2").click(function () {
                var $cq = $("<li id=\"cq\" name=\"chongqing\">重庆</li>");
                $("#sh").append($cq)
                //$cq.insertAfter($("#sh"));//或者使用insertAfter讲cq加入sh后面，但是这是外部插入，能让cq与sh平级，而用appen的话cq是sh子级
            })


            //换一个情景，将成都加入到北京前面
            $("#b3").click(function () {
                var $cd = $("<li id=\"cd\" name=\"chongqing\">成都</li>");
                $cd.insertBefore($("#bj")) //用外部插入的话，才能保证城市前面的点存在
                //$("#bj").append($cd); 内插不行
            })

        })
    </script>
</head>
<body>
<ul id="city">
    <li id="bj" name="beijing">北京</li>
    <li id="sh" name="shanghai">上海</li>
    <li id="jl" name="jilin">吉林</li>
    <li id="my" name="mianyang">绵阳</li>
</ul>
<input type="button" id="b6" onclick="test1()" value="添加重庆到上海下(使用dom的传统方法)"/>
<br/>
<br/>
<input type="button" id="b1" value="添加重庆 到 上海下(dom)"/><br/><br/>
<input type="button" id="b2" value="添加重庆 到 上海下(jquery)"/><br/><br/>
<input type="button" id="b3" value="添加成都 到 北京前"/><br/><br/>
<input type="button" id="b4" value="添加成都 到 北京和重庆之间"/><br/><br/>
<input type="button" id="b5" value="添加成都 到 吉林前面"/><br/>
</body>
</html>
```





## 九、Json

Json实际上是一门独立于java整个体系的语言，像php、go等语言都是可以用Json的。

在java中，Json更多是构成前后端对象直接沟通的桥梁。并且Json是写在Js下的





### 9.1 定义

Json的使用通常是将Json先定义出一个对象，该对象内有各种属性（属性由“字典”定义），其定义方式如下：

```javascript
var 变量名 = {
	"k1" : value, // Number 类型
	"k2" : "value", // 字符串类型
	"k3" : [],// 数组类型
	"k4" : {}, // json 对象类型
	"k5" : [{},{}] // json 数组
};
```

相当于python里的字典形式，一个key对应一个value。

其实例如下：

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function () {
        //定义一个Json对象
            var myJson = {
                "key1": "helloworld", // 字符串
                "key2": 123, // Number
                "key3": [1, "hello", 2.3], // 数组
                "key4": {"age": 12, "name": "jack"}, //json 对象
                "key5": [ //json 数组
                    {"k1": 10, "k2": "milan"},
                    {"k3": 30, "k4": "smith"}
                ]
            };

            //取出key
            alert("key1 = " + myJson.key1)
            alert("key2 = " + myJson.key2)
            alert("key3 = " + myJson.key3)//得到整个数组的情况
            alert("key3 = " + myJson.key3[2])//取出key3的数组里的某个具体值
            alert("key4 = " + myJson.key4)//得到整个字典里的数据类型，此处为两个object
            alert("key4 = " + myJson.key4.age)//取key下面的key来得到具体的value
            alert("key5 = " + myJson.key5)
            alert("key5 = " + myJson.key5[0].k1)//当取json数组下面的json时，先用索引定义到大括号的位置，再通过key得到具体value
        }
    </script>
</head>
<body>

</body>
</html>
```



### 9.2 转换

前面说过，Json是搭建起了前端和后端对象相互沟通的桥梁，也就是说，后端定义的对象是可以通过Json传入前端的，同理前端的对象也可以传入后端。

但是在前后端转换之前，要先知道Json在前端如何实现Json内容和字符串之间的转换。



#### 9.2.1 Json和字符串

Json提供了两个方法：Stringfly和parse。前者用来将Json对象转成字符串，后者则将字符串转为Json对象。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
    //JSON 是JavaScript的内置对象，该对象有两个方法  ：其中一个就是Stringify，用来讲json对象转为字符串;另一个是Parse，用来将字符串转成Json对象
    //1、Json对象转String
    var jsonPerson = {
        "name":"jack",
        "age":20
    }
    alert(jsonPerson)

    var StringPerson = JSON.stringify(jsonPerson)
    alert(StringPerson)


    //2、String转Json，String想转Json，一定要让String的格式是能转成Json的格式
    var StringDog = "{\"name\":\"jack\",\n" + "\"age\":20}"
    var JsonDog = JSON.parse(StringDog)
    alert(StringDog)
    alert(JsonDog)

  
  </script>
</head>
<body>

</body>
</html>
```

当想让String转成Json对象时，要注意String的格式一定要是能满足Json的格式。

要注意，通过Stringify、parse两种方法进行转换后，不影响原对象，即字符串转Json对象后，原字符串还存在，反之亦然可以理解为数据类型的转换：`int n = 1;double m = (double)n`，转换完后，n也存在、m也存在。



#### 9.2.2 前端后端转换

java对象转json对象有大概两种：javabean对象转Json对象、list对象转Json对象。

> javabean转json

java对象和json对象可以相互转换：java对象可转为json字符串，然后通过response等方式传给前端去解析出该字符串对应的json对象；java也可通过request得到json字符串后转为java对象。这些操作都需要通过第三方库——Gson提供的方法来完成。

```java
//先简单做一个javabean的原型
package _01_JavaToJSON;

public class _01_person {
    private String name;
    private int age;

    public _01_person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void run(){
        System.out.println("run");
    }


}

```

```java
package _01_JavaToJSON;

import com.google.gson.Gson;
import com.google.gson.reflect.TypeToken;
import com.sun.xml.internal.ws.api.model.wsdl.WSDLOutput;

import java.lang.reflect.Type;
import java.util.ArrayList;
import java.util.List;


public class _02_toJson {
    //进行json和java的沟通

    public static void main(String[] args) {

        //1、创建一个gson对象，作为一个工具对象使用，该对象由gson包提供
        Gson gson = new Gson();

        //2、做一个java对象
        _01_person person = new _01_person("jack",20);

        //3、java对象转json字符串（转完json字符串后，该字符串再从前端转成json对象）
        String strPerson = gson.toJson(person);//用toJson方法来将java对象转为字符串以便向Json输出，下面fromJson相反
        System.out.println(strPerson);//此处输出的是一个字符串形式的内容

        //4、json字符串转java对象
        _01_person person1 = gson.fromJson(strPerson,_01_person.class);//通过fromJson方法将json字符串转成java对象，后面要指定转成哪个类
        System.out.println(person1);//此处输出的是一个java对象
    }
}
```



> list转Json对象

list转起来要相对麻烦点，因为list本身就是一个类了，而list里面装的又是另一个类的对象，所以在字符串转java对象时反射不好反射。

此时需要用到Gson里提供的Typetoken类中的type方法来得到list的地址，从而使用fromJson方法来得到java对象。

```java
package _01_JavaToJSON;

import com.google.gson.Gson;
import com.google.gson.reflect.TypeToken;
import com.sun.xml.internal.ws.api.model.wsdl.WSDLOutput;

import java.lang.reflect.Type;
import java.util.ArrayList;
import java.util.List;


public class _02_toJson {
    //进行json和java的沟通

    public static void main(String[] args) {

        //创建一个gson对象，作为一个工具对象使用，该对象由gson包提供
        Gson gson = new Gson();

        //1、list对象转json字符
        List<_01_person> personList = new ArrayList<>();
        personList.add(new _01_person("tom",12));
        personList.add(new _01_person("smith",13));

        String strlistPseron = gson.toJson(personList);//将list转成json字符的底层逻辑是，遍历list，进行逐个转换，之后进行拼接
        System.out.println(strlistPseron);

        //2、json转list，此处要复杂一点，因为list本身就是一个类，然后这个list里又要指定好person类，算是一个复合的类型，故不能直接通过fromJson方法来进行json转java
        //要通过一个typeToken对象来进行一个中转
        TypeToken<List<_01_person>> typeToken = new TypeToken<List<_01_person>>(){};//此处必须得加一个大括号，因为若不加大括号，相当于是调用typetoken类里的无参构造器，而typetoken的无参构造器是protect的，不能从外部直接调用。
        //加了一个大括号后，此处实例化的就是一个继承了typeToken的匿名内部类，而匿名内部类的实例化是靠父类的构造器的（并且可以直接访问父类的protect类型构造器），
        //故这里通过一个没有方法体的typetoken类下的匿名内部类（该内部类由于继承了typetoken而自己又没有方法体，故约等于是完全的typetoken类，拥有typetoken的全部属性和方法）
        //绕过了typetokne的受保护的构造器，完成typetoken的实例化。
        Type type = typeToken.getType();//通过gettype方法得到typetoken的泛型的具体类的地址
        System.out.println(type);//通过typetoken来得到一个具体的java类的class类型数据，然后将该路径传入fromjson方法，让其知道该把json字符串转成到底哪个类
        List<_01_person> personList1 = gson.fromJson(strlistPseron,type);
        System.out.println(personList1);

    }
}

```



## 十、Ajax

Ajax是一种局部请求与响应的操作，就是说向请求某个服务，不必一定要去浏览器里重新输入一个url、或者提交某个界面转到另一个界面，而是可以通过ajax方法，在一个界面的局部地区发送请求，让响应响应在界面的局部地区。

Ajax的核心是一个叫`XMLHttprequset`的对象，该对象的方法和属性构成了ajax的整个操作。简单举个例子，并有如下流程：

![image-20230907220001628](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20230907220001628.png)



### 10.1 JS实现Ajax

举一套完整的例子，从数据库到服务器到浏览器全程：Domain（某个内容类）——>DB（数据库，装载Domain对象的信息，此处先不写）——>DAO（操作数据库的方法（增删改查等））——>Serivice（花式调取DAO来操作数据库（怎么增、怎么删、怎么改、怎么查等））——>servlet（花式调取serivice，拿到数据库的信息后的操作）——>前端。

> Domain

```java
package _02_Ajax.domain;

/**
 * 这里做一个登录界面所需信息的java映射，即常规意义上的javabean
 */
public class _01_User {
    private Integer id;
    private String name;
    private String pwd;
    private String email;

    public _01_User() {
    }

    public _01_User(Integer id, String name, String pwd, String email) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
        this.email = email;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}

```



> Serivice

```java
package _02_Ajax.Service;

import _02_Ajax.Dao.UserDao;
import _02_Ajax.domain._01_User;

public class UserService {
    UserDao userDao = new UserDao();

    public _01_User getUserByName(String username){
        _01_User user = userDao.querySingle("select * from `ajaxuser` where username=?", _01_User.class, username);
        return user;
    }

}
```



> Servlcet

```java
package _02_Ajax.servlet;

import _02_Ajax.Service.UserService;
import _02_Ajax.domain._01_User;
import com.google.gson.Gson;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;

public class _02_CheckServlet extends HttpServlet {

    UserService userService = new UserService();
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.addHeader(  "Access-Control-Allow-Origin","*");//允许所有来源访同
        response.addHeader(  "Access-Control-Allow-Method","POST,GET");//允许访问的方式
        //这里是单独加的，跟视频无关。因为html的端口是6965、tomcat是8080，进行了跨域，不知道得怎么调，故在这里加了个跨域可行的代码

        response.setContentType("text/html;charset=utf-8");

        //1、得到请求里的用户名
        String uname = request.getParameter("username");//将qian'du发送的请求里的uname信息取出

        //2、对用户名加限制，如果用户名是XXX，则不予通过；或与数据库中已有name重合，也不予通过
        _01_User user = userService.getUserByName(uname);
        if (user != null){//如果user不为空，说明该user存在，则返回该user的json格式
            Gson gson = new Gson();
            String s = gson.toJson(user);
            response.getWriter().write(s);
        }else {
            response.getWriter().write("");
        }


    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        doGet(request,response);
    }
}
```

注:此处有一个Utils包和Dao包没有写，不重要。



实际上后端部分也就是最基本的流程，没啥特别，主要前端变化大。



> 前端

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>用户注册</title>
    <script type="text/javascript">
        window.onload = function () {
            var checkButton = document.getElementById("checkButton")
            checkButton.onclick = function (){
                //1、创建XMLHttpRequest对象（Ajax引擎对象）
                var xhr = new XMLHttpRequest();

                //获取用户填写的用户名
                var uname = document.getElementById("uname").value;

                //2、准备发送指定数据:open、send方法
                xhr.open("GET","http://localhost:8080/_09_Json_Ajax/check?username=" + uname,true)
                //open方法是ajax对像规范转发请求的方法，用该方法来向servlet发送请求。open有三个参数：get表示发送的请求格式、第二个表示发送的请求的内容、第三个表示是否为处理（一般都是true）、
                //此时请求并没有发布出去，而是定义好了请求的具体格式

                //4、在send方法调启动前，给xht绑定一个事件：onreadystatechange。该事件表示，可以去指定一个函数，当xhr变化时，会触发该事件。xhr有0、1、2、3、4共五种状态，3是请求处理中，2是请求已接受、4是响应完成
                //这里实际上完成的就是局部刷新的任务
                xhr.onreadystatechange = function () {
                    var responseText = xhr.responseText;
                    console.log(xhr)
                    if(xhr.readyState == 4 && xhr.status == 200){//取出完全响应后的响应内容
                        var responseText = xhr.responseText;
                        //把返回的响应信息展示在div中
                        document.getElementById("div1").innerText = responseText;
                        if(responseText != ""){//若取出的响应不为空，证明是非法字符
                            document.getElementById("myres").value = "用户名不可用"
                        }else {//若响应内容为空，则证明是合法字符，用户名可用
                            document.getElementById("myres").value = "用户名可用"
                        }
                    }
                }

                //3、正式发送请求
                xhr.send()
                //send方法是向下一级发送请求的方法（这里是发送给_02_checkServlet），其有个细节，当发送的请求格式被open定义为get之后，此处send是不用写内容的，因为具体的请求信息在get请求的url后面会有
                //但是如果是post请求，则open里的url部分只有"http://localhost:8080/_09_Json_Ajax/check"，后面的"username=" + uname则写在send里（因为post请求的url是不应该包含信息的）
            }
        }
    </script>
</head>
<body>
<h1>用户注册</h1>
<form action="http://localhost:8080/_09_Json_Ajax/check" method="post">
    用户名字:<input type="text" name="username" id="uname">
    <input type="button" id="checkButton" value="验证用户名">
    <input style="border-width: 0;color: red" type="text" id="      myres"><br/><br/><!--隐藏格，用来提示用户名不合法-->
    用户密码:<input type="password" name="password"><br/><br/>
    电子邮件:<input type="text" name="email"><br/><br/>
    <input type="submit" value="用户注册">
</form>
<h1>返回的 json 数据</h1>
<div id="div1"></div>
</body>
</html>
```



### 10.2 Jquery实现Ajax





## 十一、 ThreadLocal

threadlocal相关知识算是一个补充内容了，独立于其他知识。

### 11.1 源码分析

```java
public class Dog{
    
}//随便建一个domain类
```

```java
public class run{
    public static void mian(String[] args){
        Dog dog = new Dog();//实例化domain类的对象，准备放入thread中
		Threadlocal<Dog> threadlocalDog = new threadLocal<>();//先新建一个threadlocal对象，泛型就定义为Dog类
		threadlocal.set(dog);//调用threadlocal的set方法。ctrl+B进入该方法
    }

}

```



在分析源码前，先搞清楚所属关系：

首先看ThreadLocal类的关系：ThreadLocal类是主类，该类里有一个内部类叫ThreadLocalMap，ThreadLocalMap类里又有一个内部类叫Entry。

之后就可以看全局的关系了：最大的是线程（Thread），线程里维护了一个map类叫ThreadLocalMap，该map实际上是ThreadLocal类的内部类，并且该map类实例化后叫做ThreadLocals，里面存放的是ThreadLocalMap的内部类——Entry类的实例化对象。而Entry里就存放键值对，key是ThreadLocal、value就是该ThreadLocal通过set方法放进去的对象。

```java
public void set(T value) {//传入泛型指定的类的对象
    Thread t = Thread.currentThread();//获取当前threadlocal对象——ThreadlocalDog所处在的线程
    ThreadLocalMap map = getMap(t);//获取当前线程维护的ThreadLocalMap
    if (map != null) {//如果线程里已经有Map了
        map.set(this, value);//则直接在map里set进this和value。其中this就是调用set方法的对象——ThreadLocalDog，value就是dog对象。这一组键值对会存放在ThreadLocalMap里维护的Entry表里。
    } else {
        createMap(t, value);//如果当前线程还没有创建Map，就调用creatMap方法，ctrl+B进入该方法
    }
}
```

```java
void createMap(Thread t, T firstValue) {//传入当前线程，与set的value值——dog对象
    t.threadLocals = new ThreadLocalMap(this, firstValue);//将线程里的threadLocals属性通过ThreadLocalMap类的构造器新建出来，传入的参数为当前threadlocalDog对象与dog对象，而该有参构造器则会直接在map里维护的entry表中添加一组键值对——this（threadLocalDog),dog对象
}
```



## 十二、文件上传与下载





# 项目

这里做一个大点的项目，完成一个家具商城的全流程。

具体流程从上层到下层如下：

前端界面（web）——>web服务器（Servlet）——>具体服务（Service）——>数据库操作（Dao）——>javaBean类<——数据库（mysql）

实现的时候，从底层向上层实现。下面会按照底层向上层的顺序来写出整个项目（这实际上并不是正式写项目的顺序，而是这样方便总结）



## 一、Utils

先看看整个项目需要的工具包都有哪些。

### 1.1 JDBCUtils

最核心的工具包，用来连接后端和数据库的工具。

```java
package JiajuUtils;

import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/**
 * @author 韩顺平
 * @version 1.0
 * 基于druid数据库连接池的工具类
 */
public class JDBCUtilsByDruid {

    private static DataSource ds;

    //定义一个存放连接Connection的线程ThreadLocal
    private static ThreadLocal<Connection> connectionThreadLocal = new ThreadLocal<>();



    //在静态代码块完成 ds初始化
    static {
        Properties properties = new Properties();
        try {
            //web项目的工作路径在out下，不再src下，故该路径得用类加载器
            properties.load(JDBCUtilsByDruid.class.getClassLoader().getResourceAsStream("druid.properties"));
            //properties.load(new FileInputStream("src\\druid.properties"));
            ds = DruidDataSourceFactory.createDataSource(properties);
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    //编写getConnection方法
    //从线程里获得connection，从而包装一个线程里的连接是同一个连接
    public static Connection getConnection()  {
        Connection connection = connectionThreadLocal.get();//尝试从线程里获得连接
        if (connection == null){//如果没获得到，表示现在线程里还么有连接，则放一个连接进去

            try {
                connection = ds.getConnection();

                connection.setAutoCommit(false);//阻止连接自动提交，改为手动提交
            } catch (SQLException e) {
                e.printStackTrace();
            }
            connectionThreadLocal.set(connection);//从连接池中取一个连接放入threadLocal中
        }

        return connection;
    }

    //关闭连接, 再次强调： 在数据库连接池技术中，close 不是真的断掉连接
    //而是把使用的Connection对象放回连接池
    public static void close(ResultSet resultSet, Statement statement, Connection connection) {

        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    //编写事务提交的方法
    public static void commit(){

        Connection connection = connectionThreadLocal.get();//得到线程里的连接
        if (connection != null){//若线程是确实是有连接的，则把连接提交
            try {
                connection.commit();
            } catch (SQLException e) {
                e.printStackTrace();
            }finally {
                try {
                    connection.close();//提交完后将连接还给连接池
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        connectionThreadLocal.remove();//让线程移除这个还给了连接池的连接
    }

    //提供回滚事务的方法
    public static void rollBack(){
        Connection connection = connectionThreadLocal.get();
        if (connection != null){

            try {
                connection.rollback();
            } catch (SQLException e) {
                e.printStackTrace();
            }finally {
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        connectionThreadLocal.remove();

    }
}

```



### 1.2 datautils

该工具包用来实现简易的封装流程，将前端读取到的信息直接通过该包做成一个javabean对象，从而简化正面的代码量。

还提供了一个将string转成int的方法

```java
package JiajuUtils;

import org.apache.commons.beanutils.BeanUtils;

import java.util.Map;

/**
 * 封装工具
 */
public class DataUtils {

    /*
    将前端标签里的值封装成javabean对象
     */
    public static <T> T copyParamToBean( T bean ,Map value ){
        try {
            //使用BeanUtils这个外部包的populate方法，传入需要封装的bean、value是request请求里带的parameter参数值的集合
            //这一步是将这个参数集合按顺序封装近javabean的属性里
            //但是有一点要注意，前端里表单中的数据字段名一定要和javabean里的属性名一致（因为底层也是用的反射机制，要求名称一一对应）
            BeanUtils.populate(bean,value);
        }catch (Exception e){
            e.printStackTrace();
        }
        //这里返回的bean对象实际上就是传入的bean对象，但是区别是传入的bean对象是无参构造器构造的，属性值都是0或默认，通过populate操作后，变成了封装好的有属性的bean对象返回出去了。
        return bean;
    }

    public static int parseInt(String val, int defaultVal){//将输入的字符串转成int，转换失败就返回defaultval

        try {
            return Integer.parseInt(val);
        }catch (NumberFormatException e){
            System.out.println("格式不正确");
        }
        return defaultVal;


    }
}
```



### 1.3 ajaxutils

提供一个判断请求是不是ajax请求的方法，主要是为了处理ajax请求让过滤器失效这一问题的。

```java
package JiajuUtils;

import javax.servlet.http.HttpServletRequest;

public class WebUtils {

    //Ajax请求会使过滤器的请求转发失效，因此要提供一个判断请求是不是Ajax的工具，来恢复被ajax失效掉的请求转发
    public static boolean isAjaxRequest(HttpServletRequest request){
        return "XMLHttpRequest".equals(request.getHeader("X-Requested-With"));//Ajax特有的请求头，看看请求头里是否有该串字符，如有，就是Ajax请求
    }
}
```



## 二、javabean

完成一个商城项目，需要以下几个结构：用户、家具、购物车、订单、分页（数据分页视为类来操作），javabean是对接数据库的，即都哪些信息要存放在数据库中，就把谁做成一个javabean。

### 2.1 用户（Member）

用户的情况简单，就用户id、用户名、密码、邮箱这几个属性。每一个用户信息都会存放在数据库中。

```java
package javabean;

public class Member {
    private Integer id;//这里id使用integer而别用int，因为有时候可能会传空进入，让主键自增，而int不能接受空值
    private String username;
    private String password;
    private String email;

    public Member(){};//创建一个无参构造器以供之后反射使用


    public Member(Integer id, String username, String password, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```





### 2.2 家具（Furn）

家具商城，家具信息肯定也要存放在数据库中，主要属性为：家具id、家具姓名、家具制造商、家具售价、家具销售量、家具存量。

```java
package javabean;

import java.math.BigDecimal;

public class Furn {
    private Integer id;
    private String name;
    private String maker;
    private BigDecimal price;//BigDecimal是一种大容量的数据
    private Integer sales;
    private Integer stock;

    //以后有可能会有图片路径传空的情况，为了以后方便处理，这里做一次判断，如果构造javabean时路径传空了，则赋默认值
    private String imgPath = "assets/images/product-image/default.jpg";

    public Furn(){};
    public Furn(Integer id, String name, String maker, BigDecimal price, Integer sales, Integer stock, String imgPath) {
        this.id = id;
        this.name = name;
        this.maker = maker;
        this.price = price;
        this.sales = sales;
        this.stock = stock;
        //若传图片路径的值了，则用这个值覆盖调默认值
        if(!(null == imgPath || "".equals(imgPath))) this.imgPath = imgPath;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getMaker() {
        return maker;
    }

    public void setMaker(String maker) {
        this.maker = maker;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public Integer getSales() {
        return sales;
    }

    public void setSales(Integer sales) {
        this.sales = sales;
    }

    public Integer getStock() {
        return stock;
    }

    public void setStock(Integer stock) {
        this.stock = stock;
    }

    public String getImgPath() {
        return imgPath;
    }

    public void setImgPath(String imgPath) {
        this.imgPath = imgPath;
    }

    @Override
    public String toString() {
        return "Furn{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", maker='" + maker + '\'' +
                ", price=" + price +
                ", sales=" + sales +
                ", stock=" + stock +
                ", imgPath='" + imgPath + '\'' +
                '}';
    }
}
```



### 3.3 分页信息（page）

这个有点抽象，要把分页信息做成一个javabean类来看待。这个分页信息是不需要对接数据库的，他只是用来方便管理信息列表。分页bean实际上就是furnbean的升级版，因为pagebean里有一个list属性，专门存放具体furn。到后面使用时就会明了了。

```java
package javabean;

import java.util.List;

/**
 * 将分页信息作为一个javabean来对待
 * 这里将page类做成泛型，以为可能会为员工表分页、也可能为家具表分页，最后分谁传谁就行
 */
public class Page<T> {

    //显示每页有几条记录其他地方也可能用的到，故设成常量
    public static final Integer PAGE_SIZE = 4;

    private Integer pageNo;//表示显示当前页面的值（显示是第几页）
    private Integer pageSize = PAGE_SIZE;//表示每页显示几条记录，先默认赋值上面的常量
    private Integer totalRow;//表示共有多少条信息
    private Integer pageTotalCount;//表示共有多少页，由totalRow÷pageSize得到

    private List<T> items;//表示当前页面要展示的具体数据

    private String url;//用于分页导航条的字符串

    public Page(){

    }

    public Page(Integer pageNo, Integer pageSize, Integer totalRow, Integer pageTotalCount, List<T> items, String url) {
        this.pageNo = pageNo;
        this.pageSize = pageSize;
        this.totalRow = totalRow;
        this.pageTotalCount = pageTotalCount;
        this.items = items;
        this.url = url;
    }

    public Integer getPageNo() {
        return pageNo;
    }

    public void setPageNo(Integer pageNo) {
        this.pageNo = pageNo;
    }

    public Integer getPageSize() {
        return pageSize;
    }

    public void setPageSize(Integer pageSize) {
        this.pageSize = pageSize;
    }

    public Integer getTotalRow() {
        return totalRow;
    }

    public void setTotalRow(Integer totalRow) {
        this.totalRow = totalRow;
    }

    public Integer getPageTotalCount() {
        return pageTotalCount;
    }

    public void setPageTotalCount(Integer pageTotalCount) {
        this.pageTotalCount = pageTotalCount;
    }

    public List<T> getItems() {
        return items;
    }

    public void setItems(List<T> items) {
        this.items = items;
    }

    public String getUrl() {
        return url;
    }

    public void setUrl(String url) {
        this.url = url;
    }

    @Override
    public String toString() {
        return "page{" +
                "pageNo=" + pageNo +
                ", pageSize=" + pageSize +
                ", totalRow=" + totalRow +
                ", pageTotalCount=" + pageTotalCount +
                ", items=" + items +
                ", url='" + url + '\'' +
                '}';
    }
}

```



### 4.4 购物车（cart）

这个项目中，购物车信息使用session来保存，不向数据库中进行记录，即每次打开服务器后，购物车记录都清空（类似美团点外卖时）。所以这里也是不接入数据库的。



一个购物车里可能会存放多种类型的家具，每个家具又可能存放多个，这部分代码表示的是每个家具的信息。由以下属性 组成：家具id、家具姓名、家具单价、家具数量、家具总价。如向购物车添加了两个桌子，则会给桌子做一个cartItem对象，这个对象中记录桌子的单价，两个桌子的总价这些信息。

```java
package javabean;

import java.math.BigDecimal;

/**
 * 表示购物车里家具的数据
 */
public class CartItem {
    private Integer id;
    private String name;
    private BigDecimal price;
    private Integer count;
    private BigDecimal totalPrice;

    public CartItem() {
    }

    public CartItem(Integer id, String name, BigDecimal price, Integer count, BigDecimal totalPrice) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.count = count;
        this.totalPrice = totalPrice;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public Integer getCount() {
        return count;
    }

    public void setCount(Integer count) {
        this.count = count;
    }

    public BigDecimal getTotalPrice() {
        return totalPrice;
    }

    public void setTotalPrice(BigDecimal totalPrice) {
        this.totalPrice = totalPrice;
    }
}

```



这个bean则是表示购物车里全部的家具情况，它的核心属性就一个：HsahMap<integer,cartItem>，用来记录多个cartItem，如添加了两个桌子和三个椅子，两个桌子和三个椅子分别对应自己的cartitem对象，然后cart对象中则是直接把这两个cartitem对象放入自己的hashmap中，用来记录购物车一共有多少种物品。

cartbean类种，不仅定义了属性，还将具体操作方法也进行了记录，因为不介入数据库，所以直接在这里操作也可以，方便一点。提供了一些购物车的核心方法：添加方法、计算购物车中物品总量的方法、计算购物车中总价钱的方法等等。

```java
package javabean;

import java.math.BigDecimal;
import java.math.BigInteger;
import java.util.HashMap;
import java.util.Set;

/**
 * 这里是购物车，将整个购物车视为一个javaBean（类似Page），其内部包含了CartItem（类比ThreadLocal的思路）
 */
public class Cart {


    //定义一个属性，就是这个哈希表。
    private HashMap<Integer, CartItem> items = new HashMap<>();//设定一个哈希表来存放cartItem数据，k-v：key是id，v就是id对应的家具

    //直接再类里提供一个添加数据的方法
    public void addItem(CartItem cartItem){
        //判断是否可以添加此数据
        CartItem item = items.get(cartItem.getId());//先尝试从哈希表里取出传入的cartItem的id，若取不出，则代表表里还没有这个数据，可以添加
        if (null == item){
            items.put(cartItem.getId(),cartItem);
        }else {//若购物车里已经有这个数据了，代表之前添加过一次这个数据，再次添加则表示买两个，那么数量和价格都要改变
            item.setCount(item.getCount() + 1);//数量在原有的基础上加一
            item.setTotalPrice(item.getPrice().multiply(new BigDecimal(item.getCount())));//价格直接拿单价×数量得到当前总价（也可也拿上一时刻的总价加上一个单价的值，但是要保证加如的数据数量只有一才行）

        }

    }

    public Integer getTotalCount(){
        int totalCount = 0;
        //遍历哈希表，计算每个词条的总量，求和得到整个购物车的总量
        Set<Integer> keys = items.keySet();//取出哈希表里的所有key，放入集合中
        for (Integer id : keys){
            totalCount += ((CartItem)items.get(id)).getCount();
        }

        return totalCount;

    }

    //获得当前购物车里所有东西的总价
    public BigDecimal getCartTotalPrice() {
        BigDecimal CartTotalPrice = new BigDecimal(0);//初始化为0

        Set<Integer> keys = items.keySet();
        for (Integer id : keys){
            CartItem cartItem = items.get(id);
            CartTotalPrice = CartTotalPrice.add(cartItem.getTotalPrice());
        }
        return CartTotalPrice;
    }

    //修改指定cartItem的数量和总价
    public void updateItemCount(int id , int count){
        CartItem cartItem = items.get(id);
        if (null != cartItem){
            //更新当前词条数量
            cartItem.setCount(count);
            //更新当前词条总价
            cartItem.setTotalPrice(cartItem.getPrice().multiply(new BigDecimal(cartItem.getCount())));
        }

    }

    //删除指定CartItem
    public void deleteItem(int id){
        items.remove(id);
    }

    //清空购物车
    public void clean(){
        items.clear();
    }

    public HashMap<Integer, CartItem> getItems() {
        return items;
    }

    public void setItems(HashMap<Integer, CartItem> items) {
        this.items = items;
    }



}

```



### 5.5 订单（order）

订单是接入数据库的信息，结构类似购物车，由两部分组成，一部分是大的，订单的整体信息：订单号、订单生成时间、订单金额、订单状态、订单对应的会员。

```java
package javabean;

import java.math.BigDecimal;
import java.util.Date;
import java.util.HashMap;
import java.util.Timer;

/*
`id` VARCHAR(64) PRIMARY KEY, -- 订单号
`create_time` DATETIME NOT NULL, -- 订单生成时间
`price` DECIMAL(11,2) NOT NULL, -- 订单的金额
`status` TINYINT NOT NULL, -- 状态 0 未发货 1 已发货 2 已结账
`member_id` INT NOT NULL -- 该订单对应的会员id
 */
public class Order {
    private String id;
    private Date date;
    private BigDecimal price;
    private Integer status;
    private Integer memberId;


    public Order() {
    }

    public Order(String id, Date date, BigDecimal price, Integer status, Integer memberId) {
        this.id = id;
        this.date = date;
        this.price = price;
        this.status = status;
        this.memberId = memberId;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public Date getDate() {
        return date;
    }

    public void setDate(Date date) {
        this.date = date;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    public Integer getMemberId() {
        return memberId;
    }

    public void setMemberId(Integer memberId) {
        this.memberId = memberId;
    }
}

```



还有一部分就是细节，即订单具体信息，但是与购物车不同的是，订单具体信息没有存放在订单整体信息中，即两者是没有关联的。

```java
package javabean;

import java.math.BigDecimal;

public class OrderItem {
    private Integer id;
    private String name;
    private BigDecimal price;
    private Integer count;
    private BigDecimal totalPrice;
    private String orderId;

    public OrderItem() {
    }

    public OrderItem(Integer id, String name, BigDecimal price, Integer count, BigDecimal totalPrice, String orderId) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.count = count;
        this.totalPrice = totalPrice;
        this.orderId = orderId;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public BigDecimal getPrice() {
        return price;
    }

    public void setPrice(BigDecimal price) {
        this.price = price;
    }

    public Integer getCount() {
        return count;
    }

    public void setCount(Integer count) {
        this.count = count;
    }

    public BigDecimal getTotalPrice() {
        return totalPrice;
    }

    public void setTotalPrice(BigDecimal totalPrice) {
        this.totalPrice = totalPrice;
    }

    public String getOrderId() {
        return orderId;
    }

    public void setOrderId(String orderId) {
        this.orderId = orderId;
    }
}

```



## 三、Dao

Dao层是处理数据库与javabean之间信息的，主要完成如：将数据库信息提取为javabean对象、将javabean对象信息保存在数据库中等操作。

在实际使用中，Dao层一般分为三部分：basicDao类（具体的数据库操作方法），javabeanDao接口（为每个连接数据库的javabean都单独做一个Dao，该Dao继承basicDao），javabeanDaoImplement类（该类实现具体的javabeanDao接口）。



### 3.1 basicDao

核心Dao，要在这里完成数据库与javabean的对接，这里理所应当的会继承JDBCUtilsByDruid这个工具包，因为要完成数据库的连接。

这里提供了：更新数据库的操作（传入sql语句和具体的更新参数，即实现javabean信息返回数据库的过程）、查找数据库的操作（传入sql语句、需要返回的数据的类型、具体的查找参数，即实现了数据库信息提取成javabean的操作）、查找单个数据的操作（原理同上）、查找具体值的操作（同上）。

```java
package dao;


import JiajuUtils.JDBCUtilsByDruid;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;

import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

/**
 * 开发BasicDAO , 是其他DAO的父类
 */
public class BasicDAO<T> { //泛型指定具体类型

    private QueryRunner qr =  new QueryRunner();

    //开发通用的dml方法, 针对任意的表
    public int update(String sql, Object... parameters) {

        Connection connection = null;

        try {
            connection = JDBCUtilsByDruid.getConnection();
            int update = qr.update(connection, sql, parameters);
            return  update;
        } catch (SQLException e) {
           throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        }

    }

    //返回多个对象(即查询的结果是多行), 针对任意表

    /**
     *
     * @param sql sql 语句，可以有 ?
     * @param clazz 传入一个类的Class对象 比如 Actor.class
     * @param parameters 传入 ? 的具体的值，可以是多个
     * @return 根据Actor.class 返回对应的 ArrayList 集合
     */
    public List<T> queryMulti(String sql, Class<T> clazz, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return qr.query(connection, sql, new BeanListHandler<T>(clazz), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        }

    }

    //查询单行结果 的通用方法
    public T querySingle(String sql, Class<T> clazz, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new BeanHandler<T>(clazz), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        }
    }

    //查询单行单列的方法,即返回单值的方法

    public Object queryScalar(String sql, Object... parameters) {

        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new ScalarHandler(), parameters);

        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        }
    }

}
```



下面依照javabean的顺序，逐一写出各个javabean对应的Dao接口及DaoImplement类。

### 3.2 Member

针对Memberjavabean的具体操作。

#### 3.2.1 MemberDao

对用户的操作，一般都是根据用户名得到该用户名对应的对象、保存新注册的用户、验证用户账号密码等等，这个三个需求对应了下面三个方法。

```java
package dao;

import javabean.Member;

public interface MemberDao {

    //根据现实需要，提供一些方法接口

    //1、根据用户名返回Member对象
    public Member queryMenberByUsername(String username);

    //2、保存好像保存的Member对象
    public int saveMember(Member member);//返回1则保存成功、返回0则保存失败

    //3、根据用户名和密码来查询member对象
    public Member queryMenberByUsernameAndPassword(String usernam,String password);


}

```



#### 3.2.2 MemberDaoImplement

这里是MemberDao的具体实现，所有的实现类在实现了自己对应的接口的同时，还及继承了basicDao类。

```java
package dao.implement;

import dao.BasicDAO;
import dao.MemberDao;
import javabean.Member;

//实现MemberDao接口
public class MemberDAOImp extends BasicDAO<Member> implements MemberDao {
    @Override
    public Member queryMenberByUsername(String username) {
        String sql = "SELECT `id`, `username`,`password`,`email` FROM `member` WHERE `username` = ?";
        Member member = querySingle(sql,Member.class,username);

        return member;
    }

    @Override
    public int saveMember(Member member) {
        String sql = "INSERT INTO `member`(`username`,`password`,`email`) VALUES(?,MD5(?),?)";
        int i = update(sql,member.getUsername(),member.getPassword(),member.getEmail());
        return i;
    }

    @Override
    public Member queryMenberByUsernameAndPassword(String usernam, String password) {
        String sql = "SELECT `id`, `username`,`password`,`email` FROM `member` WHERE `username` = ? and `password` = md5(?)";
        Member member = querySingle(sql,Member.class,usernam,password);
        return member;
    }


}

```



> queryMenberByUsername方法

使用``String sql = "SELECT `id`, `username`,`password`,`email` FROM `member` WHERE `username` = ?";``这个语句来在数据库中进行查找；

`Member member = querySingle(sql,Member.class,username);`传入的具体参数则为形参列表中接收的username，并且指定返回的类型为Member型。



> saveMember方法

使用``String sql = "INSERT INTO `member`(`username`,`password`,`email`) VALUES(?,MD5(?),?)";``来向数据库中添加新数据，具体参数为从形参列表中接收的member对象的信息，返回i为受影响的条数。



> queryMenberByUsernameAndPassword方法

根据接收的账号和密码来查找是否数据库中有对应的member信息，有则返回member对象，没有则null。



### 3.3 Furn

针对家具信息的操作。

#### 3.3.1 FurnDao

```java
package dao;
import javabean.Furn;
import java.util.List;

public interface FurnDao {

    //提供返回所有家具信息的方法
    public List<Furn> queryFurn();

    //提供添加家具的方法
    public int addFurn(Furn furn);//int表示返回的行数

    //提供删除家具的方法
    public int delFurn(int id);//int表示受影响的行数

    //提供查询家具的方法
    public Furn selectFury(int id);//通过id查询对应的家具

    //提供修改家具的方法
    public int updateFurn(Furn furn);//修改传入的家具信息
}

```



#### 3.3.2 FurnDaoImplement

```java
package dao.implement;

import dao.BasicDAO;
import dao.FurnDao;
import javabean.Furn;

import java.util.List;

public class FrunDaoImp extends BasicDAO<Furn> implements FurnDao {

    @Override
    public int addFurn(Furn furn) {
        String sql = "INSERT INTO furn (`id`,`name`,`maker`,`price`,`sales`,`stock`,`img_path`) VALUES(NULL, ?, ? ,? ,? ,? ,?)";
        return update(sql,furn.getName(),furn.getMaker(),furn.getPrice(),furn.getSales(),furn.getStock(),furn.getImgPath());

    }

    @Override
    public int delFurn(int id) {
        String sql = "DELETE from furn WHERE id = ?";
        return update(sql,id);

    }

    @Override
    public Furn selectFury(int id) {
        String sql = "SELECT `id`,`name`,`maker`,`price`,`sales`,`stock`,`img_path`imgPath FROM furn WHERE id = ?";
        return querySingle(sql,Furn.class,id);
    }

    @Override
    public int updateFurn(Furn furn) {
        String sql = "UPDATE `furn` SET `name` = ? , `maker` = ? , `price` = ?, `sales` = ?, `stock` = ? ,`img_path` = ? WHERE id = ?";
        return update(sql,furn.getName(),furn.getMaker(),furn.getPrice(),furn.getSales(),furn.getStock(),furn.getImgPath(),furn.getId());
    }

    @Override
    public List<Furn> queryFurn() {
        String sql = "SELECT `id`,`name`,`maker`,`price`,`sales`,`stock`,`img_path`imgPath FROM furn";
        //此处有一点需要注意，数据库里图像路径的命名为img_path，而javabean里furn类的图像路径变量名叫imgPath，这两个名字不一样，通过queryMulti方法
        //反射得到属性时就匹配不上，会导致imgPtah属性为空，此时只需要在查询语句的img_path后面直接加上imgPath，即别名即可。
        return queryMulti(sql,Furn.class);
    }
}
```

各种方法的具体实现操作和上面差不多，就不细说了。



### 3.4 page

虽然page本身在数据库中并没有信息，但是其一般是伴随furn出现的，这时候就需要获取到furn的信息，这些信息需要从数据库中得到，因此有必要做一个pagedao

#### 3.4.1 pageDao

```java
package dao;

import javabean.Furn;

import java.util.List;

/**
 * dao层是连接数据库用的，因此哪些属性是可以通过数据库得到的，就将这些属性的相关方法在dao层定义
 */
public interface PageDao {
    //pageNo是前端传输的，不用从数据库获取
    //pageSize是定义的常量，不用从数据库获取
    //totalRow是词条总量，是从数据库获取的
    //pageTotalCount是通过计算来的，不从数据库获取
    //items是数据库查找的，从数据库获取
    //故只有totalRow和items是需要Dao的方法的。

    //获取总词条量
    public int getTotalRow();

    //获取当前页要显示的家具，begin表示从第几个词条开始展示；pageSize表示这一页展示几个词条
    public List<Furn> getPageItems(int begin, int pageSize);

    //获取与某些关键字相关的词条的总量
    public int getTotalRowByName(String name);


    //根据begin、pageSize和name来得到相关的家具信息，即名字里有name的第begin条到第pageSize条词条
    public List<Furn> getPageItemByName(int begin, int pageSize, String name);
}

```



#### 3.4.2 pageDaoImplement

可以看到，这里的所以sql语句，操作的数据库都是furn数据库。下面代码里还注释了模糊查询时的技巧，记得着重看一下。

```java
package dao.implement;

import dao.PageDao;
import dao.BasicDAO;
import javabean.Furn;
import javabean.Member;

import java.util.List;

public class PageDaoImp extends BasicDAO implements PageDao {
    @Override
    public List<Furn> getPageItemByName(int begin, int pageSize, String name) {
        String sql = "SELECT `id`,`name`,`maker`,`price`,`sales`,`stock`,`img_path`imgPath FROM furn WHERE `name` LIKE ? LIMIT ?,?";
        return queryMulti(sql,Furn.class,"%" + name + "%",begin,pageSize);
    }

    @Override
    public int getTotalRowByName(String name) {
        String sql = "SELECT COUNT(*) FROM `furn` WHERE `name` LIKE ?";//此次使用模糊查询来查询相关词条的总量
        return ((Number)queryScalar(sql,"%" + name + "%")).intValue();//模糊查询的格式是得在查询词旁边加百分号的
    }

    @Override
    public List<Furn> getPageItems(int begin, int pageSize) {
        String sql = "SELECT `id`,`name`,`maker`,`price`,`sales`,`stock`,`img_path`imgPath FROM furn LIMIT ?,?";
        return queryMulti(sql,Furn.class,begin,pageSize);
    }

    @Override
    public int getTotalRow() {
        String sql = "SELECT COUNT(*) FROM `furn`";
        return ((Number)queryScalar(sql)).intValue();//查询语句的返回类型是Object，此时需要将其转换为int型。
    }
}
```



### 3.5 order

再有就是订单的数据库操作了，这个相对简单，因为订单下了之后就不会再修改了，因此大部分时候只 提供保存订单的方法和提取订单的方法就行。

#### 3.5.1 orderDao

```java
public interface OrderDao {

    public int saveOrder(Order order);


}
```

```java
package dao;

import javabean.OrderItem;

import java.util.List;

public interface OrderItemDao {

    public int saveOrderItem(OrderItem orderItem);

    public List<OrderItem> getOrderItem();
}

```

这里是总订单和订单细节的两个人的dao，不负责，就写一块了



#### 3.5.2 orderDaoImplemnet

```java
package dao.implement;

import dao.BasicDAO;
import dao.OrderDao;
import javabean.Furn;
import javabean.Order;

import java.util.Date;

public class OrderDaoImp extends BasicDAO<Order> implements OrderDao {

    @Override
    public int saveOrder(Order order) {
        String sql = "INSERT INTO `order`(`id`,`create_time`,`price`,`status`,`member_id`) VALUES(?,?,?,?,?)";

        return update(sql,order.getId(),order.getDate(),order.getPrice(),order.getStatus(),order.getMemberId());

    }
}

```

```java
package dao.implement;

import dao.BasicDAO;
import dao.OrderItemDao;
import javabean.Order;
import javabean.OrderItem;

import java.util.List;

public class OrderItemDaoImp extends BasicDAO<OrderItem> implements OrderItemDao {
    @Override
    public int saveOrderItem(OrderItem orderItem) {
        String sql = "INSERT INTO `order_item`(`id`,`name`,`price`,`count`,`total_price`,`order_id`) VALUES(NULL,?,?,?,?,?) ";

        return update(sql,orderItem.getName(),orderItem.getPrice(),orderItem.getCount(),orderItem.getTotalPrice(),orderItem.getOrderId());

    }

    @Override
    public List<OrderItem> getOrderItem() {
        String sql = "SELECT * FROM order_item";
        return queryMulti(sql,OrderItem.class);
    }
}

```

实现方法也写一块了。



### 3.6 cart

购物车是没接入数据库的，但是按理说也应该有对cart对象进行的操作，不过这些操作写在了cart的javabean底下，就不再这里再写一次了。



## 四、service

在操作数据库的方法写完了之后，就该综合这些操作数据库的方法，根据servlcet的需求来进行大方向上的使用了，这就是service做的事情。

service的结构也是类似于dao，都是现有接口再有实现类，不过service没有一共basic的类了，直接是service和对应的serviceImplement。

### 4.1 member

实现有关用户的一些操作，一般是登录界面和注册界面。

#### 4.1.1 memberService

```java
package service;

import javabean.Member;

public interface MemberService {

    //根据需求写服务

    //1、提供一个注册用户的方法
    public boolean registerMember(Member member);

    //2、判断用户是否存在的方法
    public boolean isExistsUsername(String username);

    //3、判断用户账户名和密码是否正确(通过界面输入的用户和密码构建member对象)
    public Member UserLogin(Member member);

    public Integer getMemberId(Member member);

}
```



#### 4.1.2 memberServiceImp

主要通过调用memberDaoImp来实现，在Dao的基础上添加一点点的判断

```java
package service.ServiceImplement;

import dao.MemberDao;
import dao.implement.MemberDAOImp;
import javabean.Member;
import service.MemberService;

public class MemberServiceImp implements MemberService {
    MemberDao memberDao = new MemberDAOImp();
    @Override
    public boolean registerMember(Member member) {
        int i = memberDao.saveMember(member);
        if (i == 1) return true;
        else return false;
    }

    @Override
    public boolean isExistsUsername(String username) {
        Member member = memberDao.queryMenberByUsername(username);
        if(member != null) return true;
        else return false;
    }

    @Override
    public Member UserLogin(Member member) {
        Member memberDB = memberDao.queryMenberByUsernameAndPassword(member.getUsername(), member.getPassword());
        return memberDB;
    }

    @Override
    public Integer getMemberId(Member member) {
        String username = member.getUsername();
        Member member1 = memberDao.queryMenberByUsername(username);
        return member1.getId();
    }
}

```



### 4.2 Furn

对具体家具的操作，一般用在管理员账号登录后对具体家具信息进行更改。

#### 4.2.1 FurnService

```java
package service;

import javabean.Furn;

import java.util.List;

public interface FurnService {

    //提供一个返回家具信息的方法
    public List<Furn> queryFurns();

    //提供一个添加家具的方法
    public int addFurn(Furn furn);

    //删除家具的方法
    public int delFurn(int id);

    //根据id查询家具的方法
    public Furn selectFurn(int id);

    //提供更改家具的方法
    public int updateFurn(Furn furn);

    //提供查询家具存量的方法
    public int queryStock(int id);
}

```



#### 4.2.2 FurnServiceImp

这里几乎全部都是Dao的操作，没有出现一个服务用多个Dao的情形还。

```java
package service.ServiceImplement;

import dao.FurnDao;
import dao.implement.FrunDaoImp;
import javabean.Furn;
import service.FurnService;

import java.util.List;

public class FurnServiceImp implements FurnService {
    FurnDao furnDao = new FrunDaoImp();

    @Override
    public int addFurn(Furn furn) {
        return furnDao.addFurn(furn);
    }

    @Override
    public int delFurn(int id) {
        return furnDao.delFurn(id);
    }

    @Override
    public int updateFurn(Furn furn) {
        return furnDao.updateFurn(furn);
    }

    @Override
    public int queryStock(int id) {
        return furnDao.selectFury(id).getStock();
    }

    @Override
    public Furn selectFurn(int id) {
        return furnDao.selectFury(id);
    }

    @Override
    public List<Furn> queryFurns() {
        List<Furn> furns = furnDao.queryFurn();
        return furns;
    }
}

```



### 4.3 page

page的服务要复杂点，主要围绕furn进行分页处理。

#### 4.3.1 pageService

```java
package service;

import javabean.Furn;
import javabean.Page;

public interface PageService {

    //提供一个初始化page的方法
    public Page<Furn> page(int pageNo, int pageSize);

    //提供一个检索page的方法
    public Page<Furn> pageByName(int pageNo, int pageSize , String name);
}
```

这里就看出，直接引用了furn的javabean，主要对furn进行分页处理。



#### 4.3.2 pageServiceImp

主要是对page对象做一个初始化，page对象里放入当页要展示的furn对象，以供前端使用。

```java
package service.ServiceImplement;

import dao.PageDao;
import dao.implement.PageDaoImp;
import javabean.Furn;
import javabean.Page;
import service.PageService;

import java.util.List;

public class PageServiceImp implements PageService {
    PageDao pageDao = new PageDaoImp();
    Page<Furn> page = new Page<>();//page没有数据库中的信息，所以这里直接实例化一个page以供操作

    @Override
    public Page<Furn> page(int pageNo, int pageSize) {//在这里将page的所有属性（除url外）全部初始化
        //其中pageNo和pageSize由形参列表里面拿
        page.setPageNo(pageNo);
        page.setPageSize(pageSize);

        //totalRow由数据库里取
        int totalRow = pageDao.getTotalRow();
        page.setTotalRow(totalRow);

        //pageTotalCount由计算的来
        int pageTotalCount = totalRow/pageSize;
        if (totalRow % pageSize > 0) pageTotalCount += 1;
        page.setPageTotalCount(pageTotalCount);

        //pageItems由该算法从数据库中取
        int begin = (pageNo - 1) * pageSize;
        List<Furn> pageItems = pageDao.getPageItems(begin, pageSize);
        page.setItems(pageItems);
        return page;
    }

    //跟上面的方法几乎一样，就是一些小细节改了改
    @Override
    public Page<Furn> pageByName(int pageNo, int pageSize, String name) {
        page.setPageNo(pageNo);
        page.setPageSize(pageSize);

        //这里改了改，要根据name来返回词条总数
        int totalRow = pageDao.getTotalRowByName(name);

        page.setTotalRow(totalRow);
        int pageTotalCount = totalRow/pageSize;
        if (totalRow % pageSize > 0) pageTotalCount += 1;
        page.setPageTotalCount(pageTotalCount);
        int begin = (pageNo - 1) * pageSize;

        //这里改了改，要根据name来得到相关的家具信息
        List<Furn> pageItems = pageDao.getPageItemByName(begin, pageSize,name);
        page.setItems(pageItems);

        return page;
    }


}

```



### 4.4 cart

 cart由于没有接入数据库，是通过session操作的，所以可以直接再后面的sevlet层进行具体细节的控制，这里不用写。以下的service就是一个表意的过程，就是说如果接入数据库，大概会有这么个东西。

#### 4.4.1 cartService

```java
package service;

import javabean.CartItem;

import java.math.BigDecimal;

/**
 * 由于购物车没接数据库，而是通过session进行处理信息，所以可以绕过service，直接通过servlet操作
 */
public interface CartService {
    public void addItem(CartItem cartItem);//添加一条新家具进购物车

    public Integer getTotalCount();//得到购物车内物品的总量

    public BigDecimal getCartTotalPrice();//得到购物车的总价格

}

```



#### 4.4.2 cartServiceImp

```java
package service.ServiceImplement;

import javabean.Cart;
import javabean.CartItem;
import service.CartService;

import java.math.BigDecimal;
import java.util.Set;

public class CarServiceImp implements CartService {
    Cart cart = new Cart();
    @Override
    public void addItem(CartItem cartItem) {
        //判断是否可以添加此数据
        CartItem item = cart.getItems().get(cartItem.getId());//先尝试从哈希表里取出传入的cartItem的id，若取不出，则代表表里还没有这个数据，可以添加
        if (null == item){
            cart.getItems().put(cartItem.getId(),cartItem);
        }else {//若购物车里已经有这个数据了，代表之前添加过一次这个数据，再次添加则表示买两个，那么数量和价格都要改变
            item.setCount(item.getCount() + 1);//数量在原有的基础上加一
            item.setTotalPrice(item.getPrice().multiply(new BigDecimal(item.getCount())));//价格直接拿单价×数量得到当前总价（也可也拿上一时刻的总价加上一个单价的值，但是要保证加如的数据数量只有一才行）
        }
    }

    @Override
    public Integer getTotalCount() {
        int totalCount = 0;
        //遍历哈希表，计算每个词条的总量，求和得到整个购物车的总量
        Set<Integer> keys = cart.getItems().keySet();//取出哈希表里的所有key，放入集合中
        for (Integer id : keys){
            totalCount += ((CartItem)cart.getItems().get(id)).getCount();
        }

        return totalCount;
    }

    @Override
    public BigDecimal getCartTotalPrice() {
        BigDecimal CartTotalPrice = new BigDecimal(0);//初始化为0

        Set<Integer> keys = cart.getItems().keySet();
        for (Integer id : keys){
            CartItem cartItem = cart.getItems().get(id);
            CartTotalPrice = CartTotalPrice.add(cartItem.getTotalPrice());
        }
        return CartTotalPrice;
    }
}

```

以上操作在整个项目中并没有用到。



### 4.5 order

处理订单相关的信息，此处也将order和orderItem两者写到一块

#### 4.5.1 orderService

总订单方面，提供一个保存订单的服务，保存订单时，传入的参数是购物车的参数，因为后面保存订单的入口是在购物车中，并且订单的细节也是购物车相关的。

```java
package service;

import javabean.Cart;
import javabean.Order;

import java.util.Date;

public interface OrderService {

    //提供根据购物车来生成订单的方法，并且由于订单是跟用户关联的，也要接受一个用户id
    public Order saveOrder(Cart cart,int memberId);


}
```



订单细节方面，提供一个获取订单的服务

```java
package service;

import javabean.OrderItem;

import java.util.List;

public interface OrderItemService {
    public List<OrderItem> getOrderItem();
}

```



#### 4.5.2 orderServiceImp

```java
package service.ServiceImplement;

import dao.FurnDao;
import dao.OrderDao;
import dao.OrderItemDao;
import dao.implement.FrunDaoImp;
import dao.implement.OrderDaoImp;
import dao.implement.OrderItemDaoImp;
import javabean.*;
import service.OrderService;

import java.util.Date;
import java.util.HashMap;
import java.util.Set;

public class OrderServiceImp implements OrderService {
    /**
     * 在生成订单时，设计到多表，因此会涉及到多表事务问题，需要用ThreadLocal+Mysql+事务机制+过滤器完成
     */
    OrderDao orderDao = new OrderDaoImp();
    OrderItemDao orderItemDao = new OrderItemDaoImp();
    FurnDao furnDao = new FrunDaoImp();
    @Override
    public Order saveOrder(Cart cart, int memberId) {

        //先通过cart对象构建对应的order对象，在此之前，要先生成一个唯一id作为Order的属性
        String orderId = System.currentTimeMillis() + "" + memberId;//由当前时间加传入的用户id作为唯一id
        Order order = new Order(orderId, new Date(), cart.getCartTotalPrice(), 0, memberId);

        //保存生成的order
        orderDao.saveOrder(order);//第一个表更新

        //通过cart对象提出CartItem，CartItem的内容就和OrderItem差不多了，来构造OrderItem
        HashMap<Integer, CartItem> items = cart.getItems();
        Set<Integer> keys = items.keySet();
        for(Integer id : keys){
            CartItem cartItem = items.get(id);
            OrderItem orderItem = new OrderItem(null,cartItem.getName(),cartItem.getPrice(),cartItem.getCount(),cartItem.getTotalPrice(),orderId);
            orderItemDao.saveOrderItem(orderItem);//第二个表更新

            //更新furn表的销量和存量
            Furn furn = furnDao.selectFury(id);//先根据家具id取出这个家具
            furn.setSales(furn.getSales() + cartItem.getCount());//当前销量加上购物车结算的数量
            furn.setStock(furn.getStock() - cartItem.getCount());//当前存量减去购物车结算的数量

            furnDao.updateFurn(furn);//第三个也就是最后一个表更新。最后一个表更新完成后，就可以提交整个事务了

        }
        //订单结束后清空购物车
        cart.clean();




        return order;
    }


}
```

在生成order订单后，有个细节要注意，买的那些家具对应的数量应该进行更改，比如下了两个桌子的订单，所以桌子的销售额应该加2，库存应该减2。

并且看代码可以发现，下一个订单的过程，改变了三个表：总订单表、订单细节表、家具信息表。为了保证这三个表同时被更改或者同时更改失败，就需要使用线程+事务操作来提供保障。这是后话了。



## 五、servlet

servlet层的作用就是对接前端，并根据需求调用service层的操作。

servlet是相对来说最复杂的一层了，因为这里要实现业务逻辑，并且对接前端，事情非常多，而且servlet层的构建不是基于javabean了，而是基于业务需求，有一个业务就需要一共servlet来对应。

写servlet时，使用了一个设计模式，做一个basicSevlet，在这个servlet中实现doget和doposet方法，其他servlet继承完该类后通过反射机制得到具体要运行的方法。



### 5.1 basicServlet

```java
package web;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.Method;

/**
 * 写一个base的抽象Servlet，使用设计模式来更方便的完成servlet的实现。
 * 抽象servlet不用去web.xml里配置，因为它不用亲自实现，它的子类配置好就行
 * 这里相当于一个总类，以后所有的servlet就只有这里有doget和dopost方法了，其他的只需要写具体需要实现的内容，然后继承该类。
 */
public abstract class BasicServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置编码格式
        req.setCharacterEncoding("utf-8");
        //获取请求的类型
        String action = req.getParameter("action");

        //使用反射，获取当前对象的方法
        try {
            //这里this是继承了BasicServlet的某个子类。即前端请求哪个servlet，就会请求这个servlet的dopost方法，而这个servlet的dopost方法是继承的BasicServlet的
            //故会来这里找，此时this就是刚刚的servlet。
            Method declaredMethod = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);//得到请求的servlet里的action对应的方法
            declaredMethod.invoke(this,req,resp);//拿到方法后，通过反射运行该方法
        } catch (Exception e) {

            //这里捕获到异常之后传递，让过滤器去同一处理异常
            throw new RuntimeException(e);
        }


    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

这是一个抽象类，不需要去xml里配置。

在这里规定，前端发出的请求，得是action请求。即只接收action请求中的方法。

拿到请求头里的action对应的方法后，通过反射，得到对应的继承了该basicServlet类的servlet类中的方法，进而进行运行。



### 5.2 AdmainServlet

先看这个自成一派的servlet。admainservlet是用来判断管理员登录情况的，即管理员登录后看到的界面和普通用户登录后看到的界面不一样，但是这里偷了个懒，管理员账户和普通用户账户没做区分，都放在了同一个数据库中，所以只要账户密码正确，都可以登录管理员账户。

```java
package web;

import javabean.Member;
import service.MemberService;
import service.ServiceImplement.MemberServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class AdmainServlet extends BasicServlet{
    MemberService memberService = new MemberServiceImp();

    public void login(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("user-name");
        String password = request.getParameter("user-password");
        Member m = new Member(null,username,password,null);

        if (memberService.UserLogin(m) == null){//数据库里没该用户信息
            //把错误细信息存放在request域里
            request.setAttribute("errMsg","用户名或密码错误");
            request.setAttribute("username",username);
            request.getRequestDispatcher("/views/manager/manage_login.jsp").forward(request,response);
        }else {
            //将得到的member对象放入session中，以记录登录情况
            request.getSession().setAttribute("member",m);
            request.getRequestDispatcher("/views/manager/manage_menu.jsp").forward(request,response);
        }


    }

}

```

在继承了basicServlet后，就不需要在具体的servlet中写doget方法了，因为多态的原理，会直接在basicServlet中通过反射得到这里的具体的方法，如此处就是login方法（basicServlet中写的挺清楚了）。

这里提供一个判断用户是否登录正确的方法，从请求头中得到用户名和密码，判断用户名和密码是否正确，如果正确，则将该用户名和密码对应的member用户放入session中记录登录情况，以防止每个新界面都得重新登录（新节目时只需要判断此时session中是否有member就行，如果有member，则不再登录）；如果不正确，则将错误信息放入request域中，以便在前端界面展示错误信息。



### 5.3 MemberServlet

memberServlet实际上是AdmainServlet的拓展，AdmainServlet只是做了登录验证，这里多了注册方法。

```java
package web;

import com.google.gson.Gson;
import javabean.Member;
import javabean.Order;
import service.MemberService;
import service.ServiceImplement.MemberServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

import static com.google.code.kaptcha.Constants.KAPTCHA_SESSION_KEY;

/**
 * 做一个大Servlet，处理跟Member相关的业务，就是将LoginServlet和RegisterServlet合起来
 */
public class MemberServlet extends BasicServlet {
    MemberService memberService = new MemberServiceImp();

    //这里login方法和register方法实际上就是将LoginServlet和RegisterServlet中的doget方法粘贴过来，然后把方法名改了。
    protected void login(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("user-name");
        String password = request.getParameter("user-password");
        Member m = new Member(null,username,password,null);

        if (memberService.UserLogin(m) == null){//数据库里没该用户信息
            //把错误细信息存放在request域里
            request.setAttribute("errMsg","用户名或密码错误");
            request.setAttribute("username",username);
            request.getRequestDispatcher("/views/member/login.jsp").forward(request,response);
        }else {
            //将得到的member对象放入session中，以记录登录情况
            request.getSession().setAttribute("member",m);
            request.getRequestDispatcher("/views/member/login_ok.jsp").forward(request,response);
        }
    }

    protected void register(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //接受用户的注册信息
        String username = request.getParameter("user-name");
        String parameter = request.getParameter("user-password");
        String email = request.getParameter("user-email");

        //判断用户名是否可用
        //if (memberService.isExistsUsername(username)){
        //    System.out.println("用户名存在，不可注册");
        //    request.getRequestDispatcher("/views/member/login.jsp").forward(request,response);//返回注册界面重新注册
        //}else{
        //    Member member = new Member(null, username, parameter, email);
        //    if(memberService.registerMember(member)){//注册成功后请求转发给下一界面
        //        request.getRequestDispatcher("/views/member/register_ok.html").forward(request,response);
        //    }
        //    else {//注册失败后请求转发给注册界面
        //        request.getRequestDispatcher("/views/member/register_fail.html").forward(request, response);
        //    }
        //}

        //判断验证码是否正确
        //获取用户提交的验证码
        String code = request.getParameter("code");

        //先从session中提取
        String token = (String)request.getSession().getAttribute(KAPTCHA_SESSION_KEY);

        //取到后立即删除session，防止重复实验验证码，只在后台使用token就行
        request.getSession().removeAttribute(KAPTCHA_SESSION_KEY);

        //开始判断
        if (token != null && token.equalsIgnoreCase(code)){
            //判断用户名是否可用
            if (memberService.isExistsUsername(username)){
                System.out.println("用户名存在，不可注册");
                //request.getRequestDispatcher("/views/member/login.jsp").forward(request,response);//返回注册界面重新注册
            }else{
                Member member = new Member(null, username, parameter, email);
                if(memberService.registerMember(member)){//注册成功后请求转发给下一界面
                    request.getRequestDispatcher("/views/member/register_ok.jsp").forward(request,response);
                }
                else {//注册失败后请求转发给注册界面
                    request.getRequestDispatcher("/views/member/register_fail.jsp").forward(request, response);
                }
            }

        }else {
            request.setAttribute("errorMsg","验证码不对");
            //带回一个信息展示到注册页面
            request.setAttribute("active","register");
            request.getRequestDispatcher("/views/member/login.jsp").forward(request,response);
        }

    }

    //提供一个退出账号的方法，思路就是把session退掉就行
    public void logOut(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.getSession().invalidate();//让当前session的生命周期立即到期，或者remove掉应该也行
        //然后重定向到首页
        response.sendRedirect(request.getContextPath());
    }

    //使用ajax来进行局部访问与刷新
    public void isExistUserName(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{

        //先获取注册的用户名
        String username = request.getParameter("user-name");

        //调用service方法来查询是否存在该用户
        boolean existsUsername = memberService.isExistsUsername(username);

        //使用json来将数据返回给前端
        Map<String, Object> resultMap = new HashMap<>();//将需要返回的数据存放在map里方便导出
        resultMap.put("isExist",existsUsername);
        String resultJson = new Gson().toJson(resultMap);//使用toJson方法将map改为前端格式
        response.getWriter().write(resultJson);//将其写入前端

    }
}

```

这里的login方法和admainservlet中的login方法一样，regist方法则有些细节要说明一下。

首先是验证码方面，拿到验证码（由谷歌提供，引个包就行）后，要及时的将谷歌的验证码从session中移除，防止多次重复判断。之后的细节和登录方法的细节差不多。

退出登录没啥细节，就是单纯的将member从session中移除，并重定向到首页，准备再次登录或关闭界面。

再有就是ajax的局部判断了，这里将用户注册的name是否存在（true/false）以ajax的形式传输入前端。



### 5.4 FurnServlet

furnservlet中提供展示家具服务、增删改查家具服务、得到家具信息服务等，其中展示家具服务好像是被pageservlet给平替掉了，其他服务是管理员界面使用的。

```java
package web;

import JiajuUtils.DataUtils;
import javabean.Furn;
import org.apache.commons.beanutils.BeanUtils;
import service.FurnService;
import service.ServiceImplement.FurnServiceImp;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.InvocationTargetException;
import java.math.BigDecimal;
import java.util.List;

public class FurnServlet extends BasicServlet{
    private FurnService furnService = new FurnServiceImp();

    //获取家具信息
    public void list(HttpServletRequest request , HttpServletResponse response) throws ServletException, IOException {
        //取出家具集合
        List<Furn> furns = furnService.queryFurns();

        //将该集合放入request域
        request.setAttribute("furns",furns);//key为furns、value为furns集合

        //请求转发给新界面
        request.getRequestDispatcher("/views/manager/furn_manage.jsp").forward(request,response);

    }

    //添加新家具
    public void addFurn(HttpServletRequest request , HttpServletResponse response) throws ServletException, IOException {

//        String name = request.getParameter("name");
//        String maker = request.getParameter("maker");
//        String price = request.getParameter("price");
//        String sales = request.getParameter("sales");
//        String stock = request.getParameter("stock");
        //图片路径使用默认

        /**
         * 先假设输入的是正确的，下面的注释部分就先看个思路
         */
        //可以思考到一个问题，如果前端界面填写的数据格式不对，如给销量写成了字符串形式，该怎么办呢？
        //一种办法是在前端进行输入校验，之前在写注册登录界面时使用过该校验。
        //也可也在后端进行判断，如果验证不通过，则原地请求转发

//        Furn furn = null;
//
//        //尝试捕捉新建furn对象时出的错误，如果网页上在sales里输入的是字符串，那它势必转换不成Integer，这里就会报错
//        try {
//            furn = new Furn(null, name, maker, new BigDecimal(price), new Integer(sales), new Integer(stock), "assets/images/product-image/default.jpg");
//
//        }catch (NumberFormatException e){
//
//            //一旦捕捉到了错误，则进行原地转发
//            request.setAttribute("managerErrMsg","数据格式有误");
//            request.getRequestDispatcher("/views/manager/furn_add.jsp").forward(request,response);
//            //转发完之后直接return出方法，不再向后执行
//            return;
//        }
//
//        //若前面都没错，则进行正常添加数据
//        furnService.addFurn(furn);

        /**
         * 下面为正常流程
         */
//        Furn furn = new Furn(null, name, maker, new BigDecimal(price), new Integer(sales), new Integer(stock), "assets/images/product-image/default.jpg");
//
//        furnService.addFurn(furn);
//        //添加完毕后，请求转发给家具显示界面，这里可以直接从list方法过去，即FurnServlet-addFurn方法转发到FurnServlet-List方法，list方法再转发到家具显示界面
//        //但是不能直接使用请求转发，因为直接使用请求转发的话，当用户刷新界面时，会重新发送添加请求，会造成数据的重复提交。故要使用请求重定向。
//
//        //重定向实际上是让浏览器重新发送请求，故此url最好是一个完整的url，以便让浏览器识别
//        response.sendRedirect(request.getContextPath() + "/FurnServlet?action=list");


        /**
         *  上述javabean对象的创建是可以通过一个外部库来完成封装的，会使代码简洁很多
         */
        Furn furn = new Furn();
        DataUtils.copyParamToBean(furn,request.getParameterMap());
        furnService.addFurn(furn);
//        response.sendRedirect(request.getContextPath() + "/FurnServlet?action=list");
        response.sendRedirect(request.getContextPath() + "/PageServlet?action=page&pageNo=" + request.getParameter("pageNo"));

    }

    public void delFurn(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{
        int id = DataUtils.parseInt(request.getParameter("id"),0);//将从前端得到的id进行int抓换
        furnService.delFurn(id);
        response.sendRedirect(request.getContextPath() + "/PageServlet?action=page&pageNo=" + request.getParameter("pageNo"));//重定向而不请求转发


    }

    public void selectFurn(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
        int id = DataUtils.parseInt(request.getParameter("id"),0);
        Furn furn = furnService.selectFurn(id);
        request.setAttribute("furnsingle",furn);

        //前端中，修改数据的url是转发到此方法的，而前端传过来的请求头里有一个数据pageNo该方法不处理，而是留给该方法下一个请求中处理，即"/views/manager/furn_update.jsp"
        //此时可以在"/views/manager/furn_update.jsp"中使用page.pageNo来存放该数据

        request.getRequestDispatcher("/views/manager/furn_update.jsp").forward(request,response);

    }

    public void updateFurn(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{
        Furn furn = new Furn();
        DataUtils.copyParamToBean(furn,request.getParameterMap());
        furnService.updateFurn(furn);
        response.sendRedirect(request.getContextPath() + "/PageServlet?action=page&pageNo=" + request.getParameter("pageNo"));//重定向而不请求转发
    }

    public void getstock(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{
        int furnId = DataUtils.parseInt(request.getParameter("furnId"),0);
        furnService.queryStock(furnId);
        request.setAttribute("furnId",furnId);
    }


}
```



list方法简单明了，使用furnservice的get方法得到家具列表，然后将该列表放入request域中，以便前端使用，再请求转发到家具展示的界面即可。

addfurn方法使用完工具包里的封装工具后也简单明了，将请求头里得到信息封装成一个furn对象，然后使用service的add方法添加进数据库就算完成。之后本来是请求转发给furnservlet的list方法的，但是page优化后，就转发给page了。

删改查都是同一个思路，就不再赘述了。



### 5.5 pageServlet

```java
package web;


import JiajuUtils.DataUtils;
import javabean.Furn;
import javabean.Page;
import service.PageService;
import service.ServiceImplement.PageServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.List;

public class PageServlet extends BasicServlet  {
    PageService pageService = new PageServiceImp();

    public void page(HttpServletRequest request , HttpServletResponse response) throws ServletException , IOException{
        int pageNo = DataUtils.parseInt(request.getParameter("pageNo"), 1);
        int pageSize = DataUtils.parseInt(request.getParameter("pageSize"), Page.PAGE_SIZE);//若pageSize传输的格式有误，则使用默认的PAGE_SIZE

        Page<Furn> page = pageService.page(pageNo, pageSize);
        //将page放入request域
        request.setAttribute("page", page);

        List<Furn> items = page.getItems();

        //请求转发到furn_manage.jsp
        request.getRequestDispatcher("/views/manager/furn_manage.jsp").forward(request,response);

    }



}
```

pageServlet就提供了一个page方法，用来分页展示家具，算是家具中list的优化。

首先尝试从请求头中得到pageNo和pageSize的信息，如果得不到，就用1和默认size。

再有就是初始化一个page对象，由于page对象里做了一个list来存放家具信息，所以不用担心前端拿不到furn的情况。

之后将page对象放入request域中并请求转发给家具管理界面，以供前端使用了。



### 5.6 CartServlet

```java
package web;

import JiajuUtils.DataUtils;
import com.google.gson.Gson;
import javabean.Cart;
import javabean.CartItem;
import javabean.Furn;
import service.CartService;
import service.FurnService;
import service.ServiceImplement.CarServiceImp;
import service.ServiceImplement.FurnServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

public class CartServlet extends BasicServlet{
    private FurnService furnService = new FurnServiceImp();
    private CartService cartservice = new CarServiceImp();

    public void addItem(HttpServletRequest request , HttpServletResponse response) throws ServletException, IOException{

        //得到添加家具的id
        int id = DataUtils.parseInt(request.getParameter("id"),0);

        //看看这个id在家具总部里是否有对应，即看看这个id存不存在furn
        Furn furn = furnService.selectFurn(id);
        //如果不存在，则提示从新添加
        //todo

        //如果存在，则准备根据furn创建cartItem
        CartItem cartItem = new CartItem(furn.getId(), furn.getName(), furn.getPrice(), 1, furn.getPrice());//默认一次添加一个

        //从session中获取cart对象，以准备将cartItem放入cart中
        Cart cart = (Cart) request.getSession().getAttribute("cart");
        //进行session里有没有cart的判断，如果是第一次创建cart，则需要进行一下初始化
        if (null == cart){//若从session里取出来的是空，则表示session里是没cart的
            //创建cart
            cart = new Cart();
            request.getSession().setAttribute("cart",cart);
        }
        cart.addItem(cartItem);


        //添加完毕后，返回到原始页面
        String referer = request.getHeader("Referer");
        response.sendRedirect(referer);
    }

    public void updateCount(HttpServletRequest  request , HttpServletResponse response) throws ServletException,IOException{
        int id = DataUtils.parseInt(request.getParameter("id"),0);
        int count = DataUtils.parseInt(request.getParameter("count"),1);

        Cart cart = (Cart)request.getSession().getAttribute("cart");
        if (null != cart){
            cart.updateItemCount(id,count);
        }

        response.sendRedirect(request.getHeader("Referer"));

    }

    public void deletItem(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{
        int id = DataUtils.parseInt(request.getParameter("id"),0);

        Cart cart = (Cart)request.getSession().getAttribute("cart");
        if (null != cart){
            cart.deleteItem(id);
        }

        response.sendRedirect(request.getHeader("Referer"));
    }

    public void clean(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{

        Cart cart = (Cart)request.getSession().getAttribute("cart");
        if (null != cart){
            cart.clean();
        }

        response.sendRedirect(request.getHeader("Referer"));
    }

    //用来局部刷新购物车右上角的数量
    public void addItemByAjax(HttpServletRequest request, HttpServletResponse response) throws ServletException,IOException{
        //得到添加家具的id
        int id = DataUtils.parseInt(request.getParameter("id"),0);

        //看看这个id在家具总部里是否有对应，即看看这个id存不存在furn
        Furn furn = furnService.selectFurn(id);
        //如果不存在，则提示从新添加
        //todo

        //如果存在，则准备根据furn创建cartItem
        CartItem cartItem = new CartItem(furn.getId(), furn.getName(), furn.getPrice(), 1, furn.getPrice());//默认一次添加一个

        //从session中获取cart对象，以准备将cartItem放入cart中
        Cart cart = (Cart) request.getSession().getAttribute("cart");
        //进行session里有没有cart的判断，如果是第一次创建cart，则需要进行一下初始化
        if (null == cart){//若从session里取出来的是空，则表示session里是没cart的
            //创建cart
            cart = new Cart();
            request.getSession().setAttribute("cart",cart);
        }
        cart.addItem(cartItem);

        //添加完毕后返回json数据，前端拿到json数据后局部刷新即可
        //规定json格式
        Map<String, Object> resultMap = new HashMap<>();
        resultMap.put("cartTotalCount",cart.getTotalCount());//将购物车的当前数量放入map中，以便转成json格式

        //转成json
        String resultJson = new Gson().toJson(resultMap);
        //返回前端
        response.getWriter().write(resultJson);

    }


}
```

购物车中提供的方法：增删改查方面的操作、ajax请求刷新界面的操作。

首先看增删改查，代码的注释写的挺清晰的，看看就行。

有个小细节要注意就是说，cart是放在session中的，其在首次向购物车添加家具时创建。然后cart中存放具体的cartItem。

addItem最后请求转发给原界面了，明显不太合理，只是添加个家具，就将整体刷新了一次，会很浪费资源，因此优化为additemByAjax方法

additemByAjax部分，前半段和addItem一致，只是添加完成后，不再整体的刷新界面，而只是将右上角的购物车容量刷新（看前端时就知道了），其将购物车总数放入了map中通过ajax写回前端，前端提取到后，只局部刷新右上角就行。



### 5.7 OrderServlet

老规矩，Order和OrderItem写在一起

```java
package web;

import JiajuUtils.DataUtils;
import javabean.Cart;
import javabean.Member;
import javabean.Order;
import service.MemberService;
import service.OrderService;
import service.ServiceImplement.MemberServiceImp;
import service.ServiceImplement.OrderServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Date;

public class OrderServlet extends BasicServlet{
    OrderService orderService = new OrderServiceImp();
    MemberService memberService = new MemberServiceImp();

    public void saveOrder(HttpServletRequest request , HttpServletResponse response) throws ServletException, IOException{


        //生成订单
        Cart cart = (Cart)request.getSession().getAttribute("cart");
        //如果购物车为空，则转发到首页让其购买点东西再说
        if (cart.getItems().size() == 0 || null == cart){//注意，这里不能用items==null来判断cart里面有没有内容，因为添加再删除后，其并不为null，故应该用cart的size=0才行
            request.getRequestDispatcher("/index.jsp").forward(request,response);
            return;
        }
        Member member = (Member)request.getSession().getAttribute("member");

        if (null == member){//当用户还没登录时，禁止结账，要先登录，遂转发到登录界面
            request.getRequestDispatcher("/views/member/login.jsp").forward(request,response);
            return;//转发过去后停止方法
        }
        int memberid = memberService.getMemberId(member);

        //当上面两个都不空时，则生成订单

        Order order = orderService.saveOrder(cart, memberid);

        request.getSession().setAttribute("order",order);



        //使用重定向返回到checkout.jsp
        response.sendRedirect(request.getContextPath() + "/views/order/checkout.jsp");
    }
}

```

orderServlet触发主要是通过生成订单button触发的，点击生成订单后，服务器会首先尝试从session中得到购物车总体信息，得到不了就代表还没有完成首次向购物车添加家具，购物车中为空，不能生成订单，转发回首页让他买货。

之后看看session中有没有member，若没有，代表还没登陆，则跳转到登录界面让他登录。

两个判断完了之后，再通过service的方法将order保存在数据库中，并同时生成以供order的session，以便后面使用。



```java
package web;


import javabean.OrderItem;
import service.OrderItemService;
import service.ServiceImplement.OrderItemServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.List;

public class OrderItemServlet extends BasicServlet {
    OrderItemService orderItemService = new OrderItemServiceImp();
    public void getOrderItem(HttpServletRequest request , HttpServletResponse response) throws ServletException, IOException{
        List<OrderItem> orderItems = orderItemService.getOrderItem();
        request.setAttribute("orderItems",orderItems);

        request.getRequestDispatcher("views/order/order_detail.jsp").forward(request,response);
    }

}

```

订单细节方面，其主要是为了之后展示订单用的，故将orderItem信息初始化成功后，直接放入request中，然后就准备去转发到的界面展示就行。



### 5.8 CustomerServlet

这个是用户还没登录时使用的服务。

```java
package web;

import JiajuUtils.DataUtils;
import javabean.Furn;
import javabean.Page;
import service.PageService;
import service.ServiceImplement.PageServiceImp;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 当顾客还没有登录时，浏览的界面
 */
public class CustomerServlet extends BasicServlet{
    PageService pageService = new PageServiceImp();
    //做一个分页服务
    //public void page(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{
    //    int pageNo = DataUtils.parseInt(request.getParameter("pageNo"), 1);
    //    int pageSize = DataUtils.parseInt(request.getParameter("pageSize"), Page.PAGE_SIZE);//若pageSize传输的格式有误，则使用默认的PAGE_SIZE
    //
    //    Page<Furn> page = pageService.page(pageNo, pageSize);
    //    //将page放入request域
    //    request.setAttribute("customerPage", page);
    //    //请求转发到furn_manage.jsp
    //    request.getRequestDispatcher("/views/customer/index.jsp").forward(request,response);
    //}

    //有此方法后，就可以代替上面的page方法了，因为下面有一个灵魂的byname算法，把传统的page方法视为name参数为空，默认查找全部家具就行
    public void pageByName(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{
        int pageNo = DataUtils.parseInt(request.getParameter("pageNo"), 1);
        int pageSize = DataUtils.parseInt(request.getParameter("pageSize"), Page.PAGE_SIZE);//若pageSize传输的格式有误，则使用默认的PAGE_SIZE

        //如果传过来的name没有值，则接受到的是""，此时会查找所有词条；如果压根没有name这个参数，那么也应该认为其传来的是空，进行所有词条的查找
        String name = request.getParameter("name");
        if (null == name) name = "";

        Page<Furn> page = pageService.pageByName(pageNo, pageSize,name);

        //此时还有个问题就是，目前情况只有刚开始检索时能定位到检索后的界面，一旦点击下面的导航，就又回到没检索的情况了
        //这个时候就要用到page类里定义的url来方便定位了
        StringBuilder url = new StringBuilder("CustomerServlet?action=pageByName");//这一部分的内容是不变的，不管检索不检索，都有这部分
        if (!"".equals(name)){//如果说请求里面的name不为空，则将这串内容拼接到url后面，以便检索
            url.append("&name=").append(name);
        }
        page.setUrl(url.toString());
        //将page放入request域
        request.setAttribute("customerPage", page);
        //请求转发到furn_manage.jsp
        request.getRequestDispatcher("/views/customer/index.jsp").forward(request,response);
    }

}

```

在用户还没登录时，其权限只要浏览首页展示的家具信息，家具的list方法又被page优化过，故还是调用page来实现。



## 六、web

整个前端中东西挺多的，资源包外部库格式库什么的这里就不写了，只写跟后端接壤的部分，也是关键的部分。

web的笔记流程按照浏览转发流程来写了。

### 6.1 index

首先是服务器默认界面（index.jsp），这里将默认界面转发到还没登录时的服务(CustomerServlet)，在服务中，又转到了未登录时的界面(/views/customer/index.jsp)。

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%--默认访问整个项目时，用户还没登录，故需要先转发到没有登录时的服务，即整个网站的入口界面--%>
<jsp:forward page="/CustomerServlet?action=pageByName&pageNo=1"></jsp:forward>
```



### 6.2 Customer

Customer包中有两个界面：index.jsp和cart.jsp。

#### 6.2.1 Customer/index.jsp

先看index.jsp，这是未登录时浏览的界面，也是第一个看到的界面

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge" />
    <title>家居网购~</title>
    
 一、
    <base href="<%=request.getContextPath() + "/"%>">
    <!-- 移动端适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css">
    <%--引入jquery--%>
    <script type="text/javascript" src="script/jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        
 二、
        $(function () {
            //绑定添加购物车事件
            $("button.add-to-cart").click(function () {
                //获取到点击的家具的id
                var furnId = $(this).attr("furnId");

                //发出添加家具的请求，使用ajax优化
                //location.href = "CartServlet?action=addItem&id=" + furnId;
                $.getJSON(
                    "CartServlet",
                    {"action":"addItemByAjax",
                    "id":furnId},
                function (data) {//进行局部刷新,data就是后端传来的json对象的映射

                        if (data.url == undefined){//ajax判断机制，如果过滤器没有得到ajax请求，则正常运行
                            $("span.header-action-num").text(data.cartTotalCount);
                        }else {//如果这次请求确实是ajax请求，则在这里进行跳转
                            location.href = data.url;

                        }

                })
            })
        })
    </script>
</head>

<body>
<!-- Header Area start  -->
<div class="header section">
    <!-- Header Top  End -->
    <!-- Header Bottom  Start -->
    <div class="header-bottom d-none d-lg-block">
        <div class="container position-relative">
            <div class="row align-self-center">
                <!-- Header Logo Start -->
                <div class="col-auto align-self-center">
                    <div class="header-logo">
                        <a href="index.jsp"><img src="assets/images/logo/logo.png" alt="Site Logo"/></a>
                    </div>
                </div>
                <!-- Header Logo End -->

                <!-- Header Action Start -->
                <div class="col align-self-center">
                    <div class="header-actions">
                        <div class="header_account_list">
                            <a href="javascript:void(0)" class="header-action-btn search-btn"><i
                                    class="icon-magnifier"></i></a>
                            <div class="dropdown_search">
                                <form class="action-form" action="CustomerServlet">
                                    <input type="hidden" name="action" value="pageByName">
                                    <input class="form-control" placeholder="输入家具名称关键字" type="text" name="name">
                                    <button class="submit" type="submit"><i class="icon-magnifier"></i></button>
                                </form>
                            </div>
                        </div>
                        
 三、
                        <!-- Single Wedge Start -->
                        <%--根据用户是否登录成功来确定右上角的展示情况--%>
                        <%--这里的思路是，判断session中的用户信息是否为空，若为空则用户还没登录过，展示登录界面；若不为空，则展示欢迎界面--%>
                        <%--每次定向到index.jsp时，都会进行这次判断来决定右上角显示什么东西--%>
                        <c:if test="${empty sessionScope.member}">
                            <div class="header-bottom-set dropdown">
                                <a href="http://localhost:8080/AllUse/views/member/login.jsp">登录|注册</a>
                            </div>
                        </c:if>

                        <c:if test="${not empty sessionScope.member}">
                            <div class="header-bottom-set dropdown">
                                <a>欢迎: ${sessionScope.member.username}</a>
                            </div>
                            <div class="header-bottom-set dropdown">
                                <a href="#">订单管理</a>
                            </div>
                            <div class="header-bottom-set dropdown">
                                <a href="MemberServlet?action=logOut">退出账号</a>
                            </div>
                        </c:if>

                        <!-- Single Wedge End -->
                        <a href="views/customer/cart.jsp"
                           class="header-action-btn header-action-btn-cart pr-0">
                            <i class="icon-handbag">购物车</i>
                            <span class="header-action-num">${sessionScope.cart.totalCount}</span>
                        </a>
                        <a href="#offcanvas-mobile-menu"
                           class="header-action-btn header-action-btn-menu offcanvas-toggle d-lg-none">
                            <i class="icon-menu"></i>
                        </a>
                    </div>
                </div>
                <!-- Header Action End -->
            </div>
        </div>
    </div>
</div>
<br/>


<!-- Product tab Area Start -->
<div class="section product-tab-area">
    <div class="container">
        <div class="row">
            <div class="col">
                <div class="tab-content">
                    <!-- 1st tab start -->
                    <div class="tab-pane fade show active" id="tab-product-new-arrivals">
                        <div class="row">
                            
 四、
                            <c:forEach items="${requestScope.customerPage.items}" var="furn">
                            <div class="col-lg-3 col-md-6 col-sm-6 col-xs-6 mb-6" data-aos="fade-up"
                                 data-aos-delay="200">
                                <!-- Single Prodect -->
                                <div class="product">
                                    <div class="thumb">
                                        <a href="shop-left-sidebar.html" class="image">
                                            <img src="${furn.imgPath}" alt="Product"/>
                                            <img class="hover-image" src="${furn.imgPath}"
                                                 alt="Product"/>
                                        </a>
                                        <span class="badges">
                                                <span class="new">New</span>
                                            </span>
                                        <div class="actions">
                                            <a href="#" class="action wishlist" data-link-action="quickview"
                                               title="Quick view" data-bs-toggle="modal" data-bs-target="#exampleModal"><i
                                                    class="icon-size-fullscreen"></i></a>
                                        </div>
                                        <c:if test="${furn.stock > 0}">
                                            <button title="Add To Cart" furnId="${furn.id}" class=" add-to-cart">
                                                添加购物车
                                            </button>
                                        </c:if>
                                        <c:if test="${furn.stock == 0}">
                                            <button title="Add To Cart">
                                                无法添加，库存为0
                                            </button>
                                        </c:if>

                                    </div>
                                    <div class="content">
                                        <h5 class="title">
                                            <a href="shop-left-sidebar.html">${furn.name} </a></h5>
                                        <span class="price">
                                                <span class="new">家居:　${furn.name}</span>
                                            </span>
                                        <span class="price">
                                                <span class="new">厂商:　${furn.maker}</span>
                                            </span>
                                        <span class="price">
                                                <span class="new">价格:　${furn.price}</span>
                                            </span>
                                        <span class="price">
                                                <span class="new">销量:　${furn.sales}</span>
                                            </span>
                                        <span class="price">
                                                <span class="new">库存:　${furn.stock}</span>
                                            </span>
                                    </div>
                                </div>
                            </div>
                            </c:forEach>
                        </div>
                    </div>
                    <!-- 1st tab end -->
                </div>
            </div>
        </div>
    </div>
</div>
    
五、
<!--  Pagination Area Start -->
<div class="pro-pagination-style text-center mb-md-30px mb-lm-30px mt-6" data-aos="fade-up">
    <ul>
        <li><a href="CustomerServlet?action=page&pageNo=1">首页</a></li>
        <%--只有当前页大于1时才存在上一页，否则当前页就是首页--%>
        <c:if test="${requestScope.customerPage.pageNo > 1}">
            <li><a href="${requestScope.customerPage.url}&pageNo=${requestScope.customerPage.pageNo - 1}">上页</a></li>
        </c:if>

        <%-- 做中间页--%>
        <%--定义好开始和结束的变量--%>
        <c:set var="begin" value="1"/>
        <c:set var="end" value="${requestScope.customerPage.pageTotalCount}"/>

        <%--开始循环--%>
        <c:forEach begin="${begin}" end="${end}" var="i">
            <%--标记出当前页，即判断如果i与当前页码相同，则对该页面使用class格式--%>
            <c:if test="${i == requestScope.customerPage.pageNo}">
                <li><a class="active" href="${requestScope.customerPage.url}&pageNo=${i}">${i}</a></li>
            </c:if>
            <c:if test="${i != requestScope.customerPage.pageNo}">
                <li><a href="${requestScope.customerPage.url}&pageNo=${i}">${i}</a></li>
            </c:if>
        </c:forEach>




        <%--只有当前页小于最末页时才存在下一页，否则当前页就是末页--%>
        <c:if test="${requestScope.customerPage.pageNo < requestScope.customerPage.pageTotalCount}">
            <li><a href="${requestScope.customerPage.url}&pageNo=${requestScope.customerPage.pageNo + 1}">下页</a></li>
        </c:if>
        <li><a href="${requestScope.customerPage.url}&pageNo=${requestScope.customerPage.pageTotalCount}">末页</a></li>
    </ul>
</div>


```

上面只保留了核心代码，将一些无关紧要的代码删了，看源码去idea中看。

从上到下说说细节：

1、首先配置base路径`  <base href="<%=request.getContextPath() + "/"%>">`

2、随后进行了一个添加购物车的ajax绑定，使用的是`getJSON`方法，传入请求的servlet和action，得到返回的数据（即cartServlet写入的map，存放的key为cartcurrentCount），然后将返回的数据展示在前端，中间穿插了一个ajax判断过滤器的阶段，后面再说。

3、使用el表达式来判断此时session中是否存在member信息，若存在则在前端提供更进一步的操作选择，若不存在，则在前端只提供登录/注册选择

4、这里就是未登录时展示的家具选项了，前面说过，家具的list已经被page优化了，并且在默认页跳转到该界面时，选择的服务是`/CustomerServlet?action=pageByName&pageNo=1`，是CustomerServlet里的pagebyname方法，而该方法中，向request存放了一个初始化完成的page进去，该page已经存放了当前页要展示的furn信息（在item属性中）。因此在这里将item取出，并循环展示item中的家具属性即可。

值得一提的是，这里加了一个库存数量的判断，若当前家具还有库存，才可以有添加购物车的选择，否则不可再添加购物车了。

5、做了一个分页导航，每个页码实际上是一个超链接，点击一个页码就是请求/CustomerServlet?action=pageByName&pageNo=1，只不过最后的pageNo变成了所点的页码。



#### 6.2 Customer/cart.jsp

在这个项目中，提供了一个方便，让当前未登录的用户也可先添加购物车，直到生成订单时才进行session的member判断。因此customer中也提供了购物车的jsp。

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge"/>
    <title>家居网购</title>
    <base href="<%=request.getContextPath() + "/"%>">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/>
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css"/>

    <script type="text/javascript" src="script/jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        
 一、
        $(function () {
            //绑定删除号
            $("a.deletItem").click(function () {
                var ItemName = $(this).parent().parent().find("td:eq(1)").text();

                return confirm("确定删除 【"+ItemName + "】？")

            })

            //绑定清空购物车
            $("a.clean").click(function () {

                return confirm("确定清空购物车？")

            })


 二、
            //绑定加减号
            var CartPlusMinus = $(".cart-plus-minus");
            CartPlusMinus.prepend('<div class="dec qtybutton">-</div>');
            CartPlusMinus.append('<div class="inc qtybutton">+</div>');
            $(".qtybutton").on("click", function() {
                var $button = $(this);
                var oldValue = $button.parent().find("input").val();
                if ($button.text() === "+") {
                    var newVal = parseFloat(oldValue) + 1;
                } else {
                    // Don't allow decrementing below zero
                    if (oldValue > 1) {
                        var newVal = parseFloat(oldValue) - 1;
                    } else {
                        newVal = 1;
                    }
                }
                $button.parent().find("input").val(newVal);
                var furnId = $button.parent().find("input").attr("furnId");

                location.href = "CartServlet?action=updateCount&count=" + newVal + "&id=" + furnId;
            });

        })
    </script>


</head>

<body>



<!-- Cart Area Start -->
<div class="cart-main-area pt-100px pb-100px">
    <div class="container">
        <h3 class="cart-page-title">Your cart items</h3>
        <div class="row">
            <div class="col-lg-12 col-md-12 col-sm-12 col-12">
                <form action="#">
                    <div class="table-content table-responsive cart-table-content">
                        <table>
                            <thead>
                            <tr>
                                <th>图片</th>
                                <th>家居名</th>
                                <th>单价</th>
                                <th>数量</th>
                                <th>金额</th>
                                <th>操作</th>
                            </tr>
                            </thead>
                            
三、
                            <tbody>
                            <%--只有当cart里面存放有items时才进行循环--%>
                            <c:if test="${not empty sessionScope.cart.items}">
                                <%--这里要注意，每次循环取出的都是一组kv值，而不是value本身--%>
                                <c:forEach items="${sessionScope.cart.items}" var="entry">
                                    <tr>
                                        <td class="product-thumbnail">
                                            <a href="#"><img class="img-responsive ml-3" src="assets/images/product-image/1.jpg"
                                                             alt=""/></a>
                                        </td>
                                        <td class="product-name"><a href="#">${entry.value.name}</a></td>
                                        <td class="product-price-cart"><span class="amount">${entry.value.price}</span></td>
                                        <td class="product-quantity">
                                            <div  class="cart-plus-minus">
                                                <input furnId="${entry.value.id}" class="cart-plus-minus-box" type="text" name="qtybutton" value="${entry.value.count}"/>
                                            </div>
                                        </td>
                                        <td class="product-subtotal">${entry.value.totalPrice}</td>
                                        <td class="product-remove">
                                            <a class="deletItem" href="CartServlet?action=deletItem&id=${entry.value.id}" ><i class="icon-close"></i></a>
                                        </td>
                                    </tr>
                                </c:forEach>
                            </c:if>


                            </tbody>
                        </table>
                    </div>
                    <div class="row">
                        <div class="col-lg-12">
                            <div class="cart-shiping-update-wrapper">
                                <h4>共${sessionScope.cart.totalCount}件商品  总价${sessionScope.cart.cartTotalPrice}元</h4>
                                <div class="cart-shiping-update">
                                    <a href="OrderServlet?action=saveOrder">生 成 订 单</a>
                                </div>
                                <div class="cart-clear">
                                    <button>继 续 购 物</button>
                                    <a class="clean" href="CartServlet?action=clean">清 空 购 物 车</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </form>

            </div>
        </div>
    </div>
</div>
<!-- Cart Area End -->


```

1、绑定了删除和清空购物车的案件，具体操作是由具体标签内跳转的href所指向的servlet请求完成的，这里只是在前端做了一个弹窗（使用confirm关键字），只有点确定才会进行href的servlet操作。

2、绑定加减号时，主要是为了防止出现负数。

3、这里的循环展示操作和index中的展示差不多，不同就是这里是从session里的cart对象中取数据，上面是从request里的page对象中取数据



### 6.3 member

刚刚的所有操作都是在未登录的情况下完成的，现在看看登录注册相关的操作。

#### 6.3.1 member/login.jsp

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge" />
    <title>家居网购</title>
    <!--设置一个base路径，方便使用-->
    <base href="<%=request.getContextPath() + "/"%>">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css"/>
    <!--引入jq包-->
    <script type="text/javascript" src="script/jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        $(function () {//页面加载完成后执行该function
            //注册失败后保持注册页不动
            <%--if("${requestScope.active}" == "register"){--%>
            <%--    $("#register_tab")[0].click();--%>
            <%--}--%>

一、
            //给用户名输入的位置绑定一个失去焦点的事件（即鼠标移走输入框后触发该事件）
            $("#username").blur(function () {
                var username = this.value;
                $.getJSON(
                    "MemberServlet",
                    {"action":"isExistUserName",
                    "user-name":username
                    },
                    function (data){
                        if (data.isExist){
                            $("span.errorMsg").text("用户名已存在");
                        }else {
                            $("span.errorMsg").text("用户名可用");
                        }
                    }
                )

            })


二、
            //绑定验证码刷新事件
            $("#codeImg").click(function () {
                this.src = "<%=request.getContextPath()%>/KaptchaServlet?d=" + new Date()//newDate用来向网站请求，因为有的网站会不理睬这次刷新
                // this.src = "http://localhost:8080/AllUse/KaptchaServlet"
            })
            //绑定点击事件
            $("#sub-btn").click(function () {//绑定用户注册事件（判断用户注册是否合法）
                //获取到用户申请的用户名
                var usernameVal = $("#username").val();

                //编写正则表达式来验证用户名合法性
                var usernamePattern = /^\w{3,10}$/;//规定用户名长度在3—10之间
                //验证
                if(!usernamePattern.test(usernameVal)){//如果验证不通过，则显示注册失败的界面
                    $("span[class='errorMsg']").text("用户名格式有误")
                    return false;//反回false来阻止请求发送给后端，下同
                }

                //验证密码
                var passwordVal = $("#password").val();
                var passwordPattern = /^\w{6,12}$/;//规定密码长度在6-12之间
                if (!passwordPattern.test(passwordVal)){
                    //错误密码展示
                    $("span.errorMsg").text("密码格式有误");//上面的用户名使用的是Jquery的属性过滤器、这里用另一种方法——基本过滤器，都可以成功
                    return false;
                }

                //两端密码相同
                var repwdVal = $("#repwd").val();
                if(repwdVal != passwordVal){
                    $("span.errorMsg").text("两次密码不相同");
                    return false;
                }

                //验证邮箱
                var emailVal = $("#email").val();
                var emailPattern = /^[\w-]+@([a-zA-Z]+\.)+[a-zA-Z]+$/;
                if(!emailPattern.test(emailVal)){
                    $("span.errorMsg").text("电子邮箱格式有误");
                    return false;
                }

                //验证验证码不为空
                var codeText = $("#code").val();
                codeText = $.trim(codeText);
                if(codeText == null || codeText == ""){
                    $("span.errorMsg").text("验证码不正确");
                    return false;
                }

                return true;//只有验证通过，才返回true来向后端发请求


            })
        })
    </script>

</head>

<body>

<!-- Header Area End  -->
<!-- login area start -->
<div class="login-register-area pt-70px pb-100px">
    <div class="container">
        <div class="row">
            <div class="col-lg-7 col-md-12 ml-auto mr-auto">
                <div class="login-register-wrapper">
                    <div class="login-register-tab-list nav">
                        <a class="active" data-bs-toggle="tab" href="#lg1">
                            <h4>会员登录</h4>
                        </a>
                        <a id="register_tab" data-bs-toggle="tab" href="#lg2">
                            <h4>会员注册</h4>
                        </a>
                    </div>
                    <div class="tab-content">
                        <div id="lg1" class="tab-pane active">
                            <div class="login-form-container">
                                <div class="login-register-form">
                                    <%-- 提示错误信息 --%>
                                    <span style="color: red;font-size: 10pt;font-weight: bold;float:right">
                                        ${requestScope.errMsg}
                                    </span>

                                        <form action="MemberServlet" method="post">
                                        <!--增加一个隐藏域，表示该请求是什么请求，以方便servlet匹配-->
                                        <input type="hidden" name="action" value="login">
                                        <input type="text" name="user-name" value="${requestScope.username}" placeholder="输入账号"/>
                                        <input type="password" name="user-password" placeholder="输入密码"/>
                                        <div class="button-box">
                                            <div class="login-toggle-btn">
                                                <input type="checkbox"/>
                                                <a class="flote-none" href="javascript:void(0)">Remember me</a>
                                                <a href="#">忘记密码?</a>
                                            </div>
                                            <button type="submit"><span>登录</span></button>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                        <div id="lg2" class="tab-pane">
                            <div class="login-form-container">
                                <div class="login-register-form">
                                    <span class="errorMsg" style="color: red;font-size: 10pt;font-weight: bold;float:right">
                                        ${requestScope.errMsg}
                                    </span>
                                    <form action="MemberServlet" method="post">
                                        <!--增加一个隐藏域，表示该请求是什么请求，以方便servlet匹配-->
                                        <input type="hidden" name="action" value="register">
                                        <input type="text" id="username" name="user-name" placeholder="Username"/>
                                        <input type="password" id="password" name="user-password" placeholder="输入密码"/>
                                        <input type="password" id="repwd" name="user-password" placeholder="确认密码"/>
                                        <input name="user-email" id="email" placeholder="电子邮件" type="email"/>
                                        <input type="text" id="code" name="code" style="width: 50%" placeholder="验证码"/>　　
                                        <img id="codeImg" alt="" src="KaptchaServlet">
                                        <div class="button-box">
                                            <button type="submit" id="sub-btn"><span>会员注册</span></button>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<!-- login area end -->


```

这里是实现用户登录和注册的界面。

1、绑定了一个注册时的ajax请求，让鼠标移开的同时就能知道这个用户名是否存在。ajax请求依旧是通过getJSON方法发送的，向MemberServlet的 isExistUserName方法发送请求，同时将input框（即用户名输入框）中的value传过去，返回的数据是一个boolean型变量，根据变量内容来决定文本框上写什么内容。

2、注册信息的各种验证，看一下就知道是干啥的。



member中还有login_ok.jsp、register_ok.jsp等无关紧要的前端内容，这些里面只涉及到跳转首页的超链接，这里就不再展开了。



### 6.4 order

当用户点击生成订单后，会申请一个`OrderServlet?action=saveOrder`服务，这个服务里的重定向指向了checkout.jsp

#### 6.4.1 order/checkout.jsp

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge"/>
    <title>家居网购</title>
    <base href="<%=request.getContextPath() + "/"%>">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/>
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css"/>

</head>
<body>
<!-- Header Area start  -->
<div class="header section">
    <!-- Header Top Message Start -->
    <!-- Header Top  End -->
    <!-- Header Bottom  Start -->
    <div class="header-bottom d-none d-lg-block">
        <div class="container position-relative">
            <div class="row align-self-center">
                <!-- Header Logo Start -->
                <div class="col-auto align-self-center">
                    <div class="header-logo">
                        <a href="index.html"><img src="assets/images/logo/logo.png" alt="Site Logo"/></a>
                    </div>
                </div>
                <!-- Header Logo End -->
                <!-- Header Action Start -->
                <div class="col align-self-center">
                    <div class="header-actions">
                        <div class="header-bottom-set dropdown">
                            <a>欢迎: ${sessionScope.member.username}</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="#">订单管理</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="memberServlet?action=logout">安全退出</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<!-- Header Area End  -->
<!-- login area start -->
<div class="login-register-area pt-70px pb-100px">
    <div class="container">
        <div class="row">
            <div class="col-lg-7 col-md-12 ml-auto mr-auto">
                <div class="login-register-wrapper">
                    <div class="login-register-tab-list nav">
                        <a class="active" href="views/order/order.jsp">
                            <h4>订单已生成, 订单号:${sessionScope.order.id}</h4>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<!-- login area end -->

```

这个jsp中实际上没啥有价值的内容，值得一说的也就右上角的显示用户姓名。这个jsp主要是一个超链接引出下一个jsp，订单号那里是一个超链接，点击订单号，进而去访问`/order/order.jsp`



#### 6.4.2 order/order.jsp

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge"/>
    <title>家居网购</title>
    <base href="<%=request.getContextPath() + "/"%>">
    <!-- 移动端适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/>
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css">
</head>

<body>
<!-- Header Area start  -->
<div class="header section">
    <!-- Header Top  End -->
    <!-- Header Bottom  Start -->
    <div class="header-bottom d-none d-lg-block">
        <div class="container position-relative">
            <div class="row align-self-center">
                <!-- Header Logo Start -->
                <div class="col-auto align-self-center">
                    <div class="header-logo">
                        <a href="index.jsp"><img src="assets/images/logo/logo.png" alt="Site Logo"/></a>
                    </div>
                </div>
                <!-- Header Logo End -->
                <!-- Header Action Start -->
                <div class="col align-self-center">
                    <div class="header-actions">
                        <div class="header-bottom-set dropdown">
                            <a>欢迎:${sessionScope.member.username}</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="#">订单管理</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="#">安全退出</a>
                        </div>
                    </div>
                </div>
                <!-- Header Action End -->
            </div>
        </div>
    </div>
</div>
<!-- Cart Area Start -->
<div class="cart-main-area pt-70px pb-100px">
    <div class="container">
        <h3 class="cart-page-title">订单管理</h3>
        <div class="row">
            <div class="col-lg-12 col-md-12 col-sm-12 col-12">
                <form action="#">
                    <div class="table-content table-responsive cart-table-content">
                        <table>
                            <thead>
                            <tr>
				                <th>订单</th>
                                <th>日期</th>
                                <th>金额</th>
                                <th>状态</th>
                                <th>详情</th>
                            </tr>
                            </thead>
                            <tbody>
                            <tr>
				                <td class="product-name">${sessionScope.order.id}</td>
                                <td class="product-name">${sessionScope.order.date}</td>
                                <td class="product-price-cart"><span class="amount">${sessionScope.order.price}</span></td>
                                <td class="product-name"><a href="#">${sessionScope.order.status}</a></td>
                                <td class="product-remove">
                                    <a href="OrderItemServlet?action=getOrderItem"><i class="icon-eye"></i></a>
                                </td>
                            </tr>
                            </tbody>
                        </table>
                    </div>
                </form>
            </div>
        </div>
    </div>
</div>
```

这里实际上也没啥，就是从session中提出order，将order的各种信息做一个展示。

之后这里又有一个服务请求，`<a href="OrderItemServlet?action=getOrderItem">`，进而通过这个请求中的重定向，访问到order/order_detail.jsp。此时，这个请求中已经将orderItem对象放入了request域中，以便order/order_detail.jsp使用



#### 6.4.3 order/order_detail.jsp

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge"/>
    <title>家居网购</title>
    <base href="<%=request.getContextPath() + "/"%>">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"/>
    <link rel="stylesheet" href="assets/css/vendor/vendor.min.css"/>
    <link rel="stylesheet" href="assets/css/plugins/plugins.min.css"/>
    <link rel="stylesheet" href="assets/css/style.min.css"/>
</head>

<body>
<!-- Header Area start  -->
<div class="header section">
    <!-- Header Top Message Start -->
    <!-- Header Top  End -->
    <!-- Header Bottom  Start -->
    <div class="header-bottom d-none d-lg-block">
        <div class="container position-relative">
            <div class="row align-self-center">
                <!-- Header Logo Start -->
                <div class="col-auto align-self-center">
                    <div class="header-logo">
                        <a href="index.html"><img src="assets/images/logo/logo.png" alt="Site Logo"/></a>
                    </div>
                </div>
                <!-- Header Logo End -->
                <!-- Header Action Start -->
                <div class="col align-self-center">
                    <div class="header-actions">
                        <div class="header-bottom-set dropdown">
                            <a>欢迎: ${sessionScope.member.username}</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="#">订单管理</a>
                        </div>
                        <div class="header-bottom-set dropdown">
                            <a href="#">安全退出</a>
                        </div>
                    </div>
                </div>
                <!-- Header Action End -->
            </div>
        </div>
    </div>
    <!-- Header Bottom  Start 手机端的header -->
    <div class="header-bottom d-lg-none sticky-nav bg-white">
        <div class="container position-relative">
            <div class="row align-self-center">
                <!-- Header Logo Start -->
                <div class="col-auto align-self-center">
                    <div class="header-logo">
                        <a href="index.jsp"><img width="280px" src="assets/images/logo/logo.png"
                                                  alt="Site Logo"/></a>
                    </div>
                </div>
                <!-- Header Logo End -->
            </div>
        </div>
    </div>
    <!-- Main Menu Start -->
    <div style="width: 100%;height: 50px;background-color: black"></div>
    <!-- Main Menu End -->
</div>

<div class="cart-main-area pt-100px pb-100px">
    <div class="container">
        <h3 class="cart-page-title">订单-16248893425621</h3>
        <div class="row">
            <div class="col-lg-12 col-md-12 col-sm-12 col-12">
                <form action="#">
                    <div class="table-content table-responsive cart-table-content">
                        <table>
                            <thead>
                            <tr>

                                <th>家居名</th>
                                <th>单价</th>
                                <th>数量</th>
                                <th>金额</th>

                            </tr>
                            </thead>
                            <tbody>
                            <c:forEach items="${requestScope.orderItems}" var="order">
                                <tr>
                                    <td class="product-name"><a href="#">${order.name}</a></td>
                                    <td class="product-price-cart"><span class="amount">${order.price}</span></td>
                                    <td class="product-quantity">${order.count}</td>
                                    <td class="product-subtotal">${order.totalPrice}</td>
                                </tr>
                            </c:forEach>
                            </tbody>
                        </table>
                    </div>
                    <div class="row">
                        <div class="col-lg-12">
                            <div class="cart-shiping-update-wrapper">
                                <h4>总价 ${sessionScope.order.price}元</h4>
                                <div class="cart-clear">
                                    <a href="#">继 续 购 物</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </form>

            </div>
        </div>
    </div>
</div>
<!-- Cart Area End -->

```

这里也没啥细节，就是将放入request的orderItem拿出来展示罢了



### 6.5 manager

之后就是自成一派的manager了。manager是自己一套独立的jsp，跟客户的jsp互不冲突，主要处理家具的具体细节。这里的细节和正面的细节大差不差，就不再赘述了



