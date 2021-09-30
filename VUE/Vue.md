

Vue

### 简介

**一个容器对应一个vue实例,**

容器里的代码仍然符合HTML规范,加入了一些js表达式

root容器里的代码成为**VUE模板**

{{xxx}} 可以写js表达式,且xxx会自动读取到data中的素有属性

## 模板语法

### 插值语法

解析标签体的内容

```js
//插值语法  将值插入标记的位置 {{xxx}},xxx可以直接读取到data中的内容
	通常指定标签体内容
<h3>你好,{{name}}</h3>


```

### 指令语法

解析标签,标签属性,标签体内容,绑定事件...

各种指令 v-xxx

```js
// v-bind可以动态的绑定代码	
	//v-bind:声明url为js表达式执行  或者直接 : 声明
<a v-bind:href="url">点击跳转</a>
	url:"www.baidu.com"
```

## 数据绑定

单向绑定 v-bind  简写  : 属性=""

​	可以通过data的值改变绑定的值,不能通过改变绑定值的value来改变data

双向绑定v-model  简写 v-model = "value"

​	将 data的值和元素绑定到一块,同时修改。默认手机value值

​	**只能用于表单类元素**

## 

### el的两种写法

```js
//方法一  在vue构造时链接用el
	 el:"#root",
//方法二	调用vue的原型函数进行连接
      const v=  new Vue({         
            data:{
                name:"晨灰",
                url:"http://www.baidu.com"
            }
        })
        v.$mount("#root"); //通过vue实例调用vue的原型函数
```

### data的两种写法

```js
//方法一 对象形式
	        data:{
                name:"晨灰",
                url:"http://www.baidu.com"
            }
//方法二  函数式 必须一般函数形式,不能用箭头函数
            data:function(){ //简写 data(){
                return{	//需要的数据放在return中
                    name:"晨灰",
                }
            }
```

## MVVM模型

M:model,     data中的数据

V:view,	DOM

VM: ViewModel  VUE

data中的属性最后出现在了vm上,vm进入了DOM中

## 数据代理

### object.defineProperty

向一个对象中添加属性，添加的属性默认不可枚举，不可修改，不可删除

```js
Object.defineProperty(obj,属性名,{
    value:xx
    enumerable:true //设置是否可以被枚举
     writeable:true //设置是否可以修改
     configable:true //设置是否可被删除
     //当有人读取person的age属性时,get函数被调用,返回值作为age的值
    get(){  
        return 
    }
    //当有人修改age属性时,set函数setter被调用,且会收到就是age的值
    set(value){
        number = value
    }
})
```

### 数据代理

通过一个vm对象代理里一个对象中_data值的操作,_

**vm把vue实例中的data当做自己的_data**  图中黄框-->绿框

通过Object.defineProperty() **将_data所有对象添加到vm自己上**，并加上getter/setter操作_data的值

![1632234688068](F:\新建文件夹\学习\前端\前端\VUE\数据代理.png)

## 事件绑定处理

然后在vue实例的,methods:{}对象中实现函数

**methods:{}里的函数不要用箭头函数,会被window使用,vue会丢失this**

### v-on:/@

绑定事件监听器,指定行为,或者简单的JS语句

给各种元素绑定事件,**使用指令v-on:/@xxx= functionname**绑定事件函数,xxx是事件名

事件的回调需要配置在methods:{}里,最终会归为vm

事件响应函数可以直接跟(,$event)里传入参数,如果无参数就不加括号。$event是event的占位符,保护event

```js

<button v-on:click="showinfo">点击弹窗</button>
<button v-on:click="showinfo2($event,123)">点击弹窗参数</button>
methods: {
	showinfo(){
		alert("vue实例里的函数")
		}
    	showinfo2(event,number){
		alert(number)
		}
   },
```

### 事件修饰符

在@事件后加上一个修饰词,修改元素/事件的行为,可以连写

#### **.prevent**

阻止事件的默认行为

```js
//点击链接不再跳转
<a href="http://www.baidu.com" @click.prevent="showinfo($event)">点击显示</a> 
event.preventDefault()
```

#### **.stop**

阻止事件冒泡,捕获执行完不冒泡给父元素

#### **.once**

事件只触发一次回调

#### .capture

使用事件的捕获模式,一般修饰在父元素,在捕获阶段就执行事件

#### .self

event.target是当前操作的元素才触发事件,与冒泡触发其他元素相关

#### .passive

事件默认行为立即执行,**无需等待事件的回调函数**,监听到事件响应就表现,跳过响应函数

事件的默认执行顺序:监听到事件响应-->执行响应函数内容回调-->行为表现出来响应事件

### 键盘事件

#### @keydown=""

#### @keyup=""    

后面可以加**修饰词,别名,自定义别名,key值,keycode**(.enter :当enter)对应键抬起时,事件函数执行

vue中常用的按键别名:**回车=>>enter； 删除/推格=>>delete;	退出=>>ESC; 	空格=>>space;	换行=>>tab(适合用keydown);	上=>>up;	下=>>down;	左=>>left;	右=>>right**

没有别名的按键:根据原始key值绑定 @keyup.name(e.key获取得到的,按键的真正名字),多个单词构成的需要大写转小写,单词间用-连接kebab-case(短横线命名)

```js
<input type="text" placeholder="按下回车提示输入" @keyup.caps-lock="keyup($event)">
```

```js
//自定义键名
Vue.config.keyCodes.自定义键名 = 键码
```

系统修饰符:Ctrl,shift,win,Alt  后面可跟其他按键.keyboard

​	keyup:按下修饰键同时,按下其他键,当其他键up时,事件才触发

​	keydown:按下时就触发

## 计算属性

声明一个不存在的属性,通过一个**已有的,vue监控得到的属性**计算而来,**将计算后的属性直接给vm**,后续可视为vm的属性进行插值语法调用 ;实现利用了Object.defineproperty的方法的getter,setter,

计算属性可以利用cache >method

```js
        computed:{ //声明计算属性
            fullname:{	//计算属性设计为对象形式
                //funllname的getter 1.初次读取时调用 2.被计算的值变化时调用
                get(){ //get里的this已经被vue指向了vue实例
                    return this.name.slice(0,3) +"_"+this.zi
                },
                //当计算属性有需求进行修改时,要配置setter
			 set(value){
                 //由于getter调用原因2,所以要更新页面需要对被计算数据进行修改
                    this.name =value.xxx ,
                   this.zi=value.xxx
                }
            }
        },
```

**简写**

**当只计算,不修改时 才可以简写**

```js
        computed:{
            //简写
            fullname(){ //function就是getter  ,fullname为声明的属性名
                return this.name.slice(0,3) +"_"+this.zi
            }
        },
```

## 监视属性

监控属性是否发生变化,监视的属性变化时,**回调函数自动调用**

监控的属性可以是**data里的属性,也可以是计算属性** ,但是必须存在

```js
//方法一: vm实例中写
	watch:{
            //被监控的属性,也可以监控计算属性 写成配置对象的形式
            isHot:{
                immediate:true,//当为true时,初始化时就调用一次handler
                //当监控对象isHot发生变化时调用
                handler(newvalue,oldValue){
                    console.log(newvalue,oldValue);
                }
            }
        }

//方法二 :通过单独的vm实例
        vm.$watch('isHot',{
            //配置对象
             immediate:true,
                handler(newvalue,oldValue){
                    console.log(newvalue,oldValue);
              }
        })
//简写      vm.$watch('isHot',function(){}) //function相当于handler
```

### 深度监视

```js
data:{number:{a:xx,	b:xx}}

//监视多级结构中的某个属性的变化
    "numbers.a":{ //使用原始的构造对象格式
      handler(){}
      }

//监视多级属性中所有属性的变化
      numbers:{
        deep:true,//开启深度监视,属性变化,就认为numbers变化
        handler(){}
        }

//简写形式 (不需要 immediate,deep情况下), 直接将监控属性写为函数形式
	isHot(newValue,oldValue){ //相当于handler
        
    }
	
```

## watch与computed

**计算属性可以直接对现有属性计算得出新的属性;但是监视属性可以异步操作数据**

**computed能做的watch都能做;watch额外能做异步操作**

**vue管理的函数,最好写成普通函数,这样this指向vm或组件实例对象**

**不被vue管理的函数,(定时器的回调函数,ajax的回调函数,Promise的回调函数),最好写成箭头函数,这样,保证this还是指向vm或组件实例对象,不被更改**

## 绑定样式

### 绑定class

给样式v-bind/:绑定,再绑定事件进行修改 

**字符串写法,样式类名不确定,需要动态绑定**

**class = "xxx" ,可以是字符串,对象,数组**

```JS
<div class="box" :class="box1"></div>
vue的data里声明box11,通过methods进行修改box1的值,从而修改class的值
```

**数组写法,适用于要绑定的样式个数不确定,名字也不确定**

```js
//要变更维护的类放在classArr数组中,放在vue的data中
<div class="box" :class="classArr"></div> 

```

**对象写法,适用于样式个数确定,名字确定,动态决定是否使用**

```js
obj:{box1:false,	box2:true}
//classobj对象样式存在vue的data中,用false/true选择是否使用
<div class="box" :class="classobj"></div>
```

### 绑定style

数组写法 :style= "[a,b]" a,b是样式对象

对象写法 :style="{ fontSize:xxx}

```JS
styleobj:{backgroundColor:'red'} //小驼峰命名法
//将样式key:value写在styleobj对象内
<div class="box" :style="styleobj"></div>
```

## 条件渲染

**满足某些条件才进行渲染**,当xxx为true/false时进行对应节点渲染操作

**v-show**="xxx"

​		根据等式后的代码的bool值决定元素是否设置**display=none**来显示隐藏元素

适合节点切换频繁

**v-if**="xxx"

​		如果等式结果为false,则将**整个元素的结构消除**,在DOM中增删节点

```js
//vue提供的模板标签,当v-if成立时将template里的内容渲染,但并没有template标签自身,便于操作一系列需要相同条件才渲染的元素   
仅能配合v-if使用
<template v-if="">
            <div>
                
            </div>
</template>
```

**v-else-if**="xxx"

​		当v-if节点条件不满足时,来判断v-else-if的节点。若v-if的条件满足，跳过所有（?)v-else-if的节点

**v-else**

​		不用跟判断,当v-if,v-else-if都不满足时,自动渲染v-else的节点

当一组条件判断结构中间掺杂其他节点被打断时,后面的判断都不奏效,**不渲染**

## 列表渲染

v-for = "( item ,index) in XXX"  :key="kkk"

​		key必须是唯一,不重复的值

XXX可以是, 遍历**数组,对象,**字符串,指定次数

v-for中有两个参数每一个是xxx里的对象/数组 ,另一个是对象在xxx里的索引值

### key

key是虚拟DOM的标识,当数据发生变化时,新旧DOM可进行对应的对比

**应尽量使用数据的唯一标识作为key,若不存在对数据的逆序修改,使用index作为key可以**

### vdom对比

1.拿新旧同key的DOM进行对比,相同部分直接复用页面的真实DOM,不同部分进行生成新的dom替换旧的,

2.新key没有可比较的就直接生成新DOM,渲染到页面 

虚拟DOM里并没有真实页面DOM的值value,**仅比较节点?**

### index作为key的问题

当index的顺序被逆序增加,逆序删除破坏

​	1.在对比时生成新DOM,效率低

​	2.若有输入类DOM,会产生错误的DOM更新

**当修改数据破坏index值时,index不适合作为key** 

![key](F:\新建文件夹\学习\前端\前端\VUE\key.png)

**选用数据的唯一标识作为key**

![1632646064553](F:\新建文件夹\学习\前端\前端\VUE\key_id.png)

### 列表过滤

列表循环的属性可以是监控属性,计算属性

通过对原数据的监控/计算,将过滤后的属性返回给列表渲染

### 列表更新问题

**vue检测数据更新原理**

​	vue创建一个监控对象实例,将监控对象的数据放到实例上,监控对象实例_data作为中转

​	监控对象内部的对象同样能够监测到,给检测到的对象都添加get(),setter()

响应式对象:

vue可以用**Vue.set(obj,key,value)	,vm.$set(obj,key,value)**向vm中的**响应式属性中添加新的响应式属性**,但是不能向vue实例或vue实例的根对象中添加

数组:

vue更新数组里的数据要想让vue知道,需要用到**修改原数组的方法**,:push,shift,splice...

#### Vue监视数据的原理

vue监视data中所有层次的数据,

**监测对象中的属性**

​	通过setter监视,在new vue时就传入要监视的数据,vue会给**每个对象属性配置get,set**

​	对象直接追加的属性不是响应式的; 要**添加响应式**属性需要使用api:

```js
Vue.set(target, propetyName/index, value);
this.$set(target, propetyName/index, value);
```

**监测数组中的数据**

​	通过**包裹重载更新元素的方法**实现,新方法:

​		1:调用原生对应方法对数组进行更新

​		2:重新解析模板,进而更新页面

​	**vue修改数组元素方法**:

​		1.使用包裹后的修改原数组的api:

```js
	push(),pop(),shift(),unshift(),splice(),sort(),reverse()
	
//	非修改原数组的方法filter(),...:可以将返回的数组,替换掉原数组
```

​		2.使用Vue.set() /vm.$set()

**Vue.set() /vm.$set()不能向vm或vm的根对象中添加**

## 收集表单数据

用户可以输入的数据直接v-model收集数据

对于用户不能输入的表单需要配置value

```html
<input type="text">
	v-model收集的是value,就是用户输入输入的value
<input type="radio" value="">
	v-model收集的是value,需要配置value
<input type="check" value="">
	若v-model初始值是非数组,则v-model收集的是多选框是否选中true/false
	若v-model初始值是数组&&则收集各个value形成的数组

v-model的修饰词
	lazy:当元素失去焦点时,再收集数据
	number:对输入的数据进行转换为number类型
	trim:对输入的数据过滤首尾空格
```

## 过滤器

对一些数据进行格式化后在显示,**适用于简单的处理**

过滤器可以串联 

```js
//注册过滤器
Vue.filter(name,function(value){}) //全局过滤器
new vue{ //局部过滤器
    filters:{}
}
//使用
{{xxx | 过滤器名 [| 过滤器名]}}
v-bind:属性 = "xxx | 过滤器名 [| 过滤器名]"
```

过滤器可以自己传入参数,但是**默认xxx永远是传入的**,并不改变原数据,而是return过滤后的数据