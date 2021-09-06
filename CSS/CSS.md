## CSS

是用于渲染HTML**元素标签**的样式。通常用于连接到外部样式表。

### 用法：

- 内联样式- 在HTML元素中使用"style" **属性**

  ​	对于每一个标签元素定义样式

- 内部样式表 -在HTML文档头部 <head> 区域使用<style> **元素** 来包含CSS

  ​	定义全局基本样式

- 外部引用 - 使用外部 CSS **文件**

  ```html
  <head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
  </head>
  ```

最好的方式是通过外部引用CSS文件.

## 图像

```html
<img src="url" alt="some_text" width="" height=">
```

alt用于当图片加载失败时,显示"some_text"作提示。

src：文件路径注意。相对路径/绝对路径

设置图片大小(相对/绝对)保持页面整体布局

假如某个 HTML 文件包含十个图像，那么为了正确显示这个页面，需要加载 11 个文件。加载图片是需要时间的，所以我们的建议是：慎用图片。

图像映射:图像可以点击作为链接。

```html 
<img src="planets.gif" width="145" height="126" alt="Planets" usemap="#planetmap">
<map name="planetmap"> 
	<area shape="rect" coords="0,0,82,126" href="sun.htm" alt="Sun">  
    <area shape="circle" coords="90,58,3" href="mercur.htm" alt="Mercury">
    <area shape="circle" coords="124,58,8" href="venus.htm" alt="Venus">
</map>  
```

<map> 标签用于客户端图像映射。图像映射指带有可点击区域的一幅图像。

<img>中的 usemap 属性可引用 <map> 中的 id 或 name 属性（取决于浏览器），所以我们应同时向 <map> 添加 id 和 name 属性。

area 元素永远嵌套在 map 元素内部。area 元素可定义图像映射中的区域。

## 表单和输入

用于获取用户操作信息

常用name标记(id-JavaScript,name-aspPHP,class区别)

```html
<form>
<input type=" ">
<form>
```

表单中的单选按钮可以设置以下几个属性：value、name、checked

-  value：提交数据到服务器的值（后台程序PHP使用）
-  name：为控件命名，以备后台程序 ASP、PHP 使用
-  checked：当设置 checked="checked" 时，该选项被默认选中

```html 
<form>
<p>你生活在哪个国家？</p>
<input type="radio" name="country" value="China" checked="checked">中国<br />
<input type="radio" name="country" value="the USA">美国
</form>
```

## 框架

用于一个窗口显示不止一个页面

```html
<iframe src=" "> </iframe>
```

## 脚本

<script>声明</script>
## 字符实体

| 音标符 | 字符 | Construct | 输出结果 |
| :----- | :--- | :-------- | :------- |
| ̀       | a    | a&#768;   | à        |
| ́       | a    | a&#769;   | á        |
| ̂       | a    | a&#770;   | â        |
| ̃       | a    | a&#771;   | ã        |
| ̀       | O    | O&#768;   | Ò        |
| ́       | O    | O&#769;   | Ó        |
| ̂       | O    | O&#770;   | Ô        |
| ̃       | O    | O&#771;   | Õ        |

| 显示结果 | 描述        | 实体名称          | 实体编号 |
| :------- | :---------- | :---------------- | :------- |
|          | 空格        | &nbsp;            | &#160;   |
| <        | 小于号      | &lt;              | &#60;    |
| >        | 大于号      | &gt;              | &#62;    |
| &        | 和号        | &amp;             | &#38;    |
| "        | 引号        | &quot;            | &#34;    |
| '        | 撇号        | &apos; (IE不支持) | &#39;    |
| ￠       | 分          | &cent;            | &#162;   |
| £        | 镑          | &pound;           | &#163;   |
| ¥        | 人民币/日元 | &yen;             | &#165;   |
| €        | 欧元        | &euro;            | &#8364;  |
| §        | 小节        | &sect;            | &#167;   |
| ©        | 版权        | &copy;            | &#169;   |
| ®        | 注册商标    | &reg;             | &#174;   |
| ™        | 商标        | &trade;           | &#8482;  |
| ×        | 乘号        | &times;           | &#215;   |
| ÷        | 除号        | &divide;          | &#247;   |

[html字符实体参考手册]: https://www.runoob.com/tags/ref-entities.html

 [HTML ISO-8859-1 参考手册 | 菜鸟教程 (runoob.com)](https://www.runoob.com/tags/ref-entities.html) 

url字符编码 [HTML ISO-8859-1 参考手册 | 菜鸟教程 (runoob.com)](https://www.runoob.com/tags/ref-entities.html) 

### 常用速查内容:

 [HTML 速查列表 | 菜鸟教程 (runoob.com)](https://www.runoob.com/html/html-quicklist.html) 

```html
基本标签（Basic Tags）
<h1>最大的标题</h1>
<h2> . . . </h2>
<h3> . . . </h3>
<h4> . . . </h4>
<h5> . . . </h5>
<h6>最小的标题</h6>
 
<p>这是一个段落。</p>
<br> （换行）
<hr> （水平线）
<!-- 这是注释 -->
```

文本格式化（Formatting）

```html 

<b>粗体文本</b>
<code>计算机代码</code>
<em>强调文本</em>
<i>斜体文本</i>
<kbd>键盘输入</kbd> 
<pre>预格式化文本</pre>
<small>更小的文本</small>
<strong>重要的文本</strong>
 
<abbr> （缩写）
<address> （联系信息）
<bdo> （文字方向）
<blockquote> （从另一个源引用的部分）
<cite> （工作的名称）
<del> （删除的文本）
<ins> （插入的文本）
<sub> （下标文本）
<sup> （上标文本）
```

