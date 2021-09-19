# DOM

文档对象模型。将文档的各个内容,即HTML页面的元素,转换为对象，然后对对象进行操作。模型可以体现节点与结点的关系。

![](F:\新建文件夹\学习\前端\前端\DOM树.png)

## 节点Node

构成HTML文档最基本的单元，HTML的任何东西都是节点

文档节点：整个HTML文档

元素节点：HTML中的HTML标签元素

属性节点：元素的属性

文本节点：HTML标签中的文本内容

**浏览器提供了文档对象，代表整个页面，可以直接使用document**

## 事件

用户和浏览器进行的交互

**可以为事件绑定响应处理函数的形式来响应事件**

​			1.获取事件对象	2.绑定响应事件

**window.onload = function(){}**

## DOM查询

### 文档的方法

```js
document对象
    getElementById()
	getElementsByTagName()
	getElementsByName()

元素对象方法
	getElementsByTagName()	通过标签名,包括body

	属性:
	children   表示当前元素的所有子元素
	childNodes 表示当前节点的所有子节点(元素节点,文本节点) 标签中的空白会作为节点>IE8
    firstChild  表示当前节点的第一个子节点
    firstElementChild	表示当前元素节点的第一个子元素节点 >IE8
    lastChild 	表示当前节点的最后一个子节点
    
具体节点的方法:

    属性:
	parentNode 父亲节点
     previousSibling	前一个兄弟节点
     previousElementSibling
     nextSibling	后一个兄弟节点
innerHTML 获取标签内的文字
innerText	仅获取到元素内部的文本
//读取标签的属性
单表对象.属性名  (除了class; 用className)
```

```js
获取body
	document.getElementsByTagName("body")[0];
	document.body;

//根标签HTML
	document.documentElement
    
//页面所有元素
	document.all
	document.getElementsByTagName("*")

//根据元素的class查询
	document.getElementsByClassName(); 	>IE8
```

### **查询选择器**

```js
//需要一个选择器的字符串作为参数,可以根据CSS选择器来查询一个元素节点的对象;	只返回第一个符合要求的
document.querySelector()
document.querySelectorAll()	//会返回多个元素,封装到NodeList数组
```

## DOM增删改

```JS
//创建元素节点
var 变量名 = document.createElement("标签名");

//获取父节点方法
子节点.parentElement

//创建文本节点
var 变量名 = document.createTextNode("文本内容")

//父节点中添加子节点
父节点.appendChild(子节点);
子节点.parentElement.appendChild(子节点);

//在指定子节点前插入新节点
父节点.insertBefore(NewNode,refNode);

//指定新节点替换旧节点
父节点.replaceChild(NewNode,OldNode);

//删除节点
父节点.removeChild(OldNode);
```

## 操作css

通过js修改元素样式

```javascript
获取到对应元素
元素.style.样式属性 = "value" ;  //  是当做内联样式修改操作的  等级<!important 
						//如果样式属性含有- 之类符号,需要将符号去掉,符号后首字母大写backgroundColor 
    
获取元素当前显示样式	只读:
	//元素.currentStyle.样式属性 = "value" ;   仅IE支持
    Object = getComputedStyle(要获取的元素对象,伪类/null)[样式属性] ; Object.样式属性 
    						window的方法,可以直接使用, 返回含有样式属性对象,>IE8
    
    //兼容的自定获取样式函数,obj:要获取的样式的元素, name:要获取样式的属性
			function getStyle(obj,name){
				
				if(window.getComputedStyle){
					//一般浏览器
				return getComputedStyle(obj,null)[name];
				}else{
					//IE8
				return obj.currentStyle[name];
				}
				
				
				
			}
```

其他操作样式

```js
//只读,不可赋值修改
//获取元素可见宽高数值,包括内容区的内边框,不带px单位, 可以直接计算
		元素.clientHeight
		元素.clientWidth

//获取元素整个大小,clientWidth + border
		元素.clientHeight
         元素.offsetHeight

//获取元素的定位开启poistion祖先元素 
		元素.offsetParent

//获取元素相对于定位父元素的偏移量
		el.offsetLeft		
		el.offsetTop 

//获取元素的整体宽高  Height,Width
		el.scrollHeight
//获取元素滚动的距离 left,top
		el.scrollLeft
		//scrollHeight + scrollTop == clientHeight 时说明滚动条到底

```



**以上方式修改样式时,每修改一次,浏览器就会渲染一次; 可以将要修改的属性包装成另一个类,修改时将原类名修改为新类名 .className =**   ,**也可以继承原样式,加上新类名** className="name name2"

**box.className+=" name2"** //空格





## 事件对象

当事件的响应函数被触发时,浏览器每次都会将一个事件对象作为实参传递给响应函数,

在事件对象中封装了当前事件的一切**相关信息**

```js
//鼠标在元素中移动时触发,event中封装了所有信息,网上查
Object.onmousemove = function(event){	
//兼容操作
    event = event ||window.event
    
//滚动时鼠标与div产生偏移	
    var X = event.clientX; 	>IE8  //可见窗口的X坐标,与实际坐标相差滚动条滚动的距离
    //var X = window.event.clientX  <=IE8,事件对象当做window的属性。不兼容火狐
    var Y = event.clientY;
    
    
    var X = event.pageX; //相对于整个页面	>IE8
    var Y = event.pageY;
     
     
}


	
```

### 事件冒泡Bubble

后代元素上的事件被触发时,祖先元素的**相同事件**也会触发

取消冒泡:通过事件对象取消 		

```
event.cancelBubble = true ;
```

### 事件的委派

将**多个兄弟元素**的相同的响应函数绑定给共同的**祖先元素**,就可以只绑定一次

通过祖先的响应函数来处理响应事件

```

```

### 事件的绑定

```js
对象.事件 = function(){};函数赋值形式一个事件对象顺序绑定多个响应事件时,后续的响应函数会覆盖前面的

//绑定多个响应函数,需要兼容
参数:事件动作 回调函数 是否在捕获阶段触发事件false/true,一般false
对象.addEventListener("click",function(){	    //>IE8	先绑定先执行	
    alert("?");
    //this指绑定的事件对象
	},false)
	//IE8	attachEvent() 参数:事件的字符串要on,回调函数		先绑定后执行
		对象.attachEvent("onclick",function(){
        //this指window    
        })
	
	
		//兼容性解决
		//obj:绑定对象  eventstr:事件字符串(不带on) callback:回调执行函数
				function bind(obj,eventstr,callback){
					//大部分兼容的
					if(obj.addEventListener){
						obj.addEventListener(eventstr,callback,flase);
					}else{
					//IE8
					obj.attachEvent("on"+eventstr,function(){
						//将this统一为事件对象: 一名函数中自己使用回调函数
						callback.call(obj);
					});
					}

				}

```



### 事件的传播

由里向外:子元素向外部祖先元素

由外向里:外部祖先元素到子元素

W3C将事件的响应划分为3个阶段

​		1.捕获阶段:**由外向里捕获**到子元素;不触发事件

​		2.目标阶段:事件捕获到目标元素,准备在目标上执行事件

​		3.冒泡阶段:事件**从目标向祖先元素传递**,依次触发祖先元素上的事件

如果要在捕获阶段执行:obj.addEventListener(eventstr,callback,**true**);

### 元素拖拽

```js
				function drag(obj){		//对象需要开启position
					obj.onmousedown = function (event){
					//将鼠标的操作全部连接到obj上
				obj.setCapture&&obj.setCapture();
				event = event ||window.event;
				var X= event.clientX  -box1.offsetLeft;
				var Y = event.clientY - box1.offsetTop;

					//获取鼠标在窗口的位置
					document.onmousemove = function (event){			
						event = event||window.event;
						var left = event.clientX-X;
						var top = event.clientY-Y;

						box1.style.left = left+"px";
						box1.style.top = top+"px";
					};
					
					//元素松开,固定位置---取消onmouesedown
					document.onmouseup = function(){
						document.onmousemove =null;
						//取消document.onmouseup事件
						document.onmouseup = null;
						
						//取消拦截所有事件
						obj.releaseCapture&&obj.releaseCapture();
					}
					//拖拽事件与浏览器默认行为冲突
					return false;
				};
				}
```

## 取消浏览器的默认行为

```JS
//对于函数绑定的事件
	return false;
//对于addEventListener绑定的事件
	event.preventDefault();		>IE8
 event.preventDefault &&event.preventDefault();
```



## 事件

### 滚轮

```js
onmousewheel  
滚轮移动:event.wheelDelta;
//火狐不支持:DOMMouseScroll 绑定滚动事件
	obj.addEventListener(DOMMouseScroll,callback,flase);
	滚轮移动:event.detail 向上滚-3	向下滚 3

```

### 键盘事件

一般绑定给可以获取焦点的事件或者document

```码
	onkeydown 按键按下,事件可以一直触发
	onkeyup	 按键松开
    event.keyCode 获取按键事件按钮的Unicode码
    event.altKey,shiftKey,ctrlKey 判断是否被按下,false/true
```

