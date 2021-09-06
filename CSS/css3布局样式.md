## 边框

border 外边框 随圆角变化

outline 轮廓 :不影响可见框大小

## 阴影

box-shadow 设置盒子的阴影 :不改变盒子大小

​					0 0 10px	rgba()

​						:value1水平偏移量  value2垂直偏移量 value3阴影模糊值  颜色 value4 模糊颜色

​							value>0||value<0

## 圆角

border-radius: value value value value 顺时针方向

​						value-x/value-y 四个角的

​						value value 左上/右下  右上/左下

border-top-left-radius:value-x value-y 圆角的x,y方向半径

border-top-right-radius:

border-bottom-left-radius

border-bottom-right-radius

## 浮动

**宏观**

设置float非none时,布局的等式就不必成立

设置float后,元素会脱离文档流,不占据文档流中位置

​		脱离文档流:不在区分块元素与行内元素

​			块元素不占一行,宽高取决于内容

​			行内元素类似块元素,可设置宽高

**可以使多个元素水平排列**

float

float不会盖住文字,所以可以设置文字浮动效果

#### 高度塌陷

父元素width,height不固定,子元素设置float脱离文档流,会使父元素高度塌陷,即父元素区域预期之外缩减,高度丢失。

解决：

​	1.父元素高度写死

​	**2.BFC（Blocking Formating context）块级格式化环境**

​		CSS的隐含布局属性。开启BFC的元素成为独立的布局区域。

​		特点：**开启BFC的元素不会被浮动元素覆盖**

​					开启BFC的元素子元素和父元素（hidden）外边距不会重叠

​					**开启BFC的元素可以包含浮动的子元素**

​		方式：通过特定属性的设置

​					1.float		！宽度也会取决于子元素

​					2.display：inline-block		！有行与块的特点和缺点

​					**3.overflow：非visible（推荐）**  overflow：hidden

​	3.属性clear				

​		清除浮动元素对**当前元素**的影响(浏览器为元素添加上外边距,使其位置不受影响)

​		可选:left 清除左侧浮动对此元素的影响

​				right

​				both 两侧中影响较大的

​	4.::after伪类clear浮动元素的影响

​				父元素::after{

​					content:' ';

​					display:block;

​					clear:both;}

​	5.classfix解决外边距重叠和高度塌陷

```html
.classfix::before,.classfix::after{
context: ' ';
dispaly:table;//设置为表格,内容为空时不占空间
clear:both;
}
```

解决外边距重叠2:

​	外边距设置border

## 定位

**微调**

position 更高级的布局手段,可以将元素摆放到页面任意位置,不影响布局和其他元素位置.

**相对布局的坐标参照为自己文档流中位置,即自身原位置**

相对布局会提升元素层级,但不脱离文档流,不改变块或行性质

​			开启position后可以通过偏移量(offset)改变自身位置



offset:和标椎定位位置的距离

​			**top**

​			bottom

​			**left**

​			right

可选值:

​			static 默认值,未开启定位

​			relative 开启元素相对定位

​					需设置偏移量

​			absolute 开启元素绝对定位

​			fixed 开启元素固定定位

​			sticky 开启元素粘滞定位

### 相对定位

相对于元素原位置的偏移

坐标原点为元素左上角

### 绝对定位

**元素脱离文档流,宽高被内容撑开;是元素提升一个层级**

元素坐标相对于包含块

包含块:

​			正常的包括块:离当前元素最近的**祖先块**

绝对定位的包含块:

​			离它最近的开启了定位的祖先元素,直至根元素

### 固定定位 fixed

属于一种绝对定位

**永远参考浏览器可视窗口定位** ,如侧边导航栏

### 粘滞定位 sticky

和相对定位类似

随页面滚动条滑动后,到达一定位置后固定

### 层级z-index

对开启了定位的元素设定层级;值越大,越靠上

祖先元素层级必定小于后代元素

## 字体font

颜色:color(前景色)

font-family:字体1,字体2, . . .大类

## 图标字体icon

将图标设置为字体,通过font-face引入

1.通过CSS和webfont文件引入,link引入HTML,在标签中设置class

2.设置伪元素::XXXX{

content:'\编码';

//fas:Font Awesome 5 Free

fab: Font Awesome 5 Brands

font-family:' ';

//fas:

font-weight:900;

}

3.class引入fas/fab,然后通过实体码引入&#x图标码;

## 文本

水平对齐:	text-align: justify 两端对齐  

垂直对齐:	vertical-align:baseline 基线对齐

​										top	父子元素顶部对齐

​										bottom  父子元素底部对齐

​										middle 居中对齐;子元素中线和基线对齐

​										100px;

over-flow:hidden

设置网页空白: white-space: normal

​											nowrap 不换行

​											pre 保留文本格式,空行,空格全保留

设置文本多余:text-overflow :ellipsis 显示". . . "

## 背景

background-img:url("")

background-repeat: 背景图片重复方式

​								repeat,	repeat-x,	 repeat-y,	no-repeat

background-position: **top center right bottom left 的两两组合**控制图片位置

​								或水平-垂直的偏移量,	类似阴影

backgro-clip:	设置背景范围

​						border-box:	背景会出现在边框的下边

​						padding-box	背景仅在内容区和内边距

​						content-box	背景仅在内容区

background-origin:	背景图片偏移量计算的原点

​									padding-box	content-box	border-box	

background-size:	背景图片尺寸

​								width-height,	cover保持图片比例将元素覆盖,	contain图片比例不变,是图片完整显示

background-attach:ment	背景图片是否随着元素滚动条移动								

​								scroll,	fixed

**雪碧图**

​	1.一次加载大图

​	2.为图片设定对应空间

​	3.将背景图移入对应空间中

## 渐变

**渐变是图片**,可以同时制定多张颜色,默认平均分配, 也可以在颜色后指定开始渐变的位置

线性渐变:

​				background-image: linear-gradient([ control,]red起始色,yellow导向色);

​						to left,right,bottom,top;	XXXdeg多少度线性																	                            

线性重复渐变:background-image: repeating-linear-gradient(red,blue); 在颜色后指定位置后对整个区域进行均分

径向渐变:

​				向多个方向渐变

​			 background-image:radial-gradient([ value1,value2,]	skyblue中心色,black)

​												value可以指定径向渐变的大小

​												value设定circle/ellipse指定形状

​												指定圆心位置value1,value2 at left . . .

​												closest/farthest-side/corner at value指定渐变规模