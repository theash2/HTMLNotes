## javascrip

ECMAScript:**ES** W3C定义的JavaScript和JScript的标椎

底层采用Unicode编码,包括utf-8

用于描述网页行为的脚本代码,面向对象 -----jscrip

alter()

docume.write() 在页面中输出

console.log()

可以写在<scrip></script>中,或标签属性如onclick中;或外部引入

```HTML
<script type="text/JavaScript" src=""></script>
<a href="javascript:代码"></a>
```

## 字面量

常量

不可改变的值,如1,3,99;可以直接使用

基本数据类型

保存在栈内存中

String  字符串中特殊字符可以用\转义

​			可以直接进行'+'拼接操作

Number 包括整数和浮点数, 最大值:Number.MAX_VALUE

​				正无穷 infinity ;  NaN: not a number

​				**整数**可以直接赋值时计算,**浮点数**则会有误差

​				**精确计算不要用JS**

Boolean

Null 为空的object

Undefined 未赋值

引用数据类型

属性保存在堆内存中,**对象引用地址**保存在栈内存中

Object

![](F:\新建文件夹\学习\前端\前端\对象内存.png)

## 变量

保存字面量,可以改变

**定义变量用var关键字**,可以定义中文关键字。变量声明提前？预编译

## 类型转换

ToString

​		变量.toString() 将转换的结果返回  	

​		null,undefined没有该方法

​		调用String()函数	String(变量) 将转换的结果返回,各个类型变量都可用

​		+""

Tonumber

​		使用Number()函数 

​		0=Number(undefined)

​		parseInt(String[,进制]),parseFloat(String[,进制]) 将字符串中有效的第一组数字取出进行转换

​	-0

​		+变量 

ToBoolean

​		Boolean()函数

​		**0,NaN,"",null,undefined转换为FALSE**

## 其它进制

16进制:0x开头

8进制 : 0开头

2进制:0b开头

## 运算符

'+','-','*', '/', '%'

进行运算符操作时,通常将**操作数转化为Number类型**.除了含有String类型操作数的**+**操作

a = 123+"123"("123123")

## 逻辑运算

对Boolean值进行运算,非Boolean值自动换为Boolean类型再运算

! 非

​	对于非Boolean值,先将值转换为Boolean值在取反

​	!! 快捷地将其他类型的值转换为Boolean类型

&& 与

​	短路"与" ,若第一个值为FALSE直接结束运算

​	若两个数都为true,则返回后一个数

​	若含有FALSE,则返回靠前的FALSE

​	第一个值FALSE,返回第一个值

​	第一个值true,返回第二个值

​	返回操作数值

|| 或

​	短路"或 "

​	返回操作数值

​	操作数含有true,返回第一个值

​	操作数第一个为FALSE,返回第二个值

## 相等运算

== 

当比较数类型不一样时会自动转换类型

String,Boolean->number

**null==0 FALSE**

**NaN不等于任何值**  isNaN(变量)

===

全等:类型也得相同

!==

不全等:类型相同的不同

## 条件运算符

条件表达式?语句1:语句2;   会返回结果

条件表达式为true 执行语句1

​						FALSE 语句2

## 运算符优先级

"&&" > "||"

由高到低,同行同级

![](F:\新建文件夹\学习\前端\前端\运算符优先级.png)

## 流程控制语句

### 条件判断语句

if(){}

if(){} else{}

if(){} else if(){}... else{}



```js
switch(n){
    case 1:语句1
    		break;
    case 2:语句2
    		break;
    case 3:语句3
    		break;
    case n:语句n
    		break;
    default:其他情况语句
       }
```

### 循环控制语句

for(){}

for/in

l	ist=[1,2,3]

​	for(x in list){  //X为集合中的下标

​						}

for/of

​	for(var value of myArray){

​			console.log(value);

​												}

while(true){ }

do{

​	执行语句

​	}while(条件) //至少执行一次

## 对象

### 内建对象

ES标椎中定义的对象,在任何ES实现中都可使用

math String Number Function . . .

### 宿主对象

JS运行环境提供的对象,浏览器提供的对象

DOM bom

### 自定义对象

开发人员自己创建的对象



```JS
//创建对象
var ObjName = new Object();
///使用对象字面量创建对象
var obj = {属性名:value,
           属性名:value,
           functionname:function(){}
           ...};

//对象添加属性
ObjName.自定属性名 = value;或
ObjName["属性名"]=value //对应读取方式
. . .

///读取对象属性
ObjName.属性
ObjName["属性名"/变量] //根据变量值查找value 

//删除对象属性
delete ObjName.属性

//判断属性是否在对象中
true/FALSE="属性名" in 对象 
```

## 函数



```js
//创建函数
var funName = new Function("代码");

//函数声明创建函数	创建提前
function 函数名([a形参1,b, . . .]){
			执行语句
            . . .
		}
//函数表达式创建函数		提前声明funName，未创建
var funName = function ([a形参1,b, . . .]){
			执行语句
            . . .
		};//匿名函数赋值给funName
//形参不必用var声明,不检查实参个数,多于的不处理


//调用函数
funName([实参]);
```

返回值

​	return 值/变量

​	**默认返回的都是结果.toString()的值,如[Object,Objetc]?**

**函数也可以作为函数的实参**。1.调用函数fun()，2.函数对象fun



### 立即执行函数

匿名函数对象创建完后直接调用

```
(function(){
)()
```

### 枚举对象的属性

for in 语句

```js
for(var n in Object){ 
    console.log(n);//每次循环将属性名赋给n
    console.log(Object[n]); //获取属性的值
}
```

### 工厂方法创建对象

```JS
//构造创造对象的函数
function createfun(){
var obj = new Object();
    赋值属性
    . . .
    return obj
}
var obj1 = createfun();
```

### **构造函数**

构造函数是一个函数(对象),用this关键字给函数赋予属性或方法,

当被调用时,返回this即赋值过后的函数(对象)

**对函数进行赋值构造,调用时转换为对象,赋值给对象**

构造函数调用需要new 关键字

构造函数=**类** ,调用构造函数的对象 = **类的实例**

instanceof

```JS
function fun(){};

//this用于承载返回的对象
function FUN(){
this.属性=;
//方法可以引用全局的函数,加快构造函数的速度和内存
this.函数=fun();//全局函数
this.name="";
. . .
}
var f = new FUN();

//修改构造函数:对构造的对象直接进行属性重置
f.name="name2";


```

### 函数对象方法

function.call(), function.apply() 可以将一个对象指定为第一个参数,对象会成为函数执行时的this

fun.call(object,实参 , . . )

fun.apply(object,[实参, . . ])

### arguments

**浏览器给函数传递的隐藏参数**,封装了实参对象,**是类数组对象**,具有数组特性。所以可以**不通过形参就使用实参**

arguments.callee 当前正在执行得到函数对象

## 作用域

#### 全局作用域

全局对象window。

全局作用域的变量都是window的属性。window.

全局作用域的函数都是window的方法。window.function()

#### 函数作用域

调用函数时创建函数作用域，函数执行后销毁

函数执行优先从自身作用域找变量，然后往上一级找。想访问全局变量：window.变量

**函数内变量,函数声明提前**

#### **this**

**浏览器向传递函数的隐含参数**

​	**以函数方式调用,this=window**

​	**以方法调用,this就是调用方法的对象**

​	**以构造函数调用,this为创建的对象**

​	**使用call,apply调用时,this是指定的对象**

​	**在时间响应函数中,响应函数是给谁绑定的,this就是谁**

## 原型prototype

每创建一个**函数**,解析器会向函数中添加一个prototype;prototype对应一个**原型对象**

**通过构造函数调用创建的对象中,都有一个隐含属性指向函数的原型对象**

**向原型中添加属性或方法: 构造函数function.prototype.属性/方法** 

```
Object.__proto_()_.访问原型对象中的属性或方法
```

![](F:\新建文件夹\学习\前端\前端\原型.png)

### 原型对象

函数对象,实例的公共访问区域

当访问对象的一个属性或方法,若自身找不到,则到原型函数中找

### 检查对象自身属性

object.hasOwnProperty();//原型的原型函数中

原型对象属性

```
object.__proto__.hasOwnProperty()
```



使用一个属性或方法;

自身寻找->原型对象寻找->原型对象的原型对象寻找->直到**Object类**对象的原型中

## 数组

**push(value, . . )**,向数组尾部添加元素,返回添加后的数组长度

**pop()** 删除数组最后一个元素,返回删除的元素

**unshift(value , . . )**  向数组头部添加元素,返回添加后的数组长度

**shift()** 删除数组开头元素,并返回删除的元素

**slice()** 从数组中提取指定元素,返回新数组

​		arr2 = arrObject.slice(start,end)  左闭右开

**splice()** 删除数组中指定元素,可传递新元素会改变原数组

​		arr[删除的数组] = arrObject.splice(start,length[ , value,value, . .])  从start开始删除length个元素,并在start插入[ , value,value, . .]

​		length= 0 ;可以插入

**concat()** 连接2个或多个数组,并返回结果

​			result = arr.concat(arr2, . . )

**join("?")** 数组转换成字符串,并用?连接间隔

​			result = arr.join();

**reverse()** 反转数组,改变原数组

**sort()** 数组排序,改变原数组;按照Unicode ,可以指定排序方式

​		**arr.sort(function(a,b){**

​			**a-b**

​			**return 1(>0 ,改变a,b位置)**

​			**return -1(< = 0,位置不变)**

​			**}**

遍历

​		1.for()循环

​		2.forEach()	**IE8以上**;参数为函数

​			数组.forEach(function(value,index,obj){ }; )(**像function这样由我们创建,但不由我们调用的函数称为回调函数**)

​			数组中有几个元素,函数就执行几次;浏览器将(遍历到的元素,该元素的index,遍历的数组object)作为实参传入函数

## Date类

```js
//当前执行时间
var d= Date();

//创建指定时间
var d = new Date("月/日/年 时:分:秒")

//获取对象时间的日,几号
getDate()
	//getMonth() +1   0:一月
	//getFullYear()
//获取对象时间的星期号
getDay() //0:周日

//返回1970/1/1到对象时间的毫秒数,即时间戳
getTime()
Date.now();
```

## 包装类

将基本数据类型转换为对象

String() Number() Boolean()

var num = new Number();

**在与基本类型比较会出问题**

## String类

```js
var str="";
//返回指定索引位置的字符Unicode编码
str.cahrCodeAt(index);

//根据value返回对应Unicode的字符
String.fromCharCode(value);

//返回字符在str中第一次出现的位置,没有则返回-1。[,index]指定从哪个位置开始查找
str.indexOf(char [, index])
str.lastIndexOf(char [,index]) //从后往前找

 //截取字符串内容[start,end)
str2  = str.slice(start,end)
str2 = str.substring(start,end)  //start恒>end >0


//按长度来截取字符串
str2 = str.substr(start,lenght)

//根据reg正则表达式效果或特定字符拆分str	默认全局
strs = str.split(/[0-9]/) 

//搜索字符串中是否有指定字符串,	返回第一次找到的索引,没有返回-1
str.search()


//根据正则表达式从字符创中提取字符。默认返回第一次 ，多次匹配正则表达式开启全局/ /g 
str.match();


//替换字符串中的内容。	默认匹配第一个
str2 = str.replace("old", "new")
```

## 正则

```js
var str ;

//对象创建
var reg  = new RegExp("正则表达式", "匹配模式");
//字面量创建
var 变量 = / 正则表达式/匹配模式

reg.test(str) ; //true or FALSE

匹配模式
	i	忽略大小写
	g	全局模式
[]	//中括号中的元素为或关系 = =  |
[^ab]  //除了ab 是否含有其他

//量词
(内容){m} 	//一个内容连续出现m次
(内容){m ,n} 	//一个内容连续出现m到n次
(内容){m ,} 	//一个内容连续出现m次或以上

//边界	同时使用^$,则要求字符串完全符合正则要求
^(内容)	//以内容开头
(内容)$	//以内容结尾     

//特殊字符匹配使用\ 转义

\w	单词,数字,_
\W	除了\w [^0-9A-z_]

```



```
验证字母：	/^[a-zA-Z]+$/
验证长度为3的字符：	/^.{3}$/
验证由26个英文字母组成的字符串：	/^[A-Za-z]+$/
验证日期YYYY-MM-DD：	/^(\d{1,4})(-|\/)(\d{1,2})\2(\d{1,2})$/
验证邮编：	/^\d{6}$/
验证日期格式YYYY-MM-DD hh:mm:ss：/^(\d{1,4})(-|\/)(\d{1,2})\2(\d{1,2}) (\d{1,2}):(\d{1,2}):(\d{1,2})$/
验证整数：	/^[-+]?\d*$/
验证小数：	/^[-\+]?\d+(\.\d+)?$/
验证中文：	/^[\u0391-\uFFE5]+$/
验证邮箱：	/^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/
验证手机号：	/^1[3456789]\d{9}$/
验证身份证：	/^\d{6}(18|19|20)?\d{2}(0[1-9]|1[12])(0[1-9]|[12]\d|3[01])\d{3}(\d|X)$/
```

![](F:\新建文件夹\学习\前端\前端\正则量词.png)

![正则匹配边界](F:\新建文件夹\学习\前端\前端\正则匹配边界.png)

![正则元字符](F:\新建文件夹\学习\前端\前端\正则元字符.png)