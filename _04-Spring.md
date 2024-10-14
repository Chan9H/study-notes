# Spring



## 一、ioc

`ioc`（Inversion Of Control）控制反转。是一种管理javabean类的方法。

传统的开发方式中，获得某个bean类的对象往往是从一个个独立的配置文件中获取的，之后使用反射机制完成在所需位置的对象创建。

在Spring中，使用ioc来控制bean对象的创立，其让bean对象在容器中先创建好，然后使用时从容器里直接拿出来用就行。



### 1.1 结构总览

首先看看`ioc`的使用语法。

```java
ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");//形参列表里传入ioc配置文件的路径（这里路径是类的加载路径，即out目录下的文件路径（out往往不写））
Object o = ioc.getBean("XXX");//通过getBean方法得到"XXX"指定的bean对象
```



在创建好ioc对象后，会发现这是一个重量级对象（内部内容非常多），下面会调一些核心属性讲解。



> beanFactory

bean工厂，ioc的核心属性，ioc目录下级的属性，里面存放着bean相关的全部信息。



> beandefinitionMap

bean定义Map，其table属性里存放着在xml文件里配置的所有bean对象信息。是beanFactory的下级属性

其table的性质时ConcurrentHashMap$Node[]，是一个匿名内部类的数组，数组中的每个数中都是一个节点，节点里存放key和value，key时配置bean时的id，value时bean对象本体。



> singletonObjects

单例对象，其中存放着配置文件中，所有定义为单例的配置对象。所谓单例对象，就是说整个流程中只创建一次的对象（构造器只启用一次），当Spring检查到某个bean的配置是单例后，会将其直接创建并存放近singletonObjects属性中，使用时直接从这里往外拿就行。这个过程往往不是懒加载过程。



> beandefinitionNames

bean定义名称集，是用来直观的观察xml文件里定义了多少bean对象的属性。



### 1.2 基于xml文件配置Bean对象

在使用Spring时，往往会定义一个beans.xml文件，该文件内定义着各种bean对象的信息，当Spring容器启动时，会扫描该文件，将这些bean配置信息读取以便，找到其中的非懒加载对象直接创建好对象放入singletonObjects属性中，当程序使用getBean方法时，直接从singletonObjects里查找并提取即可；对于懒加载对象，在程序中调用getBean方法是才进行对象的创建。

#### 1.2.0 Spring容器

在Spring中，系统会将xml里配置的对象放入容器中，那么这个识别xml的过程是什么呢？

其本质上是通过Dom4j来解析xml文件里的标签信息，把想要的标签给提取出来做进一步处理。下面实现一下：

```java
package _01_ioc._02_DoSpringContext;

import _01_ioc._01_bean.Monster;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.File;
import java.util.List;
import java.util.concurrent.ConcurrentHashMap;

/**
 * 简单的复现一个Spring的容器机制，在这里实现将xml文件的解析，对应对象的生成，放入容器，提供getBean方法等等
 */
public class ApplicationContext {

    //做一个ConcurrentHashMap类型的map，用来存放xml里解析出来的单例对象
    private ConcurrentHashMap<String,Object> singletonObjects = new ConcurrentHashMap<>();
    
    //提供一个getBean方法
    public Object getBean(String id){
        return singletonObjects.get(id);
    }

    //做一个该类的构造器，接收一个xml文件的路径
    public ApplicationContext(String iocBeanXmlFile) throws DocumentException, ClassNotFoundException, InstantiationException, IllegalAccessException {
        //1.由于xml文件的路径默认是在src下面的，而解析时要去out目录下解析（类加载路径下解析），故要先得到类加载路径
        String path = this.getClass().getResource("/").getPath();

        //2.创建一个dom4j的解析器，准备解析接收到的xml路径
        SAXReader saxReader = new SAXReader();

        //3.使用解析器解析解析xml文件为doucument对象
        Document document = saxReader.read(new File(path + iocBeanXmlFile));

        //4.获取doucment的跟元素信息，根元素为<beans>标签
        Element rootElement = document.getRootElement();

        //5.得到根元素的子元素标签，在这个实例中，使用的时beans。xml，故此时<beans>的子元素标签为<bean>
        Element bean = (Element) rootElement.element("bean");//若一个beans里有多个bean，则在后面加上.get(n)，来表示自己取的是第n+1个bean

        //6.此时bean变量表示的就是自己往xml里配置的bean标签了，可以提取出该标签的属性（不是具体bean对象的属性）（在此xml文件中，为<bean class="_01_bean.Monster" id="monster1">，class和id）
        String id = bean.attributeValue("id");
        String classFullPath = bean.attributeValue("class");
        //得到标签属性后，就可以通过反射得到具体对象了

        //7.能得到标签属性的同时，也是可以得到标签下的具体内容的，即property标签对应的部分
        //由于每个对象有多个属性，故用列表来接收property部分
        List<Element> property = bean.elements("property");

        String monsterStringId = property.get(0).attributeValue("value");//得到第一个property的value，即“01”
        Integer monsterId = Integer.parseInt(monsterStringId);//将id转为int型

        String name = property.get(1).attributeValue("value");//得到第二个property的value，即“牛魔王”

        String skill = property.get(2).attributeValue("value");//同理

        //8.使用反射机制，得到bean变量对应的对象
        Class<?> aClass = Class.forName(classFullPath);//得到classFullPath路径对应的类的Class类的实例
        Object o = aClass.newInstance();//将该类实例化，此时o实际上就是Monster了
        Monster monster = (Monster) o;

        //给monster对象赋值，科学一点的化应该是通过aClass对象来得到Monster对象下的方法池和属性池(使用aClass.getDeclaredMethods()等方法实现)，然后一一赋值给monster对象
        //这里简单点，通过解析的xml文件来赋值
        //可以看到，容器的底层是通过bean类里的setter方法来完成具体对象的构建的，因此做bean类时，一定要带上setter方法
        monster.setMonsterId(monsterId);
        monster.setName(name);
        monster.setSkill(skill);
        //此时monter对象就是完全体了

        //将monster对象放入singletonObjects的map中
        singletonObjects.put(id,monster);//这个id是bean标签下的属性，即monster1

    }

}

```



#### 1.2.1 通过类型配置bean

先做一个javabean类，这里就不笼统的单独写具体的类长什么样了，大概说一下类中的结构完事，下面使用时直接自适应。

```java
public class "XXX"{
    private int id;
    private String name;//有几个属性
    
    public XXX(){};//无参构造器
    public XXX(x,x){};//有参构造器
    
    public void set(){};//set方法
    public Object get(){};//get方法
}

```

该类bean类中，一定要做一个无参构造（以供反射使用）和set方法（以供Spring配置使用）。



然后是配置文件：

```xml
<bean class="_01_bean.Monster">  
<!--        这里这个bean绑定到了Monster这个类上,可以在配置文件中直接实例化该类的对象了-->
<!--        property标签表示bean类下的属性，此时只需要指定属性名称和属性值，就相当于配置和这个bean对象了-->
        <property name="monsterId" value="01"/><!--给对象的属性赋值,此处给monsterId这个属性赋值了，这里赋值的本质是调用bean类里的set方法，因此一定要做get和set，以方便使用-->
        <property name="name" value="牛魔王"/>
        <property name="skill" value="芭蕉扇"/><!--如果不给属性赋值,则自动赋默认值-->
    </bean>
```

这里使用的是通过类名来配置，即在bean标签下，只赋值一个属性：class，赋值为想配置bean对象的类路径。

之后就可以在程序中直接拿配置好的对象用了。但是基于类配置要注意一点，就是配置文件中，只能有一个该类的基于类配置的bean信息，不能有第二个了，否则Spring会不知道谁是谁，想解决这个问题，就可以用基于id配置。

在程序中调用方法如下：

```java
import _01_bean.Monster;

public void Run(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        Monster monster = ioc.getBean(Monster.class);
    }
```



#### 1.2.2 基于id配置

其可以视为是基于类配置的优化，在配置好class属性后，多配一个id属性，来唯一的标识当前配置的bean对象的名称

```xml
<beans>
	<bean class="_01_bean.Monster" id="monster1">  <!--指定想创建的bean对象的路径,内部会通过反射得到该类的信息,id是唯一一个再容器中的id,使用该bean对象是通过id调用-->
<!--        这里这个bean绑定到了Monster这个类上,可以在配置文件中直接实例化该类的对象了-->
<!--        property标签表示bean类下的属性，此时只需要指定属性名称和属性值，就相当于配置和这个bean对象了-->
        <property name="monsterId" value="01"/><!--给对象的属性赋值,此处给monsterId这个属性赋值了，这里赋值的本质是调用bean类里的set方法，因此一定要做get和set，以方便使用-->
        <property name="name" value="牛魔王"/>
        <property name="skill" value="芭蕉扇"/><!--如果不给属性赋值,则自动赋默认值-->
    </bean>
</beans> 

```

此时只要保证同一个bean类配置下没有两个相同的id就行了。

其调用方法如下：

```java
import _01_bean.Monster;

public void Run(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        Monster monster = ioc.getBean("monster1",Monster.class);
    }
```



#### 1.2.3 通过构造器配置

一个挺离谱的配置方法，因为一个类中不可能出现两个完全相同的构造器，所以可以根据构造器的不同，在配置时指定构造器对应参数（可通过index对应、name对应、数据类型对应）的值，就可以提取出bean配置文件中对应的bean对象了。

```xml
<beans>
    <bean class="_01_bean.people" id="people1">
<!--        constructor-arg标签表示构造器的参数，index表示这个构造器的第几个参数，除了index还可以通过name或type来指定-->
<!--        此处给有参构造器第一个参数赋值为1，第二个参数赋值为“jack”-->
        <constructor-arg value="1" index="0"/>
        <constructor-arg value="jack" index="1"/>
    </bean>
    <bean class="_01_bean.people" id="people2">
<!--        这里用name来指定构造器中具体的参数该赋哪个值，使用type的话则是对构造参数的数据类型来指定，因为一个类的构造器，不能存在两个结构相同的构造器，故可以用参数类型来指定-->
        <constructor-arg value="2" name="id"/>
        <!--<constructor-arg value="2" type="java.lang.Integer"/>-->
    </bean>
</beans>

```

其标签的细节说明都在里面了，调用则直接通过id和class调用：

```java
import _01_bean.people;

public void Run(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        People people = ioc.getBean("people1",people.class);
    }
```



#### 1.2.4 通过p名称空间配置

一种简化的配置方法，内核一个意思，就是看着简单点了。

```xml
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p">
	<bean class="_01_bean.people" id="people3" p:id="3" p:name="tom"/>
</beans> 
```

 在使用p名称空间时，要在beans标签里先引入名称空间才行。

这里配置bean对象属性，就不在`<property>`标签中了，而是直接在bean标签里使用`p`来标识出想要配置的属性，紧跟着在等号后面给属性赋值。

程序里调用方法和前面一样，就不再写了。



#### 1.2.5 通过ref注入

常用方法之一，当两个bean对象有属性完全一致的情况（这个相对继承来说不常见）时，往往会用到ref注入。比如有如下两个bean类：

```java
public class PeopleDao {}
```

```java
public class PeopleService {

    private PeopleDao peopleDao;
}
```

Service类中有一个属性是Dao类型的，此时配置Service类的peopleDao属性就需要用到ref注入了。



其配置方式如下：

```xml
<!--使用ref配置peopleDao、peopleService对象-->
<beans>
    <bean class="_03_getBean._02_refGetBean.PeopleDao" id="peopleDao"/><!--这里peopleDao里由于没有属性，故不需要配置-->
    <bean class="_03_getBean._02_refGetBean.PeopleService" id="peopleService">
        <property name="peopleDao" ref="peopleDao"/><!--peopleService有一个唯一的属性就是private PeopleDao peopleDao，该属性为Dao类的引		入，这时就可以通过ref关键字在配置文件中直接将前面配置的Dao对象注入-->
        <!--这是一种依赖注入，表示一个对象的配置需要依赖另一个对象-->
    </bean>

</beans>
```

调用方法和前面一致。



还要一种ref注入的扩展，比如不配置一个外部的Dao对象了，而是在service内部配置:

```xml
    <!--使用内部bean配置service对象(ref的拓展)-->
    <bean class="_03_getBean._02_refGetBean.PeopleService" id="peopleService2">
        <!--这里不需要再配一个于Service同级的Dao，而是再Service内部配置了一个Dao-->
        <property name="peopleDao">
            <bean class="_03_getBean._02_refGetBean.PeopleDao"/>
        </property>
    </bean>
```





#### 1.2.6 多维注入

之前配置的属性都是一个的，如一个String、一个Integer等等，如果遇到数组、集合等属性，该如何配置呢？

这里做一个实例javabean，以供直观感受。只展示属性、构造器和getset都不展示了（但是得有）

首先是monster类：

```java
public class Monster {
    private Integer monsterId;
    private String name;
    private String skill;
}
```

其次是Master类：

```java
public class Master {
    private String name;
    private List<Monster> monsterList;
    private Map<String, Monster> monsterMap;
    private Set<Monster> monsterSet;
    private String[] monsterName;
}
```

可以看出，Master类中部分属性是需要monster类来 构建的。



下面展示如何配置：

```xml
<beans>
    <!--先配置一个monster对象-->
    <bean class="_03_getBean._03_ArrayBean.Monster" id="monster31">
        <property name="name" value="银角"/>
        <property name="monsterId" value="1"/>
        <property name="skill" value="角银"/>
    </bean>
    
    
    
    
    <!--再配置一个Master对象-->
    <bean class="_03_getBean._03_ArrayBean.Master" id="master">
        <property name="name" value="太上老君"/>
        <property name="monsterList">
            <!--list是单例列表，只放value就行，这里list的value是Monster类型的对象(泛型指定的)，故直接在list标签下引入Monster对象就行-->
            <list>
                <!--可以直接在list里创建对象-->
                <bean class="_03_getBean._03_ArrayBean.Monster" id="monster331" p:name="jinjiao" p:monsterId="31" p:skill="金角"/>

                <!--也可也在list里注入-->
                <ref bean="monster31"/><!--这里注入只能注入Master所在包下的Monster类的对象（泛型规定的），最初也配置过Monster，但是由于不在一个包下，故无法注入-->
            </list>
        </property>

        <property name="monsterMap">
            <!--map相对List要复杂一点，因为map是key-valeu对，因此map标签下要做entry标签，在entry标签内指定key和value-->
            <map>
                <!--在entry下做一对key-value-->
                <entry>
                    <!--做key，该key的value为monster01-->
                    <key><value>monster01</value></key>

                    <!--该key对应的value值，也就是具体的对象内容，这里使用ref注入-->
                    <ref bean="monster31"/>
                </entry>

                <entry>
                    <key><value>monster02</value></key>

                    <!--使用内部配置来写value值-->
                    <bean class="_03_getBean._03_ArrayBean.Monster" id="monster321">
                        <property name="name" value="银角"/>
                        <property name="monsterId" value="1"/>
                        <property name="skill" value="角银"/>
                    </bean>
                </entry>
            </map>
        </property>

        <!--set和list类似，配置比map简单-->
        <property name="monsterSet">
            <ref bean="monster31"/>
        </property>

        <!--数组属性赋值-->
        <property name="monsterName">
            <!--这里根据bean类里的数组类型来决定使用什么标签，此处bean里使用的是String[]，故array下可以直接用value赋值。其他视情况而定，如如果是map[]数组，则使用map标签等等。-->
            <array>
                <value>string1</value>
                <value>string2</value>
            </array>
        </property>

        <!--properties属性的配置，properties结果为key-value，但是其key value一般都为string-->
        <property name="pros">
            <!--properties的配置就使用这种固定格式配就行-->
            <props>
                <prop key="key1">value1</prop>
                <prop key="key2">value2</prop>
            </props>
        </property>
    </bean>

</beans>
```

具体细节全在代码注释里，看一遍就行。



#### 1.2.7 静态工厂

上面将bean对象配置进Spring容器中的方法都是零散的，即将各个bean类逐一配置的，那有没有一种方法能将多个对象放入一个bean类中，然后配置到Spring容器时只将这个集合类配置进去就行的了方法呢？这个就可以用静态工厂实现。

静态工厂的思路是，做一个工厂类提供若干个静态属性，每个静态属性都是map类型的，用来存放泛型规定的bean对象，之后在静态代码块中将各个属性初始化好，最后提供一个get方法来获取map中的对象。

```java
public class staticFactory {
    private static Map<String, Monster> monsterMap;

    //做一个静态代码块，加载类时就把monsterMap初始化完毕
    static {
        monsterMap = new HashMap<>();
        monsterMap.put("monster01",new Monster(1,"jack","run"));
        monsterMap.put("monster01",new Monster(2,"tom","eat"));
    }

    //提供一个方法，返回monster对象
    public static Monster getMonster(String key){
        return monsterMap.get(key);
    }
}
```

这里为了方便，就只做了一个map。



之后就是配置文件部分：

```xml
<beans>
    <!--id是配置的bean对象的id，class是静态工厂类的全路径，factory-method是指定使用静态工厂的哪个方法来得到配置对象-->
    <bean id="monster41" class="_03_getBean._04_BeanFactory.staticFactory" factory-method="getMonster">

        <!--这个value是跟factory-method属性相关的，表示向factory-method方法中传入的参数-->
        <constructor-arg value="monster01"/>
    </bean>

</beans>
```

在bean标签里指定好factory-method方法后，在bean体内使用构造器标签`constructor-arg`来完成对象的配置。



#### 1.2.8 实例工厂

思路和静态工厂是一个思路，不过实现方法有所不同，静态工厂是以工厂类为基准的（静态跟类联系紧密），而实例工厂则是跟工厂对象相关联的。

实例工厂中，属性不做成静态的，代码块也不做成静态的，这样的话，每次创建一个实例工厂实例时，都会做一次map的构建。

这样的话，两者的区别也显而易见，静态工厂做的bean类，都是一个地址，因为其只实例化一次，以后再做就是引用了；而实例工厂每次都是一个新的bean。

```java
public class InstanceFactory {
    private static Map<String , Monster> monsterMap;

    //使用普通代码进行Map的初始化，静态工厂使用的是静态代码块
    {
        monsterMap = new HashMap<>();
        monsterMap.put("monster01",new Monster(1,"jack","run"));
        monsterMap.put("monster02",new Monster(2,"tom","eat"));
    }

    //提供一个返回monster对象的方法
    public Monster getMonster(String key){
        return monsterMap.get(key);
    }
}

```



实例工厂的配置也与静态工厂有所不同：

```xml
<!--使用实例工厂得到配置信息，静态工厂可以直接通过类来使用，故不需要配置出具体的工厂对象，而实例工厂则得配置好工厂对象-->
    <!--做一个实例工厂对象-->
    <bean class="_03_getBean._04_BeanFactory.InstanceFactory" id="InstanceFactory"/>

    <!--id为此处配置的对象的id，factory-bean指的是使用哪个实例工厂对象，factory-method指的是使用示例工厂对象的哪个方法-->
    <bean id="monster42" factory-bean="InstanceFactory" factory-method="getMonster">

        <!--这个value是跟factory-method属性相关的，表示向factory-method方法中传入的参数-->
        <constructor-arg value="monster01"/>
    </bean>
```



#### 1.2.9 FactoryBean

Spring还提供了一种基于FactoryBean的对象配置方法。细节边看代码边说。

```java
public class MyFuctoryBean implements FactoryBean<Monster> {

    private String key;//做一个String类型的key，方便在配置文件内指定
    private Map<String,Monster> MonsterMap;//做一个map，在代码块中初始化

    {
        MonsterMap = new HashMap<>();
        MonsterMap.put("monster431",new Monster(1,"jery","eat"));
        MonsterMap.put("monster432",new Monster(2,"marcl","shoot"));
    }


    @Override
    public Monster getObject() throws Exception {
        return MonsterMap.get(key);
    }

    @Override
    public Class<?> getObjectType() {
        return Monster.class;
    }

    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }

    public String getKey() {
        return key;
    }

    public void setKey(String key) {
        this.key = key;
    }
}
```

首先是bean类，该bean类会实现FactoryBean接口，并指定泛型。实现接口后，会同时实现接口下的三个方法，分别用来：得到对象、得到类、设置是否为单例。

Spring在识别到配置文件中的类路径指向的是myFactoryBean后，会自动调用这三个方法，从而得到该工厂bean中存储的对应的bean类。



```xml
    <!--配置MyFactoryBean,本质是monster对象-->
    <bean class="_03_getBean._04_BeanFactory.MyFuctoryBean" id="monster431">
        <property name="key" value="monster431"/><!--给该myFuctoryBean对象的key赋值，赋值为monster431-->
    </bean>
```

当spring扫描xml文件后，去`_03_getBean._04_BeanFactory.MyFuctoryBean`这个路径，发现这个路径是实现了FactoryBean的类，则Spring就会通过上面三个方法得到property中配置的信息的对应的bean类，进而去实例化那个类。所以看似此处配置的好像是MyFactoryBean类的对象，但实质上还是monster对象。

#### 1.2.10 自动装配

上面所讲的内容都是我们自己一行一行配置出来的，下面介绍一种让Spring自己识别处理配置的方法。

先做三个相关的Bean类

```java
//DAO
public class Dao {

    public void saveDao(){
        System.out.println("saveDao");
    }
}

//Service，使用了Dao
public class Service {
    private Dao dao;

    public Dao getDao() {
        return dao;
    }

    public void setDao(Dao dao) {
        this.dao = dao;
    }
}

//Servlet，使用了Service
public class Servlet {
    private Service service;
    public int id;

    public Service getService() {
        return service;
    }

    public void setService(Service service) {
        this.service = service;
    }
    
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}
```

以往出现这种一个类里包含了另一个类中的信息的情况，都是使用ref注入来配置id，但是Spring也提供了一种自动装配的方法，其会自动识别xml里合适的信息放入合适的位置。



配置方法如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="_01_ioc._04_doItSelf.Dao" id="dao"/>
    <!--传统的引入是使用ref来引入的，service使用ref引入dao、servlet使用ref引入service。现在使用自动装配-->
<!--    <bean class="_01_ioc._04_doItSelf.Service" id="service" p:dao-ref="dao"/>-->
<!--    <bean class="_01_ioc._04_doItSelf.Servlet" id="servlet" p:service-ref="service"/>-->

    <!--使用autowire=bytype时，spring容器在创建service时，通过类型的方式给对象属性完成自动赋值。
    如此处Service中有属性Dao，则Spring会在容器中找有没有Dao类型的对象，如果有，就自动装配到Service的属性中
    这里根据Type配置的话，要求容器中不能有两个Dao类的实例。-->
    <bean autowire="byType" class="_01_ioc._04_doItSelf.Service" id="service"/>

    <!--除了bytype的方式配置外，还要byName的方式，autowire=”byName“，通过名字完成自动装配。
    此处Servlet有service属性，之后Spring会查找Servlet中的setter方法，通过setter方法反射出属性
    要注意，setXXX方法后的XXX要和刚刚配置的service的id相同才行-->
    <bean autowire="byName" class="_01_ioc._04_doItSelf.Servlet" id="servlet">
    	<property name="id" value="1"/><!--这里除了可以通过自动装配将部分信息直接配置好之外，也可手动配置一些无法自动装配的信息-->
    </bean>
</beans>
```



#### 1.2.11 拓展

##### 1.2.11.1 继承

我们都知道，当子类继承父类后，是需要在构造器内将父类的属性构造出来的（要么继承父类构造器，要么自己构造），那么配置时也需要考虑继承问题。当一个bean是继承了另一个bean时，子bean是无法触及到父bean属性的，需要用继承标签来将父bean属性配置好。

```xml
<!--这里abstract属性可有可无，有了的话则代表该配置只供别人继承，自己不能实例化（类似抽象类）-->    
<bean id="monster10" class="_01_bean.Monster" abstract="true">
        <property name="monsterId" value="10"/>
        <property name="name" value="蜈蚣精"/>
        <property name="skill" value="蜇人"/>
    </bean>
```

上面假设是父bean，则下面为子bean 的配置：

```xml
<bean id="monster11" parent="monster10">
	<property name="age" value="100"/>
</bean>
```

使用parent标签将父类的属性继承来，然后在自己的property标签内配置自己特有的属性。



##### 1.2.11.2 单例和多例

单例在这里是指一个配置文件只生成一个对象，不管getBean()多少次，都是指向同一个内存空间，得到的都是同一个配置对象；
多例则是指每getBean（）一次，都得到的是一个全新的对象。

即单例配置的话，构造器只会执行一次，而多例配置则每次getbean都会执行一次构造器

那么Spring如何判断一个配置信息是单例还是多例呢？根据scope标签来判断，平常不写scope标签的话，默认是单例的，Spring发现该bean为单例后，就会即刻创建一个该文件的bean对象保存到singletonObject中（之前讲过）；如果发现是多例的话，则不进行创建，而是在程序中getbean时才创建，该方式称为懒加载。

```xml
<!--之前所有的配置都是默认为单例的，因为配置标签里有一个属性scope默认为singleton-->
    <bean class="_01_bean.Single" id="single1" scope="singleton">
        <property name="id" value="1"/>
    </bean>

    <!--配置一个多例的-->
    <bean class="_01_bean.Single" id="single2" scope="prototype">
        <property name="id" value="2"/>
    </bean>
```

scope为singleton是表示单例、为prototype时表示多例。



此时看程序中代码：

```java
 public void singleton(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        Single single1 = ioc.getBean("single1",Single.class);
        Single single2 = ioc.getBean("single1",Single.class);
        Single single3 = ioc.getBean("single2",Single.class);
        Single single4 = ioc.getBean("single2",Single.class);

        System.out.println(single1);
        System.out.println(single2);
        System.out.println(single3);
        System.out.println(single4);
        //1和2的地址一样，因为其是单例配置实例化的，而3和4不同，因为其不是单例，每次实例都是一个新对象。

        //单例配置，在容器启动时就会创建好对象，并存放如singletonObjects集合中
        //多例配置，在执行getbean方法时才会创建对象，
        

    }
```

如果单例配置时，也想让其对象创建在getbean时而不是加载容器时，则将加载变为懒加载就行（将bean标签的lazy-init属性设为true）。懒加载就是什么时候用才什么时候加载。



##### 1.2.11.3 生命周期

像vue、线程等一样，ioc也有生命周期，执行构造器-->执行set方法-->后置处理器before-->调用初始化方法（init）-->后置处理器after-->使用bean-->关闭容器(destory)

其重要的周期就两个：init和destory。

init是在setter方法执行后执行的，也就是说当配置文件中的`<propery>`标签（或其他的任何有初始化对象属性的标签）起作用后触发的；

destory是Spring容器销毁时触发的。

这两个生命周期的钩子函数，要在配置时的bean标签属性内指定。

先做一个javabean：

```java
public class Life {
    public String name;

    //程序员自定义两个方法：init、destory(名字不是固定的，想起啥起啥，只要知道是干啥的就行)
    public void init(){
        System.out.println("init被执行");
    }
    public void destory(){
        System.out.println("destory被执行");
    }



    public String getName() {
        return name;
    }

    public void setName(String name) {
        System.out.println("life的set方法被执行");
        this.name = name;
    }

    public Life() {
        System.out.println("life构造函数被执行");
    }

    public Life(String name) {
        this.name = name;
    }
}

```



将该bean配置进容器：

```xml
    <!--生命周函数的启用是在bean标签里操作的，使用init-method属性来指定该bean对象的初始化生命周期函数是哪个、使用destory-method属性来指定bean对象的销毁生命周期函数是哪个-->
    <!--init方法的执行时机，是在setter方法后执行，destory方法的执行，是在spring容器关闭时执行的。-->
    <bean class="_01_bean.Life" id="life" init-method="init" destroy-method="destory">
        <property name="name" value="life"/>
    </bean>
```



演示看看：

```java
    public void Life(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        Life life = ioc.getBean("life", Life.class);

        //关闭容器，ioc的编译类型ApplicationContext里是没有提供close方法的，所以要转型成一个ApplicationContext的一个实现类——ConfigurableApplicationContext来接收ioc，并使用其中的close方法
        ((ConfigurableApplicationContext)ioc).close();

    }
```

最后执行顺序为：life构造函数被执行、lifeset函数被执行、init函数被执行、destory函数被执行。



##### 1.2.11.4 后置处理器

在spring的ioc容器中可以配置 bean 的后置处理器，该处理器会在bean初始化方法调用前和初始化方法调用后被调用，具体功能由程序员自己指定。

下面展示一下用法。

首先写一个后置处理器的程序：

```java
package _01_ioc._01_bean;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class MyBeanPostProcessor implements BeanPostProcessor {//实现了 BeanPostProcessor接口的类就是后置处理器了
    /**
     * 下面两个方法都是在扫描完xml文件并准备逐一创建非懒加载对象时调用，每创建一个<bean></beans>中对应的对象，都会执行一次，其传入的参数，就是当前bean里存放的信息。
     * postProcessBeforeInitialization方法在bean的init方法执行前被调用（若没指定init方法，则在默认的set方法被调后调用）
     * @param bean 接收的bean为xml文件里配置的bean
     * @param beanName 接收的beanName为xml文件里配置的的bean对应的id
     * @return 一般来说该方法会将接收的bean对象进行修改，然后return回这个被修改的bean
     * @throws BeansException
     */
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println(bean + beanName);
        return BeanPostProcessor.super.postProcessBeforeInitialization(bean, beanName);
    }

    /**
     * postProcessAfterInitialization方法在init方法后被调用
     * @param bean 同上
     * @param beanName 同上
     * @return 同上
     * @throws BeansException
     */
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println(bean + beanName + 1);
        return BeanPostProcessor.super.postProcessAfterInitialization(bean, beanName);
    }
}

```



再从XML中配置该处理器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--这里配置bean后置处理器-->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--由于life里有init函数，故就直接配life省事了-->
    <bean id="life" class="_01_ioc._01_bean.Life" init-method="init">
        <property name="name" value="lifeAfter"/>
    </bean>

    <!--配置后置处理器-->
    <!--配置好后置处理器后，该后置处理器就会作用于该容器（afterBean.xml）中的所有配置信息中-->
    <bean id="after" class="_01_ioc._01_bean.MyBeanPostProcessor"/>


</beans>
```



最后运行一下结果如下：

```
life构造函数被执行
life的set方法被执行
_01_ioc._01_bean.Life@c81cdd1life
init被执行
_01_ioc._01_bean.Life@c81cdd1life1
```



### 1.3 基于注解配置Bean对象

基于xml文件配置bean是将对象实例化在xml文件中，之后spring会扫描xml文件进行配置。而基于注解配置对象，是将需要实例化的类进行各类注解标签，然后再xml中配置好需要被放入容器的对象所在类的路径，之后spring会去路径中解析对象并放入容器。



使用用于配置Spring对象的注解有四个：

 `@Component` ：表示组件，当不好将该类归类，但是又需要放入Spring容器中，就将此类标记为Component。

`@Controller`：表示当前注解标识的是一个控制器，通常用于 Servlet

` @Service`：表示标识的目标为Service类或对象

`@Repository`： 表示当前注解标识的是一个持久化层的类，通常用于 Dao 类



#### 1.3.1应用

下面做一个web服务流程：Dao-->service-->servlet，再顺便做一个没用特殊功能的类（使用Component标识）

```java
import org.springframework.stereotype.Repository;

//Respository标识，代表标识的目标是一个持久化的类/对象
@Repository(value = "dao")//这里给该注解指定一个id，Spring在创建该bean的实例时，“dao”就是这个类的id了，否则默认为首字母小写的全类名。
public class MyDao {

}
```

```java
import org.springframework.stereotype.Service;

import javax.annotation.Resource;


//Service，表示标识的目标为Service类或对象
@Service
public class MyService {
    //在servlet里展示了如何使用Autowrit来配置需要注入的属性，这里使用另一种注解——Resource
    //Resource可以直接指定想要容器中哪个对象注入此处属性中（name="id"），而不受属性名的影响
    //也可通过Type来指定(Type=ClassName.Class)，这种方式要求容器中只有该类唯一的bean
    //若Resource注解后面什么都不写，则默认先使用name方式，传入的id为属性名；若name查不到，则使用type形式；若都不成功，则报错
    @Resource(name = "dao")
    private MyDao mydao;

    public void hi(){
        System.out.println("serviceHi");
    }
}
```

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

//Controller，表示标识的目标为一个控制器（一般标识在Servlet上）。
@Controller
public class MyServlet {

    //此处使用Autowired来配置Servlet类里的其他类属性。
    //该注解的作用是：查找ioc容器中待装配的组件的类型，如果有唯一的bean匹配，则使用这个匹配的bean来放入该组件。
    //如果待装配类型对应的bean在容器中有多个，则使用待装配组件的属性名作为id再次进行匹配查找，找到则存入。找不到对应的id则报错。
    @Autowired
    private MyService myService1;

    public void ok(){
        System.out.println("ServletOk");
        myService1.hi();
    }


    public MyService getMyService() {
        return myService1;
    }

    public void setMyService(MyService myService) {
        this.myService1 = myService;
    }
}
```



```java
import org.springframework.stereotype.Component;


//Component，表示组件，当不好将该类归类，但是又需要放入Spring容器中，就将此类标记为Component。
@Component
public class MyComponent {
}
```



其xml配置如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd">

    <!--注解的方式配置容器-->
    <!--配置细节-->
    <!--首先将context的名称空间引入，
    component-scan：对指定包进行注解扫描，如果包下的某个类有注解，则将其配置进容器。
    base-package:用来指定具体要扫描的包是哪个
    扫描的具体注解为以下几个：@Controller、@Service、@Respository、@Component，扫描完后，将这些注解标识的类实例化后放入容器
    当然，Spring不会识别上面四个标签的意思，它只是看到这几个标签就将其实例化，这些注解实际上是为了让程序员看懂的。
    -->
    <context:component-scan  base-package="_01_ioc._05_Annotation"/>
    <!--这样配置完后，程序中就可以像之前那样通过ioc来getbean了，在get时可能会有一个疑问，传入的形参中，id该是谁呢？
    id默认为class对应类的首字母小写后的全类名，如ioc.getBean("myDao",MyDao.class)
    -->
    <!--当然，也可也指定id为什么，但是指定的位置是在具体的注解中-->

    <!--补充细节：
    若上述四个注解中，我们并不想让其中几种注解被实例化进容器，则可以通过exclude-filter标签来指定出这些被排除在外的标签，其中type属性表示排除哪种方式的配置，这里指定为注解形式，最后expression指定出排除哪种注解类型的全路径。
    <context:component-scan  base-package="_01_ioc._05_Annotation">
        <context:exclude-filter type="anntation expression="org.springframework.stereotype.Repository"/>
    </context>
    -->

    <!--上面这个排除的filter还有一个反方法，即只配置指定的注解标签。使用标签为include-filter。再使用该方法前，先在context标签中将属性use-default-filters设置成false，即不让其使用默认配置方法。
    其他和上面一致
    <context:component-scan  base-package="_01_ioc._05_Annotation" use-default-filters="false>
        <context:include-filter type="anntation expression="org.springframework.stereotype.Repository"/>
    </context>
    -->



    <!--该service对象主要是为了来判别Autowrit对容器中同一类型的对象不同id的处理方法的区别-->
    <!--若servlet中，Service类型的属性名为myService1，则会匹配该对象-->
    <bean id="myService1" class="_01_ioc._05_Annotation._01_component.MyService"/>
</beans>
```



> 自动装配

观察可以发现，在部分属性上有` @AutoWired`或` @Resource`标注。这个标注的意思是完成自动装配，其原理和基于xml配置bean是一致的，区别就在于一个是spring解析xml发现自动装配标签进行装配；一个是spring解析注解类发现自动装配注解进行装配。



#### 1.3.2 手动实现

现在手动实现一下Spring解析注解的流程。

先做一个bean

> bean

```java
package _01_ioc._06_DoAnnotation.bean;

public class bean {
}

```



> @interface

在手动实现中，采用配置类来代替配置文件。实际上两者没啥大差别，使用配置文件时，是在容器中通过dom4j来解析文件并 得到文件内的配置内容；而使用配置类则是使用反射来得到配置类内的配置内容。

此处自定义的注解的作用是模拟xml文件中的“base-package="XXX"“的功能，用来在配置类内注明具体要解析哪里的路径。

```java
package _01_ioc._06_DoAnnotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 自定义注解，此注解的作用是替代xml文件中“base-package="XXX"“的功能，value接收一个要解析的包的地址，供Spring处理
 */
@Target(ElementType.TYPE)//target用于修饰注解，指定被修饰的注解能用于修饰哪些程序元素。此处标记该注解（myComponentScan）能可以修饰TYPE元素（其内包含class、interface、enum）
@Retention(RetentionPolicy.RUNTIME)//Retention用于修饰注解，指定该注解可以保留多长时间。将其赋值为runtime表示注解在java程序运行时起作用
public @interface MyComponentScan {

    String value() default "";//这一行表示myComponentScan注解在标识其他类时，可以接收一个String类型的参数，作为myComponentSacn的value

}
```



> ConifgClass

做一个配置类，功能类似配置文件

```java
package _01_ioc._06_DoAnnotation;

/**
 * 将xml配置文件模拟为一个配置类，逻辑上差不多，xml文件是通过dom4j来解析，这里这个类通过反射解析
 */

@MyComponentScan(value = "_01_ioc._05_Annotation._01_component")//这里传入的是要解析的路径。起"base-package="_01_ioc._05_Annotation"的作用。此处直接用上一讲的包了。
public class SpringConfig {
}
```



> SpringApplicationContext

做一个Spring容器

```java
package _01_ioc._06_DoAnnotation;

import org.springframework.stereotype.Component;
import org.springframework.stereotype.Controller;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;
import org.springframework.util.StringUtils;

import java.io.File;
import java.io.FileOutputStream;
import java.lang.annotation.Annotation;
import java.net.URL;
import java.util.concurrent.ConcurrentHashMap;

/**
 * 模拟Spring原生的ioc容器
 */
public class MySpringApplicationContext {
    private Class configClass;//定义一个Class属性，用来接收配置类
    private ConcurrentHashMap<String,Object> ioc = new ConcurrentHashMap<>();//做一个容器属性，用来存放容器实例化的对象。

    public MySpringApplicationContext(Class configClass){
        this.configClass = configClass;//构造容器时直接接收配置类

        //1、通过得到的反射对象，解析该对象中的注解。在此处为：得到的反射对象为：SpringConfig、反射对象中的注解为：MyComponent
        MyComponentScan myComponentScan = (MyComponentScan)this.configClass.getDeclaredAnnotation(MyComponentScan.class);

        //2、拿到注解里配置的value，即容器要扫描的包
        String path = myComponentScan.value();
        //System.out.println(path);

        //3、获取扫描包下所有的.class文件（这里的.class文件，是out目录下（工作目录）的文件，我们平常用的src目录里的文件，后缀都是.java，工作目录是将.java编译后的结果）
        //3.1得到类加载器
        ClassLoader classLoader = MySpringApplicationContext.class.getClassLoader();
        //3.2通过类加载器获取到要扫描包的url（工作目录url）
        path = path.replace(".","/");//这里有一个讲究，刚刚得到的注解中的value值是用.来分隔文件夹的，而正经路径得是用/来分割的，故做一个替换
        //System.out.println(path);
        URL resource = classLoader.getResource(path);

        //System.out.println(resource); //此处输出为file:/D:/Code/JavaCode/_04_Spring/out/production/_04_Spring/_01_ioc/_05_Annotation/_01_component

        //3.3遍历路径下的文件
        String name = resource.getFile();//讲url地址通过getFile方法转为String类型
        File file = new File(name);//把目录作为一个文件创建

        if (file.isDirectory()){//当file确实是存在的的时候
            File[] files = file.listFiles();//将file下的子文件都逐一取出放入files数组中

            //将目录文件下的所有子文件逐一取出，并通过反射实例化其具体对象
            for (File f : files){
                //System.out.println(f.getName());输出为MyComponent.class、MyDao.class、MyService.class、MyServlet.class
                String absolutePath = f.getAbsolutePath();//拿到具体class文件的绝对路径
                // 此处为：D:\Code\JavaCode\_04_Spring\out\production\_04_Spring\_01_ioc\_05_Annotation\_01_component\MyServlet.class、、、
                // 此处绝对路径是通过\来分隔的，后面要改为.分隔，并且最后反射时，要求最后的.class后缀时没有的。

                //这里最好做一个过滤，只处理.class文件
                //if(absolutePath.endsWith(".class")){ }


                //先得到类名
                String classname = absolutePath.substring(absolutePath.lastIndexOf("\\") + 1 , absolutePath.indexOf(".class"));//将最后一个\到.class直接的内容截取出来，也就是将类名截取出来
                //System.out.println(classname);

                //再得到全类名
                String classFullName = path.replace("/",".") + "." + classname;
                //System.out.println(classFullName);

                //判断得到的类里是否有注解，该注解是否需要实例对象放入容器中，即该类里是否有那四个注解
                try {
                    //通过类加载器加载一个全类名，得到该类名对应的class。也可用Class.forName(classFullName)方法得到，但是该方式会默认调用此类的静态方法(相对完善)，下面的方法并不会（相对轻量级一点）。
                    Class<?> aClass = classLoader.loadClass(classFullName);
                    //判断类中是否有这四个注解
                    if (aClass.isAnnotationPresent(Component.class) || aClass.isAnnotationPresent(Controller.class)
                    || aClass.isAnnotationPresent(Repository.class) || aClass.isAnnotationPresent(Service.class)){
                        Class<?> clazz = Class.forName(classFullName);//得到具体类的class对象
                        Object o = clazz.newInstance();//将类实例化

                        //这里还有一个逻辑是判断四大注解里有没有value，有value的话需要把value值作为ioc里内容的key来代替classname。

                        //将类的首字母小写后，将其作为key放入ioc中，key也就是平常在xml里配置bean时所用的id。
                        classname = StringUtils.uncapitalize(classname);
                        ioc.put(classname,o);

                    }
                } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
                    e.printStackTrace();
                }


            }
        }


    }

    //编写一个返回容器中对象的方法，即getBean方法
    public Object getBean(String name){
        return ioc.get(name);
    }

}

```



## 二、 AOP

AOP是一种动态代理的方式，因此要学习AOP之前，先看看动态代理是干什么的。

### 2.1 动态代理

> 问题提出

对于某一个业务，我们需要两个类都输出里有一部分内容是完全一样的，比如如下业务：

```java
//一个交通工具接口
public interface Vehicle {

    public void run();
}

//一个汽车类，实现接口
public class Car implements Vehicle{
    @Override
    public void run() {
        System.out.println("交通工具启动");
        System.out.println("汽车启动");
        System.out.println("交通工具停止运行");
    }
}

//一个轮船类，实现接口
public class Ship implements Vehicle{
    @Override
    public void run() {
        System.out.println("交通工具启动");
        System.out.println("轮船启动");
        System.out.println("交通工具停止运行");

       
    }
}


//运行类
public void run(){
        Vehicle vehicle = new Car();
        //Vehicle vehicle = new Ship();
        vehicle.run();
}
```

 

观察可以发现ship类中的第一个输出和第三个输出和car类中的输出一模一样（语句一模一样），代码相对冗余，此时可以使用动态代理来统一管理这些内容。



> 问题解决

解决上述问题，就可以使用动态代理来实现。

动态代理的思路为，将一个实现了接口的类通过代理类处理后得到一个代理对象，之后再运行方法时会先走代理类里的方法，然后再通过多态定位到具体类的方法上，这样就可以即运行公共的代码，又运行自己单独的代码了。

```java
package _02_Aop._01_DynamicProxy._02_beterOut;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

//该类返回一个代理对象
public class VehicleProxyProvider {

    //target_vehicle用来接收真正要执行的对象。
    //该对象实现Vehcie接口
    private Vehicle target_vehicle;


    //提供构造器
    public VehicleProxyProvider(Vehicle target_vehicle) {
        this.target_vehicle = target_vehicle;
    }

    //编写一个方法，返回一个代理对象
    public Vehicle getProxy(){

        /**
         * public static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces,InvocationHandler h)
         * newProxyInstance用来返回一个代理对象。
         * newProxyInstance方法接收三个参数：类加载器、接口类型、调用处理器
         *  ClassLoder loader，类加载器，一般通过当前代理对象得到类加载器（实际上无所谓是哪个类，能得到类加载器就行）
         *  Class<?>[] interfaces，接口类型，传入将来要代理的对象的接口信息，一般通过代理对象通过反射得到代理对象所属的接口类型
         *  InvocationHandler h，调用处理器/对象，内部有一个invoke方法，通过反射得到具体内容。
         */
        //1、得到类加载器
        ClassLoader classLoader = target_vehicle.getClass().getClassLoader();

        //2、得到接口类型
        Class<?>[] interfaces = target_vehicle.getClass().getInterfaces();//此处代理对象为target_vehicle，通过反射得到其接口类型为Vehicle

        //3、得到调用处理器
        //由于InvocationHandler为接口，但是又要用到其内部的invoke方法，这时就需要有一个该接口的实例才行，但是接口不能直接实例化，就要用到匿名对象来进行调用方法了
        InvocationHandler invocationHandler = new InvocationHandler(){
            /**
             * invoke方法是将来执行target_vehicle对象（代理对象）的方法时会调用
             * @param proxy 接收一个代理对象
             * @param method 通过代理对象调用方法时触发的方法。
             * @param args 调用代理对象方法时，需要向方法形参列表里传入的参数
             * @return 返回代理对象调用方法后返回的对象
             * @throws Throwable
             */
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

                //处理方法，将之前每个vehicle接口实例类下的具体方法放入代理中实现
                System.out.println("交通工具启动");
                Object result = method.invoke(target_vehicle, args);//通过反射触发target_vehicle里的方法，并传入参数
                System.out.println("交通工具停止");

                return result;
            }
        };

        Vehicle proxy = (Vehicle)Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);


        return proxy;
    }
}

```

动态代理的使用方式如下：

```java
public void run(){
        Vehicle vehicle = new Car();//做一个实现了Vehicle接口的对象

        VehicleProxyProvider vehicleProxyProvider = new VehicleProxyProvider(vehicle);//将上面做的对象做成一个代理对象

        Vehicle proxy = vehicleProxyProvider.getProxy();//通过代理类得到代理对象
        //此时proxy对象的编译类型是Vehicle，运行类型是Proxy(该类型是getProxy方法中newProxyInstance方法所在类的类型)
        //由于proxy的运行类型不是最开始的Car了，所以当运行run方法时，会在vehicleProxyProvider类里的newProxyInstance方法中通过invoke反射方法去找run方法。
        //进而会执行重写的invoke方法里的一套新体系。
        proxy.run();
        System.out.println(proxy.fly(10));

}
```



> 优化

动态代理中实际上是可以添加钩子函数的，即生命周期函数，在合适的位置可以进行合适的处理，下面做一个单独的动态代理类来指明一下都哪里可以放函数:

```java
package _02_Aop._01_DynamicProxy._03_deep;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;
import java.util.Arrays;

public class AnimalableProxyProvider {

    private Animalabel target_animalable;

    public AnimalableProxyProvider(Animalabel target_animalable) {
        this.target_animalable = target_animalable;
    }


    public Animalabel getProxy(){
        ClassLoader classLoader = target_animalable.getClass().getClassLoader();

        Class<?>[] interfaces = target_animalable.getClass().getInterfaces();

        InvocationHandler invocationHandler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

                Object result = null;
                try {
                    //前置通知（横切关注点），定义在method反射执行之前，相当于生命周期中的钩子函数
                    System.out.println("前置通知" + method.getName() + Arrays.asList(args));

                    result = method.invoke(target_animalable, args);

                    //返回通知（横切关注点），定义这method反射执行之后，类似钩子函数
                    System.out.println("返回通知：正常执行，得到结果为" + result);

                } catch (Exception e) {
                    e.printStackTrace();
                    //如果反射过程中出现了异常，进入catch阶段。这里也是一个横切关注点——异常通知
                    System.out.println("异常通知:方法执行异常" + method.getName() + "异常类型" + e.getClass().getName());
                } finally {//不管是否出现异常，最后都回执行finally，这里也是一个横切关注的——最终通知
                    System.out.println("最终通知:方法执行结束");
                }
                return result;
            }
        };

        Animalabel o = (Animalabel)Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);
        return o;
    }
}

```

上面这几个通知的地方，都可以换成有具体功能的函数。



### 2.2 AOP

AOP（面向切面编程）是一种高级的动态代理机制，Spring中，会将动态代理中的核心——代理类给封装起来，只保留bean类和run类。但是封装起来不代表舍弃掉了，其内核还是使用代理类来进行动态代理，只是我们看不到了。

在封装起来了代理类的同时，AOP比一般动态代理高级的地方在于，其提供了一个切面类（AOP的核心）。之所以说切面类是AOP的核心，一方面是因为只有在切面类里配置了注解`@Aspect`才能让Spring知道要使用动态代理机制了，可以说是切面类就说AOP的入口；另一方面就是切面类里定义了整个AOP流程的横切关注点（相当于生命周期函数），用来插入到代理类的各个钩子存放处，这个后面具体说明。



下面看看具体使用方法。

下面一整套流程都使用注解配置进Spring容器中

> bean

先做一个基本的bean接口和bean类

```java
public interface SmartAnimalable {

    public float getSum(float i , float j);

    public float getSub(float i , float j);
}


@Component //使用Component注解，不再在程序里new一个对了，而是用注解来将SmartDogd对象配置进spring容器中
public class SmartDog implements SmartAnimalable{
    @Override
    public float getSum(float i, float j) {
        System.out.println("dogSum");
        return i + j;
    }

    @Override
    public float getSub(float i, float j) {
        System.out.println("dogSub");
        return i - j;
    }
}
```



> 切面类

```java
package _02_Aop._02_realAop;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.Signature;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

import java.lang.reflect.Method;
import java.util.Arrays;

/**
 * 切面类，内部定义具体的切面方法
 */
@Component  //使用Component注解来将界面类放入容器
@Aspect //使用Aspect注解来注明这个类是切面类，系统扫描到该类为切面类后，会自动将动态代理机制加入该类
public class SmartAnimalAspect {

    //做一个方法，这里直接做前置通知了，看着方便。实际上此处可以是任何方法（方法名随便定义，如f1、f2啥的），并且该方法也可以插入到任何地方。
        /*
        之前是在代理类中引用该方法来做前置方法的，即在内部类中重写的invoke方法内， result = method.invoke(target_animalable, args)方法调用前，调用此before方法。
        由于invoke方法本身就接收method参数和args参数，故定义before时可以在形参列表内直接接收这两个参数
        public static void before(Method method , object[] args){
            System.out.println(method.getName() + Arrays.asList(args));旧方法
        }
         */
    //既然是前置方法，则可在该方法中直接通过注解——Before来标注要把此方法配置到哪个method(具体方法)前面
    @Before(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))")//这里value里面写的是具体插入的方法，注意方法名部分写完整的路径，并且形参列表里只写传入参数的类型
    public void beforeMethod(JoinPoint joinPoint){//形参列表只有一个属性：JoinPoint，该属性把传入参数笼统的概括了进去

        Signature signature = joinPoint.getSignature();//使用getSignature方法可以得到方法签名，即得到Before内配置的方法
        System.out.println(signature.getName() + joinPoint.getArgs());//通过方法签名获得被前置的方法的name（singnature.getName代替了method.getName）；joinpoint又是表示参数，故其内部是有args属性的，直接提取就行(代替args)
    }


    //明白了上面一整套流程后，其他切面方法就简单了，都是一个流程。
    //后置通知
    //在后置通知的注解里，可以根据需要来确定是否添加一个属性用来接收以后被调用方法的返回值。如果选择添加，就如下格式，相当于多加一个value属性——returning，之后在写后置方法时，在形参列表里加入该returning就行
    //这个方法只能添加在后置通知里，因为returning接收的是方法运行后的返回的值，如果在前置通知里，则那个时候还么有运行具体的方法本身，何谈返回值？也就是说，returning是后置方法的特有属性
    /*
    总的来说就是动态代理的这一部分：
    res = method.invoke(target_animalable, args);//待通过反射运行完目标方法后，接收一个返回值，这个返回值在AOP中的体现就是returning=res
    //返回通知
    System.out.println("返回通知：正常执行，得到结果为" + res);//然后将res传入返回通知中，表现为afterMethod的形参列表。
     */
    @AfterReturning(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))" ,returning = "res")
    public void afterMethod(JoinPoint joinPoint,Object res){
        Signature signature = joinPoint.getSignature();
        System.out.println(signature.getName() + joinPoint.getArgs() + res);
    }

    //异常通知
    //异常通知里，也有一个和返回通知中特有属性类似的属性——throwing。表示catch住的e，即这部分：
    /*
    catch (Exception e) {//抓住异常，表现为throwing = "tro"
      e.printStackTrace();
      System.out.println("异常通知:方法执行异常" + method.getName() + "异常类型" + e.getClass().getName());//将异常传入异常通知方法里进行处理
    }
     */
    @AfterThrowing(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))",throwing = "tro")
    public void ThrowingMethod(JoinPoint joinPoint,Throwable tro){
        Signature signature = joinPoint.getSignature();
        System.out.println(signature.getName() + joinPoint.getArgs() + tro);
    }

    //最终通知
    @After(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))")
    public void Last(JoinPoint joinPoint){
        Signature signature = joinPoint.getSignature();
        System.out.println(signature.getName() + joinPoint.getArgs());
    }

}

```



> 配置

将xml部分配置完成

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--引入基于注解的AOP功能-->
    <!--在SmartAnimalAspect类创建时做了一个Aspect注解，如果不引入下面的功能，是识别不到该注解的-->
    <!--
    在引入了该功能后，Spring会将整个xml配置文件按照aop的方式进行创建。
    AOP是高级的动态代理，其将整个动态代理类（即前面的AnimalableProxyProvider类）彻底的封装进内部了，并不是不用了。而动态代理类接受的参数是一个接口类型的参数
    即动态代理类底层实际上代理的是一个接口类型，具体使用方法时，使用的是实例化了该接口的类的方法。
    故引入aop功能后，再想实例化xml里配置的类时，就需要使用接口类型来接收而不是使用本类类型接收了，如果使用本类类型接收，其无法传入代理类里，则整个aop流程走不通。
    也就是说，引入aop功能后，该xml配置里的bean类的编译类型都应该是某个接口类型，bean类的运行类型则变成了Proxy类型，如动态代理时所说：
    Vehicle proxy = vehicleProxyProvider.getProxy();//通过代理类得到代理对像，此时proxy对象的编译类型是Vehicle，运行类型是Proxy(该类型是getProxy方法中newProxyInstance方法所在类的类型)

    上面整个流程，是在bean生命周期的after方法中触发，没用进行到after方法时，原生对象还是正常的运行类型和编译类型都是具体类的对象，一旦触发了之后，就执行上面的流程，变成代理类型了。
    -->
    <aop:aspectj-autoproxy/>


    <!--配置注解包-->
    <context:component-scan base-package="_02_Aop._02_realAop"/>


</beans>
```



> 运行

```java
package _02_Aop._02_realAop;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * AOP，实际上就是高级一点的动态代理
 */
public class run {

    @Test
    public void run(){
        /*
        老方法
        public void run(){
        Animalabel animalabel = new DogAnimalable();
        AnimalableProxyProvider animalableProxyProvider = new AnimalableProxyProvider(animalabel);
        Animalabel proxy = animalableProxyProvider.getProxy();
    }
         */

        /*
        首先可以发现，使用Spring的Aop后，直接把刚刚手动实现动态代理的AnimalableProxyProvider类给优化掉了，即将该类封装起来了。
        再仔细观察可以发现，实例化dog对象时，其运行类型是接口类型，并且做的代理对象是传入接口类型（做的是该接口的代理对象）。而由于Aop将代理类封装起来了，并不是拿掉不要了
        故这里通过注解得到的对象也应该是接口类型，方便后面AOP封装的代理类识别并使用。
        也就是说，再aop机制下，通过容器得到对象时（getbean之后），其已经默认走完了上面的流程了（getbean之前还是正常的对象存放在容器中）：
        先做了一个接口类型的实现类对象，然后将该对象放入了代理类中，最后通过代理类的getProxy方法得到接口类型的对象；
        故此时存入容器中的对象，编译类型应该时接口、运行类型应该时Proxy。所以提取时，应该用编译类型（即接口类型）来接收
         */
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_02_Aop/Aop.xml");
        SmartAnimalable smartDog = ioc.getBean("smartDog", SmartAnimalable.class);//这里要得到接口类型的对象
        //SmartDog smartDog1 = ioc.getBean("smartDog", SmartDog.class);//这时已经会报错了，因为AOP的机制要求返回的类型时接口类型
        System.out.println(smartDog.getClass());

        smartDog.getSum(1,1);

        smartDog.getSub(1,1);


        //若一个类并没有实现接口，那么Spring在AOP中也是可以实例化它的，它的接口类型是某种父类类型
        //CGLib
        NoInteface noInteface = ioc.getBean("noInteface", NoInteface.class);
    }

}

```



### 2.3 细节

再刚刚整个AOP流程中，有几个应该注意的细节。

#### 2.3.1 切入表达式的写法

上面使用的切入表达式是最基本的最简单的切入表达式，其写法规范如下：`execution([权限修饰符] [返回值类型] [简单类名/类全名].[方法名] (参数列表))`

而其他的切入表达式都是以这个语法为基础的扩展。

如：

```java
@Aspect
public class _01_CutIn {
    //1、正常指定切入到某个单个方法里
    @Before(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))")
    public void f1(){}

    //2、切入到一系列满足条件的方法里：这里表示切入到SmartDog类里，并且切入到所有权限为publice的方法里，参数任意
    @Before(value = "execution(public * _02_Aop._02_realAop.SmartDog.*(..))")
    public void f2(){}

    //在一系列切入时还有个细节，如果切入到了一个接口中，如SmartAnimalable，那么所有实现了该接口的满足切入表达式的方法都会被切入
    @Before(value = "execution(public float _02_Aop._02_realAop.SmartAnimalable.getSum(float, float))")
    public void f3(){}
    //这样一来，不管是dog还是cat，是要是运行getsum方法时，都会执行该切入函数


    //3、还有一些其他拓展，看一眼就直到是咋回事，就是这些关键字的排列组合罢了

}

```



#### 2.3.2 关于joinPoint

joinPoint是在执行切入类函数时所使用的参数，其是具体参数的概总，可以通过joinPoint来得到具体函数的具体参数信息（bean类里的具体方法的信息）。

```java
public class _02_JoinPoint {

    public void before(JoinPoint joinPoint){
        joinPoint.getSignature().getName();//得到当下运行的方法的方法名
        joinPoint.getSignature().getDeclaringTypeName(); // 获取目标方法所属类的类名
        joinPoint.getSignature().getModifiers(); //获取目标方法声明类型(public、private、protected)
        Object[] args = joinPoint.getArgs(); // 获取传入目标方法的参数，返回一个数组
        joinPoint.getTarget(); // 获取被代理的对象
        joinPoint.getThis(); // 获取代理对象自己

    }
}
```



#### 2.3.3 关于切入点

在切入类中做切入函数时可以发现，又是往往一个bean类的方法要切入很多次，那么就可以给这个方法做一个切入点，再切入函数时直接用切入点就行。

```java
/**
 * 在做切入函数时，可以发现每个切入函数都是注解的同一个方法，而这一个方法写了好多遍，写的麻烦，这个时候可以用切入点表达式
 */
@Aspect
public class _03_pointCut {

    @Pointcut(value = "execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))")//这里的value就是重复的那段，即具体方法的方法声明部分
    public void myPointCut(){

    }

    @Before(value = "myPointCut()")//之后这里直接用切入点就行
    public void f1(){}
}
```



#### 2.3.4 优先级

如果同一个方法，有多个切面在同一个切入点切入，那么执行的优先级如何控制？

有时往往一个类里不止有一个切面类，那么不同的切面类是可以设置不同的优先级的。如果都没有设置优先级，那就按照切面类切入的顺序来执行，如果设置切面类优先级了，那就按照高优先级到低优先级来执行。配置优先级的方法如下：

```java
@Aspect //表示这个类是一个切面类 
@Order(value = 2) 
@Component //需要加入 IOC 容器
public class SmartAnimalAspect2 {}
```



这里再着重说明一下不同切面类作用于同一方法上的执行方式。

其执行方式和过滤器的执行方式一样，都是先执行的包裹着后执行的。也就是说，虽然有一个切面类优先级高，但是其执行完是最晚的（最早开始，最晚接收，中间包裹着低优先级的全部过程）



### 2.4 基于xml配置AOP

AOP除了可以通过注解配置之外，也可通过xml配置文件配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">


    <!--之前展示的都是基于注解配置的aop，现在展示一下如何通过xml配置aop-->

    <!--配置切面类的对象-->
    <bean class="_02_Aop._02_realAop.SmartAnimalAspect" id="smartAnimalAspect"/>

    <!--配置具体实现类的对象-->
    <bean class="_02_Aop._02_realAop.SmartDog" id="smartDog"/>

    <!--配置切面类-->
    <aop:config>
        <!--先配置切入点，也可也不配。但是如果配，就一定要在切面对象的前面-->
        <aop:pointcut id="myPoint" expression="execution(public float _02_Aop._02_realAop.SmartDog.getSum(float, float))"/>

        <!--指定哪个对象为切面对象，后面的order为优先级，指定的话就按照指定的来，不指定就默认-->
        <aop:aspect ref="smartAnimalAspect">
            <!--之后就可以在切入对象里配置切入函数了-->
            <!--指定前置通知的方法是哪个，切入点是哪个，如果没配切入点，就把注解里那一部分全拿过来就行-->
            <aop:before method="beforeMethod" pointcut-ref="myPoint"/>

            <aop:after-returning method="afterMethod" pointcut-ref="myPoint" returning="res"/>

            <aop:after-throwing method="ThrowingMethod" pointcut-ref="myPoint" throwing="tro"/>

            <aop:after method="Last" pointcut-ref="myPoint"/>
        </aop:aspect>

    </aop:config>

</beans>
```



## 三、手动实现Spring

这次手动实现不分模块写了，按照实现的流程写，相对会更复杂一点。

实际上整个Spring也就分为两个大部分：IOC部分、AOP部分，下面就按照先IOC后AOP的来实现Spring。

### 3.1、IOC

IOC部分主要任务是初始化容器，而想要初始化容器，就要进行各种注解的解析，这里就连带了很多知识点了，下面一步一步完成



#### 3.1.1 容器注解

用于容器的注解有四类：组件类（Dao、Service、Servlet、Component组成）、自动装配类（AutoWride）、路径扫描类（ComponentScan）、单例多例类（Scope）。这四类注解不分先后，都需要创建。

在使用下列注解前，先说明两个java中自带的注解：Target和Retention。

Target注解用来指示被标注的注解可以作用的位置，如`TYPE`就是注解到类上、`METHOD`就是注解到方法上、`FIELD`就是注解到字段上等等。

Retention注解用来指示被标注的注解起作用的时间，一般都是RUNTIME，即整个程序运行时起作用。

> 组件类注解

```java
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 组件注入容器注解
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Component {
    String value() default "";//指定注入容器时的id是什么，没有指定就默认首字母小写的类名
}

```



> 自动装配类注解

```java
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD,ElementType.FIELD})//修饰属性和方法
@Retention(RetentionPolicy.RUNTIME)
public @interface AutoWired {
}
```



> 路径扫描类注解

```java
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 扫描路径注解
 */
@Target(ElementType.TYPE)//target用于修饰注解，指定被修饰的注解能用于修饰哪些程序元素。此处标记该注解（myComponentScan）能可以修饰TYPE元素（其内包含class、interface、enum）
@Retention(RetentionPolicy.RUNTIME)//Retention用于修饰注解，指定该注解可以保留多长时间。将其赋值为runtime表示注解在java程序运行时起作用
public @interface ComponentScan {

    String value() default "";//这一行表示myComponentScan注解在标识其他类时，可以接收一个String类型的参数，作为myComponentSacn的value

}
```



> 单例多例类注解

```java
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 用来指定Scope标记的类是单例（singleton）还是多例(prototype)
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Scope {
    //通过value来指定是单例的还是多例的
    String value() default "";
}
```



#### 3.1.2 基本对象

基本的测试用的Dao对象、Service对象等等也是需要写出来的，要不刚刚建的注解标注谁呢？

提前说明以下，因为本部分主要是讲解Spring机制，因此会淡化其他部分，只要能说明Spring机制就行，这里的数据库、Servlet等内容就不再创建了，只创建个Dao和Service，用来说明内部的自动装配关系。

> Dao

```java
package _03_DoMySpring._02_Component;


import _03_DoMySpring._01_Annotation.Component;//引入自己的注解

@Component
//不指定Scope，默认为单例
public class MonsterDao {

    public void hi(){
        System.out.println("DaoHi~");
    }
}

```

这个Dao对象就是最基本的Dao对象，注解为Component，即需要注入容器，并且不用Scope注解，默认为单例。



> Service

```java
package _03_DoMySpring._02_Component;

import _03_DoMySpring._01_Annotation.AutoWired;
import _03_DoMySpring._01_Annotation.Component;//引入自己的注解
import _03_DoMySpring._01_Annotation.Scope;
import _03_DoMySpring._04_processor.MyInitializingBean;

@Component
@Scope(value = "prototype")//指定为多例
public class MonsterService implements MyInitializingBean {

    //使用AutoWired修饰MonsterDao属性，表示该属性是通过Spring容器实现依赖注入的
    @AutoWired
    private MonsterDao monsterDao;

    public void h1(){
        monsterDao.hi();
    }


    //实现接口的方法，即初始化方法（init方法）
    @Override
    public void afterPropertiesSet() throws Exception {
        //该方法里可以写初始化的具体业务
        System.out.println(this + "初始化方法被调用");

    }
}

```

Service的内容也同样简单，使用Component标注表示要将其注入容器，同时Scope标注为多例，以展示和单例不同的效果。内部MonsterDao属性则使用AutoWired自动装配。



其他的如`MyInitializingBean`、`afterPropertiesSet`等内容后面再介绍



> noComponent

除了需要注入容器的bean对象外，再做一个不使用Componet标注的类来展示一下不注入容器的判断

```java
package _03_DoMySpring._02_Component;

public class noComponent {
}
```



#### 3.1.3 容器

这里就是ioc的核心了，容器的搭建。



> Bean定义类

在正式搭建容器之前，先做一些必备的准备工作。

首先是一个bean的定义类——MyBeanDefinition类。该类中包含了一个bean对象的两个属性：单例或多例以及该bean对象的所属类。myBeanDefinition对象最后会放入MyBeanDefinitionMap集合中，再使用时会直接从集合中取出合适的myBeanDefinition对象。提一嘴，

```java
package _03_DoMySpring._03_ioc;

/**
 * 用来存放扫描包下需要放入容器的bean对象信息。包括：单例多例、bean对应的class
 */
public class MyBeanDefinition {
    private String scope;
    private Class clazz;

    public String getScope() {
        return scope;
    }

    public void setScope(String scope) {
        this.scope = scope;
    }

    public Class getClazz() {
        return clazz;
    }

    public void setClazz(Class clazz) {
        this.clazz = clazz;
    }

    @Override
    public String toString() {
        return "BeanDefinition{" + "scope='" + scope + '\'' + ", clazz=" + clazz + '}';
    }
}

```



> 扫描方法beanDefinitionScan

讲解容器的搭建过程就按照逻辑的实现流程来说明，第一步就是经典的，确定容器扫描哪个包下的类。

在说明此方法之前，先提前说两个跟此方法有关的内容：

```java
//1、传入该方法的实参为一个类的类对象，此类为：
package _03_DoMySpring._03_ioc;

import _03_DoMySpring._01_Annotation.ComponentScan;

@ComponentScan("_03_DoMySpring/_02_Component")
public class MyStringConfig {
}


//该类被一个注解注释，用来表示扫描的包的路径，此注解为：
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 扫描路径注解
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface ComponentScan {
    String value() default "";//这一行表示myComponentScan注解在标识其他类时，可以接收一个String类型的参数，作为myComponentSacn的value
}



//2、有一个大类中的属性在这个方法被使用，就是一个类对象承载属性。
private Class configClass;//定义一个Class属性，用来接收反射的Class
//定义一个BeanDefinitionMap，用来存放BeanDefinition
private ConcurrentHashMap<String,MyBeanDefinition> BeanDefinitonMap = new ConcurrentHashMap<>();

```



> 扫描包以注入容器

注入容器是通过扫描`@ComponentScan("_03_DoMySpring/_02_Component")`这里对应的文件目录来确定其目录下谁被`Component`标注了，从而将谁放入到容器中。

```java
//将之前的构造器变为一个方法，在构造器中直接调用该方法完成扫描
    public void beanDefinitionScan(Class configClass)  {
        this.configClass = configClass;//构造容器时直接将反射内容初始化好

        //1、通过得到的反射对象，解析该对象中的注解。在此处为：得到的反射对象为：SpringConfig、反射对象中的注解为：MyComponent
        ComponentScan myComponentScan = (ComponentScan) this.configClass.getDeclaredAnnotation(ComponentScan.class);

        //2、拿到注解里配置的value，即容器要扫描的包
        String path = myComponentScan.value();

        //3、获取扫描包下所有的.class文件（这里的.class文件，是out目录下（工作目录）的文件，我们平常用的src目录里的文件，后缀都是.java，工作目录是将.java编译后的结果）
        //3.1得到类加载器
        ClassLoader classLoader = MySpringApplicationContext.class.getClassLoader();
        //3.2通过类加载器获取到要扫描包的url（工作目录url）
        path = path.replace(".", "/");//这里有一个讲究，刚刚得到的注解中的value值是用.来分隔文件夹的，而正经路径得是用/来分割的，故做一个替换
        URL resource = classLoader.getResource(path);

        //System.out.println(resource); //此处输出为file:/D:/Code/JavaCode/_04_Spring/out/production/_04_Spring/_01_ioc/_05_Annotation/_01_component

        //3.3遍历路径下的文件
        String name = resource.getFile();//讲url地址通过getFile方法转为String类型
        File file = new File(name);//把目录作为一个文件创建

        if (file.isDirectory()) {//当file确实是存在的的时候
            File[] files = file.listFiles();//将file下的子文件都逐一取出放入files数组中

            //将目录文件下的所有子文件逐一取出，并通过反射实例化其具体对象
            for (File f : files) {
                String absolutePath = f.getAbsolutePath();//拿到具体class文件的绝对路径


                //这里最好做一个过滤，只处理.class文件
                if(absolutePath.endsWith(".class")){
                    //先得到类名
                    String classname = absolutePath.substring(absolutePath.lastIndexOf("\\") + 1, absolutePath.indexOf(".class"));//将最后一个\到.class直接的内容截取出来，也就是将类名截取出来

                    //再得到全类名
                    String classFullName = path.replace("/", ".") + "." + classname;

                    //判断得到的类里是否有注解，该注解是否需要实例对象放入容器中，即该类里是否有那四个注解
                    try {
                        //通过类加载器加载一个全类名，得到该类名对应的class。也可用Class.forName(classFullName)方法得到，但是该方式会默认调用此类的静态方法(相对完善)，下面的方法并不会（相对轻量级一点）。
                        Class<?> clazz = classLoader.loadClass(classFullName);
                        //判断类中是否有这四个注解（用一个component来代替）
                        if (clazz.isAnnotationPresent(Component.class)) {
                            System.out.println(classname + "是一个Component注解的类，会注入容器");

                            //通过反射得到Component注解，以获取其内部value值，得到该值后方便将该值当为key记入BeanDefinitonMap中
                            Component componentAnnotation = clazz.getDeclaredAnnotation(Component.class);
                            String beanName = componentAnnotation.value();
                            if("".equals(beanName)){//如果没用定义好beanName，则默认为首字母小写作为beanName
                                beanName = StringUtils.uncapitalize(classname);
                            }
                            MyBeanDefinition beanDefinition = new MyBeanDefinition();//做一个beanDefinition，承载该bean的信息以准备放入map
                            beanDefinition.setClazz(clazz);//将clazz装入beanDefinition

                            if(clazz.isAnnotationPresent(Scope.class)){//判断是否写了Scope，写了则判断是单例还是多例，没写则默认单例
                                Scope scopeAnnotation = clazz.getDeclaredAnnotation(Scope.class);
                                beanDefinition.setScope(scopeAnnotation.value());
                            }else {//没写，默认单例
                                beanDefinition.setScope("singleton");
                            }

                            //2、将初始化好的beanDefinition放入map中
                            BeanDefinitonMap.put(beanName,beanDefinition);

                            //3、判断是否为后置处理器，通过看当前类对象中是否实现了MyBeanPostProcessor接口来判断
                            if(MyBeanPostProcessor.class.isAssignableFrom(clazz)){//这里对比不能用instanceof来，因为此时clazz是一个类对象，不是实例对象，而instanceof是看运行类型的，而不是实例对象就没有运行类型

                                //如果实现了，就将当前类对象实例化，实例化为一个实现了MyBeanPostProcessor接口的对象
                                MyBeanPostProcessor myBeanPostProcessor = (MyBeanPostProcessor)clazz.newInstance();
                                beanPostPorceList.add(myBeanPostProcessor);//将对象放入list列表中，有需要就从列表取
                            }

                        }else {
                            System.out.println(classname +  "不是一个Component注解的类，不注入容器");
                        }
                    } catch (Exception e) {
                        e.printStackTrace();
                    }

                }
            }
        }
    }
```

以上流程就是标准流程，先解析出待扫描包对应的类路径，得到此路径下的所有类并遍历之，判断类上的注解是否有`Component`和`Scope`，如果有则分别进行处理，并做好该类对应的`BeanDefinition`存放`BeanDefinitionMap`中。

但是这一方法并不是具体初始化容器的方法，但是完成这个方法后，离初始化容器只有一步之遥了——创建单例对象方法：



> 创建对象方法

上面扫描完包后，只是把所有应该放入容器的类都做了一个`BeanDefinition`，并放入`BeanDefinitionMap`中，其中包含单例和多例类，但是并没有具体实例化单例对象到单例池中。

这里要做一个创建bean对象的方法，以便于实例对象。

```java
   //提供一个创建bean对象的方法，具体什么时间创建，由单例还是多例决定。
    private Object creatBean(MyBeanDefinition beanDefinition){//通过MyBeanDefinition中存放的class信息来反射创建bean对象

        //先拿到beanDefinition的信息
        Class clazz = beanDefinition.getClazz();
        String beanName = clazz.getName();
        beanName = beanName.substring(beanName.lastIndexOf(".") + 1);//将类路径裁剪到最后一部分，得到具体类名

        //通过反射得到实例
        try {
            Object o = clazz.newInstance();


            //实现依赖注入，得到当前要实例化的类中的所有注解，判断是否有需要依赖注入的属性
            for (Field field : clazz.getDeclaredFields()){

                //如果有AutoWired修饰的信息（属性、方法等等），
                if (field.isAnnotationPresent(AutoWired.class)){
                    //就得到该信息的名称（一般是属性，就得到了该属性的名字）
                    String name = field.getName();

                    //然后在容器中，得到属性名字对应的对象
                    Object bean = getBean(name);

                    //进行组装，将刚得到的name组装进当前要实例化类中
                    //而由于要考虑属性是私有化的，不能外部直接访问，要进行一次爆破
                    field.setAccessible(true);
                    field.set(o,bean);
                }
            }

            /*
            下方是生命周期的实现
             */

            //init方法前的后置处理器before方法
            for (MyBeanPostProcessor myBeanPostProcessor : beanPostPorceList){
                o = myBeanPostProcessor.before(o, beanName);//直接用o本身来接收后置处理器处理o后的结果，这也是后置处理器的意义——对对象做一次优化，老o进去，新o出来
                //这里实际上还有一个判断o是否为null的逻辑，如果o为空，则返回未经后置处理器处理前的o。这里不写了，一个if(o==null)的判断就完事
            }

            //下面业务是判断bean类是否需要实现生命周期的init方法
            if(o instanceof MyInitializingBean){//先判断该类是否实现了MyInitializingBean接口，如果实现了，就执行init方法
                try {
                    ((MyInitializingBean)o).afterPropertiesSet();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }

            //init方法后的后置处理器after方法
            for (MyBeanPostProcessor myBeanPostProcessor : beanPostPorceList){
                o = myBeanPostProcessor.after(o,beanName);//同理，用o直接接收
            }

            return o;


        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }

        return null;//如果反射失败，则返回空
    }
```

这里又涉及到一个知识——依赖注入问题。

为了实现依赖注入，都是在需要被注入的地方用`AutoWired`注解标注的。该注解如下：

```java
package _03_DoMySpring._01_Annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD,ElementType.FIELD})//修饰属性和方法
@Retention(RetentionPolicy.RUNTIME)
public @interface AutoWired {
}

```

道理也很简单，判断一个待实例化类里有没有需要依赖注入的字段，如果有，则去单例池中找对应的属性名的已经实例化好了的对象（这里写的忽略了一个细节，就是先把没有依赖注入的类实例化，再实例化有依赖注入的类）来放入此处的属性中。使用的是getBean方法，如下：

```java
//提供一个getbean方法
    public Object getBean(String name) {
        MyBeanDefinition beanDefinition = BeanDefinitonMap.get(name);//先得到name对应的beanDefinition

        if (BeanDefinitonMap.containsKey(name)) {//若该name是合法的name，即存在于Spring容器中

            //判断该name对应的类的Scope类型
            if ("singleton".equalsIgnoreCase(beanDefinition.getScope())) {//若为单例的，则直接从单例池里返回创建好的对象
                return singletonObjects.get(name);
            } else {//若不是单例的，则每次getbean时都创建一个新的对象
                return creatBean(beanDefinition);
            }
        }else {//若name不合法，则抛出空指针异常
            throw new NullPointerException("没有该bean");
        }
    }
```



> 容器初始化

在有了这些工作之后，就可以进行容器的初始化了，容器初始化在 构造器中实现。

```java
package _03_DoMySpring._03_ioc;

import _03_DoMySpring._01_Annotation.AutoWired;
import _03_DoMySpring._01_Annotation.Component;
import _03_DoMySpring._01_Annotation.ComponentScan;
import _03_DoMySpring._01_Annotation.Scope;
import _03_DoMySpring._02_Component.BeanPostPorce;
import _03_DoMySpring._04_processor.MyBeanPostProcessor;
import _03_DoMySpring._04_processor.MyInitializingBean;
import org.springframework.util.StringUtils;

import java.io.File;
import java.lang.reflect.Field;
import java.net.URL;
import java.util.ArrayList;
import java.util.Enumeration;
import java.util.List;
import java.util.concurrent.ConcurrentHashMap;

public class MySpringApplicationContext {
    private Class configClass;//定义一个Class属性，用来接收反射的Class

    //定义一个BeanDefinitionMap，用来存放BeanDefinition
    private ConcurrentHashMap<String,MyBeanDefinition> BeanDefinitonMap = new ConcurrentHashMap<>();

    //定义一个SingletonObjects，用来存放单例对象。多例对象不做集合存放，因为多例对象随getbean方法调用才开始创建
    private ConcurrentHashMap<String,Object> singletonObjects = new ConcurrentHashMap<>();

    //定义一个属性，存放后置处理器。这里是为了方便这么写的，一般来说是存放在单例池中的（用getbean、creatbean等方法创建出来的）
    private List<MyBeanPostProcessor> beanPostPorceList = new ArrayList<>();


    public MySpringApplicationContext(Class configClass) {
        beanDefinitionScan(configClass);

        //得到beanDefinitionMap中的所有key，放入枚举中
        Enumeration<String> keys = BeanDefinitonMap.keys();
        while (keys.hasMoreElements()){//遍历keys(枚举的遍历方法)
            String beanName = keys.nextElement();//得到所有的beanname

            MyBeanDefinition beanDefinition = BeanDefinitonMap.get(beanName);//通过beanname得到该name对应的beanDefinition对象

            //而beanDefinition对象中存放有Scope信息，故从这里读取该信息，判断是单例还是多例
            if("singleton".equalsIgnoreCase(beanDefinition.getScope())){
                singletonObjects.put(beanName,creatBean(beanDefinition));//若为单例，则将该对象通过creatBean实例化后放入单例池里
            }//由于beanDefinitionScan中已经处理了Scope为空的情况（处理为：若空，则赋值为singleton），故这里就不用管了，只处理singleton和propretotyep两种情况
        }

    }
```

有关容器的所有方法都在这个类下，这里通过构造器初始化容器，首先Scan指定包，将有`Component`的类放入z`BeanDefinitionMap`中，之后遍历此Map，看看里面的类是否有单例，如果有则使用`CreatBean方法`将其实例化后放入单例池`SingletonObjects`中。至此就算将容器初始化完成。

上面还有些细节没有提到，如后置处理器，生命周期等等内容，这些都是AOP的东西了。



### 3.2、AOP

AOP的底层是动态代理，之前的手动实现AOP是将动态代理单独列到了一个类里，但是实际的动态代理过程是在后置处理器的after方法里实现的，即一个正确的bean类在Spring中的状态随生命周期转变如下：

```
生命周期: bean构造器 --> bean的set方法 --> 后置处理器的前置方法 --> init方法 --> 后置处理器的后置方法 --> 销毁
运行类型: bean本体   -->  bean本体    -->     bean本体       --> bean本体 -->  代理对象类型 
```

因此AOP的核心在于后置处理器。

但是在说明后置处理器前，先把生命周期做出来



#### 3.2.1 生命周期

> 初始化

```JAVA
package _03_DoMySpring._04_processor;
/**
 * 做一下生命周期中的初始化方法（init）方法，该方法在set之后执行，当一个bean实现这个接口后，就实现该接口中的方法，即初始化方法
 */
public interface MyInitializingBean {
    void afterPropertiesSet() throws Exception;
}

```



> 后置处理器

```java
package _03_DoMySpring._04_processor;

import org.springframework.beans.BeansException;

/**
 * 模拟一下后置处理器的使用，其before方法作用于init方法之前，after方法作用于init方法之后
 */
public interface MyBeanPostProcessor {

    //default修饰接口中的方法后，是允许在接口中实现该方法的，即在接口中可以有被default修饰的方法存在方法体（并且default修饰后必须有方法体）
    default Object before(Object bean, String beanName) {
        return bean;
    }

    default Object after(Object bean,String beanName){
        return bean;
    }

}
```



生命周期用接口来指定，如果一个类实现了init接口，就执行init接口中对应的方法，否则执行空（但是也是有这个周期的）。

后置处理器接口则不需要具体bean类来实现，其是通过后置处理器类来实现的，如果一个包中有一个类实现了后置处理器接口，那么这个包中所有的类都会进行后置处理器中的after和before操作。



#### 3.2.2 基本对象

在AOP机制中再做一套基本对象。

要注意，当AOP机制完善后，之前的基本对象里，依赖注入功能会失效报错。即Service对象实例化会失败，因为其中有monsterDao的依赖注入，而Dao经过动态代理后变成了Proxy类型的对象并保存再容器中，其无法注入到Service中了。具体怎么优化，还不会。。。这里先不做讨论了干脆。因此再重新做一套基本对象来应用于AOP中。

> 接口

动态代理过程常常是将一个具体的bean类的编译类型转为其接口类型，运行类型转为proxy类型。而如果没有接口，那么编译类型就转为其内部分配的一个类型。这里讨论接口类型的情况。

```java
package _03_DoMySpring._02_Component;

public interface AopInterface {
    public float getsun(float i, float j);

    public float getsub(float i , float j);
}

```

简单的接口，提供一个加法和一个减法。



> 切面类

AOP必不可少的就是切面类，在切面类里注解`Aspect`来告诉Spring说，该类所在包下的所有类都使用动态代理机制，应用AOP。

```java
package _03_DoMySpring._02_Component;

import _03_DoMySpring._01_Annotation.After;
import _03_DoMySpring._01_Annotation.Aspect;
import _03_DoMySpring._01_Annotation.Before;
import _03_DoMySpring._01_Annotation.Component;

@Aspect
@Component
public class AopAspect {

    @Before(value = "execution(public float _03_DoMySpring._02_Component.AopBean.getSum(float, float))")
    public static void showBeginLog(){
        System.out.println("前置通知");
    }

    @After(value = "execution(public float _03_DoMySpring._02_Component.AopBean.getSum(float, float))")
    public static void showSuccessLog(){
        System.out.println("返回通知");
    }
}
```

这里写了一个简单的切面类，提供了一个前置通知和返回通知。并且Spring识别Aspect注解的机制也不再写了，主要聚焦于AOP的机制。

Before、After注解也就意会一下就行，不再做实现了。



> bean类

最后就是实现接口的Bean类的创建了。

```java
package _03_DoMySpring._02_Component;

import _03_DoMySpring._01_Annotation.Component;

@Component
public class AopBean implements AopInterface{
    @Override
    public float getsun(float i, float j) {
        float res = i + j;
        System.out.println("getsun方法运行" + res);
        return res;
    }

    @Override
    public float getsub(float i, float j) {
        float res = i - j;
        System.out.println("getsub方法运行" + res);
        return res;
    }

}
```

实现接口，并填充方法即可。



#### 3.2.3 后置处理器

下面就看看AOP的核心部分，动态代理机制的使用。该机制是用于后置处理器上的，并且详细应用于后置处理器的after方法中。后置处理器会实现后置处理器接口，重写一下接口中提供的两个方法，其中before方法就简单写自己需要有什么实现就行，但是after方法中要写明具体的动态代理机制。

```java
package _03_DoMySpring._02_Component;

import _03_DoMySpring._01_Annotation.Component;
import _03_DoMySpring._04_processor.MyBeanPostProcessor;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

/**
 * 实现后置处理器接口，重写其方法。
 * 要注意，Spring中，将后置处理器也视为一个bean对象来放入容器中，故也用Component注释一下
 * 后置处理器的实现路径，是看后置处理器对象，即下面要写的类写在了哪个包下，写哪个包下，则这个包下的所有dao都会用到此后置处理器（容器中配置的）
 */

@Component
public class BeanPostPorce implements MyBeanPostProcessor {
    @Override
    public Object before(Object bean, String beanName) {
        System.out.println(bean + "后置处理器的before使用");
        return bean;
    }

    //前面讲过，动态代理过程是在后置处理的after方法处完成的，在after之前，具体bean对象的运行类型和编译类型都还原本的类型，
    // 一旦通过了after之后，编译类型成了接口类型、运行类型成了Proxy类型。
    //因此，这里要实现一下代理类的转换
    @Override
    public Object after(Object bean, String beanName) {
        System.out.println(bean + "后置处理器的after使用");
        Object proxy = Proxy.newProxyInstance(BeanPostPorce.class.getClassLoader(), bean.getClass().getInterfaces(), new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("method=" + method.getName());

                //插入前置通知
                AopAspect.showBeginLog();

                //调用方法
                Object invoke = method.invoke(bean, args);

                //插入后置通知
                AopAspect.showSuccessLog();

                return invoke;
            }
        });
        return proxy;//这里return回proxy，这样通过after之后，bean对象的运行类型就从bean本身变为了proxy
        //这里会发现，如果return的是bean，则这个匿名内部类不会使用，
        // 因为只有当运行类型时proxy时，执行某方法后，proxy对象会从invoke方法里找具体的方法，从而顺带执行了前置通知后置通知等内容；
        // 而如果时bean对象，则只会运行bean里的方法，不经过动态代理了
    }
}

```

在动态代理中，使用上切面类里提供的前置通知和后置通知。

到此为止，AOP机制的准备工作就做完了，具体应用到SPring中，就在容器类里实现。



#### 3.2.4 应用

实际上加入动态代理机制的代码就在IOC里讲的容器中写完了，这里强调一下。



> Scan方法内

首先是容器的扫描方法中，会在遍历包下类是，在已经是`Component`的前提下判断每个类是否实现了`MyBeanPostProcessor `接口，即动态代理接口（动态代理类已经是被Component注解了，所以讲Component的前提条件加入判断），如果是，则讲实现该接口的类——动态代理类放入一个动态代理类集合中，因为有时会有多条动态代理要同时使用，这是就要去集合中看谁优先级最高就先用谁。

```java
public class MySpringApplicationContext {
    //定义一个属性，存放后置处理器。这里是为了方便这么写的，一般来说是存放在单例池中的（用getbean、creatbean等方法创建出来的）
    private List<MyBeanPostProcessor> beanPostPorceList = new ArrayList<>();
    
     public void beanDefinitionScan(Class configClass)  {
         ...;
         
         //3、判断是否为后置处理器，通过看当前类对象中是否实现了MyBeanPostProcessor接口来判断
         if(MyBeanPostProcessor.class.isAssignableFrom(clazz)){//这里对比不能用instanceof来，因为此时clazz是一个类对象，不是实例对象，而instanceof是看运行类型的，而不是实例对象就没有运行类型

         //如果实现了，就将当前类对象实例化，实例化为一个实现了MyBeanPostProcessor接口的对象
         MyBeanPostProcessor myBeanPostProcessor = (MyBeanPostProcessor)clazz.newInstance();
         beanPostPorceList.add(myBeanPostProcessor);//将对象放入list列表中，有需要就从列表取
              
     }
}

```



> creat方法内

在动态代理类集合中存在了动态代理类之后，Spring就会判断某些类到底用不用动态代理了，如果用，则在其bean生命周期的after时刻将其代理掉。这里简单点，就不做判断，所有类都进行动态代理。在creat方法中，将完整的实现bean的生命周期方法（before、init、after，其他的如构造器调用在creat方法最开始通过反射得到实例时就使用了、set方法则在对字段初始化时使用了）。

```java
private Object creatBean(MyBeanDefinition beanDefinition){
    ...;
    //init方法前的后置处理器before方法
    for (MyBeanPostProcessor myBeanPostProcessor : beanPostPorceList){
        o = myBeanPostProcessor.before(o, beanName);//直接用o本身来接收后置处理器处理o后的结果，这也是后置处理器的意义——对对象做一次优化，老o进去，新o出来
     //这里实际上还有一个判断o是否为null的逻辑，如果o为空，则返回未经后置处理器处理前的o。这里不写了，一个if(o==null)的判断就完事
     }

      //下面业务是判断bean类是否需要实现生命周期的init方法
      if(o instanceof MyInitializingBean){//先判断该类是否实现了MyInitializingBean接口，如果实现了，就执行init方法
         try {
             ((MyInitializingBean)o).afterPropertiesSet();
         } catch (Exception e) {
             e.printStackTrace();
         }
      }

       //init方法后的后置处理器after方法
       for (MyBeanPostProcessor myBeanPostProcessor : beanPostPorceList){
           o = myBeanPostProcessor.after(o,beanName);//同理，用o直接接收
       }

      return o;
    
}
```

这么一来，Spring中应该被动态代理的对象就都被代理好了，并且切面方法也已经插入完毕，就已经可以运行了。



### 3.3 运行

```java
public class run {
    public static void main(String[] args) {
        MySpringApplicationContext ioc = new MySpringApplicationContext(MyStringConfig.class);
        AopInterface aopBean = (AopInterface)ioc.getBean("aopBean");
        System.out.println(aopBean.getClass());
        aopBean.getsub(1,1);
    }
}
```

其结果为：

```
AopAspect是一个Component注解的类，会注入容器
AopBean是一个Component注解的类，会注入容器
AopInterface不是一个Component注解的类，不注入容器
BeanPostPorce$1不是一个Component注解的类，不注入容器
BeanPostPorce是一个Component注解的类，会注入容器
MonsterDao是一个Component注解的类，会注入容器
MonsterService是一个Component注解的类，会注入容器
noComponent不是一个Component注解的类，不注入容器
_03_DoMySpring._02_Component.BeanPostPorce@452b3a41后置处理器的before使用
_03_DoMySpring._02_Component.BeanPostPorce@452b3a41后置处理器的after使用
_03_DoMySpring._02_Component.AopBean@3f99bd52后置处理器的before使用
_03_DoMySpring._02_Component.AopBean@3f99bd52后置处理器的after使用
_03_DoMySpring._02_Component.AopAspect@85ede7b后置处理器的before使用
_03_DoMySpring._02_Component.AopAspect@85ede7b后置处理器的after使用
_03_DoMySpring._02_Component.MonsterDao@1be6f5c3后置处理器的before使用
_03_DoMySpring._02_Component.MonsterDao@1be6f5c3后置处理器的after使用
class com.sun.proxy.$Proxy6
method=getsub
前置通知
getsub方法运行0.0
返回通知
```

可以发现，MonsterService的后置处理器并没使用，这是因为其在初始化时就没初始化好（依赖注入失败了），所以运行不到后面的内容。



## 四、JDBCTemplate

想要让一个框架面向服务，那接入数据库是必不可少的了。Spring也有接入数据库的方法，也是通过配置来实现。



### 4.1 基本介绍

JdbcTemplate 是 Spring 提供的访问数据库的技术。可以将 JDBC 的常用操作封装为模板方法。



### 4.2 应用

JDBCTemplate是通配置来实现的，那么下面就按顺序配出来



> 数据库连接配置

想用数据库，肯定先要跟数据库建立连接。在使用连接时，一般都是先将连接信息（账户、密码、端口等）写到一个文件里，然后在像配置bean对象一样将连接信息配置到Spring容器中。

```properties
jdbc.user=root
jdbc.pwd=123456hlh789
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/spring
```



> 容器配置

跟之前的Spring容器配置别无二致了只能说。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--引入配置的jdbc.properties文件-->
    <context:property-placeholder location="classpath:_04_JdbcTemplate/jdbc.properties"/>

    <!--配置数据源对象-->
    <bean class="com.mchange.v2.c3p0.ComboPooledDataSource" id="dataSource">
        <!--给数据源配置属性-->
        <property name="user" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.pwd}"/>
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
    </bean>

    <!--配置JdbcTemplate对象，把这个对象当作常规的bean对象就行-->
    <bean class="org.springframework.jdbc.core.JdbcTemplate" id="jdbcTemplate">
        <property name="dataSource" ref="dataSource"/>
    </bean>
</beans>
```

先引入刚刚的连接配置，然后做一个数据源对象，该对象实际上就是连接数据库用的，其中属性就是连接数据库的必备属性了。

在配置好数据源对象后，就正式配JDBCTemplate对象了，该对象只要求一点，就是属性中ref指向刚刚配的数据源对象即可。



> 具体使用

先简单做个类：

```java
package _04_JdbcTemplate;

public class monster {
    private int id;
    private String name;
    private String skill;

    @Override
    public String toString() {
        return "monster{" + "id=" + id + ", name='" + name + '\'' + ", skill='" + skill + '\'' + '}';
    }

    public monster() {
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSkill() {
        return skill;
    }

    public void setSkill(String skill) {
        this.skill = skill;
    }
}

```



开始使用：

```java
package _04_JdbcTemplate;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;

import javax.sql.DataSource;
import java.util.ArrayList;
import java.util.List;

public class run {

    @Test
    public void connection(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_04_JdbcTemplate/jdbcTemplate.xml");
        DataSource bean = ioc.getBean(DataSource.class);
        System.out.println(bean);
        System.out.println("ok");
    }

    @Test
    public void addDataByJdbcTemplate(){//向数据库添加信息
        //调用Spring容器里的jdbcTemplate对象
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_04_JdbcTemplate/jdbcTemplate.xml");
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        String sql = "INSERT INTO monster VALUES(400,'红孩儿','枪法')";
        //添加方式一，直接添加
        jdbcTemplate.execute(sql);
        System.out.println("添加成功");

        //添加方式二，防止注入型添加
        String sql2 = "INSERT INTO monster VALUES(?,?,?)";
        jdbcTemplate.update(sql2,500,"红孩儿2","枪法2");
        System.out.println("添加成功");

    }

    @Test
    public void updateDataByJdbcTemplate(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_04_JdbcTemplate/jdbcTemplate.xml");
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        //添加语句，也用update方法
        String sql = "UPDATE monster SET skill=? WHERE id=?";
        jdbcTemplate.update(sql,"吐丝","300");
        System.out.println("修改成功");
    }

    @Test
    public void addBatchDataByJdbcTemplate(){//批量添加数据
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_04_JdbcTemplate/jdbcTemplate.xml");
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        String sql = "INSERT INTO monster VALUES(?,?,?)";
        List<Object[]> batchArgs = new ArrayList<>();
        batchArgs.add(new Object[]{600,"老鼠精","偷吃"});
        batchArgs.add(new Object[]{700,"狐狸精","偷人"});
        int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
        for(int aint : ints){
            System.out.println(aint);
        }
        System.out.println("批量添加成功");

    }

    @Test
    public void selectDataByJdbcTemplate(){//查询数据库，并返回该查询结果封装好的对象
        ApplicationContext ioc = new ClassPathXmlApplicationContext("_04_JdbcTemplate/jdbcTemplate.xml");
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        //单个查找
        String sql = "SELECT id ,name,skill FROM monster WHERE id = 100";
        //rowMapper是一个接口，可以将查询的结果封装到指定的be'an
        RowMapper<monster> rowMapper = new BeanPropertyRowMapper<>(monster.class);
        monster monster = jdbcTemplate.queryForObject(sql, rowMapper);
        System.out.println(monster);

        //批量查找
        String sql2 = "SELECT id name,skill FROM monster WHERE id>=?";
        RowMapper<monster> rowMapper2 = new BeanPropertyRowMapper<>(monster.class);

        List<_04_JdbcTemplate.monster> query = jdbcTemplate.query(sql2, rowMapper, 200);
        for(monster monster1: query){
            System.out.println(monster1);
        }

        //单行单列查询
        String sql3 = "SELECT name FROM monster WHERE id=100";
        String name = jdbcTemplate.queryForObject(sql3, String.class);
        System.out.println(name);

    }
}

```

就这么简单，从容器中取出配置的JDBCTemplate，然后写好sql语句，就可以用JdbcTemplate中自带的方法去向数据库操作了。



## 五、声明式事务

