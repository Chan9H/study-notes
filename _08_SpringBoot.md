## yaml

基本语法：

1、形式为key: value，注意冒号后面有空格；

2、区分大小写；

3、使用缩进表示层级关系（python类）；

4、缩进一般不适用tab，使用空格；

5、缩进的空格数无所谓，只要统一集的同程度缩进即可；

6、字符串无需加引号，加了也不影响；

7、yaml中，注释使用`#`，跟python一样。



数据类型：

字面量：单个的，不可再分的值。date、boolean、string、number、null等。如下写法L:

```yaml
number: 1
name: tom
man: true
```



对象：键值对的集合，比如map、hash、set、object等等。如下写法：

```yaml
key1: {key2: value2, key3: value3}

key1:
  key2: value2
  key3: value3
```



数组：一组按次序排列的值，比如array、list等，写法如下：

```yaml
key1: [v1,v2,v3]

#注意写减号
key1: 
 -v1
 -v2
 -v3
```



## 静态资源

类路径：编译代码时的src-->main-->resources里的resources目录就是常说的类路径，为什么呢？因为这个路径对应了运行时目录——target路径下的target-->classes目录，classes目录就是类路径了。

只要静态资源放在类路径中的以下路径之一：/static，/public、/resources、/META-INF/resources，都是可以直接被访问的。这个是由WebProperties类中指定好的。

常见的静态资源如下：JS、CSS、图片、字体文件等等

访问方式为：项目根路径/+静态资源名。如:`http://localhost:8080/静态资源名`。这个访问方式也是WebProperties类中指定的。



细节：

静态资源的访问原理为：默认静态映射为`/**`，也就是说会拦截所有请求，当一个新请求进来后，会先看看当前的controller能不能处理，如果不能处理的就交给静态资源处理器，如果静态资源处理器也不能处理了，就返回404界面。

比如，有请求如下：`http://localhost:8080/1.jpg`，当服务器接受到该请求后，会先查看是否有controller的RequestMapping为`1.jpg`，如果没有，则去静态资源处理器中查看静态资源目录（上面介绍的四个目录）中是否有有`1.jpg`，如果有，则加载，没有则返回404。



当静态资源路径和controller的requestMapping冲突后，可以通过改变requestMapping来解决，也可以通修改静态资源的路径来修改，修改方式如下：

做一个名为`application`的配置文件，放在resources目录下。application文件中配置如下：

```yaml
spring:
 mvc:
  static-path-pattern: /newUrl/**
```

（刚学了yaml，因此这里用yaml格式的配置文件来写了，常规的application.properties配置文件也可）

(这里的/**必须要有，表示拦截下newUrl下的所有内容)

如此一来，静态资源访问的url就为：`http://localhost:8080/newUrl/1.jpg`了。



## Rest风格请求

想启动Rest风格的请求，要配置好过滤器才行。





## Thymeleaf

替代JSP的，概括来说是一个java库，作为SpringMVC的web应用中的view层

Thymeleaf页面不需服务器渲染，可直接被浏览器运行。类似于html文件直接用浏览器打开

Thymeleaf是服务器渲染技术，其数据是在服务器端进行渲染的。比如XX.html文件中有一段Thymeleaf代码，则在用户请求该界面时，后端处理引擎来处理这段代码并将结果返回。

要注意，使用了Thymeleaf技术后，就不是前后端分离的项目了，前后端的数据交互是在域中完成的，无论是request域还是session域等等，总之是在服务器端进行的渲染。



## 异常

默认情况下，SpringBoot提供`/error`来处理所有错误的映射，也就是说出现错误时，SpringBoot底层会请求转发到`/error`路径



## 过滤器和拦截器

使用范围不同：

过滤器是Servlet的一个接口，而这个接口是在Servlet规范中定义的，也就是说Filter的使用要依赖于Tomcat等容器，Filter只能在web程序中使用

拦截器（Interceptor）是Spring的组件，由Spring容器管理，并不依赖Tomcat，可以单独使用。不仅能应用在Tomcat中，还可以在Application中使用。



触发时机不同：

FIlter是Tomcat拿到请求后经过的；Interceptor是Tomcat——>Filter——>核心控制器之后，再经过拦截器的；过完拦截器后，下一步就是经过controller了。



过滤器不会处理请求转发，而拦截器会处理请求转发。请求重定向则全部都会处理（请求重定向相当于发了个新请求）。

请求转发是servlet内部处理的事，所以不经过过滤器。而请求重定向是外部打向tomcat的，会经过过滤器。也就是说，过滤器是外层的、拦截器是内层的。



要注意一点，拦截器是DispatcherServlet（核心控制器）的功能。这里梳理一下两种流程：

一，走核心控制器的：Tomcat——>Filter——>DispatcherServlet-->拦截器-->controller-->myBatis-->数据库。这是spring流程

二、走自定义servlet的：Tomcat——>Filter——>myServlet-->service-->dao-->数据库。这是tomcat流程

可见，核心控制器和自定义的servlet是同级的。当走的不是核心控制器时，是不会通过拦截器的。

当请求DispatcherServlet时，其路径为`localhost:8080/`；而当请求自定义的servlet时，其路径是自定义的具体url，如`localhost:8080/myservlet`。





