## Bom

浏览器对象模型,通过js操作浏览器

提供了一组对象来完成浏览器的操作:

Window,

​	整个浏览器的窗口,也是浏览器的全局对象

Navigator,

​	代表当前浏览器的信息集合对象,可以识别不同浏览器

Location,

​	代表地址栏,可以后的地址栏信息,跳转

History,

​	代表浏览器的历史记录,可以通过该对象操作浏览器历史。由于隐私原因，不能获取具体历史，只能向前或向后翻页，当次访问有效

Screen

​	代表用户屏幕信息，通过该对象可以访问到用户浏览器信息

**这些对象都是window的全局对象，可以通过window对象过直接访问**

## navigator

判断浏览器: 

1.  navigator.userAgent

​	正则判断 : /firefox/i.test( navigator.userAgent)

谷歌:

​	Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36

火狐:

​	 "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0" 

edge:

​	Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36 Edg/93.0.961.44

IE:

​	"Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; rv:11.0) like Gecko"

2. 通过浏览器特有对象

   IE独有:window.ActiveXObject

   ​	"ActiveXObject" in window   = true/false

## History

用来操作浏览器向前向后翻页

```js
//当前访问过的url的个数
history.length
//返回上一个页面
history.back()
//返回下一个页面
history.forward();
//跳转到指定的历史网页中
history.go(1/-1); //向前/后跳转一个页面
```

## Location

封装了地址栏信息

```js
//地址栏完整路径,直接打印
location

//直接修改会让网页进行跳转
location = "url"

//加载新网址,与直接修改location效果相同
location.assign(url);
//重新加载当前页面. 当参数为true时,强制清空缓存刷新
location.reload()
//使用新页面替换当前页面,也会跳转,不生成history不能回退
	location.replace()

```

## 定时器

```js
//定时调用,每隔时间执行一次,会返回number的数字来标识定时器
var time = setInterval(function(){},3000); //参数1:执行的回调函数  参数2:间隔时间毫秒
//取消标识对应的setInterval设置的定时器
clearInterval(定时器标识数字time)


//计时器 指定时间后执行
time =setTimeout(function, milliseconds)
//取消setTimeout的设定
clearTimeout(time)



//多个对象定时,自己可见自己的定时器
将定时器的表示放入obj中,
    obj.timer = setInterval
```

