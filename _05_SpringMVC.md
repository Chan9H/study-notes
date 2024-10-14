# SpringMVC 

SpringMVC 是 WEB 层框架。SpringMVC 接管了 Web 层组件, 比如控制器, 视图, 视图解析, 返回给用户的数据格式, 同时支持 MVC 的开发模式/开发架构。

SpringMVC 通过注解，让Bean成为控制器，不需要继承类或者实现接口。

SpringMVC 采用低耦合的组件设计方式，具有更好扩展和灵活性。

SpringMVC支持 REST 格式的 URL 请求。

SpringMVC 是基于 Spring 的, 也就是 SpringMVC 是在 Spring 基础上的。SpringMVC 的核心包 spring-webmvc-xx.jar 和 spring-web-xx.jar。



先提前梳理一下 Spring、SpringMVC、SpringBoot 的关系：
1. Spring MVC 只是 Spring 处理 WEB 层请求的一个模块/组件, Spring MVC 的基石是Servlet（Java WEB）

2. Spring Boot 是为了简化开发者的使用, 推出的框架(约定优于配置，简化了 Spring 的配置流程), SpringBoot 包含很多组件/框架，Spring就是最核心的内容之一，也包含 SpringMVC

3. 他们的关系大概是: Spring Boot > Spring > Spring MVC。

   

## 一、执行流程

在具体进入SpringMVC之前，先看看SpringMVC的执行流程：

![image-20231115175456396](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20231115175456396.png)

由图可以看出，SpringMVC的核心就是DispatcherServlet（核心控制器），它负责解析浏览器发送的http请求来判断需要哪个服务，调度具体服务来得到相应的结果，调用视图解析器来确定服务得到的结果会返回给哪个界面。之后在手动实现时会进一步理解这个流程。





## 二、配置

SpringMVC是面向web的框架，并且核心还是Servlet那一套，那么其势必是要配置Servlet到web.xml文件里的。但是SpringMVC与之前的javaWeb相比，不需要繁琐的去web.xml里配置多个Servlet来对应不同的服务，只需要在web.xml里配置好核心控制器就行，其他的工作会交给核心控制器的。因此SpringMVC相比javaWeb简化的许多。



### 2.1 DispatcherServlet配置

首先配置核心控制器的内部需要信息。SpringMVC之所以叫Spring，那是因为其应用了Spring的机制——IOC和AOP。而作为SpringMVC的核心——核心控制器，其势必也用到了Spring的功能，在配置时，常用的功能也就是IOC机制了。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/cache"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd">

<!--    Spring配置文件-->

<!--    配置自动扫描的包-->
    <context:component-scan base-package="web"/>

<!--    配置视图解析器(Spring提供的)-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">

<!--        配置该解析器的两个属性：前缀和后缀。主要是在自己的servlet服务里的方法中return好retrun，比如UserServlet里login方法
            retrun的是"login_ok"，该视图解析器拿到后，就会自动拼接上前缀和后缀，变为"/WEB-INF/pages/login_ok.jsp"，然后根据该路径去找请求访问的服务-->
        <property name="prefix" value="/_01_base/pages/"/>
        <property name="suffix" value=".jsp"/>
    </bean>



</beans>
```

在核心处理器中，要配置的就是一个视图解析器。视图解析器的作用就是当处理完请求后，正准备向前端返回。则用视图解析器来确定返回给哪个jsp。



### 2.2 web.xml配置

当配置好核心控制器内部后，就该把核心控制器给配到web项目中了（以Servlet的形式）。

这里配置进web项目的流程也很简单，就是将其作为一个常规servlet服务，配配`Servlet`、配配`servlet-mapping`就完事了。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

<!--    Web配置文件-->

<!--    配置核心控制器。用户的请求会通过该控制器处理。该控制器是引入的包中存在的，不需要自己创建-->
    <servlet>
        <servlet-name>SpringDispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

<!--        除了配置servlet内容之外，还要配置一个属性，用来指定该servlet去操作的spring配置文件，若不在这里配置，那么会去默认路径下找配置文件：
            WEB-INF/springEDispatcherServlet-servlet.xml，这个就是默认文件，若不在这里配，那么就得保证这个文件存在-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:MyapplicationContext_mvc.xml</param-value>
        </init-param>

<!--        在web项目启动时，自动加载该servlet-->
        <load-on-startup>1</load-on-startup>

    </servlet>
    <servlet-mapping>
        <servlet-name>SpringDispatcherServlet</servlet-name>
<!--        urlpattern配置成/，表示所有的请求都通过此控制器-->
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```



## 三、用法

当配置好SpringMVC后，就该开始准备使用了。下面逐条讲解一下该如何使用该框架。



### 3.1 入门使用

直接上案例：

```java
package web._01_base._01_out;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

/**
 * 回想一下在没学spring时，像做一个servlet类就要让其继承HTTPServlet类重写get和post方法才行，这里不需要再继承了
 * 直接用Controller注解一下就行。注解完之后，Spring扫描到就注入容器了（IOP原理）
 */
@Controller
public class _01_Out_UserServlet {

    //编写方法响应用户请求，这里也得用注解标注才行
    @RequestMapping(value = "/login")
    //此处标注使用的是RequestMapping,其value表示了请求头里发送的请求方法。比如：http://localhost8080/Alluse/FurnServlet/login，
    // 这个在原来表示访问的是allUse项目下的FurnServlet服务中的login方法，
    // 而这里标注一下就相当于把web.xml里的配置全省了，并且省去了servlet的配置（通过@Controller配好了），直接访问该value就可以请求到该方法
    //http://localhost:8080/Alluse/login，这样就可以直接访问到该方法
    public String login(){
        System.out.println("login..ok");
        return "login_ok";
        //此处返回的结果会给到视图解析器（InternalResourceViewResolver），视图解析器会根据配置来决定跳转到哪个界面，
        //返回的结果要指向一个jsp文件，即return回的字符串，要是一个jsp文件的文件名
    }
}

```

简单解释一下，

首先这个类用`Controller`注解一遍之后就成了一个handller，核心控制器就可以去handller集合中找到该类并解析出请求对应的方法了。

其次login方法上标注的注释`RequestMapping`则指代了该方法的url路径，核心控制器就是通过解析出http请求发现具体的url，来控制使用具体的方法的。

最后返回的目前看来是一个String，但是实际上是一个视图解析器，不过SpringMVC中，默认将String也视为视图解析器的一种了（最简单的视图解析器）。



### 3.2 RequestMapping

`RequestMapping`--请求映射，可以指定控制器的某个方法的请求的 url, 基本用法前面我们讲过了。

RequestMapping 可以修饰方法和类 。RequestMapping 注解可以修饰方法，还可以修饰类。当同时修饰类和方法时，请求的 url 就是组合` /类请求值/方法请求值`。



#### 3.2.1 类定义

```java
@RequestMapping(value = "/user")
@Controller
public class _02_RequestMapping_UserHandler {
    
}
```

这里在类上也配置了一个RequestMapping，则浏览器在访问该类下的方法时，其url要加上该value才行。



#### 3.2.2 组合请求

```java
@RequestMapping(value = "/user")
@Controller
public class _02_RequestMapping_UserHandler {
    
    /**
 * 1. method=RequestMethod.POST: 表示请求 buy 目标方法必须是 post
 * 2. RequestMethod 常用的四个选项 POST, GET, PUT, DELETE
 * 3. 若不写method=RequestMethod，则SpringMVC 控制器默认支持 GET 和 POST 两种方式
 * @return
 */
    @RequestMapping(value = "/buy",method = RequestMethod.POST)
    public String buy() {
        System.out.println("购买商品");
        return "success";
    }
}
```

这里，buy方法的请求为——`http://localhost:8080/SpringMVC/user/buy`

细节在代码中已经说明了，就不再赘述。



#### 3.2.3 含参使用

RequestMapping 可指定 params 和 headers 支持简单表达式 。

其常见的使用方式如下：

`param1`: 表示请求必须包含名为 param1 的请求参数；

`!=param1`: 表示请求不能包含名为 param1 的请求参数；

`param1 != value1`: 表示请求包含名为 param1 的请求参数，但其值不能为 value1；

`{"param1=value1", "param2"}`: 请求必须包含名为 param1 和 param2 的两个请求参数，且param1参数的值必须为value1。



先看下案例：

```java
@RequestMapping(value = "/user")
@Controller
public class _02_RequestMapping_UserHandler {
    
    @RequestMapping(value = "/find",params = "bookId")
    public String search(String bookId){
        System.out.println(bookId);
        return "success";
    }
}
```

这里在请求中，要求了得带上一个参数名为`bookId`的参数，并且在方法中使用了该参数。

此时需要发送的请求就变为了：`http://localhost:8080/SpringMVC/user/buy?bookId=xxx`



#### 3.2.4 Ant风格

`RequestMapping`支持 Ant 风格资源地址

`?`：匹配文件名中的一个字符

`*`：匹配文件名中的任意字符

`**`:匹配多层路径

举例如下:

`/user/*/createUser`: 匹配 /user/aaa/createUser、/user/bbb/createUser 等 URL;
`/user/**/createUser`: 匹配 /user/createUser、/user/aaa/bbb/createUser 等 URL;
`/user/createUser??`: 匹配 /user/createUseraa、/user/createUserbb 等 URL。



看看例子：

```java
@RequestMapping(value = "/user")
@Controller
public class _02_RequestMapping_UserHandler {
    @RequestMapping(value = "/message/**")
    public String message(){
        System.out.println("1");
        return "success";
    }
}

```

此时需要的请求为:`http://localhost:8080/SpringMVC/user/message/aa/bb/cc/d(后面abcd任意)`



#### 3.2.5 占位符

直接看例子就行

```java
/**
 * 1. @RequestMapping 还可以配合 @PathVariable 映射 URL 绑定的占位符。
 * 2. 这样就不需要在 url 地址上带参数名了，更加的简洁明了
 * 以往写前端请求都是：/SpringMMV/***Servlet?userName=xiaoming&userId=1234
 * 看起来费劲，现在就不需要了，可以优化成/SpringMVC/***Servlet/xiaoming/1234
 */
@RequestMapping(value = "/mi/{username}/{userid}")
public String mi(@PathVariable("username") String name,
                @PathVariable("userid") String id){
    System.out.println(name + " " + id);
    return "success";
}
```



### 3.3 Rest请求

#### 3.3.1 说明

 REST：即 Representational State Transfer。(资源)表现层状态转化。是目前流行的请求方式。它结构清晰, 很多网站采用。

HTTP 协议里面，常用四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE 用来删除资源。

而我们一些操作一遍都是只支持get或post请求的，如form表单，这时想用Put、Delelte请求就得需要Rest来操作了。



其使用总结如下：

当浏览器只支持 post/get 请求时，为了得到 put/delete 的请求方式需要使用 Spring 提供的 HiddenHttpMethodFilter 过滤器进行转换；

HiddenHttpMethodFilter：浏览器 form 表单只支持 GET 与 POST 请求，而 DELETE、PUT 等 method 并不支持，Spring 添加了一个过滤器，可以将这些请求转换为标准的 http 方法，使得支持 GET、POST、PUT 与 DELETE 请求；

这个过滤器需要在 web.xml 中配置。

```xml
 <filter>     
 	<filter-name>hiddenHttpMethodFilter</filter-name>     
 	<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>     
 </filter>     
 <filter-mapping>     
 	<filter-name>hiddenHttpMethodFilter</filter-name>     
 	<url-pattern>/*</url-pattern>     
 </filter-mapping>     
```

在所有的路径中都使用REST过滤。



#### 3.3.2 使用

使用就没什么好说的了，流程还是之前的流程，直接拿来用就行。

```java
package web._01_base._03_Rest;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

/**
 * Rest是目前主流的请求方式，很多网站采用，其核心是个过滤器，将get或post请求转变成下面四种请求
 * HTTP协议中，常见四种请求：GET（用来获取资源）、POST（用来新建资源）、PUT（用来更新资源）、DELETE（用来删除资源）
 */
@RequestMapping(value = "/book")
@Controller
public class _03_Rest {

    @RequestMapping(value = "/getbook/{id}",method = RequestMethod.GET)
    public String getBook(@PathVariable("id") String id){
        System.out.println(id);
        return "success";
    }


    @RequestMapping(value = "/addbook",method = RequestMethod.POST)
    public String addBook(String bookName){
        System.out.println(bookName);
        return "success";
    }

    @RequestMapping(value = "/delbook/{id}",method = RequestMethod.DELETE)
    public String delBook(@PathVariable("id") String id){
        System.out.println(id);
        return "success";
    }

}

```



### 3.4 请求映射

当前端打过来一个请求后，会出来一个请求头，服务器往往是解析这个请求头的。

那么如果请求头的格式与想要服务的格式对不上号该怎么办呢？这时就可以使用某种请求映射关系来一一对应上其中的内容。



#### 3.4.1 映射属性

举个例子说明一下问题：

```java
@RequestMapping("/vote")
@Controller
public class _04_VoteHandler {

    @RequestMapping("/vote01")
    public String vote1(String username){
        System.out.println(username);
        return "success";
    }
}
```

比如有一个服务为vote1，其接受的参数名称为"username"。但是如果前端打来的请求为`vote/vote01?name=jack`，此时会发现，服务可以正常启动，但是其内部参数由于参数名没对上，故为null。



此时就可以使用请求映射的注解来解决这个问题：`@RequestParam`

```java
/**
     * 若使用注解则可以避免空值
     * @RequestParam : 表示说明一个接受到的参数
     * value="name" : 接收的参数名是 name
     * required=false : 表示该参数可以有，也可以没有 ,如果 required=true,表示必须传递该参数
     */
    @RequestMapping("/vote02")
    public String vote2(@RequestParam(value = "name" ,required = false) String username){
        System.out.println(username);
        return "success";
    }
```



并且不止可以获取请求中的参数，还可以获取请求头、请求字段等内容：

```java
/**
     * 在请求中，不止参数可以获取，还可以获取请求头、字段等内容
     *
     */
    @RequestMapping("/vote03")
    public String vote3(@RequestHeader("Accept-Encoding")String ae,
                        @RequestHeader("Host")String host){
        System.out.println(ae + host);
        return "success";
    }
```





#### 3.4.2 映射对象

再扩展一下，回顾一下之前的web项目，想从前端传来的数据中实例化一个对象放入数据库，都是解析出请求头里的对象数据，然后再手动封装进实例里，但是SpringMVC中就简单多了，其可以自动封装好。

```java
     * 1、方法的形参用需要的类型来指定一下就行，如这里想做一个master对象，则直接用master来接受，SpringMVC会自动封装。
     * 要求对象属性和前端传入的参数名一致
     * 2、如果master中有另一个对象，如dog，则通过字段名.字段名赋值，如dog.id
     */
    @RequestMapping("/vote04")
    public String vote4(master master){
        System.out.println(master);
        return "success";
    }
```

就是对前端数据格式有要求，必须与后端的bean对象属性完全一致才行。

如，后端bean如下：

```java
public class master {
    private Integer id;
    private String name;
    private dog dog;

}
```

则前端jsp则必须如下传递内容:

```jsp
<h2>封装对象</h2>
<form action="vote/vote04" method="post">
  主人号:<input type="text" name="id"><br>
  主人名:<input type="text" name="name"><br>
  宠物名:<input type="text" name="dog.name"><br>
  <input type="submit" value="添加主人">
</form>
```

即，前端表单提交的数据的`name`要和后端bean对象的属性一致，才能让SpringMVC完成自动封装。



 

### 3.5 request域



#### 3.5.1 放入对象

考虑一个场景，前端提交了一个表单，那么这个表单会存在于request域中吗？答案是会的，SpringMVC会自动将前端发来的信息打包进request域中，其流程为：提交完表单的那一刻，第一步是先封装对象，根据表单里的文本框名称与调用的servlet形参中的类相对应，去创建该类的实例对象封装起来，然后将对象放入request域。

比如前端提交表单为：

```html
<br/><hr/> 
<h1>添加主人信息[测试 Map ]</h1> 
<form action="vote/vote06" method="post"> 
主人号:<input type="text" name="id"><br> 
主人名:<input type="text" name="name"><br> 
宠物号:<input type="text" name="pet.id"><br> 
宠物名:<input type="text" name="pet.name"><br> 
<input type="submit" value="添加主人和宠物"> 
</form> 
```

这里的bean对象就是上一节例子里举的master对象。



则后端中可以这样处理：

```java
  @RequestMapping(value = "/model")     
  public String test05(Master master, HttpServletRequest request, HttpServletResponse response) {     
  //1. springmvc 会自动把获取的 model 模型，放入到 request 域中，名字就是 master   
  //2. 也可以手动将 master 放入到 request
     //request.setAttribute("master", master);
       //返回到一个结果
       return "vote_ok";
       }
```

springmvc 会自动把获取的 model 模型，放入到 request 域中，名字就是 形参列表中类名的首字母小写master，即默认做了一个request.setAttribute("master", master)；也可以手动将 master 放入到 request —— request.setAttribute("master", master)

当前，这是有个前提的，就是前端界面的文本框属性名要和bean类里的属性名对应，如    宠物号:`<input type="text" name="dog.id"><br>`，要和master的dog属性的id属性名称一样，都叫id。



经过后端的SpringMVC自动装入request后，就可以再次在前端取出request中的东西了：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>vote_ok </title>
</head>
<body>
<h1>获取的的数据显示页面</h1>
<hr>
取出 request 域的数据
<br>
address: ${address }<br>
主人名字= ${requestScope.master.name }
主人信息= ${requestScope.master }
宠物名字= ${requestScope.master.pet.name }
</body>
</html>
```



#### 3.5.2 放入Map

这里标题起为放入Map不太准确，实际上是放入Map里的内容到request中。如：

```java
@RequestMapping("/test")
publice void test(Map<String,String> myMap){
    
    Map<String,String> myMap = new Map<>();
	myMap.put("keyA","valueA");
	myMap.put("keyB","valueB");
    
}

```

有一个服务如上例所示，注意，哪怕前端传来的形参中没用Map，服务里的形参列表里也是可以有Map的，只不过是空（是{}而不是null）而已，并且如果形参列表里有其他bean类，则myMap里又会不同，等下细说。

当对myMap里put入两条信息后，SpringMVC会执行如下操作：

```java
request.setAttribute("KeyA", "valueA");
request.setAttribute("KeyB", "valueB");
```

也就是说，放入request域中的不是Map本体，而是遍历Map里存放的数据并依次放入request中。



下面看个实际场景：

```html
<h1>02</h1>
<form action="Model/model02" method="post">
    主人号:<input type="text" name="id"><br>
    主人名:<input type="text" name="name"><br>
    宠物号:<input type="text" name="dog.id"><br>
    宠物名:<input type="text" name="dog.name"><br>
    <input type="submit" value="添加主人和宠物">
</form>
```

前端提交如上表单。



后端对应的服务如下：

```java
    @RequestMapping("/model02")
    public String model02(master m , Map<String,Object> map){//自动将m封装进map里
        map.put("address","beijing");//随便向map里添加一个属性

        map.put("master",null);//这里如果在map中添加一个master-null对，则springMvc在遍历map时，会将key为master位置的value改为null。而之前将对象放入request时，已经放入过一个master了，这时就给这个覆盖掉了。
        return "Model_ok";

    }
```

这里提一个细节，当后端的形参列表既有bean对象又有Map时，那么SpringMVC会自动将bean对象放入该map中，key为bean对象的类名、value为bean对象的属性集合——`{master = master{id=null, name='null', dog=null}`。

而如果后面在map里将master对应的value从bean对象改为null后，返回的前端`Model_ok`也会显示null，由此可见，自动将map装入request域是在后端服务提交后完成的，也就是return后，SpringMVC解析出Map内部存放的信息并放入request中



```jsp
<body>
<h1>获取的的数据显示页面</h1>
<hr>
取出 request 域的数据
<br>
address: ${address }<br>
${requestScope.master.name }
${requestScope.master }
${requestScope.master.dog.name }


<hr>
取出session数据<br>
address:${sessionScope.address}
主人名字= ${sessionScope.master.name }
主人信息= ${sessionScope.master }
</body>
</html>
```



#### 3.5.3 ModelAndView

Springmvc还提供了一个对象叫做ModelAndView，其也可以携带数据并被SpringMVC放入到request中的。其流程和map一致，都是将master对象放入request先，然后判断servlet里有没有ModelAndView对象，如果有，则将ModelAndView遍历，将其内部属性逐一放进request中。

严格来说，之前的所有返回，如 return "Model_ok"，本质是返回的ModelAndView对象，只不过我们返回的string字符串被SpringMVC自动封装ModeAndView对象里了。

下面展示一下如何手动向ModelAndView中放入request域数据。

```java
@RequestMapping("/model03")
    public ModelAndView model03(master m){

        ModelAndView modelAndView = new ModelAndView();

        modelAndView.addObject("address","beijing");
        modelAndView.addObject("master",null);//这里效果和map调整master值的效果一样，都给request最初放入的master覆盖掉了

        modelAndView.setViewName("Model_ok");//与之前的方法不同，这里是将要跳转的界面也放入modelAndView对象中，然后返回的是该对象，SpringMVC会在对象中解析出其属性，就知道要跳转到哪了

        return modelAndView;
    }
```

最开始ModelAndView和Map一样，都是先默认将服务的形参列表里带的bean对象放入自己内部，最后也都是提交后给Spring解析出内部存放的各种key-value，然后放入request中。



#### 3.5.4 拓展

就不详细说了，一个是放入session域中，和放入request域中一个操作，不同的就是SpringMVC不会自动放入session，需要自己调用HttpSession对象手动放入。

再有一个就是前置通知方法，通过`@ModelAttribute`标识一个方法后，执行该contorller下的所有服务都会先调用此方法

```java
/**
     * 之前都是将对象放入request域中，下面展示一下如何放入session中
     * 实际上没啥特别的，就是用session调一次set方法就行
     *
     */
    @RequestMapping("/model04")
    public String model04(master m, HttpSession session){
        session.setAttribute("master",m);
        session.setAttribute("address","beijing");
        return "Model_ok";
    }


    /**
     * SpringMVC中也可也使用Spring里的前置通知方法的。
     * 使用ModelAttribut标识，标识完之后，该Controller下的其他servlet调用时，都会调用此前置方法
     */
    @ModelAttribute
    public void prepaer(){
        System.out.println("ModelAttribute方法执行了");
    }
}
```



### 3.6 视图



#### 3.6.1 自定义视图解析器

之前所有的return都是return给了SpringMVC默认的视图解析器，也就是配置SpringMVC时配置的：

```xml
    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
<!--        属性order标识视图解析器的优先级，这里把优先级置后（值越小优先级越高），而默认解析器的优先级是最低，其默认值是Integer.MAX_VALUE
            故这里会先用自己的解析器-->
        <property name="order" value="1"/>
    </bean>
```



我们也可也有自己的视图解析器：

```java
@Component(value = "myView")//将该视图作为组件放入容器中
public class MyView extends AbstractView {

    /**
     * 此方法为完成视图渲染的方法，继承AbstractView后必须实现的方法。
     * 并且该方法决定需要跳转的界面
     */
    @Override
    protected void renderMergedOutputModel(Map<String, Object> map, HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        System.out.println("进入自己的视图成功");


        //请求转发到下面的地址
        httpServletRequest.getRequestDispatcher("/_01_base/pages/viewSuccess.jsp").forward(httpServletRequest,httpServletResponse);
    }
}

```

继承了AbstractView的类可以视为一个视图使用。

在定义好自己的视图后，后端就可以有选择性的将一部分服务return到自己的视图解析器上。这里要注意一点，要将自己定义的视图解析器的优先级设置的比系统默认的视图解析器的优先级高，否则还是会return到系统的视图解析器上。

```java
@RequestMapping("_01_base/goods")
@Controller
public class GoodsHandler {

    @RequestMapping("/buy")
    public String buy(){
        System.out.println("buy方法被调用");
        return "myView";
    }
}
```



 自定义视图: 创建一个 View 的 bean, 该 bean 需要继承自 AbstractView, 并实现renderMergedOutputModel 方法，并把自定义 View 加入到 IOC 容器中。

自定义的视图处理器也需要配置到 ioc 容器，

MyView的调用优先级需要设置一下，设置 order 比 Integer.MAX_VAL 小的值. 以确保其在 InternalResourceViewResolver (系统默认解析器)之前被调用。



自定义视图-工作流程：

SpringMVC 调用目标方法, 返回自定义 View 在 IOC 容器中的 id；

SpringMVC 调用 BeanNameViewResolver 解析视图: 从 IOC 容器中获取 返回 id 值对应的 bean, 即自定义的 View 的对象；

SpringMVC 调用自定义视图的 renderMergedOutputModel 方法渲染视图；

注意，如果在 SpringMVC 调用目标方法, 返回自定义 View 在 IOC 容器中的 id, 不存在， 则仍然按照默认的视图处理器机制处理。





#### 3.6.2 请求转发和重定向

请求转发和重定向主要提一点，就是，重定向，不能重定向到WEB-INF目录下，因为该目录是tomcat内部运行目录，而重定向的内部逻辑则是浏览器请求服务器。服务器返回一个新url让浏览器重新请求，相当于外部访问，故无法访问到。

具体某个服务中的请求转发和请求重定向的操作方式如下：

```java
@RequestMapping("/order")
    public String order(){
        System.out.println("order");

        //请求转发到/_01_base/pages/myView。关键字forward表示请求转发
        return "forward:/_01_base/pages/viewSuccess.jsp";

        //redirect关键字表示重定向
        //return "redirect:/_01_base/pages/viewSuccess.jsp";
    }
```





## 四、手动实现SpringMVC

了解了SpringMVC的基本用法之后，就该进行原理方面的深入理解了。这里通过手动实现SpringMVC来一步一步加深认识。

手动实现SpringMVC的过程与手动实现Spring的过程一样，都是按照实现顺序来的而不是按照项目的顺序来的。



### 4.1 容器

在Spring中，容器是无论如何都要实现的。但是这里主要讲的SpringMVC，因此弱化一下容器的内容，有关单例多例的就不写了，某认都是单例的，直接存放入容器中。再提一嘴，AOP机制干脆就不实现了，其与SpringMVC并不交叉，写了也是各玩各的。



#### 4.1.1 属性

```java
public class MyApplicationContext {
    //定义一个属性，保存解析出来的包下的类名，以list形式保存。之后具体是否实例化这些类，要看类中是否有注解标注
    private List<String> classFullPathList = new ArrayList<>();

    //定义一个属性，用来存放反射后生成的bean对象（无论单例还是多例）
    public ConcurrentHashMap<String, Object> ioc = new ConcurrentHashMap<>();

    //定义一个属性，用来表示配置文件
    private String configLocation;
}
```

在这里，容器中定义三个属性，全类名集合、容器池、配置文件。

实际上简单点的化只有一个容器池就行（说白了就是单例池），全类名集合属性是解析xml文件时为了处理有多个包需要解析而做的；configLocation则更是可以在该容器构造器时当有参构造器的形参直接传入的。但是这里这么写了，那就按分开的来看。







#### 4.1.2 方法

> 构造器

```java
public class MyApplicationContext {
    public MyApplicationContext() {
    }

    public MyApplicationContext(String configLocation) {
        this.configLocation = configLocation;
    }
}
```

一个简单有参构造器和无参构造器，这里有参构造器只初始化了配置文件，其他啥也没干。



传入该构造器的形参（带解析的包）为：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans>
    <!--指定要扫描的包-->
    <component-scan base-package="Controller,Service"/>
</beans>
```

其String为：`classpath:mySpringMVCContext.xml`



> 初始化方法

先提前说一嘴，这个初始化方法是可以优化进有参构造器里面的。

```java
public class MyApplicationContext {
    
    public void init() {
        String basePackagePath = XMLparser.getBasePackage(configLocation.split(":")[1]);//通过XMLparser解析出xml文件里的待扫描的包，用冒号将classpath:mySpringMVCContext.xml给前后分隔开，只取后半部分
        String[] basePackages = basePackagePath.split(",");//将其按,分割开，放入String数组中。如，将”Controller,Service“按逗号分开
        if (basePackages.length > 0) {
            for (String pack : basePackages) {//遍历数组，得到各个具体的包，之后进行包扫描，将包下的类存放如classFullPathList中。
                scanPackage(pack);
            }
        }
        executeInstance();//初始化ioc容器，将该注入的注入
        executeAutoWired();//初始化完ioc容器后，对ioc容器内的bean该装配的装配

    }
    
}
```

这里也就完成的是容器的构建，其中的具体各个方法（XMLparser、scanPackage、executeInstance、executeAutoWired）下面依次讲解。

总之其初始化流程就是：将需要初始化的路径通过dom4j（XMLparse）解析出来，然后分别扫描好这些路径，该放入的放入、该注入的注入、该装配的装配。就完事了。



> XMLparser类

这里使用了一个xml文件解析类（自己写的），主要用于解析出xml文件里配置的需要注入容器的包的路径。

```java
package mySpringMVC.XMLparser;

import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.InputStream;

/**
 * 通过dom4j解析XML文件
 */
public class XMLparser {
    //编写一个方法用来解析父包
    public static String getBasePackage(String xmlFile){

        //1、得到解析器
        SAXReader saxReader = new SAXReader();

        //2、得到传入路径对应的类路径
        InputStream InputStream = XMLparser.class.getClassLoader().getResourceAsStream(xmlFile);


        try {
            //3、通过解析器读取该类路径，得到文档
            Document document = saxReader.read(InputStream);

            //4、得到文档里的跟节点，此处解析的为容器配置文件“mySpringMVCContext.xml”，其内部的跟节点为<beans>
            Element rootElement = document.getRootElement();

            //5、得到跟节点下的子元素"component-scan"
            Element componentScanElement = rootElement.element("component-scan");
            //6、得到该元素下的属性"base-package"，从而得到要放入容器的类的路径
            Attribute attribute = componentScanElement.attribute("base-package");
            String basePackage = attribute.getText();

            return basePackage;


        } catch (DocumentException e) {
            e.printStackTrace();
        }

        return "";
    }
}

```

思路很简单，拿到具体的xml文件，因为指导该文件的结构，因此直接找到子元素component-scan就能解析出该元素中的值，即包名。然后返回包名就行。



> scanPackage

扫描包的内容，将包内的各个类的路径放入到属性`classFullPathList`中，以便后面注入容器。

```java
public class MyApplicationContext {
    
    public void scanPackage(String myPackage) {
        //1、通过类加载器，得到传入的myPackage对应的工作路径下的路径，因此要将.改为\
        URL url = this.getClass().getClassLoader().getResource("/" + myPackage.replaceAll("\\.", "/"));

        //2、根据路径，对其进行扫描，得到该包下的类的全路径，保存到classFullPathList中
        String path = url.getFile();//将目录视为文件，得到该文件的path
        File dir = new File(path);//此目录做成一个文件

        //3、遍历dir文件，其内部可能是文件（子包），也可能是具体类。
        for (File f : dir.listFiles()) {

            if (f.isDirectory()) {//如果这个是子目录，则继续递归
                scanPackage(myPackage + "." + f.getName());//将子包名称拼接上当前包路径，继续扫描
            } else {//只要不是目录，无论是类(.class文件)还是其他类型文件都先放入list中，因为后续注入容器是看类里的注解，不影响以后实例出错
                String s = f.getName().replaceAll(".class", "");//得到全类名（全类名是不包含后面的.class后缀的，因此用空字符替代掉）
                String fullName = myPackage + "." + s;
                classFullPathList.add(fullName);
            }
        }

    }
}
```

流程也比较简单，就是无限的搜索传入包下的类，直到把类的路径全部放入到`classFullPathList`为止。



> executeInstance

将类注入容器的方法。通过刚刚扫描得到的类的全路径，判断这些类里是否被Comtroller、Service等需要注入容器的注解标注，如果被标注了，则放入属性`ioc`中：

```java
public class MyApplicationContext {
    
    public void executeInstance() {
        //若还没用扫描到类，则退出该方法
        if (classFullPathList.size() == 0) {
            return;
        }

        try {
            for (String classFullPath : classFullPathList) {
                Class<?> clazz = Class.forName(classFullPath);//根据全类名反射出该类名对应的类对象
                if (clazz.isAnnotationPresent(Controller.class)) {//如果类对象中存在注解Controller，则放入实例容器中
                    String simpleName = clazz.getSimpleName().substring(0, 1).toLowerCase() + clazz.getSimpleName().substring(1);//将首字母小写，简单点，就不考虑COntroller里value的情况了
                    ioc.put(simpleName, clazz.newInstance());//实例化该类对象，放入ioc中。
                } else if (clazz.isAnnotationPresent(Service.class)) {
                    Service serviceAnnotation = clazz.getAnnotation(Service.class);
                    String beanName = serviceAnnotation.value();//写Controller时没处理value，这里处理一下，展示展示
                    if ("".equals(beanName)) {//如果注解时没用给Service注解赋值，则使用默认机制注入Service，此时Controller就可以进行上面的内容了。
                        //但是Service不一样，因为Service类是实现的Service接口，故Service的默认机制是既用其实现的接口来作为容器中的key来标识，也用其类名来标识。即一个Service对象被多个key标注
                        //1、首先使用接口标注bean对象
                        Class<?>[] interfaces = clazz.getInterfaces();//得到该类实现的接口集合（可能不止实现了一个接口）
                        Object o = clazz.newInstance();//先做一个对象，以防止后面反复创建

                        for (Class<?> anInterface : interfaces) {//遍历接口集合，将每个被实现接口都作为一个key来存放如ioc中(同时首字母小写)
                            String beanName2 = anInterface.getSimpleName().substring(0, 1).toLowerCase() + anInterface.getSimpleName().substring(1);
                            ioc.put(beanName2, o);
                        }
                        //2、再使用本类名标注,与Controller一样
                        String simpleName = clazz.getSimpleName().substring(0, 1).toLowerCase() + clazz.getSimpleName().substring(1);//将首字母小写，简单点，就不考虑COntroller里value的情况了
                        ioc.put(simpleName, clazz.newInstance());//实例化该类对象，放入ioc中。
                    }
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

经典的注入容器过程。但是有一个值得一提的小细节，容器`ioc`集合中放的是key-value对，key直接就是类名，value则是类对应的对象。

但是在web项目中，service是由serviceImp类实现的service接口来实现的，那么ioc中则应该把这些全部识别出来，即将serviceImp实现的各个接口每一个当作一个key对应此serviceImp放入ioc中，同时还将serviceImp类自己类名当作key放入容器中。



> executeAutoWired

将容器的类自动装配的方法。这里实现容器的方法和Spring中不同，Spring中是创建好一个对象，并将其属性set好后再放入容器。而这里则换了一种方式先使用无参构造器将对象通过`executeInstance`放入容器先，然后再遍历一遍容器，同时使用此自动装配方法将容器中的类装配好。

```java
public class MyApplicationContext {
    
    public void executeAutoWired() {
    if (ioc.isEmpty()) {//若此时ioc还是空的，那就不用配了，直接退出
        return;
    }

    for (Map.Entry<String, Object> entry : ioc.entrySet()) {//遍历ioc中的所有内容。
        //ioc是currentHashMap类型的，其内部维护的是一个entry集合。故这里是用Entry来承载ioc遍历内容的
        String key = entry.getKey();//key就是存放如ioc的标识名
        Object bean = entry.getValue();//value就是具体bean对象

        //1、遍历bean对象，再遍历每个bean对象里的字段，看看字段是否被自动装配标识。目前已经在遍历bean对象的过程中了，故这里遍历bean对象的字段
        Field[] declaredFields = bean.getClass().getDeclaredFields();//先取出字段集合
        for (Field field : declaredFields) {//遍历字段集合
            //判断字段是否被AutoWired标注
            if (field.isAnnotationPresent(AutoWired.class)) {//若被装配，则去ioc中根据装配的value找对应的bean，并存放如该属性中
                //1、首先尝试得到AutoWired的值，若有值，则按这个值去ioc中找，若没用，则按默认值去找
                AutoWired autoWiredAnnotation = field.getAnnotation(AutoWired.class);
                String beanName = autoWiredAnnotation.value();//先尝试直接从注解里得到value
                if ("".equals(autoWiredAnnotation.value())) {
                    //若自动装配中没用赋值，则按bean类的首字母小写来找，而bean类也就是当前字段的类型，故字段类型首字母小写就行
                    Class<?> type = field.getType();//得到字段类型
                    beanName = type.getSimpleName().substring(0, 1).toLowerCase() + type.getSimpleName().substring(1);

                }
                //若注解里的value不是空，则进行以下判断
                if (null == ioc.get(beanName)) {//若配置的名字不存在于ioc中，则表示配置错名字了，抛出异常
                    throw new RuntimeException("ioc容器中不存在装配的bean对象");
                }

                //此时不管是通过默认的还是通过value的，总是是拿到了一个beanName，则继续通过反射set当前字段，同时防止字段是private，暴力破解一下
                field.setAccessible(true);
                try {
                    field.set(bean, ioc.get(beanName));//第一个Object是当前字段所属的bean，第二个Object是当前字段的类型
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

装配过程就相对简单了，逻辑前面已经实现了很多遍，就不再多说了。





#### 对比

最后说明一下SpringMVC中的容器和Spring中的容器实现对比



### 4.2 注解

注解没什么新鲜的，都是前面见过的注解，就集中写在这里，不再多做解释了。



> 自动装配注解

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

@Target(ElementType.FIELD)//Type标识标注的是类，FiELD表示标注的是字段
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface AutoWired {
    String value() default "";
}

```



> Controller注解（Servlet注解）

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

/**
 * 标识一个servlet
 */

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Controller {
    String value() default "";
}

```



> 路径映射注解

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

/**
 * 用来指定被标记类的映射路径
 */
@Target(ElementType.METHOD)//这里省点事，就不标记为type（标记在类上），只标记为方法的路径映射
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface RequestMapping {
    String value() default "";//做一个默认属性，空
}

```



> 请求映射注解

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

@Target(ElementType.PARAMETER)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface RequestParam {
    String value() default "";
}

```



> Json格式注解

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

/**
 * 该注解是用来标注方法，表示该方法的返回值是一个json的数据
 */
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface ResponseBody {
}
```



> Service注解

```java
package mySpringMVC.annotation;

import java.lang.annotation.*;

/**
 * 标注service，并注入容器中
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Service {
    String value() default "";
}

```



### 4.3 核心控制器

完成了容器的构建之后，就该开始考虑如何运行SpringMVC了，而运行SpringMVC必不可少的就是调用核心控制器，这里就先完成核心控制器，之后再按照SpringMVC项目的运行顺序依次完成：HandlerMapping、HandlerAdaptet、ViewResolver。



#### 4.3.1 属性

核心控制器中，属性有两个：handler映射、容器:

```java
public class MyDispatcherServlet extends HttpServlet {

    //定义一个属性，handlerList，保存myHandler对象，每个对象都是一组url和RequestMapping的映射
    private List<MyHandler> handlerList = new ArrayList<>();

    //定义一个属性，自己的Spring容器
    MyApplicationContext myApplicationContext = null;
}
```

其中handler映射是用来匹配前端的url请求的，即将后端中的handler的请求方式保存在一个集合中，当前端发来请求后，解析请求内容去这个集合中看看与哪个handler匹配就调用哪个handler

容器则就是常规容器，存放bean对象。



#### 4.3.2 方法

> 构造器

这里与其说是构造器，不如说是构造方法。核心处理器是一个Servlet，其继承HttpServlet类来完成doget和dopost的处理，那么其也可使用HttpServlet中的其他方法，如这里的构造方法：

```java
public class MyDispatcherServlet extends HttpServlet {
    //初始化方法，当tomcat调用该servlet时，会默认同时执行此init方法。而这个servlet又是核心控制器，并且配置时设定了tomcat启动时默认调用此控制器，故init方法会随着tomcat启动而调用
    //这里init方法，实际上是有两个的，一个无参的init，一个有参的init，参数为ServletConfig，该参数就是自己的配置文件，可以动态获取配置，因此选有参的init方法重写
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        super.init(servletConfig);
        String config = servletConfig.getInitParameter("MyContext");
        myApplicationContext = new MyApplicationContext(config);
        myApplicationContext.init();//初始化容器
        initHandlerMapping();//初始化Mapping映射
    }
}
```

这个是HttpServlet中的初始化方法，当tomcat调用该servlet时，会默认同时执行此init方法。而这个servlet又是核心控制器，并且配置时设定了tomcat启动时默认调用此控制器，故init方法会随着tomcat启动而调用。

 这里init方法，实际上是有两个的，一个无参的init，一个有参的init，参数为ServletConfig，该参数就是自己的配置文件，可以动态获取配置，因此选有参的init方法重写。

在这个方法里，通过`myApplicationContext.init()`初始化了容器属性；通过`initHandlerMapping()`初始化了handler映射属性。具体怎么实现的，后面慢慢看。



> doGet、doPost

核心处理器是Servlet，所以其必然要进行doGet处理或doPost处理，这也是继承 HttpServlet后应该完成的任务。

```java
public class MyDispatcherServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        executeDispatch(req,resp);
    }
}
```

这里在doGet中直接跳向doPost，doPost中使用请求分配方法来具体实现前端请求。请求分配方法后面讲解。



> initHandlerMapping

下面就按照执行流程来一步一步讲解SpringMVC的实现了。

看流程可以直到，当前端过来一个请求后，核心处理器会去HandlerMapping中找到这个请求对应的Handler，这里就先完成每个handler的映射，即属性`handlerList`的初始化（构造方法中的`initHandlerMapping()`）。



在使用`initHandlerMapping`之前，先看看handler类的结构，因为要保存到`handlerList`中的内容被泛型定义为了handler类型：

```java
/**
 * 该类记录请求的url与RequestMapping注解中返回的路径之间的映射关系。
 * 即web上请求了一个url，如何找到这个url对应的Controller（Servlet方法），就通过这个类来找，因为这个类就是保存两者之间映射关系的
 */
public class MyHandler {
    private String url;//请求的url
    private Object controller;//具体的controller对象
    private Method method;//准备反射调用controller对象中的方法

    public MyHandler(String url, Object controller, Method method) {
        this.url = url;
        this.controller = controller;
        this.method = method;
    }
}
//get和set就在笔记里写了，其在代码中是存在的。
```

在Handler里，会以某个方法为核心，记录访问该方法的url、该方法所属的类、以及该方法本身。



下面就看看如何初始化核心控制器的`handlerList`：

```java
public class MyDispatcherServlet extends HttpServlet {
    /**
     * 编写一个方法，完成url与Controller里方法的映射，即,将被RequestMapping注解标识了的方法放入HandlerList中，
     * 这样前端在请求某个url后，核心处理器就会直接从HandlerList中遍历寻找与请求url相对应的方法，进而通过反射调用该方法。
     */
    private void initHandlerMapping(){
        //因为是得到Controller方法里对应的url映射，所以要先判断容器中有没有Controller对象的实例，如果对象都没有，就谈不上对象里的方法了
        if (myApplicationContext.ioc.isEmpty()){//如果容器中还没有实例化的对象，那么直接退出方法即可
            return;
        }

        //遍历ioc中的bean对象，然后进行url映射处理
        for(Map.Entry<String, Object> entry: myApplicationContext.ioc.entrySet()){
            //通过getValue得到具体的实例化对象，然后通过getClass方法得到其Class类，这样才能得到其中的注解以及方法名
            Class<?> clazz = entry.getValue().getClass();

            //得到该class下的所有方法
            Method[] declaredMethods = clazz.getDeclaredMethods();

            //遍历之，判断方法上有没有注解RequestMapping，如果有了则进一步处理
            for(Method declaredMethod : declaredMethods){
                if (declaredMethod.isAnnotationPresent(RequestMapping.class)){
                    //若存在RequestMapping注解，则取出其值
                    RequestMapping annotation = declaredMethod.getAnnotation(RequestMapping.class);
                    String url = annotation.value();//这个值就是想请求该服务时前端需要请求的地址
                    String contextPath = getServletContext().getContextPath();
                    url = contextPath + url;


                    //将此地址与此Controller与此方法共同放入一个handler中保存，当前端请求后，会从handlerList中找与前端请求对应的handler，进而反射出其方法
                    MyHandler handler = new MyHandler(url,entry.getValue(),declaredMethod);
                    handlerList.add(handler);
                }
            }
        }
    }
}
```



实际上这里完成的工作，举个例子就是：

```java
@Controller
public class _02_RequestMapping_UserHandler {
    @RequestMapping(value = "/buy")
    public String buy() {
        System.out.println("购买商品");
        return "success";
    }
}
```

将这里的`"/buy"`、`_02_RequestMapping_UserHandler`、`buy()`三者保存在一个handler对象中（或者说一个handler对象记录了三者之间的联系），然后将handler对象放入核心控制器的handlerList里，这样前端打来一个url请求后，就可以根据该url去handlerlist中寻找。如果这个请求正好是`/buy`，那么就将这个handler取出来，反射调用handler中存放的方法`buy()`。至于具体寻找，就靠下面的getHandler方法了。



> getHandler

这个方法是接受前端打来的`request`请求，寻找该请求对应的handler的。

```java
public class MyDispatcherServlet extends HttpServlet {
    
    /**
     * 编写一个方法，通过request对象携带的url信息返回一个与该url相应的hanler映射（myHandler对象）
     */
    public MyHandler getHanler(HttpServletRequest request){
        //1、获取请求的uri，如http://localhost:8080/MySpringMVC/monster，则此uri为/MySpringMVC/monster。
        /* 要注意，此uri比保存在handler里的url多了一个工程路径名——MySpringMVC
        要解决此问题有两个方案，一是将tomcat配置里的工程路径只配一个反斜杠，另一个方案是在保存handler中的url属性时，加上拼接上工程路径getServletContext().getContextPath()
         这里采用方案二
         */
        String requestURI = request.getRequestURI();

        //2、遍历handlerList，判断是否存在该uri
        for (MyHandler handler : handlerList){
            if (requestURI.equals(handler.getUrl())){//若存在该uri，则返回该uri对应的handler，否则返回空
                return handler;
            }
        }
        return null;
    }
    
}
```

实现思路很简单，就不再多说了。



> 请求分发

可以说是核心方法了，首先使用`getHandler()`得到请求对应的url，完成执行流程的第一部分；之后通过反射调用找到的handler中存放的方法（这里内部涉及到请求映射的问题）；最后将反射方法返回的值作为View对象，返回给视图解析器，去解析最终要调哪个界面，整个流程就算结束了。

```java
/**
 * 编写方法，完成分发请求
 */
private void executeDispatch(HttpServletRequest request, HttpServletResponse response){
    //1、通过上面的方法得到request对应的url里的uri对应的服务
    MyHandler hanler = getHanler(request);


    try {
        //2、若不存在与url对应的服务，则返回404
        if (hanler == null){
            response.getWriter().write("<h1>404 NOT FOUND</h1>");
        } else {
        //3、若找到了对应的handler，则通过反射调用该handler的方法
            /**
             * 这里有大讲究。在之前用原生SpringMVC时，是可以在参数列表中使用注解的，以便于从前端拿值。
             * 如public String vote2(@RequestParam(value = "name" ,required = false)String username){}，这里就是用RequestParam标注了以下参数列表
             *
             * 这里将需要invoke的方法的参数封装到一个参数数组中，以便灵活的处理参数。并且invoke方法底层是支持可变参数的。
             */
            //3.1 得到需要被反射的方法的形参列表里的内容，将其封装到一个参数数组中
            Class<?>[] parameterTypes = hanler.getMethod().getParameterTypes();

            //3.2 根据刚刚做的形参数组做一个实参数组，以便反射方法时当作实参传入
            //首先看看request和response的情况，将此处的request和response直接拿到被反射的方法中就行，但是得按照被反射方法中的参数位置放，因此用i来记录位置
            Object[] params = new Object[parameterTypes.length];

            for (int i = 0; i < parameterTypes.length; i++){//遍历形参数组，看看里面都有哪些类型的参数，并看看这些参数的前后顺序
                Class<?> parameterType = parameterTypes[i];//取出每个形参


                if("HttpServletRequest".equals(parameterType.getSimpleName())){
                    params[i] = request;//将形参中的HttpServletRequest的位置原封不动的放到实参列表中
                }else if ("HttpServletResponse".equals(parameterType.getSimpleName())){
                    params[i] = response;
                }
            }

            //3.3 获取http请求中带的参数集合，并将该集合的数据按顺序填充到实参数组中
            //String是参数名、String[]是该参数名对应的参数值。
            // http://localhost:8080/mySpring/monster?name=jack&id=10，里，name就是参数名、第一个String；jack就是第一个String对应的参数值
            request.setCharacterEncoding("utf-8");//处理中文乱码问题
            Map<String, String[]> parameterMap = request.getParameterMap();
            for (Map.Entry<String,String[]> entry : parameterMap.entrySet()){//以entry的形式进行遍历

                String key = entry.getKey();
                String[] values = entry.getValue();
                //为了方便，这里只考虑value是单值的情况了
                String value = values[0];

                //之后开始准备将形参数组和实参数组的参数按位置一一对应上
                int indexRequestParameterIndex = getIndexRequestParameterIndex(hanler.getMethod(), key);
                if (indexRequestParameterIndex != -1) params[indexRequestParameterIndex] = value;//若确实存在一一对应的关系，则将实参数组中对应的位置存放上请求头里携带的对应key的value（即具体参数），以便反射回方法
                    //若请求头里的key与注解中的value匹配不上，则启动第二个保险，将请求头中的key尝试与目标方法中的形参列表里的参数名匹配（是参数名而不是参数类似，String s里的s），如匹配上，则依旧可以反射
                else {
                    //这里就不进行实现了，挺费劲，但是思路就是这个思路

                }

            }

            //接受以下调用方法的返回结果。然后交给视图解析器去解析该结果。
            Object result = hanler.getMethod().invoke(hanler.getController(), params);//第一个参数表示要反射到哪个类里的方法，第二个参数表示向反射方法里传入的参数

            //这里简单点，就当方法返回的值都是String，将视图解析器就简化为下面的代码
            if (result instanceof String){
                String viewName = (String) result;
                if (viewName.contains(":")){//如果返回结果中有冒号存在，则说明返回的结果为"forward:/login_ok.jsp"或redirect:/login这种类型
                    String viewType = viewName.split(":")[0];//forward 或者 redirect
                    String viewPage = viewName.split(":")[1];//具体跳转的url
                    System.out.println(viewPage);

                    if ("forward".equals(viewType)){//如果希望请求转发
                        request.getRequestDispatcher(viewPage).forward(request,response);
                    }else if("redirect".equals(viewType)){//如果想重定向
                        response.sendRedirect("/mySpringMVC" + viewPage);
                    }
                }else {//如果没用冒号，则目标方法retrun的是login_ok.jsp这种格式，则默认让其请求转发
                    System.out.println(viewName);
                    request.getRequestDispatcher("/" + viewName).forward(request,response);

                }
            }
            
            
            //再扩展一下，进行返回json格式的操作
            else if (result instanceof ArrayList){
                Method method = hanler.getMethod();
                if (method.isAnnotationPresent(ResponseBody.class)){//如果目标方法返回的类型是ArrayList，并且方法被ResponseBody标注了，那么就说明返回类型是json类型
                    //把result转成json类型的数据，然后返回，这里使用的是ObjectMapper类（jackson包下的类）
                    ObjectMapper objectMapper = new ObjectMapper();
                    String resJson = objectMapper.writeValueAsString(result);//这个方法可以直接将list数组转成json格式的字符串
                    response.setContentType("text/json;charset=utf-8");
                    PrintWriter writer = response.getWriter();
                    writer.write(resJson);
                    writer.flush();
                    writer.close();
                }
            }

        }
    }catch (Exception e) {
        e.printStackTrace();
    }
    
    
    
    //判断请求头里传入的参数key与注解中的value匹配情况，并记录于目标方法的对应参数位置上。
    //这个方法实际上是目标方法的参数位置、注解中的参数名、请求头中的参数名三方匹配的方法。
    // 如http://localhost:8080/mySpring/monster?name=jack&id=10;这里的name和id就是key
    public int getIndexRequestParameterIndex(Method method , String name){
        //得到method的所有形参的参数
        Parameter[] parameters = method.getParameters();
        //遍历之
        for (int i = 0; i < parameters.length; i++) {
            Parameter parameter = parameters[i];
            //判断该参数中是否有RequestParam注解
            boolean annotationPresent = parameter.isAnnotationPresent(RequestParam.class);
            if (annotationPresent){//如果有这个注解，则取出，以便匹配http请求里的传入参数

                //取出当前参数的RequestParam注解中的值，即取出@RequestParam(value="xxx")的xxx
                RequestParam parameterAnnotation = parameter.getAnnotation(RequestParam.class);
                String value = parameterAnnotation.value();

                //看看这个值——xxx是否能与请求头中传入的key对上，如果对上了，那么就代表找到了，返回这个参数所在的位置
                if (name.equals(value)){
                    return i;
                }

            }
        }
        return -1;
    }
}



```

在视图解析器这方面说明一个细节：重定向不能定向到/WEB-INF目录中，因为该目录是tomcat内部运行目录，而重定向的内部逻辑则是浏览器请求服务器，服务器返回一个新url让浏览器重新请求，相当于外部访问，故无法访问到。如果是请求转发是可以转发给该目录的。



### 4.4 配置

最后看看配置情况。一共需要两个配置文件，核心控制器的容器配置、web.xml的servlet配置。

> MySpringMVCContext

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans>
    <!--指定要扫描的包-->
    <component-scan base-package="Controller,Service"/>
</beans>
```



> web.xml

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>

  <!--将核心控制器配置到web.xml里，因为核心控制器本质也是一个servlet，故也应该被配置进web.xml里，让前端界面可以访问该服务-->
  <servlet>
    <servlet-name>MyDispatcherServlet</servlet-name>
    <servlet-class>mySpringMVC.servlet.MyDispatcherServlet</servlet-class>

    <!--指定要操作的spring容器文件-->
    <init-param>
      <param-name>MyContext</param-name>
      <param-value>classpath:mySpringMVCContext.xml</param-value>
    </init-param>


    <!--让核心控制器在tomcat启动时自动加载-->
    <load-on-startup>1</load-on-startup>

  </servlet>
  <servlet-mapping>
    <servlet-name>MyDispatcherServlet</servlet-name>
    <!--因为前端控制器是核心，处理前端发送的所有业务，故url部分应该为/，接受所有请求-->
    <url-pattern>/</url-pattern>
  </servlet-mapping>

</web-app>

```



