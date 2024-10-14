# Web

## 一、ES6

 ECMAScript 6.0 ,是 JavaScript 的下一个版本标准， 增加了新的语法特性，以达到让 JavaScript 语言可以用来编写复杂的大型程序，成为企业级开发语
言的目的

ECMAScript 和 JavaScript 的关系：ECMAScript 是 JavaScript 的规范/规则，JavaScript 是ECMAScript 的一种实现

### 1.1 ES6新规范

#### 1.1.1 let

`let`关键字可以一定程度上代替`var`关键字，是ES6规定的规范。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Es6Out</title>
    <script type="text/javascript">
        var VarName = "var的使用"
        let LetName = "let的使用";//ES6是一种javaScript的规范，如ES6中规定了let可代替var来标记变量
        console.log("name",VarName);
    </script>
</head>
<body>

</body>
</html>
```

但是let和var有一定的区别



1、let 声明的变量有严格局部作用域

let声明的变量如果在代码块中，则只可在代码块中使用；var声明的变量如果在代码块中，则全局可用该变量

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Es6Out</title>
    <script type="text/javascript">
        {
            var varname = "varname";
            let letName = "letname";
            console.log("varname");//可以
            console.log("letname");//可以
        }
        console.log("varname");//可以
        console.log("letname");//不可以
    </script>
</head>
<body>

</body>
</html>
```



2、let 只能声明一次, var 可以声明多次

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Es6Out</title>
    <script type="text/javascript">
        {
            var var2 = "var2";
            var var2 = "var22";//可以，相当于下面的var2覆盖掉上面的var2

            let let2 = "let2";
            //let let2 = "let2";//不可以，let只能声明一次,声明后var也不能再声明这个变量了
        }
        console.log("varname");//可以
        console.log("letname");//不可以
    </script>
</head>
<body>

</body>
</html>
```



3、let 不存在变量提升, var 存在变量提升。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Es6Out</title>
    <script type="text/javascript">
        {
            console.log(var3);//如果不定义下面的var3，只有这一行，则会报错为not defined
            var var3 = "var3";//一旦定义在了使用的下面，则报错会从not defined变为 undefund。即从没被定义变为了未找到，即此时编译器已经认为这个变量被定义过了
            //但是let不能，let不管后面有没有补充定义，都会报错can't access lexical declaration XXX before initialization。即不给你提升的机会
        }
    </script>
</head>
<body>

</body>
</html>
```



#### 1.1.2 const

const相当于后端的常量，定义一个不再改变的量

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>const</title>
    <script type="text/javascript">
        //const相当于前端的常量，用来定义一个不再改变的量
        const pi = 3.14;

        /**
         * 细节1，常量在定义时，必须赋值
         */
        //const pi1 ;//此时会报错，让你赋值

        /**
         * 细节2，常量定义后不可再改变
         */
        //pi = 3.15//报错
    </script>
</head>
<body>

</body>
</html>
```



#### 1.1.3 解构赋值

解构赋值是对赋值运算符的扩展，是一种针对数组或者对象进行模式匹配，然后对其中的变量进行赋值。主要有两种形式： 数组解构和对象解构

解构就是说将一个封装起来的东西里面的某个物件取出，赋值就是给这个物件赋个值。

> 数组结构

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>解构赋值</title>
    <script type="text/javascript">
        /**
         * 数组解构
         */
        //定义一个数组
        let arr = [1,2,3];
        
        //传统解构
        let x = arr[0], y = arr[1], z = arr[3]
        
        //ES6定义的解构
        let [a,b,c] = arr;
        let [n1,n2,n3] = [100,200,300];//一个道理，就是将定义arr和ES6解构结合在一起了。前面的let不是重点，var也可以
    </script>
</head>
<body>

</body>
</html>
```



> 对象解构

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>解构赋值</title>
<script type="text/javascript">
        /**
         * 对象解构
         */
        let monster = {name:"jack",age:18};//定义一个对象

        //传统解构
        let name = monster.name;
        let age = monster.age;

        //ES6的解构
        let{name1 , age1} = monster;
        //ES6解构得注意，let定义的属性要和对象里的属性一一对应，即monstre里有name属性，则Es6的接受属性名得是name，但是大括号里的顺序无所谓，不过一般都是按顺序一一对应的来
        //解构对象时，要用大括号包住，跟数组用中括号包住不同。

        
        //在有了这种规范后，就可以更方便的使用方法传参了
        function f({name,age}) {

        }
        f(monster)//此时可以直接传入monseter对象进去，让其在形参里进行解构匹配

    </script>
</head>
<body>

</body>
</html>
```



#### 1.1.4 模板字符串

模板字符串使用反引号 ` 将字符串包裹，其可作为普通字符串，并且可用来定义多行字符串，即可以将换行字符串原生输出；

字符串插入变量和表达式，插入时使用EL表达式—— ${}；

字符串中也可也调用函数，调用方式也是通过${}。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>模板字符串的使用</title>
    <script type="text/javascript">
        //模板字符串使用反引号 ` 将字符串包裹
        //模板字符串内部，可以随意换行，不需要拼接符
        var str = `for(int i = 0; i < 10; i++){
            sout("1");
        }`;

        //模板字符串中可以插入变量和表达式
        let name = "jack";
        let str1 = `学生名称为=${name}`//此时会找最近的name变量，进行赋值，然后得到可以解析的字符串。如果找不到这个变量，则会视为空来放入字符串中，并不报错

        let str3 =`1+2=${1+2}`;//插入表达式时也用${}来添加，并且其在内部直接计算
        
        
        //模板字符串中可以调用函数
        function f(name) {
            return name;
        }
        let str4 = `方法调用的结果为=${f(name)}`;//道理和上面的一样，调用离$最近的f方法，并向其内部传入这个实参，这里进阶一下的话，实参也可也做一个变量，去找离name最近的变量值

        console.log(str);
    </script>
</head>
<body>

</body>
</html>
```



#### 1.1.5 对象简写

> 对象定义的简写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>对象的Es6特性</title>
    <script type="text/javascript">
        const name = "jack";
        const age = 18;

        //传统对象声明
        let people = {name:name,age:age};//属性name:常量name, 属性age:常量age

        //ES6声明对象
        let people1 = {name,age};//此时，对象people1的属性就叫做name和age，其值是从本代码中找一个最近的属性名字为name和age的来匹配
        //这个属性一定要保证有的匹配才行，即前面必须存在name和age才行
    </script>
</head>
<body>

</body>
</html>
```



> 对象方法的简写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>对象的Es6特性</title>
    <script type="text/javascript">
        /**
         * 对象方法的简写
         */

        //传统的对象方法定义
        let people2 = {
            name:"tom",
            age: 20,

            //定义对象方法
            sayHi:function () {
                console.log(this.age,this.name);
            }
        }

        //ES6的对象方法定义
        let people3 = {
            name:"tom",
            age: 20,

            //定义对象方法，可以把冒号和function去掉
            sayHi(){
                console.log(this.age,this.name);
            }
        }
    </script>
</head>
<body>

</body>
</html>
```



> 对象运算符扩展

深拷贝操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>对象的Es6特性</title>
   <script type="text/javascript">
        /**
         * 拷贝操作
         */
        //传统的对象拷贝，是浅拷贝（两个变量名指向同一个内存空间），cat2也指向和cat同样的空间，cat2改变的话cat也会跟着改变
        let cat = {name:"大花猫"};
        let cat2 = cat;
        cat2.name = "小花猫"

        //ES6规定了深拷贝（两个变量名指向两个不同的内存空间）的方法
        let cat3 = {...cat};//用这种语法来完成深拷贝
        cat3.name="大白猫";//此时不再影响cat的name属性了
    </script>
</head>
<body>

</body>
</html>
```



对象合并操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>对象的Es6特性</title>
   <script type="text/javascript">
        /**
         * 对象合并操作
         */
        //ES6提供了对象合并的规范
        let monset1 = {name:"牛魔王",age:100};
        let monset2 = {hobby:"eat"};
        // let monset2 = {name:"白骨精",age:80};//如果两个欲合并的对象属性名称相同，则后一个对象的属性会覆盖掉前一个对象的属性

        let monset = {...monset1,...monset2};//合并后新对象是独立的对象，指向自己的存储空间。底层道理还是深拷贝拷贝来的
        monset1.age=120;//此时并不影响monset的属性
        console.log(monset)
    </script>
</head>
<body>

</body>
</html>
```



#### 1.1.6 箭头函数

箭头函数提供了一种更简洁的函数书写方式，其基本语法是`变量名 = (参数列表)=>{函数体}`；

箭头函数没有参数或有多个参数，要用 () 括起来，而如果箭头函数只有一个参数, 可以省略()；

箭头函数函数体有多行语句，用 {} 包裹起来，表示代码块；

函数体只有一行语句，并且需要返回结果时，可以省略 {} , 结果会自动返回；

箭头函数多用于匿名函数的定义，即只使用一次的函数。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>箭头函数</title>
    <script type="text/javascript">
        //传统的函数定义
        var f1 = function (n) {
            return n * 2;
        }

        //箭头函数的定义方式
        let f2 = (n) => {
            return n * 2;
        }
        //由于此方法的形参只有一个(可以省去形参列表的小括号)，并且方法体只有一条而且需要返回（可以省去方法体的大括号和return），故可以简写如下
        let f3 = n => n * 2;//由此就可以拓展，将箭头函数当作一个实参传入某个方法中
        let f4 = function (m) {
            m(100);//形参列表里的m，不是一个值，而是一个方法，这个方法接受一个值是100，而至于这个方法是什么，则看调用f4的方法向里传什么
        }
        f4(n => n + 100);//此时把整个箭头函数传入f4中，即此时f4的形参m就是这个箭头函数，然后m(100)相当于运算100+100了
    </script>
</head>
<body>

</body>
</html>
```



### 1.2 Promise

 一句话: Promise 是异步编程的一种解决方案, 可以解决传统 Ajax 回调函数嵌套问题， Promise 也是 ES6 的新特性。

传统的 Ajax 异步调用在需要多个操作的时候，会导致多个回调函数嵌套，导致代码不够直观，就是常说的 Callback Hell，为了解决上述的问题，Promise 对象应运而生，在 EMCAScript 2015 当中已经成为标准。

Promise 是异步编程的一种解决方案。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。



### 1.3 模块化编程

传统非模块化开发有如下的缺点：(1)命名冲突 (2)文件依赖

Javascript 代码越来越庞大，Javascript 引入模块化编程，开发者只需要实现核心的业务逻辑，其他都可以加载别人已经写好的模块。

Javascript 使用"模块"（module）的概念来实现模块化编程, 解决非模块化编程问题。

#### 1.3.1  CommonJS 模块化规范/ES5 的写法

在ES5中，每个 js 文件就是一个模块，有自己的作用域。在文件中定义的变量、函数、类/对象，都是私有的，对其他 js 文件不可见。

CommonJS 使用 `module.exports={} / exports={}` 导出模块 , 使用 `let/const 名称 = require("xx.js")` 导入模块。

```js
function.js：对象、函数、变量、常量...

//导出模块
module.exports = {
    对象,
    函数,
    变量
}
```

```javascript
use.js
//导入模块
let functionUse = require("function.js");//此时，就将function的exports出来的内容保存到了functhionUse变量中
```



> 实例使用

function.js

```js
//定义对象、变量、函数等等，并导出
const sum = function (a,b){
    return a + b;
}

const sub = function (a,b){
    return a - b;
}

let name = "jack";

const Dog = {
    name:"大黄",
    age:3,
    hi() {
        console.log("hi~");
    }
}

//导出，以对象的形式导出
module.exports = {
    mySum:sum,
    mySub:sub,
    myName:name,
    myDog:Dog
}
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Html引用js文件</title>

    <!--直接导入包就行-->
    <script type="text/javascript" src="_01_function.js"></script>
</head>
<body>

</body>
</html>
```



```js
const m = require("./_01_function");//此时m就已经是function导出的对象了

console.log(m.myDog);
console.log(m.myName);
console.log(m.mySub(1,1));
console.log(m.mySum(1,1));
```

 

#### 1.3.2 ES6



## 二、Vue

Vue 是 Vue.js 的简称，是一个前端框架, 易于构建用户界面；

 Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或项目整合；

支持和其它类库结合使用，开发复杂的单页应用非常方便；



### 2.1 简单入门

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue入门</title>
</head>
<body>

<!--简单写个标签-->
<div id="app">
    <!--{{}}插值表达式，里面的内容是从数据池里获取，如message就是存放在数据池里的信息，如果没有匹配上则为空（如最后asdf并没有进数据池）-->
    <h1>hello{{message}}，hello{{name}}，{{asdf}}</h1>
</div>

<!--引入vue-->
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">
    //创建vue对象
    let vm = new Vue({
        el:"#app",//将创建的vue实例挂载到id="app"的标签上，即让vm这个vue对象与标签id为app的标签关联上

        data:{//data表示model的数据池，内部可以存放很多数据，以key-value形式存储，具体什么key什么v根据情况来定
            message:"Vue!",//向数据池里存放这组数据
            name:"Vue~"//向数据池里存放这组数据
        }
    })

    console.log(vm);//vm是一个vue对象，其内部是有一个属性：_data，就是数据池，可以单独取出
    console.log(vm._data.message,vm._data.name);//不通过{{}}来调取数据池的话，也可也这样直接调取数据池里的内容

    //对于数据池里的数据，还可以通过vue的特性进阶读取，vue将数据池里的数据也单独构建了一下，可以通过vue对象加数据池key直接的数据池value
    console.log(vm.name,vm.message);


</script>


</body>
</html>
```

使用vue最直观的感受就是，浏览器显示的数据完全不用在标签里写了，而是写到vue对象里，完成分离。

> 注意事项

1、写vue代码时，要注意被挂载的标签在上，挂载标签的vue对象在下。

2、一般来说，所有标签都可以挂载vue，但是通常来说都用div来挂载vue，因为div是个容器，更方便使用。

3、id取名任何名都行，但是一般都用`app`标签来绑定vue

4、两个标签不能同时挂载一个vue。

5\`{{}}`是插值表达式,其只应用于标签的标签体内,不能用于标签的属性栏里:

```html
<img src="{{}}"></img>;//错误使用,会识别不到
<img>{{}}</img>;//正确使用
```



### 2.2 数据绑定

#### 2.2.1 单项绑定

单向绑定,指的是model部分绑定view部分,即vue对象里的数据单方面决定div标签里的各个属性

在使用图片时，向vue对象里做属性，一般都是`属性名：图片地址`，如果在div里使用插值表达式，会无法正常展示图片，此时就需要用渲染来完成了。

渲染一般使用v-bind语句。

v-bind语句是用于标签的属性体内的,这点不同于插值表达式，使用v-bind时，只需要在需要的属性前加上`v-bind:`即可

```vue
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml"><!--引入命名空间,解决v-bind报红事件,不引也行-->
<head>
    <meta charset="UTF-8">
    <title>单向数据绑定</title>
    <div id="app">
        <h1>{{message}}</h1>
        <!--<img src="{{img_src}}">这里不能这样使用，因为插值标签所处的位置应该时标签体内，而这里是在属性体内了,属性体内用v-bind方法-->
        <img v-bind:src="image_src" v-bind:width="image_width">//用v-bind标记上width属性，让其可以使用vue对象里的数据池数据

    </div>
</head>
<body>
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">
    let vm = new Vue({
        el:"#app",
        data: {
            message:"hellovue",
            image_src:"./srouce/1.jpg",
            image_width:"200px"
        }
    })

</script>
</body>
</html>
```



v-bind是数据池里的数据影响div里的数据，而div的数据不会影响到数据池。如果想让两者相互关联，则需要双向绑定。

#### 2.2.2 双向绑定 

 双向绑定就顾名思义了，数据池里的东西会影响div里的、反过来div里进行修改（在前端界面进行修改）也会影响数据池里的信息。

双向绑定使用关键字`v-model`

```vue
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml" xmlns:v-model="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>双向数据绑定</title>
    <div id="app">
        <h1>{{message}}</h1>
        <!--v-model是双向绑定的方法,用该方法渲染的属性,其值和数据池里的值是双向影响的,前端的数据改变,会同时改变数据池里的数据-->

        <!--第一个input是双向绑定,第二个input是单项绑定,如果改变第一个input,会发现第二个也随之改变,但是改变第二个不会影响第一个.-->
        <!--因为改变第一个后,根据双向绑定,数据池的值也随之改变,而数据池的值一旦变了,单项绑定的值也会变-->
        <input type="text" v-model:value="hobby.val"><br/><br/>
        <input type="text" v-bind:value="hobby.val"><br/><br/>

        <p>你输入的爱好是:{{hobby.val}}</p>

    </div>
</head>
<body>
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">

    let vm = new Vue({
        el:"#app",
        data:{
            message:"输入爱好",
            hobby:{
                val:"购物"
            }

        }
    })
</script>

</body>
</html>
```



###  2.3 事件绑定

之前的单项双向绑定都是针对的数据池里的数据，事件绑定实际上就是将某个属性绑定到某个事件上，这个事件则存在于vue对象的方法池里，是一个具体的方法。

#### 2.3.1 v-on

使用 v-on 进行事件处理，比如: `v-on:click` 表示处理鼠标点击事件。事件调用的方法定义在 vue 对象声明的 methods 节点中，也即方法池中。

```vue
<!DOCTYPE html>
<html lang="en" xmlns:v-on="http://www.w3.org/1999/xhtml" xmlns:>
<head>
    <meta charset="UTF-8">
    <title>事件绑定</title>
    <div id="app">
        <h1>{{message}}</h1>
        <!--使用v-on方法来将click事件与vue的方法池绑定上-->
        <button v-on:click="sayHi()">点击输出</button>
        <button v-on:click="sayHei()">点击输出</button>
        <button v-on:click="sayOk()">点击输出</button>
        <button @click="sayOk()">点击输出</button><!--简写,将v-on:全去掉,使用@代替(有的浏览器不支持)-->

        <button onclick="butClick()">点击输出</button>

    </div>
</head>
<body>
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">
    function butClick() {
        console.log("传统事件绑定")
    }

    let vm = new Vue({
        el:"#app",
        data:{
            message:"vue事件处理",
            name:"vue"
        },
        methods:{//vue的methods属性,对应的value是一个对象,对象里可以写若干方法,即methods是一个方法池(与data的数据池对应)
            sayHi:function () {//在方法池里添加一个方法
                console.log("hi");
            },

            sayHei(){//再添加一个,用简写的方式
                console.log("hei")
            },
            sayOk(){
                console.log("ok")
            }

        }

    })
</script>

</body>
</html>
```





#### 2.3.2 v-if、v-show

vue中也是可以进行true和false的判断的，这个操作可直接在前端界面进行，使用`v-if`关键字即可。这是一种条件渲染语句。

还有一个绑定词也有类似的效果——`v-show`，但是两者是有细节上的差别的，下面介绍。

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>条件绑定语句</title>
    <div id="app">
        <input type="checkbox" v-model="sel">是否同意条款(v-if实现)
        <h1 v-if="abc">test</h1><!--这里给此h1标签绑定一个vif，vif对应的值是abc，当运行时，编译器会去数据池里找key为abc对应的value，若为：null、undefi则表示false-->
        <!--而此时数据池里确实没有abc这个key，故v-if的结果是false，则不显示这条h1标签-->
        <h1 v-if="sel">你同意条款</h1>
        <h1 v-else>你不同意条款</h1>


        <input type="checkbox" v-model="sel">是否同意条款(v-show实现)
        <h1 v-show="abc">test</h1><!--道理和v-if差不多-->
        <h1 v-show="sel">你同意条款</h1>
        <h1 v-show="!sel">你不同意条款</h1>

    </div>
</head>
<body>
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">
    let vm = new Vue({
        el:"#app",
        data:{
            sel:false,


        },
        methods:{

        }
    })
</script>

</body>
</html>
```



> 区别

v-if会根据返回的值，来决定是否动态创建对应的标签，即只会实时的动态的创建v-if对应为true的标签，而为false的标签则不进行创建，因此开销比较大。

而vshow则是全部进创建，但是只展示为true的标签，不涉及动态的标签创建或销毁，只设计css的样式设计，因此开销较小。

因此如果一个组件频繁的切换，建议使用vshow来完成，如果一个条件很少改变，则可以考虑使用v-if

（整个内容切换的过程，是通过dom监听器来完成的，当dom监听到某个属性改变后，进行相应的操作）



#### 2.3.3 循环渲染

前端的操作里，循环遍历是必不可少的，因此vue也提供了一种循环的渲染方式——`v-show`。

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表渲染（使用v-for）</title>
    <div id="app">
        <h1>简单的列表渲染</h1>
        <ul>
            <li v-for="i in 3">{{i}}</li>
        </ul>

        <h1>简单的列表渲染-带索引</h1>
        <ul>
            <!--这里index可以起名为任意，但是其效果永远是表示当前循环的索引-->
            <li v-for="(i,index) in 3">{{i}}-{{index}}</li>
        </ul>

        <h1>遍历数据列表</h1>
        <!-- 语法:
        <tr v-for="对象 in 对象数组">
        <td>{{对象的属性}}</td>
        </tr>
        -->
        <table width="400px" border="1px">
            <tr v-for="(monster,index) in monsters">
                <td>{{index}}</td>
                <td>{{monster.id}}</td>
                <td>{{monster.name}}</td>
                <td>{{monster.age}}</td>
            </tr>
        </table>
    </div>
</head>
<body>
<script type="text/javascript" src="vue.js"></script>
<script type="text/javascript">
    new Vue({
        el:"#app",
        data:{
            monsters:[//一个monster数组
                {id:1,name:"牛魔王",age:800},//数组里放了两个对象
                {id:2,name:"红孩儿",age:200}
            ]
        }
    })
</script>

</body>
</html>
```

上面列举了两种for的使用方法，其核心使用方式是不变的，都是`循环量 in 集合`的格式（和python差不多）。

上面使用时，分别循环了具体的值、值对应的索引，但是这不是全部的可循环的内容，还可以在index和value之间插入一个name，表示循环的value对应的key。



### 2.3 组件化编程

先引出问题：

```vue
<!DOCTYPE html>
<html lang="en" xmlns:v-on="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="vue.js"></script>

</head>
<body>
<div id="app">
    <button v-on:click="click1()">点击次数={{count}}</button>
    <!--如果想让第二个标签和第一个标签独立起来，该怎么办？再重写一个count和click？太麻烦，使用组件化编程合适-->
    <button v-on:click="click1()">点击次数={{count}}</button>
</div>
<script type="text/javascript">
    new Vue({
        el:"#app",
        data:{
            count:0
        },
        methods:{
            click1(){
                this.count++;
            }
        }
    })

</script>

</body>
</html>
```

这个例子中，如果想让两个记录点击次数的标签独立起来，在不使用组件化编程的前提下，只能做两个方法池中的方法，并且使用的数据池的内容也不能是同一个。但是使用组件的话，就方便多了。

组件化编程，顾名思义，就是将前端界面，视为是不同组件组合起来的整体，这样需要哪个组件就用哪个组件，会方便很多。



#### 2.3.1 介绍

组件(Component) 是 Vue.js 最强大的功能之一(可以提高复用性[1.界面2.业务处理])。

组件也是一个Vue实例，也包括∶ data、methods、生命周期函数等。

组件渲染需要 html模板，所以增加了template 属性，值就是 HTML 模板。

对于全局组件，任何vue 实例都可以直接在 HTML 中通过组件名称来使用组件。

data 是一个函数，不再是一个对象， 这样每次引用组件都是独立的对象/数据（即data里的数据放入一个return函数里，这样谁用都是一个新的属于自己的值）。



#### 2.3.2 使用

定义组件的关键字是`component`，组件也是一个vue对象，vue对象能有的东西componet也能有。唯一一个特别就是component对象要比vue对象多一个template属性，这个属性来规定此组件的外观。

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>使用组件化来完成案件点击计数的优化</title>
    <script type="text/javascript" src="vue.js"></script>
    <div id="app">
        <h1>组件实现</h1>

        <!--引用全局组件-->
        <counter></counter>

    </div>

    <div id="app1">
        <h1>局部组件</h1>
        <mycounter></mycounter>

    </div>

    <div id="app2">
        <h1>局部组件</h1>
        <counter></counter>
    </div>


</head>
<body>
<script>
    /**
     * 组件的定义需要放在vue前面，放在后面就关联不上了
     */
</script>
<script type="text/javascript">
    //定义一个全局组件，命名为counter，给组件做一个模板，指明组件长什么样
    //实际上全局组件的内容和正常的vue对象内容差不多，就是不在这里进行el绑定
    Vue.component("counter", {
        template:`<button v-on:click="click()">点击次数={{count}}</button>`,//这就是规定模板的方式，使用template关键字来规定，后面用模板字符串最好
        //做一个数据池
        data(){
            //对于组件，数据池的数据使用return来返回，为了保证每个组件的数据信息独立
            return{
                count:0
            }
        },
        methods:{
            click(){
                this.count++;
            }
        }
    })
    //此处的vue实例必须有，需要去挂载
    new Vue({
        el:"#app"
    })

</script>

<script type="text/javascript">
    //定义一个局部组件
    const buttonCounter = {
        template:`<button v-on:click="click()">点击次数={{count}}</button>`,//这就是规定模板的方式，使用template关键字来规定，后面用模板字符串最好
        //做一个数据池
        data(){
            //对于组件，数据池的数据使用return来返回，为了保证每个组件的数据信息独立
            return{
                count:0
            }
        },
        methods:{
            click(){
                this.count++;
            }
        }}


    new Vue({
        el:"#app1",
        components:{
            'mycounter':buttonCounter,//将局部组件引入，此时这个局部组件的使用范围就在这个Vue实例上

        },
        template:`<mycounter/>`//这里如果给了一个template的化，前面div里就可以不用引入mycounter了（或者说引入了也没用了），这会直接显示，如果想让引入生效，注销掉这行就行
    })

    new Vue({
        el:"#app2",
        components: {
            'counter':buttonCounter,//局部组件不是代表有一个vue用了其他vue就不能用，这里声明一下的化也是可以用的。
        }
    })
    /**
     * 组件的使用，可以单独做进一个js文件中，使用的时候直接在界面上import，会方便很多
     */

</script>

</body>
</html>
```



上面的例子里，使用了两种组件——全局组件、局部组件

全局组件是属于所有Vue实例的，任何vue实例（或者说是挂载了vue的div标签）都可以使用这个组件，不需要单独声明。可以理解为设置在Vue类里的一个静态属性，随时都可以用的那种；

而局部组件则类似于某个vue对象特有的属性，其他vue使用不了，如果其他vue想使用，需要在自己的vue里声明一下引用了这个组件。



全局组件需要将所有需要的内容全部在组件内定义好，然后任何挂载了任何vue的div都可以引入全局组件；

局部组件的信息实际上最好也在组件内部定义好，但是在vue对象里也可以规定一下组件的形状（一般不这么用）。



### 2.4 生命周期

 Vue 实例有一个完整的生命周期，也就是说从开始创建、初始化数据、编译模板、挂载 DOM、渲染-更新-渲染、卸载等一系列过程，我们称为 Vue 实例的生命周期。在这整个生命周期的过程中，vue向程序员提供了几个函数，来方便程序员在vue周期的过程中进行阶段性的控制，这些函数叫做钩子函数。

![image-20231003201812785](C:\Users\changhe\AppData\Roaming\Typora\typora-user-images\image-20231003201812785.png)

#### 2.4.1 流程

整个生命周期如下：

1、new Vue()

new 了一个 Vue 的实例对象，此时就会进入组件的创建过程。此时没提供函数



2、Init Events & Lifecycle

初始化组件的事件和生命周期函数，此时也没提供函数



> 3、beforeCreate

组件创建之后遇到的第一个生命周期函数，这个阶段 data 和 methods 以及 dom 结构都未被初始化，也就是获取不到 data 的值，不能调用 methods 中的函数



4、Init injections & reactivity

这个阶段中, 正在初始化 data 和 methods 中的方法，没提供函数



> 5、created

这个阶段组件的 data 和 methods 中的方法已初始化结束，可以访问，但是 dom 结构未初始化，页面未渲染。



6、编译模板结构(在内存)，不提供函数



> 7、 beforeMount

当模板在内存中编译完成，此时内存中的模板结构还未渲染至页面上，看不到真实的数据。



8、Create vm.$el and replace ‘el’ with it
这一步，再在把内存中渲染好的模板结构替换至真实的 dom 结构也就是页面上



> 9、mounted

此时，页面渲染好，用户看到的是真实的页面数据， 生命周期创建阶段完毕，进入到了运行中的阶段。



10、生命周期运行中

> 10.1 beforeUpdate

当执行此函数，数据池的数据新的，但是页面是旧的。

10.2 Virtual DOM re-render and patch

根据最新的 data 数据，重新渲染内存中的模板结构，并把渲染好的模板结构，替换至页面上。

> 10.3 updated

页面已经完成了更新，此时，data 数据和页面的数据都是新的



> 11、beforeDestroy（不常用）

当执行此函数时，组件即将被销毁，但是还没有真正开始销毁，此时组件的 data、methods数据或方法 还可被调用



12、 Teardown……

注销组件和事件监听



> 13、destroyed（不常用）

组件已经完成了销毁



#### 2.4.2 具体细节

下面不对各个生命周期函数实际的效果，只是用来展示一下数据池和界面在不同生命周期阶段的渲染情况

```vue
<!DOCTYPE html>
<html lang="en" xmlns:v-on="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>vue生命周期函数</title>
    <script type="text/javascript" src="vue.js"></script>
    <script>
        /**
         * vue的生命周期函数是指vue从创建到销毁整个过程中，在各个阶段自动触发的函数
         * 声明周期有6个非常重要的函数：
         * beforeCreate：此时是刚刚创建了vue对象，vue里的数据池和方法池都还没有初始化，得不到其中内容的时候
         * Created：此时已经完成了数据池和方法池的初始化，可以拿其中的内容操作了，这个时候通常进行ajax请求，在还没将池子里数据渲染到界面上时，向后端更新一遍
         * beforeMount:此时将vue数据已经在内存模板解构内编译完成了，但是还没有渲染到前端
         * mounted:此时就将vue数据渲染到前端了，可以可视化的看到了
         * beforeUpdate:在mounted结束之后，整个vue进入运行周期，会实时的更新池子里的数据与渲染到前端的数据。这个方法就是池子里的数据更新完毕了，但是前端还没有被渲染上时触发的
         * updated:此时就是beforeUpdate的更进一步，池子数据和前端数据都是最新的时候触发
         * 此处展示一下触发过程，以后自己开发时，可以在各个生命周期函数里定义具体的操作
         */
    </script>
</head>
<body>
<div id="app">
    <span id="num">{{num}}</span>
    <button v-on:click="num++">+1</button>
    <h2>{{name}},加了{{num}}次</h2>
</div>


<script type="text/javascript">
    let vm = new Vue({
        //el绑定
        el:"#app",

        //数据池
        data:{
            name:`jack`,
            num:0
        },

        //方法池
        methods:{
            show(){
                return this.name;
            },
            add(){
                this.num++;
            }
        },

        /**
         * 生命周期函数
         */
        //第一个触发的是beforeCreate函数
        beforeCreate(){
            console.log("========beforeCreate============")
            console.log("数据池中数据是否加载完成【no】",this.name," ",this.num);//此时后面两个属性应该是undefined
            //console.log("方法池中数据是否加载完成【no】",this.show()," ",this.add());//此时会报错，因为还没有加载show和add方法，编译器查不到
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被渲染【no】",document.getElementById("num").innerText);//如果渲染成功，则插值表达式位置应该是被替换为数据池里的内容了，而此处还是{{num}}，并不是具体值
        },

        //第二个触发的是created函数
        created(){
            console.log("============create==============")
            console.log("数据池中数据是否加载完成【yes】",this.name," ",this.num);//此时后面两个属性应该是得到了
            console.log("方法池中数据是否加载完成【yes】",this.show()," ",this.add());//此时方法被成功调用，展示出了show的内容，并且让num自动加了1
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被渲染【no】",document.getElementById("num").innerText);//如果渲染成功，则插值表达式位置应该是被替换为数据池里的内容了，而此处还是{{num}}，并不是具体值
            //此时常常会发出ajax请求，完成局部刷新后再进行内存模板编译
        },

        //第三个触发的是beforeMount函数，此时已经完成了内存模板编译，但是还没渲染到界面，即挂载前
        beforeMount(){
            console.log("============beforeMount==============")
            console.log("数据池中数据是否加载完成【yes】",this.name," ",this.num);//此时后面两个属性应该是得到了
            console.log("方法池中数据是否加载完成【yes】",this.show()," ",this.add());//此时方法被成功调用，展示出了show的内容，并且让num自动加了1
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被渲染【no】",document.getElementById("num").innerText);//此处仍然没有，因为还没挂载上
        },

        //第四个触发的是Mount函数，此时挂载完毕，界面数据成功加载为数据池里的数据和方法池里的数据
        mounted(){
            console.log("============Mount==============")
            console.log("数据池中数据是否加载完成【yes】",this.name," ",this.num);//此时后面两个属性应该是得到了
            console.log("方法池中数据是否加载完成【yes】",this.show()," ",this.add());//此时方法被成功调用，展示出了show的内容，并且让num自动加了1
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被渲染【yes】",document.getElementById("num").innerText);//此处有具体值，因为挂载成功
        },

        //之后进入循环监听阶段，监听数据池里数据变换————更新界面信息————监听数据池中数据变换
        //循环监听的一个触发方法是beforeUpdate，发生在数据池数据改变后但是还没更新到界面上的时候
        //每次数据池里数据变换，都会调用该函数
        beforeUpdate(){
            console.log("============beforeUpdate==============")
            console.log("数据池中数据是否加载完成【yes】",this.name," ",this.num);//此时后面两个属性应该是得到了
            console.log("方法池中数据是否加载完成【yes】",this.show()," ",this.add());//此时方法被成功调用，展示出了show的内容，并且让num自动加了1
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被更新【no】",document.getElementById("num").innerText);//此处永远慢数据池中的num一步，因为此时还没有更新上数据
        },

        //当beforeUpdate后，就会进入updated函数，完成用户界面的渲染
        updated(){
            console.log("============beforeUpdate==============")
            console.log("数据池中数据是否加载完成【yes】",this.name," ",this.num);//此时后面两个属性应该是得到了
            console.log("方法池中数据是否加载完成【yes】",this.show()," ");//此时方法被成功调用，展示出了show的内容，此处一出add方法的调用，因为如果调用会进入死循环——beforeUpdate调用add使num+1，然后进入updated会再次调用add使num+1,而因为此时改变了数据池，所以会马不停蹄的再次进入beforeUpdeate去更新，进而无限循环调用这两个函数
            console.log("用户界面dom对象是否加载完成【yes】",document.getElementById("num"));//尝试得到id为num的标签，成功
            console.log("用户界面dom是否被更新【yes】",document.getElementById("num").innerText);//此时数据和num一致了
        }




    })

</script>

</body>
</html>
```

