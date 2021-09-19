## JSON

javascript object natation  : js对象表示法

就是字符串,能够被所有语言识别的字符串,并可以被转换为对象

主要用于数据储存,交互,传递

**格式类似js的对象,但是属性名必须加双引号**

属性:**对象{} 数组[]**

json允许的值:**字符串,数组,布尔值,null,普通对象,数组**

​		**undefined和函数不允许**

转换:JSON工具

​	js对象->JSON  ;

```
str = JSON.stringify(obj);
```

 JSON->JS对象

```
obj = JSON.parse(json_str);
```

**兼容性 >IE7**

​	方式一:(不推荐)

```
eval(str) :执行字符串形式的JS代码,并返回结果 ,不希望当成代码块需要字符串前后加上( )

​		eval()执行的字符串中含有{}时,会将{}当成代码块eval("("+str+")")
```

​	方式二:引入外部js文件

