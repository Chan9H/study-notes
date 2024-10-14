# MyBatis

MyBatis 是一个持久层框架(Dao层框架)， MyBatis 在 java 和 sql 之间提供更灵活的映射方案 ，mybatis 可以将对数据表的操作(sql,方法)等等直接剥离，写到 xml 配置文件，实现和 java 代码的解耦。



## 一、 快速入门

### 1.1 resource

MyBatis的使用是要有配置文件配置的。MyBatis的配置文件主要干两件事，一个是配置数据库的连接、一个是管理Mapper映射xml文件。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis的配置文件主要完成两个功能：1、配置数据库的连接；2、管理XXMapper.xml文件-->
<configuration>
    <!--这里是配置myBatis自带的日志输出，可以通过日志查看底层的sql语句执行情况-->
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>

    <!--这里是配置数据库连接部分-->
    <environments default="development">
        <environment id="development">

            <!--配置事务管理器-->
            <transactionManager type="JDBC"/>

            <!--配置数据源-->
            <dataSource type="POOLED">

                <!--配置驱动-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>

                <!--配置连接mysql的url
                1、jdbc:mysql  协议
                2、127.0.0.1:3306  mysql的IP地址加端口号
                3、mybatis  数据库的具体名称
                4、useSSL=ture  表示使用安全连接
                5、&amp  和的意思
                6、useUnicode  使用unicode编码
                7、characterEncoding=utf-8  使用utf-8编码-->
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf-8"/>

                <!--用户名和密码-->
                <property name="username" value="root"/>
                <property name="password" value="123456hlh789"/>
            </dataSource>

        </environment>
    </environments>

    
    
    <!--这里是管理具体mapper文件部分，将自己写好的mapper.xml文件配到这里-->
    <mappers>
        <mapper resource="mapper/MonsterMapper.xml"/>

        <!--如果通过注解，则可以不再使用xml文件，但是需要引入含注解的类-->
        <mapper class="mapper.AnnotationMapper"/>
    </mappers>
    
    
</configuration>
```



### 1.2  mapper

mapper中有一个mapper接口和一个mapper配置文件，其中mapper接口定义的是sql的类型，入select、update等，而mapper配置文件里则是具体的sql语句的执行信息。



#### 1.2.1 Mapper Interface

```java
/**
 * 这是一个接口，该接口用于声明操作monster的方法
 * 这些方法可以通过注解或者xml文件配置实现（不需要做实现类了）
 */
public interface MonsterMapper {

    //添加monster方法
    void addMonster(Monster monster);

    //删除monster方法
    void delMonster(int i);

    //修改monster方法
    void updateMonster(Monster monster);

    Monster getMonsterById(int i);
}

```





#### 1.2.2 Mapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--这是一个mapper配置文件，该文件可以去实现对应接口的方法-->
<!--
namespace为和该xml文件匹配的接口名称
-->
<mapper namespace="mapper.MonsterMapper">
    <!--配置mapper接口具体的方法

    1、因为是插入方法，所以用insert标签
    2、id 指定具体的接口方法名
    3、parameterType 指定形参列表的数据类型
    4、标签体内，写具体的sql语句，表名和字段名建议都带上反引号，具体value部分，则用传入形参列表的bean对象里的属性来一一对应，如age对应Moster类里的age属性
    -->
    <insert id="addMonster" parameterType="entity.Monster">
        INSERT INTO `monster` (`id`,`age`,`birthday`,`email`,`gender`,`name`,`salary`)
        VALUES(#{id},#{age},#{birthday},#{email},#{gender},#{name},#{salary})
    </insert>

    <!--同理，配置一个删除方法-->
    <delete id="delMonster" parameterType="java.lang.Integer">
        DELETE FROM `monster`
        WHERE `id`= #{id}
    </delete>

    <!--配置一个修改方法-->
    <update id="updateMonster" parameterType="entity.Monster">
        UPDATE `monster`
        SET age=#{age}, birthday=#{birthday}, email=#{email},
            gender=#{gender}, name=#{name}, salary=#{salary}
        WHERE id=#{id}
    </update>

    <!--配置一个查询方法
    这里多了一个resultType，对应于parameterType，这个是方法的返回数据类型
    这里多提一嘴，当传入的参数类型不为对象时，`id` = #{i}后面的#{i}就只是一个占位符的意思了，不再用来代表对象的某个字段，而是接受传入的实参
    -->
    <select id="getMonsterById" parameterType="Integer" resultType="entity.Monster">
        SELECT * FROM `monster` WHERE `id` = #{i}
    </select>

</mapper>
```

具体细节都在代码里注释了。



### 1.3 utils

在独立学MyBatis时，需要自己做好一个工具类，来得到SqlSession从而操作Mapper。

```java
package util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * 工具类，可以得到sqlSession。即完成：
 * 1、通过mybaits-config文件获得到sqlSessionFactory对象（可以理解为连接池）
 * 2、通过SessionFactory对象获取到sqlSession（可以理解为连接）
 */
public class MyBatisUtils {

    private static SqlSessionFactory sqlSessionFactory;//先做一个sqlSessionFactory静态属性

    //编写一个静态代码块，初始化sqlSessionFactory
    static {

        //1、指定资源文件，即mybatis-config.xml
        String resource = "mybatis-config.xml";


        try {
            //2、获取到配置文件对应的输入流（inputStream），默认在resources目录下获取，在运行时，系统会去运行目录——out下找该文件，因此要包装out目录下有此处的resource文件
            InputStream resourceAsStream = Resources.getResourceAsStream(resource);

            //3、通过输入流得到sqlSession工厂
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
            System.out.println("sqlSessionFactory=" + sqlSessionFactory.getClass());

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //编写一个方法，返回sqlSessionFactory里的slqSession
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }

}

```



### 1.4 run

在做好上面的准备工作后，就该进行使用mybaits了，使用方式如下：

```java
package _01_selfSqlUse;

import entity.Monster;
import mapper.MonsterMapper;
import org.apache.ibatis.session.SqlSession;
import org.junit.Before;
import org.junit.Test;
import util.MyBatisUtils;

import java.util.Date;

/**
 * 这里使用我们自己再xml文件里配置的sql方法来执行增删改查
 */
public class MonsterMapperTest {

    private SqlSession sqlSession;
    private MonsterMapper monsterMapper;

    //初始化Mapper的方法

    /**
     * 这里before注解表示，执行当前类的任何方法之前，都会先执行一下这个方法。
     * 而此方法又是初始化方法，因此标注一个Before再合适不过了
     */
    @Before
    public void init(){
        //获取到sqlSession
        sqlSession = MyBatisUtils.getSqlSession();

        //获取到MonsterMapper对象，这里通过sqlSession连接获取该对象。该对象实际上是一个proxy对象，即代理对象。
        //这里实际上就是一个动态代理过程，之前讲动态代理时，就是代理的某个类的实现接口的对象，而这里直接代理那个接口了，省去了创建那个接口的实现类
        monsterMapper = sqlSession.getMapper(MonsterMapper.class);
        System.out.println(monsterMapper.getClass());

    }

    @Test
    public void addMonster(){
        Monster monster = new Monster(2,10,"jack","11@qq.com",new Date(),12.1,10);
        monsterMapper.addMonster(monster);


        //增删改时，需要手动提交事务，默认是不提交事务的
        sqlSession.commit();//提交事务
        sqlSession.close();//将连接放回连接池

    }

    @Test
    public void delMonster(){
        monsterMapper.delMonster(5);
        sqlSession.commit();//提交事务
        sqlSession.close();//将连接放回连接池
    }

    @Test
    public void updateMonster(){
        Monster monster = new Monster(1,23,"tom","22@1",new Date(),30,10);
        monsterMapper.updateMonster(monster);

        sqlSession.commit();//提交事务
        sqlSession.close();//将连接放回连接池
    }

    @Test
    public void getMonsterById(){
        Monster monsterById = monsterMapper.getMonsterById(1);
        System.out.println(monsterById);
        sqlSession.commit();//提交事务
        sqlSession.close();//将连接放回连接池
    }
}

```

这里最核心的就是一点，在使用具体的mapper接口中的方法前，需要先@Before一个初始化方法，通过utils中的内容得到一个sqlSession，并通过此sqlSession的getMapper方法得到具体Mapper接口的代理对象，之后都是通过该代理对象进行调用mapper接口中的方法的。



## 二、手动实现

下面手动实现一下Mybatis的机制，核心机制实际上就是如何将Mapper.xml和Mapper接口结合起来的。



### 2.1 Bean对象

简单做一个bean对象以供数据库使用。

```java
package entity;

import lombok.*;

import java.util.Date;

/**
 * 使用lombok来简化操作。
 * 这里使用@Getter注解、@Setter注解来自动将类的所有属性生成对应的getter和setter
 * 而@ToString则自动生成该类的toString
 * 无参构造器则用 @NoArgsConstructor、全参构造器用@allArgsConstructor
 *
 */

@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
public class Monster {
    private Integer id;
    private Integer age;
    private String name;
    private String email;
    private Date birthday;
    private double salary;
    private Integer gender;
}

```

使用了Lombok注解来简化bean对象的封装操作，将构造器、getter、setter、tostring都通过注解实现了。



### 2.2 配置文件

配置文件和入门时用的配置文件结构一样，但是内容上只配置一下数据库的连接信息即可。具体连接是通过解析该xml后进行connection。

```xml
<?xml version="1.0" encoding="UTF-8" ?>

<database>
    <!--配置数据库连接信息-->
    <!--1、配置驱动-->
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>

    <!--2、配置连接信息，指定好连接哪个表，并且传入连接的各种参数如编码格式等等-->
    <property name="url" value="jdbc:mysql://127.0.0.1:3306/doselfmybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf-8"/>

    <!--3、用户名和密码-->
    <property name="username" value="root"/>
    <property name="password" value="123456hlh789"/>
</database>
```



### 2.3 Mapper

核心之一，Mapper的构建。

先构建我们看得见的 部分，即Mapper接口和Mapper.xml文件。

```java
public interface MonsterMapper {

    //查询方法
    public Monster getMonsterById(Integer id);
}

```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<mapper namespace="mapper.MonsterMapper">

    <select id="getMonsterById" parameterType="Integer" resultType="entity.Monster">
        SELECT * FROM `monster` WHERE `id` = ?
    </select>

</mapper>
```

由于是学内部机制，故这里的具体sql方法就简单举一个例子就行。



再来看Mybatis封装起来的，我们看不见的东西。

> Function类

首先是mapper.xml文件的承载类，用该类来记录mapper.xml文件里的信息，如语句类型、方法名、返回类型等等内容。可以说，一个Function对象就映射着一个xml里的执行语句，即这部分——`    <select id="getMonsterById" parameterType="Integer" resultType="entity.Monster">SELECT * FROM monster WHERE id = ?</select>`

```java
package mapper;

import lombok.*;

/**
 * 在原生mabaits中，使用时只需要一个mapper接口和一个mapper.xml文件就可以执行sql语句了。其在底层实际上是要为这两个内容各自做一个承载对象来连接的，可以理解为桥梁。
 * 核心原理实际上就是，一个对象承载上xml文件里配置的具体方法体、一个对象承载上Mapper接口中的接口路径和方法名，然后将这两个一结合就可以运行一个完整的方法了。
 * 这里做的Function是Mapper.xml的承载结构，这里是个bean类，用来记录方法体（具体的方法执行）
 */
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
public class Function {
    private String sqlType;//记录当前查询语句的类型：select、insert、delete、update之一
    private String funcName;//记录当前方法的方法名
    private String sql;//记录具体的执行语句
    private Object resultType;//记录返回类型
    private String parameterType;//记录参数类型

}
```



> MapperBean类

刚刚的Function是和一个xml文件内容对应的，而xml文件中的每条内容又和mapper接口中的每个方法对应，因此可以抽象的理解为，每个Function对象实际上就是mapper接口方法的载体，其表示了mapper接口中方法实现需要的全部内容。

那么有了方法的具体内容，再拿到方法的运行地址，就可以进行方法的反射运行了。MapperBean就是装载一个mapper方法运行所需环境的类，即既包含mapper接口方法运行所需要的内容（即Function对象），又包含mapper方法的运行地址。

```java
/**
 * Function是承载xml文件的，这里的Mapperbean则是承载Mapper接口的，用来记录方法的运行环境（路径、方法名）
 * 这里的MapperBean通过记录Function，并记录Mapper接口的全路径，就已经算是一个完整方法运行结构了。则当想调用方法时，可以直接实例化MapperBean对象来调用
 *
 * 在原生的mybatis中只使用到了Mapper接口和Mapper.xml，并没有mapperBean，是因为MapperBean之后会被动态代理掉。
 * (根本来说实际上也不是代理掉mapperBean，只是代理的时候用mapperBean中的内容做了一个判断)
 * 这里某种意义上来说，已经相当于MapperBean类实现了mapper接口了。即 class MapperBean implements Mapper{}，因此后面可以将Bean类代理为其接口类
 */
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
public class MapperBean {

    private String interfaceName;//记录当前Mapper接口的接口全路径

    private List<Function> functions;//记录当前接口下的所有方法，这里可以直接将Function记录的方法体拿过来，这样这个MapperBean对象就已经包含一个完整的方法运行结构（方法名、方法体、方法路径）了
}

```

可以说，得到一个MapperBean对象，就是得到了Mapper接口中某个方法的运行环境。也就是说，可以通过MapperBean对象来运行Mapper接口的方法了。再抽象点看，就是MapperBean类实现了Mapper接口。



### 2.4 execute

完成数据库操作sql语句的部分。

在代理之前，肯定会先做连接，进行后端和数据库的connection。

> connection

这部分通过拆包config文件完成。

```java
/**
 * 本类用来读取资源包中的xml文件，建立与数据库的连接
 */
public class MyConfiguration {


    //1、创建类加载器，公式加载器，直接这么用就能得到
    private static ClassLoader loader = ClassLoader.getSystemClassLoader();

    //2、做一个方法用来读取selfMyBatis.xml文件信息，用来建立与数据库的连接
    public Connection build(String resource){
        Connection connection = null;

        try {

            //2.1 加载selfMybatis.xml(输入的形参)，将其作为一个input流来处理
            InputStream stream = loader.getResourceAsStream(resource);

            //2.2 做一个xml解析器，读取input流
            SAXReader reader = new SAXReader();
            Document document = reader.read(stream);

            //2.3 解析根节点、子节点等信息
            Element rootElement = document.getRootElement();//获取到根元素——<database></database>
            connection = evalDataSource(rootElement);



        } catch (Exception e) {
            e.printStackTrace();
        }

        return connection;


    }

    //2.0、做一个方法，可以解析xml文件中的节点信息，只用于build方法，因此做成private
    private Connection evalDataSource(Element node){//传入一个节点进来
        //1、首先得确定传入的节点是selfMybatis.xml里的根节点——<database>标签
        if (!("database".equals(node.getName()))){
            throw new RuntimeException("root节点错误，应该为<database>");
        }

        //2、定义好需要解析的内容先
        String driverClassName = null;
        String url = null;
        String username = null;
        String password = null;

        //3、开始解析节点，遍历node下的子节点，获取其各自的属性值。遍历子标签property
        for (Object o : node.elements("property")){
            Element item = (Element) o;//此时每个item表示的都是一个property节点

            String name = item.attributeValue("name");//将标签中的name属性取出
            String value = item.attributeValue("value");//将标签中的value属性取出

            //判断是否成功取得value或name
            if (name == null || value == null){
                throw new RuntimeException("此property节点缺少属性name或属性value");
            }

            //判断name是什么
            switch (name){

                //如果当前节点的name是username
                case "username":
                    //则将刚刚定义的解析内容中的url赋值为当前节点的value。
                    //也就是说，通过当前节点的name为username判断出了当前property为：<property name="username" value="root"/>，
                    // 那么就将root赋值到刚刚定义的username上
                    username = value;
                    break;


                //同理了
                case "password":
                    password = value;
                    break;

                case "url":
                    url = value;
                    break;

                case "driverClassName":
                    driverClassName = value;
                    break;

                //若都没匹配上，那就证明property标签的属性写错了
                default:
                    throw new RuntimeException("property的name属性写的有问题");

            }
        }

        //之后就可以将url、username、password给装近一个驱动里，并通过驱动得到一个连接
        Connection connection = null;
        try {
            Class.forName(driverClassName);
            connection = DriverManager.getConnection(url, username, password);
        } catch (Exception e) {
            e.printStackTrace();
        }

        return connection;
    }
}
```

标准的通过dom4j进行的拆包流程，就不再赘述了。

上面这些只需要知道，通过MyConfiguration.build()方法可以得到一个connection连接对象即可。



> 执行

做好连接之后，理论上就可以执行sql文件了。

这里执行时规范一点，通过继承一个执行接口来做执行。

接口如下：

```java
/**
 * 操作数据库的方法，CRUD
 */
public interface Executor {

    //定一个查询方法，传入sql语句，传入需要填充进sql的参数
    public <T> T query(String sql, Object parameter);
}

```

实现类如下：

```java
/**
 * 实现对数据库的CRUD操作
 */
public class MyExecutor implements Executor{

    //定义一个连接属性，因为要对数据库操作，必然需要连接数据库，这里通过MyConfiguration的build方法来实现
    private Connection connection = new MyConfiguration().build("selfMybatis.xml");

    //查询方法，注意，这里第一个形参简化成了sql语句，原生的mybatis中传入的不是简单的sql语句，是一个statement参数，从这个参数中解析出sql语句的。
    @Override
    public <T> T query(String sql, Object parameter) {

        //先定义好返回的结果集
        ResultSet set = null;//接受查询的结果
        PreparedStatement pre = null;//讲mysql的jdbc时讲过，怕PreparedStatement对象是一种执行sql语句的对象，并且此对象可以防止sql注入
        try {
            pre = connection.prepareStatement(sql);//加载上sql语句，构建pre对象
            pre.setString(1,parameter.toString());//将传入的参数转成String类，并放入第一个问号的地方。
            set = pre.executeQuery();//执行sql语句，并将语句返回结果保存在set中

            //这里简化为new一个bean对象，但是实际上myBatis底层是通过反射创建的
            Monster monster = new Monster();
            while (set.next()){
                monster.setName(set.getString("name"));
                monster.setId(set.getInt("id"));
                monster.setEmail(set.getString("email"));
                monster.setAge(set.getInt("age"));
                monster.setGender(set.getInt("gender"));
                monster.setBirthday(set.getDate("birthday"));
                monster.setSalary(set.getDouble("salary"));
            }

            return (T)monster;


        } catch (Exception e) {
            e.printStackTrace();
        }

        return null;
    }
}
```

到此为止，就已经可以通过MyExecutor对象来完成后端到数据库的CRUD操作了。

可以说，MyExecutor完成了数据库方面的集成——连接数据库和在数据库中执行sql语句



但是这是生硬的，完全没用通过mapper接口和mapper配置文件的CRUD操作。下面要开始真正的核心内容——完成sqlSession的创建。



### 2.5 sqlSession

sqlSession是前方信息——mapper和后方信息——数据库的桥梁。

首先看看构造：

```java
/**
 * 在这个类里，要搭建Configuration和Executor之间的桥梁，
 * 会将这两个类封装进此类中
 */
public class MySqlSession {
    //定义两个属性，将Configuration、Executor做出来
    private MyConfiguration configuration = new MyConfiguration();
    private MyExecutor executor = new MyExecutor();


    //编写SelectOne方法，返回一条记录（一个对象）
    public <T> T SelectOne(String sql , Object parameter){
        return executor.query(sql,parameter);
    }


    //得到Mapper接口的动态代理对象，这里将之前讲的动态代理过程拆分开了，这里只保留了得到对象的部分，InvocationHandler匿名内部类的实现在MapperProxy中做了
    public <T> T getMapper(Class<T> clazz){
        return (T) Proxy.newProxyInstance(clazz.getClassLoader(),new Class[]{clazz},new MapperProxy(this,configuration,clazz));
    }
}
```

在这里，首先定义了连接和执行两个属性，光这俩属性就已经是刚刚的`MyConfiguration`和`MyExecuto`的综合应用了。



然后集成了一下executo类中的query方法，命名为selectOne（类似于web项目时的service层调用dao层的方法，虽然看着是直接retrun了dao层的方法，但是service层的方法中可以不止放入一个dao层的方法，要高级很多）。



最后是一个核心方法——getMapper，返回的是一个动态代理对象。观察该代理对象的形参列表里，会发现最后一个参数是new了一个MapperProxy对象，那么这个MapperProxy对象是什么呢？



> MapperProxy

前面知道了，MapperBean对象是完成了Mapper接口和Mapper.xml文件的整合；MyExecute完成了执行和连接的整合，那么谁来完成MapperBean和执行的整合呢？就是SqlSession的MapperProxy实现的。

如此一来，整个Mybatis的流程就通畅了：首先整合好前方的Mapper接口和Mapper.xml文件，让每个crud方法都有合适的sql语句相对应；再整合好后方的连接数据库和在数据库中执行sql语句的操作；最后只需要将中间连接起来，让前方mapper接口的方法可以应用到后方执行语句中就万事大吉了。

MapperProxy类的具体实现如下：

```java
package sqlSession;

import mapper.Function;
import mapper.MapperBean;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.util.List;

/**
 * 动态代理，动态生成MapperBean对象，调用Executor方法。
 * 这个类的核心目的是将MapperBean代理成一个Mapper接口类型的代理对象。
 * MapperBean虽然没有具体实现Mapper接口，但是其内部属性承载了Mapper接口的完整信息（接口全路径、接口方法（应该说是Mapperxml中配置的方法，但是一般xml的方法与接口方法是匹配的））
 * 因此先可以抽象的将MapperBean对象理解成实现了Mapper接口类型的代理对象。这样就方便动态代理了。
 *
 * 这里实现InvocationHandler接口，回顾之前的动态代理机制实现就可以发现，这个InvocationHandler接口是返回代理对象时传入的三个参数的第三个参数，
 * 其作用是运行代理对象方法时，会先来这里运行invoke方法。因此在Mapperproxy中也要实现一下invoke方法
 */
public class MapperProxy implements InvocationHandler {

    private MySqlSession mySqlSession;//想调用Executor方法就得使用SqlSession来执行
    private MyConfiguration configuration;
    private String MapperFile;//


    public MapperProxy(MySqlSession mySqlSession , MyConfiguration configuration,Class clazz){
        this.mySqlSession = mySqlSession;
        this.configuration = configuration;
        this.MapperFile = "mapper/" + clazz.getSimpleName() + ".xml";
    }

    /**
     *
     * 回顾一下之前的动态代理机制实现，在当时做InvocationHandler匿名内部类（核心是类中的invoke方法）时，是插入了前置通知、后置通知，并在两者直接插入了一个method.invoke的反射调用、
     * 当时反射调用时，传入的class类型是实现了接口的bean类。这种情况下可以说为将bean类代理为了其实现接口类。
     *
     * 但是在myBatis中，Mapper接口并没有一个实现类，也就是说，在invoke方法里无法通过method.invoke(mapperImp)来反射接口里的具体方法体，这样就没法做动态代理了吗？
     * 并不是，动态代理，哪怕在InvocationHandler匿名内部类啥也不写也算得到了一个代理对象，不过代理对象的没有执行方法罢了。所以说，广义的动态代理，不用拘泥于
     * 在代理方法里一定要实现接口中的方法，完全可以以接口中的方法为一个判断条件，一旦复合条件了，可以自己定义代理方法是什么。
     * 这里就是将接口中的方法名为判断条件，一旦接口中的方法名和mapperBean中存放的方法名匹配上了之后，就做某个操作（最简单的理解是就做一个sout操作，反正这个操作可以跟接口方法完全无关，不影响他是动态代理）
     *
     * 也就是说，一个接口，哪怕没有实现类，也完全可以实现动态代理，代理为运行类型为接口类型，编译类型为proxy类型的代理对象。
     *
     * @param proxy：代理相关的，底层原生
     * @param method ：动态代理时，代理对象的编译类型为某个接口类型（在MyBatis中为Mapper接口），因此代理时传入的method为mapper接口内部的方法
     * @param args ：方法里的参数列表
     * @return
     * @throws Throwable
     */
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        //1、首先得到“实现了”Mapper接口的mapperBean对象，准备以后代理用
        MapperBean mapperBean = configuration.readMapper(this.MapperFile);

        //2、判断当前代理对象的运行类型（Mapper接口）是否与MapperBean实现的接口相同，如果不相同，代表匹配出问题了，不进行代理方法的调用

        //因为虽然可以抽象的将Mapperbean理解为实现了Mapper接口的对象，但是MapperBean内部存放的方法实际上是Mapper.xml里配置的方法，其并不一定与Mapper接口中的方法完全匹配。
        //如，mapper接口中写上了一个update方法，但是还没有去mapper.xml文件里配置这个方法的方法体，这时就匹配不上了。
        if (!(method.getDeclaringClass().getName().equals(mapperBean.getInterfaceName()))) return null;

        //3、mapperBean中记录了Mapper接口里的所有方法，而反射时是反射其中某一个方法，因此先遍历function，找到对应的方法。
        List<Function> functions = mapperBean.getFunctions();
        if (null != functions && 0 != functions.size()){//先确定mapperBean里的function列表不为空
            for (Function function : functions){//开始遍历
                if (method.getName().equals(function.getFuncName())){//如果mapperBean的function和这里反射的method匹配上了，那就是找对了

                    //之后就可以开始根据function中的信息来确定具体如何反射方法了
                    //这里简化了，直接用类型来判断
                    if ("select".equals(function.getSqlType())){
                        return mySqlSession.SelectOne(function.getSql(),String.valueOf(args[0]));

                    }
                }
            }
        }
        return null;
    }
    
    //4、做一个方法，能够完成Mapper接口和Mapper.xml文件的连接，获取到MapperBean对象，这里通过传入mapper.xml文件路径来作为方法的起点
    public MapperBean readMapper(String MapperXmlPath){
        MapperBean mapperBean = new MapperBean();

        //1、获取到MapperXmlPath的input流
        InputStream stream = loader.getResourceAsStream(MapperXmlPath);

        try {
            //2、解析input流(Dom4j解析)

            SAXReader reader = new SAXReader();
            Document document = reader.read(stream);

            Element root = document.getRootElement();//得到根结点，即<mapper namespace="mapper.MonsterMapper">...</mapper>部分

            //3、得到跟节点的namespce属性，该属性中的内容就是具体mapper接口的全路径，是要保存到MapperBean对象中的
            String namespace = root.attributeValue("namespace").trim();//trim用来防止字符串空格的
            mapperBean.setInterfaceName(namespace);//将全路径保存到MapperBean中

            //4、得到根节点root的迭代器，用来遍历root的子节点（因为一个xml文件中可能写了多种sql语句，因此要全部识别一遍）
            Iterator rootIterator = root.elementIterator();//做一个迭代器
            List<Function> functionList = new ArrayList<>();//做一个集合，用来存放xml文件中配置的sql方法

            while (rootIterator.hasNext()){//开始遍历子节点
                /*
                子节点为这个
                <select id="getMonsterById" parameterType="Integer" resultType="entity.Monster">
                    SELECT * FROM `monster` WHERE `id` = #{id}
                </select>
                 */
                Element element = (Element) rootIterator.next();//每个子节点都是一个Element，因此直接用Element接收。此处element为<select></select>
                Function function = new Function();//先做好Function对象，准备承载遍历到的方法内容

                String sqlType = element.getName().trim();//得到当前节点的节点名——select，而select也就正好对应了sql语句的类型
                String funcName = element.attributeValue("id").trim();//得到当前节点的id属性——getMonsterById，而id属性也就对应的方法名
                String parameterType = element.attributeValue("parameterType").trim();//同理，得到parameterType，即形参类型
                String resultType = element.attributeValue("resultType").trim();//得到返回类型
                String sql = element.getText().trim();//得到当前节点的内容，即具体的sql语句

                //4.5 开始封装
                function.setSql(sql);
                function.setFuncName(funcName);
                function.setSqlType(sqlType);
                function.setParameterType(parameterType);

                //在做Function类时，ResultType是一个Object类型的，而刚刚获取的是String类型的，因此要通过反射做一个resultType的实例对象
                Object o = Class.forName(resultType).newInstance();//由于resultType已经是返回类型的类的全路径了，因此可以直接反射处此类的对象
                function.setResultType(o);

                //4.9将封装好的function对象放入List集合中
                functionList.add(function);
            }

            //5、将刚刚做好的functionList放入MapperBean中，至此，MapperBean的两个属性就算做好了
            mapperBean.setFunctions(functionList);

        } catch (Exception e) {
            e.printStackTrace();
        }
        return mapperBean;
    }
}

```

先看下面的readMapper方法，这个方法实际上也是一个dom4j的解析方法，解析完mapper.xml中的信息用来构建function对象，然后将该function对象和解析的mapper接口全路径共同构建一个MapperBean对象，相当于完成了前方信息的集成。



之后就可以看看核心代码部分——invoke方法。

该方法中实现了前方信息和后方信息的互动。概括来说就是，分析当前代理对象（Mapper接口）的运行的方法是否与MapperBean中存储的方法对应的上，如果对应的上，那么就通过反射执行sqlSession中高级化了的对应的exectrud的CRUD方法（这里简化了，直接从MapperBean类中的Function属性里取出sql语句，放入executor类中的对应方法里执行。但是这样也能更直观的感受到前方和后方的信息交互）。从而完成了前后方的信息连接。



最后看看应用。

### 2.5 run

> 连接测试

首先确保连接数据库能成功

```java
public class test {

    /**
     * 看看连接数据库的功能可不可以正常实现
     */
    @Test
    public void build(){
        MyConfiguration myConfiguration = new MyConfiguration();
        myConfiguration.build("selfMybatis.xml");
        Monster monster = new Monster();
    }
}
```



> executor测试

再确保对数据库执行sql语句能成功

```java
    /**
     * 看看执行器的query方法好用不好用
     */
    @Test
    public void query(){
        MyExecutor myExecutor = new MyExecutor();
        Monster query = (Monster)myExecutor.query("select * from monster where id=?", 1);
        System.out.println(query);
    }
```

这里直接生硬的写一个sql语句尝试执行。



> sqlSession测试

看看SqlSession是否能正常操作数据库

```java
    @Test
    public void SelectOne(){
        MySqlSession mySqlSession = new MySqlSession();
        Monster monster = (Monster)mySqlSession.SelectOne("select * from monster where id=?", 1);
        System.out.println(monster);
    }
```

这一步实际上就是对上一步的进一层封装，没啥多的内部流程。



> 动态代理测试

关键一步，看看动态代理是否能成功，如果成功，就代表可以将信息从前方的配置文件和接口中传入到数据库的执行语句里了。

```java
    @Test
    public void getMapper(){
        MySqlSession mySqlSession = new MySqlSession();
        MonsterMapper mapper = mySqlSession.getMapper(MonsterMapper.class);
        System.out.println(mapper.getClass());//代理类型
        Monster monster = mapper.getMonsterById(1);
        System.out.println(monster);
    }

```



> 最终执行

上面都通了之后，就可以来最后的流程了。

```java
    @Test
    public void sqlSession(){
        MySqlSession mySqlSession = MySessionFactory.openSession();
        MonsterMapper mapper = mySqlSession.getMapper(MonsterMapper.class);
        Monster monster = mapper.getMonsterById(1);
        System.out.println(monster);

    }
```

这里有个SessionFactory，没啥内容，类里只定义了一个openSession来得到一个new的SqlSession对象，实际上getMapper的时候就相当于把全部流程走完了。



## 三、配置细节

之前用的mapper.xml配置文件中，都是最基本的CRUD语句，传入形参单一，返回结果单一。

这里再拓展一下其他配置sql语句时的方法。



### 3.1 常用操作

> 属性占位符

可以传入类型是一个对象，然后通过占位符取出该对象内的某个属性作为查询信息。

```java
    public List<Monster> findMonsterByNameOrId(Monster monster);
```

```xml
    <!--实现方法，findMonsterByNameOrId，这里可以直接通过传入一个对象，然后从对象内取出某些值来作为查询条件-->
    <select id="findMonsterByNameOrId" parameterType="Monster" resultType="Monster">
        SELECT * FROM `monster` WHERE `id` = #{id} OR `name` = #{name}
    </select>
```

这里的`#{id}`和`#{name}`就表示取出Monster对象里的id属性值和name属性值作为查询根据。





> 集合占位符

占位符不止可以占位bean对象的属性，还可以占位集合的key，用来表示集合的value。

```java
    //通过hashMap进行查询，使用HashMap传入参数，可以不局限于对象的
    public List<Map<String,Object>> findMonsterByIdUseHashMap(Map<String,Object> map);
```

```xml
    <!--这里的#{id}用的map里k-v值中的key值-->
    <select id="findMonsterByIdUseHashMap" parameterType="map" resultType="map">
        SELECT * FROM `monster` WHERE `id` > #{id}
    </select>
```





> 模糊查询

比如想查询name里包含某个字的全部数据，就用到模糊查询。

```java
    public List<Monster> findMonsterByName(String name);
```

```xml
    <!--模糊查询时，需要用${value}取值-->
    <select id="findMonsterByName" parameterType="String" resultType="Monster">
        SELECT * FROM `monster` WHERE `name` LIKE '%${name}%'
    </select>
```

模糊查询时，首先需要在具体被查信息左右用`%**%`标记起来，然后如果是取某个bean对象里的某个属性，则该属性用`${}`包起来。



### 3.2 动态查询

在myBatis里做查询，是可以将各种条件控制语句应用进去的，下面一一举例。



> if

需求如下：

查询所有age大于某个数的对象，若输入的age不大于0，则输出所有对象。这里多了个条件是”如果“。

```java
public List<Monster> findMonsterByAge(@Param("myage") Integer age);
```

这里有个细节提一嘴，在接口的形参列表中用了`(@Param("age") Integer age)`之后，`@Param("myage")`中的myage就是该方法对应的sql语句里严格意义上的输入了，因此需要用到形参的地方都需要用myage指代。



相应的xml配置实现为：

```xml
  <!--这里使用一个逻辑来完成查询所有age大于某个数的对象，若输入的age不大于0，则输出所有对象的目标：-->
    <!--首先全部输出出来（给where后面赋值一个true），然后做一次判断（myBatis特有的，<if>标签）判断中如果age>0了，那么就多加一个条件叫age>XX，这样一来，条件就缩小到age>这里了-->
    <!--但是有一点需要注意，在标签里，是无法使用占位符的(如果是对象属性的映射是可以用的)，而解决办法是去接口的方法中使用注解——@Param来标注一下形参-->

    <select id="findMonsterByAge" resultType="Monster" parameterType="Integer">
        SELECT * FROM `monster` WHERE 1 = 1
        <if test="myage >= 0" >
            AND age > #{myage}
        </if>
    </select>
```

具体实现细节看注释即可。



> where

需求如下:

查询id>20的并且名字为jack的所有人，如果查询的名字为空，那么条件就不加上名字为jack的了，只查id>20的人；同理，如果id输入为空，那就只查jack。

```java
public List<Monster> findMonsterByIdAndName(Monster monster);
```



相应的xml配置实现为：

```xml
<select id="findMonsterByIdAndName" resultType="Monster" parameterType="Monster">
        SELECT * FROM `monster`
        <where>
            <if test="id >= 0">
                AND `id` > #{id}
            </if>
            <if test="name != null and name != ''">
                AND `name` = #{name}
            </if>
        </where>
    </select>
```

这里说一个细节，在两个if语句中都加入AND，如果两个if语句都满足了，虽然现在看来会在一条sql语句里有两个and，但是mybatis会删除多余的and，让语句通顺。

实现思路简单，看看就知道了。



> choose

需求如下：

如果给的name不为空，则按name查询；如果给的id>0则按id查询；如果两个都不满足，则按salary>100查询。

```java
public List<Monster> findByChoose(Map<String,Object> map);
```



相应的xml配置实现为：

```xml
<select id="findByChoose" parameterType="map" resultType="Monster">
        SELECT * FROM `monster`
        <choose>
            <when test="myName != null and myName != ''">
                WHERE `name` = #{myName}
            </when>
            <when test="myId > 0">
                WHERE `id` > #{myId}
            </when>
            <otherwise>
                WHERE `salary` > 10
            </otherwise>
        </choose>
    </select>
```

也是一眼懂的思路，sql语句会选择choose标签下的一个`when`的通的语句执行，如果所有`when`都不通，那么就执行`otherwise`。



> foreach

需求如下：

查询id为11，14，20的人

```
public List<Monster> findByForeach(Map<String,Object> map);
```



相应的xml配置实现为：

```xml
<select id="findByForeach" resultType="Monster" parameterType="map">
        SELECT * FROM `monster`
        <if test="ids != null and ids != ''">
            <where>
                `id` IN
                <foreach collection="ids" item="id" open="(" separator="," close=")">
                    #{id}
                </foreach>
            </where>
        </if>

</select>
```

collection="ids"表示形参输入为ids；item为遍历ids的每次结果，赋值为id；open表示从哪开始、separator表示中间用什么分隔、close表示结束标志。

乍一看有点抽象，下面举个实例：

假设map里的最终实参为：(11,14,20)，那么要是静态sql语句，则为：`SELECT * FROM monster WHERE id IN(11,14,20)`

动态查询的最终目的是组成上面的静态查询语句。

首先`SELECT * FROM monster`是不变的，直接拿来用，然后进入if判断，判断当ids不是空的时候，就进入where标签里，此时动态查询就将`where id In`部分组合上去了，之后进去foreach循环，遍历`(11,14,20)`，逐个取出来组合到后面，得到最终结果。



> set

需求如下：

对指定id进行修改，如果没有设置新的属性，则保持原来的值。

```java
public void updateBySet(Map<String,Object> map);
```



相应的xml配置实现为：

```java
<update id="updateBySet" parameterType="map">
        UPDATE `monster`
        <set>
            <if test="myAge != null and myAge != ''">
                `age` = #{myAge}
            </if>
            <if test="myEmail != null and myEmail != ''">
                `email` = #{myEmail}
            </if>
        </set>
        WHERE `id` = #{myId}
</update>
```

这里是update标签，表示修改，并且只修改set标签下满足if标签部分的内容。





## 四、resultMap

resultMap是用来代替单一的返回结果集（resultType）的。虽然resultType可以指定多种类型的返回结果，如返回Integer、String、或者某个Bean对象等等，但是依旧是不够用的，其无法处理更复杂的场景，这时就需要用到resultMap了。



### 4.1 简单应用

先看一个复杂场景里相对简单的应用。

在实际使用sql语句时，不能保证某个bean类的属性名和表的字段名是一致的，如果盲目的返回表的字段信息可能会导致无法实例化该表对应的bean类对象。如：

```xml
<select id="findAllUser" resultType="User">
    SELECT * FROM `user`
</select>
```

如果User类的属性名为:`username，userid`，而表的字段名为`user_name，user_id`，那么返回的查询结果就会以表的字段名来尝试创建User对象，导致User对象的username属性和userid属性为null。



而为了处理这种情况，就可以使用resultMap来进行优化：

```xml
    <resultMap id="ResultMapfindAllUser" type="User">

        <!--这里就表示表的字段和类的属性的对应关系了，column表示表的字段，property表示将当前column代表的值转为property代表的值-->
        <result column="user_name" property="username"/>
        <result column="user_email" property="useremail"/>
    </resultMap>

    <!--之后这里的resutlType就可以指定出刚刚的resultMap的id来对应上了-->
    <select id="findAllUser" resultType="ResultMapfindAllUser">
        SELECT * FROM `user`
    </select>
```

这里做一个resultMap，其类型是需要返回的Bean类型（代替resultType来指向对应的bean类），其内部则用多个`result`标签来分别将字段名和属性名一一对应上。最后在真正执行sql的标签——select标签里的resultType中指向一下这个resultMap的id就行了。



### 4.2 一对一表

刚刚是简单的resultMap标签的应用，现在看看其核心使用方式之一——表的一对一映射时的使用。

现在有两个bean类如下：

```java
/**
 * 这里做一个Person，其内部属性需要用到身份证信息（IdenCard）
 * 其对应的表为
 * id、name、card_id
 */
public class Person {
    private Integer id;//人物序列号
    private String name;//人物名字
    private IdenCard card;//人物身份证
}
```

```java
/**
 * 这里做一个身份证表，其包含身份证具体号和身份证序列号.
 * 其对应的表为
 * ：id、card_sn
 */
public class IdenCard {
    private Integer id;//序列号
    private String card_sn;//id号
}
```

可以看出，person和idcard是有一个一对一的关系的，即每个person中都有一个idcard属性。



在只查询idCard时很简单，通过id表的序列号直接查询就能得到序列号对应的id号：

```java
public IdenCard getIdenCardById(Integer id);
```

```xml
    <!--实现通过序列号得到身份号的方法-->
    <select id="getIdenCardById" parameterType="Integer" resultType="IdenCard">
        SELECT * FROM `idencard` WHERE `id` = #{id}
    </select>
```

这是因为构建idenCard对象时，不需要用到idCard表之外其他表的任何字段属性，所以可以直接根据查询此表的结果返回一个resultType=`idenCard`的结果。但是构建Person对象时就不能这么简单了，因为如果想构建一个person对象，就需要得到一个idCard对象的完整信息，而这个信息时person表中查不出来的，得去idcard表查。

因此就需要用到resultMap来解决这个问题了。

```java
public Person getPersonById(Integer id);
```



传统写法：

```xml
    <select id="getPersonById" parameterType="Integer" resultType="Person">
        SELECT * FROM `person` WHERE `id` = #{id}
    </select>
```

这里有一个细节，如果返回结果设置成——resultType="Person"，那么就无法将Person里的IdedCard属性赋值（会赋值为null）,导致最后getPersonById方法返回的对象里,card属性是null。

这里说明一个事情，这种传统写法是可以查到Person的card_id，但是其问题是无法将查到card_id赋值到返回的Person对象里的card属性上。



> 优化一

使用resultMap:

```xml
<resultMap id="PsersonResultMap" type="Person">
        <!--前两个属性可以简单的做一下类属性和表字段的映射,因为其属性是独立的,不包含其他内容-->
        <result property="id" column="id"/>
        <result property="name" column="name"/>

        <!--而card属性则不能用result标签来做映射了,因为该属性涉及到另一个表,所以column用不了.这里得用association标签
            在association标签里,property仍然是当前resultMap标签的type属性所指向对象的某个属性,与result标签不同的是,这里用javaType给该属性赋值了-->
        <association property="card" javaType="IdenCard">
            <!--而这里配的属性则是javaType所指向的对象的属性,即idenCard的属性,可以理解为一种依赖注入,即在一个对象的属性里配置另一个对象-->
            <result property="id" column="id"/>
            <result property="card_sn" column="card_sn"/>
        </association>
</resultMap>

    <select id="getPersonById" parameterType="Integer" resultType="PersonResultMap">
        SELECT * FROM `person` , `idencard` WHERE `person`.id = #{id} AND `person`.card_id = `idencard`.id
    </select>
```

多表联查。使用多表查询，根据person的id查person，但是先将两表进行拼接，并且AND后加入`person.card_id = idencard.id`条件来克服笛卡尔集的情况。

resultMap则做为Person对象的映射，首先将id、name做一个简单的属性和字段的匹配，因为其不涉及到Person之外的东西，因此直接用result标签即可。

重点在于association标签里，在association标签里,property仍然是当前resultMap标签的type属性所指向对象的某个属性,与result标签不同的是,这里用javaType给该属性赋值了。如此处`<association property = card javaType=IdenCard`，表示给Person对象的card属性赋值为IdenCard。

而IdenCard的具体内容，就为`<association>`标签里的各个result表示的属性。`<result property="card_sn" column="card_sn"/>`就表示，IdenCard对象的card_sn属性对应的为查找结果的card_sn列，这个列是根据多表联查得到的idCard表的列。

如此一来就完成了Person对象的赋值。



> 优化二

将多表联查转为单表操作。

```xml
<resultMap id="PersonResultMap2" type="Person">
    <result property="id" column="id"/>
    <result property="name" column="name"/>

    <!--这里改变了association的使用方式，将Person类中的card属性赋值操作交给mapper.IdenCardMapper.getIdecCardById这个方法，-->
    <!--即通过"SELECT * FROM `person` WHERE `id` = #{id}"查到了person表里的card_id字段对应值，并将该值作为实参传入"mapper.IdenCardMapper.getIdecCardById"中-->
    <!--将"mapper.IdenCardMapper.getIdecCardById"的返回值作为card属性的赋值。-->
    <association property="card" column="card_id" select="mapper.IdenCardMapper.getIdecCardById"/>
</resultMap>
<select id="getPsersonById2" parameterType="Ingeger" resultMap="PersonResultMap2">
    SELECT * FROM `person` WHERE `id` = #{id}
</select>
```

这个是最常用的优化方式，在一个查询里使用另一个查询，主查询为`select`标签里的语句，还有个副查询放入`resultMap`标签中进行查找。

首先在select标签里做一个简单的select查询，明显此时查询结果中是没用idcard属性的值的，这个部分通过`resultMap`来得到。其他的属性是可以通过该select得到的，但是其赋值也放入resultMap里操作。

在`resultMap`里，首先将主表内和主对象内的相应的信息做匹配，即person表和person对象中的id、name匹配一下先。

然后进入需要联动的idcard属性上，该属性赋值时，是通过一个副查询去idcard表中进行的，其流程如下：首先还是做一个`association`标签，该标签是为Person的card属性赋值，而赋值内容则是取出person表中欲查询的id对应的card_id字段信息作为实参，拿到`mapper.IdenCardMapper.getIdecCardById`这个方法中进行查找，将查找得到结果赋值个card属性即可。

而`mapper.IdenCardMapper.getIdecCardById`是一个接口方法的全路径，刚刚在idCard的mapper中是写了的，并且也有相应的xml配置进行实现，故可以直接直接拿来用了。

如此一来，就相当于在一个xml配置信息里调用了另一个xml配置信息（在一个mapper接口方法中调用了另一个Mapper接口方法），实现多表转单表的操作。



### 4.3 多对一表

现有bean类如下：

```java
/*
这里的多对一则用案例表示为：一个主人可以有多只宠物。即若干个pet表里的数据都指向同一个user。
 */
public class User {
    private Integer id;
    private String name;
    private List<Pet> pets;
}
```

```java
public class Pet {

    private Integer id;
    private String nickname;

    private User user;
}
```

这里是多个Per的User属性可以是同一个，即多对一。

这两个类是相互关联的，跟刚刚的Person和Idcard不一样，刚刚的Idcard是自己独立的，而Person单向的跟Idcard有关系。但是这里是User中有Pet属性、Pet中有User属性，是双向相关的。



现有查询需求如下：

```java
//根据userid查找该user
public User getUserById(Integer id);
```

```java
//根据传入的userid返回该属于该user的pets
public List<Pet> getPetByUserId(Integer userId);
```



看看两者的分别实现：

```xml
<mapper namespace="mapper.UserMapper">

    <resultMap id="getUserByIdResultMap" type="User">
        <!--无注入的属性直接从表中取值就行-->
        <result property="id" column="id"/>
        <result property="name" column="name"/>

        <!--由于pets属性是一个集合,集合使用collection标签来处理
        这里比之前学association标签时多了个 ofType属性,其表示,返回的集合属性中,要存放的数据的数据类型,即privite List<Pet> pets;中List里的Pet-->

        <!--通过SELECT * FROM `user` WHERE `id` = #{id}得到一条user记录,而user记录里的id属性对应了pet表里的user_id属性,故将其作为实参传入-->
        <!--PetMapper.getPetByUserId方法里,通过该方法返回若干条pet记录并赋值给user类里的pets属性-->
        <collection property="pets" column="id" ofType="Pet" select="mapper.PetMapper.getPetByUserId"/>
    </resultMap>
    <select id="getUserById" parameterType="Integer" resultMap="getUserByIdResultMap">
        SELECT * FROM `user` WHERE `id` = #{id}
    </select>
</mapper>
```

```xml
<mapper namespace="mapper.PetMapper">
    <resultMap id="getPetByUserIdResultMap" type="Pet">
        <result property="id" column="id"/>
        <result property="nickname" column="nikename"/>

        <!--这里一个pet只对应一个User,因此使用association;而一个User对应多个pet,所以使用collection-->
        <!--这里的select实际上是双向使用的,Usermapper那边select用的是petMapper里的方法,这里的select使用的是usermapper的方法-->

        <!--通过SELECT * FROM `pet` WHERE `user_id` = #{userId}查出一条pet记录,这条pet记录里有user_id这个属性,与user表里的id是一致的,-->
        <!--因此使用user_id属性作为实参传入userMapper里的getUserById方法,从而得到一条user记录并将其返回给此处的association,将其赋值到pet类里的user属性-->
        <association property="user" column="user_id" select="mapper.UserMapper.getUserById"/>
    </resultMap>
    <select id="getPetByUserId" parameterType="Integer" resultMap="getPetByUserIdResultMap">
        SELECT * FROM `pet` WHERE `user_id` = #{userId}
    </select>
</mapper>
```



这里有疑问，逻辑没理清，可能会出现如下问题？（不知道会不会，视频里没事，但是逻辑上好像会有这个问题）

调用 mapper.PetMapper.getPetByUserId 方法时会触发对 mapper.UserMapper.getUserById 的调用，而后者又会反过来调用 mapper.PetMapper.getPetByUserId。







## 五、缓存

默认情况下，myBatis启动的是一级缓存（本地缓存），它是SqlSession级别的（会话级别的），也就是说，如果这个会话没有关闭，一级缓存就一直存在。

当启动了一级缓存后，同一SqlSession接口对象调用了相同的select语句后，会直接从缓存里获取，而不再从数据库里重新查找了。因为操作DB的本质实际上是网络操作，每次访问都需要进行http的网络传输（计网的流程），会导致速度相对慢一点。而直接从一级缓存获取相当于从本地获取，省去了网络连接的过程，打打加快访问速度。



二级缓存则相比一级缓存来说，作用域变大了。一级缓存只用于会话级别；而二级缓存则应用于全局，针对不同的会话都有效。

myBatis进行缓存查找的流程为：先找二级缓存；如果二级缓存没有了再找一级缓存；一级缓存也没有了就去数据库里取



命中率问题，命中率是相对二级缓存来说的，查找一个信息，记录二级缓存的总此次与从二级缓存中查出该信息的此处，相除就是命中率。命中的只有是从二级缓存中得到的信息，如果是从一级缓存或者从数据库中得到的信息，算是未命中。



执行顺序

设目前二级缓存、一级缓存都打开了。当执行第一次查询时，发出sql语句从数据库获得数据，之后将数据存放在一级缓存中。如果此时将一级缓存关闭，那么一级缓存中的数据会被存放在二级缓存中。而并不会存在一级缓存与二级缓存同时存在同一个数据的情况，数据只有将一级缓存关闭了之后，才会放入二级缓存中

 





