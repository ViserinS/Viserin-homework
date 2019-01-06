##  我喜欢的javascript

​     ![img](https://pic.baike.soso.com/ugc/baikepic2/7957/20170919102641-1495808957_png_1024_1024_30976.jpg/0)

###  基本介绍

JavaScript是一种基于对象和事件驱动并具有相对安全性的客户端脚本语言。同时也是一种广泛用于客户端Web开发的脚本语言，常用来给HTML网页添加动态功能，比如响应用户的各种操作。它最初由网景公司（Netscape）的Brendan Eich设计，是一种动态、弱类型、基于原型的语言，内置支持类。JavaScript是Sun公司的注册商标。Ecma国际以JavaScript为基础制定了ECMAScript标准。JavaScript也可以用于其他场合，如服务器端编程。完整的JavaScript实现包含三个部分：ECMAScript，文档对象模型，字节顺序记号。

Netscape公司在最初将其脚本语言命名为LiveScript。在Netscape在与Sun合作之后将其改名为JavaScript。JavaScript最初受Java启发而开始设计的，目的之一就是“看上去像Java”[2]，因此语法上有类似之处，一些名称和命名规范也借自Java。但JavaScript的主要设计原则源自Self和Scheme[3]。JavaScript与Java名称上的近似，是当时网景为了营销[1]考虑与Sun公司达成协议的结果。为了取得技术优势，微软推出了JScript脚本语言。Ecma国际（前身为欧洲计算机制造商协会）创建了ECMA-262标准（ECMAScript）。现两者都属于ECMAScript的实现。尽管JavaScript作为给非程序人员的脚本语言，而非是作为给程序人员的编程语言来推广和宣传，但是JavaScript具有非常丰富的特性。

###  使用方法

一、Javascript在网页的用法

Javascript加入网页有两种方法：

1、直接加入HTML文档

这是最常用的方法，大部分含有Javascript的网页都采用这种方法，如：

<script language="Javascript">

<!--

 document.writeln("这是Javascript！采用直接插入的方法！");

//-Javascript结束-->

</script>

在这个例子中，我们可看到一个新的标签： ，而浏览器这是用Javascript编写的程序，需要调动相应的解释程序进行解释。（w3c已经建议使用新的标准：)]]>]]>

HTML的注释标签<!--和-->：用来去掉浏览器所不能识别的Javascript源代码的，这对不支持 Javascript 语言的浏览器来说是很有用的。

//-Javascript结束：双斜杠表示 Javascript的注释部分，即从//开始到行尾的字符都被忽略。 至于程序中所用到的document．write（）函数则表示将括号中的文字输出到窗口中去， 这在后面将会详细介绍。 另外一点需要注意的是，的位置并不是固定的，可以包含在...... 或.....中的任何地方。

还有一个更高级版本的嵌入脚本，它使用了HTML中的CDATA语法（Character Data，就是把CDATA中的文本全部当作纯文本处理，除非遇到CDATA的结束）

type="t]]>ext/javascript">

<!--//-->

<!CDATA[[//><!--

 //javascript代码

Javascript 的使用
Javascript 的使用
 //--><!]]>

</script>

2、引用方式

如果已经存在一个Javascript源文件（以js为扩展名），则可以采用这种引用的方式，以提高程序代码的利用率。其基本格式如下：

<script src＝url language="Javascript"></script>

其中的Url就是程序文件的地址。同样的，这样的语句可以放在HTML文档头部或主体的任何部分。 如果要实现“直接插入方式”中所举例子的效果，可以首先创建一个Javascript源代码文件“Script.js”，其内容如下：

document.writeln("这是Javascript！采用直接插入的方法！");

在网页中可以这样调用程序：<script src＝"Script.js" language="Javascript"></script> 。

###  相关特性

相关特性

面向对象性

javascript
javascript
javascript中并没有类的概念，但是javascript使用了一种叫“原型化继承”的模型，而且javascript中也有作用域、闭包、继承、上下文对象等概念

作用域

作用域是指变量存在的域，在文档中的javascript脚本的作用域都是window。在javascript，function和let分隔作用域

例如下面这个作用域的例子：

var myVariable="outside";

function myFunction(){

var myVariable="inside";

alert(myVariable);

}

myFunction();

alert(myVariable);

结果会是先弹出内容为“inside”的对话框，然后弹出内容为“outside”的对话框，这就是function建立了一个作用域，而第一次提示的是myFunction作用域内的myVariable

下面是一个let控制作用域的例子：

var myVariable="outside";

let(myVarialbe="inside") alert(myVariable); // inside

alert(myVariable); // outside

let语句是在javascript 1.7中加入的

闭包

闭包也和作用域有关，它指的就是一个封闭的作用域（拥有外部变量，函数无法访问的变量和函数），一般都是用一个匿名函数来做成闭包的

(function(){

var myVariable="private",

})();

alert(myVariable); // undefined

上下文对象

上下文对象指的就是this对象。它是一个只能读取而不能直接赋值的对象（就是你只能对this拥有的属性和方法赋值）。上下文对象在javascript可以说发挥的淋漓尽致。

如果你在一个对象（Object）中使用this，指的就是这个对象

var obj={

getThis:function(){

return this;

}

};

alert(obj.getThis===obj); // true

同样的，在作用域中已经提到过文档中javascript对象都属于window，那么下面这个例子

alert(window===this);

也将提示true。

上下文对象在事件侦听器中指的就是发生事件的对象

document.body.addEventListener('click',function(){

alert(this===document.body); // true

},false);

this在构造函数中则是指实例

function Person(name){

thisname=name;

}

var Sam=new Persom();

这里this指的就是Sam。





