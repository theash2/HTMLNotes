# 样式

### 内联样式

style:键值对.写在行内标签属性内

### 内部样式

写在<head></head>标签内,单独设置style标签为对应标签生效;修改一处可全部应用;对当前页面生效

```HTML
<style>
    p{color:red}
</style>
```

### 外部样式

引入专门的CSS文件,网页需要将其引入.在head标签中引入

```html
<link rel="stylesheet" href="">
```

# 选择器

选择页面中的指定所有相同元素,即元素

## 常用选择器

### 元素选择器

根据**标签名**选中指定的元素:p{};div{};h1{};

### id选择器

根据元素的id(唯一标识)来选择元素:**#id属性值{}**

#box{};#id_value{};

### **class/类选择器**

根据元素的class(可重复)来选择元素:**.class属性值{}**

也可以为一个元素指定多个class:class="class1 class2"

### 适配选择器

选中页面中所有元素:*{};

## 复合选择器

通过筛选元素的class选中元素:**元素.class值**

div.red{};

### 交集选择器

多个选择器,满足所有条件的被选中

交集选择器中有元素选择器的要把元素选择器放在第一个

div.class1.class2.classn{};

### 选择器分组/并集选择器

多个选择器,满足其一的被选中;选择多个选择器:选择器1,选择器2,选择器n{};

h1,span{};red,greed{};

## 关系选择器

#### 父子元素

直接互相包含的2个元素.

#### 祖先后代

直接或间接包含后代的元素的元素,可以间隔不止一层,可以有多个祖先或后代

#### 兄弟元素

拥有相同父元素,即在同一父元素下的元素

### 子元素选择器

选中父元素中的**子元素**:**父元素>子元素**

### 后代选择器

选中指定元素下的**后代元素**:**祖先 后代**

### 选择下一个兄弟

根据兄弟元素相对位置选择**后一个兄弟元素**:**前一个胸兄弟元素+后一个兄弟元素**

### 选择所有兄弟

根据兄元素选择**所有弟元素**:兄 ~ 弟元素

## 属性选择器

特定标签含有特定输定的元素被选中:**标签名**/*(所有)**[属性名**(=value)**]**

属性值^=value:选中以value开头的属性值

属性值$=value:选中以value结尾的属性值

属性值*=value:选中属性中含有value的属性值

### 伪类选择器

伪类:描述一个元素的状态,被点击,第几个

ul>li**:first-child**{

}

以:开头**:first-child :nth-child(2n+1)**(根据经所有子元素排序)

:first-of-type(同类型)

:not(:nth-child()) 排除所有满足的元素

:hover 鼠标移动状态

:link{} 连接颜色

:visited{}

:active{}

### 伪元素

页面中一些**特殊状态**的元素

### 伪元素选择器

p::first-letter{}

::first-line{}

::selection{} 被选中时

**::before{} 元素的开始位置**

**::after{} 元素的结束位置**

## 声明块 

为选择器选择的元素设定样式

块中可以多个样式声明

一个样式名:一个样式值;

## 继承

背景相关的,布局不会继承给后代

background-color

## 选择器权重

内联样式>id选择器>类/伪类选择器>元素选择器>通配选择器>继承样式(没有登记)

比较优先级时,需要将选择器优先级相加进行比较,越高月有限显示(分组选择器单独计算)

越具体优先级越高

优先级相同时,优先使用后一个

样式后加"!important"将优先级提到最高

## 大小尺寸

px:单位像素大小

em:当前元素字体大小

rem:根元素字体大小

# 布局

## 盒子模型

CSS将页面中的所有元素设置为一个矩形的盒子,以内容区为主体布局

内容区content{

width:

height:

...

}

内边距padding

边框border{

border-width:value1 4个边宽度

​					value1(上) value2(右) value3(下) value4(左) 顺时针							方向4个边框宽度 

​					value1(上) value2(右,左) value3(下) 

​					value1(上下) value2(左右)

border-XXX-width: top left right bottom 单独指定一个边框

border-color:类似width

border-style:solid实线

​			dotted 点状虚线

​			dashed 虚线

简写:

border:10px color style

border-XXX:size color style

}

### 外边距margin

![](F:\新建文件夹\学习\前端\前端\boxmodel.png)

margin-XXX 和其他元素的距离

left,top:移动自身元素

right,bottom:移动其他元素空出距离

value可以为正或负,负值反向移动

margin:上 右 下 左 同border

### 内边距padding

padding-top/left/right/bottom

盒模型样式中设置

padding:上 右 下 左 同border

border+padding+content=盒子大小尺寸

### 水平布局

元素嵌套布局在父元素的内容区,水平方向布局与父元素有关

要布局主体元素content的属性:

margin-left

border-left

padding-left

width

padding-right

border-right

margin-right



水平方向上:

margin-left+border-left+padding-left+width+padding-right+border-right+margin-right=父元素content的width

等式不满足时会对margin-right自动调整

width,margin-left,margin-right可设置为auto,等式不满足时会调整auto的值:width优先级>margin-left,margin-right

### 垂直布局

垂直方向上:子元素大小超过父元素内容区大小,会溢出

**父元素**处理溢出:overflow属性;overflow-x,overflow-y 

​							超出父元素内容区就处理

hidden

scroll 滚动

auto 根据需要生成滚动条

相邻垂直的外边距重叠,两个元素的margin-bottom与margin-top

兄弟元素:可以不处理

相邻外边距一正一负,则两者和

​					都是正/负值,取绝对值最大的

父子元素:必须要处理

子元素的margin-top会传递给父元素

### 行内元素盒模型

不支持width,height

padding,border,margin不影响垂直方向

行内元素改变宽高方式:display:

inline 将元素认定为行内元素

block 将元素认为块元素

inline-block 既可以设置宽高,又不会独占一行

table 将元素设置为一个表格

none 元素不显示



去除网页默认元素

1:

*{

margin:0;

padding:0;

}

2:

清除样式表:引入重置样式表

<head>

<link rel="stylesheet" href="">

</head>