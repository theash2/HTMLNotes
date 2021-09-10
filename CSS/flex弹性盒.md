## 弹性盒flex

一种布局手段,主要用来代替浮动。CSS3中的新属性，兼容性

可以使元素具有弹性，跟随页面大小而改变

**弹性容器**

​	要使用弹性盒，必须将一个元素设置为弹性容器

​	 display: flex; 	**块级**

​     display: inline-flex;	行内级



弹性元素

​	弹性容器的**直接子元素**就叫作弹性元素（弹性项）

​	一个元素可以即是弹性容器，也是弹性子元素

**弹性盒样式:**

```css
//指定容器中弹性元素的排列方式
	flex-direction: ;
			row 默认值,水平排列
			row-revers 水平排列,自右向左
			column 纵向
			column-rever 反向纵向,自下向上
	主轴:弹性元素的排列方向
	侧轴:与主轴垂直的方向

//设置弹性元素是否自动换行
flex-wrap: ;
	none
	wrap 沿侧轴方向换行
	wrap-reverse 沿侧轴反方向换行

简写 flex-flow: 排列方向direction 是否换行方向wrap;

//分配主轴空白空间,元素如何排列
	justify-content:;
		flex-start 沿主轴开始方向排列
		flex-end 沿主轴结束方向排列
		center 元素居中,空白两端
		space-around 空白分布到每个元素两侧
		space-evenly 空白分布到每个元素单侧  兼容性
		space-between 空白分布到元素之间 

//元素在侧轴如何对齐, 设置元素间的垂直距离
	align-items:;
		stretch		一行内的元素侧轴高度一样长
		flex-start		元素不再拉伸,沿着侧轴起边对齐
		flex-end		沿着侧轴终变对齐
		center		居中

水平垂直居中 justify-content,align-items:center;

//元素在侧轴方向上的空白分配
	align-content:;
		flex-start 沿侧轴开始方向排列
		flex-end 沿侧轴结束方向排列
		center 元素居中,空白两端
		space-around 空白分布到每个元素两侧
		space-evenly 空白分布到每个元素单侧  兼容性
		space-between 空白分布到元素之间 
```

**弹性元素样式属性:**

```css
//弹性元素伸展系数,父元素的<b>剩余空间<b/>会根据各个子元素的flex-grow比例进行分配
flex-grow:;		
	0 保持原样,不伸展
//缩短系数,父元素空间不足容纳所有元素
flex-shrink:;
	0 不收缩

//弹性元素自身的align-items
	align-self:;	值同align-items,覆盖弹性容器上的align-items

//指定元素主轴方向基础长度width/height
	flex-basis: ;
		auto 默认

简写  flex : flex-grow  flex-shrink  flex-basis
			initial; "0 1 auto"
			auto; 	"1 1 auto"
			none ; "0 0 auto"

//指定弹性元素的排列顺序	主轴方向,order由大到小
	order:;
```

