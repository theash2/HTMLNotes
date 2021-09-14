## AJAX

异步的JS和xml;

一种不刷新整个网页的数据更新技术方式,允许根据用户时间来更新部分页面内容

~没有浏览历史,存在跨域问题,SEO搜索引擎优化不友好



### XML

可扩展标记语言,被用来设计传输和存储数据,类似HTML,但是没有预定义标签,都是**自定义标签**

### JSON

替代了JSON,数据格式更好

## **使用**

### get

```js 
1.创建对象		readystate:0
	const xhr =new XMLHttpRequest();
2.初始化	设置请求方式和url     readystate:1
	xhr.open('GEt','url');
3.发送		readystate:2
	xhr.send();
4.事件绑定	处理服务器端返回的结果	readystate:4
//statechange:0 1 2 3 4
    xhr.onreadystatechange = function(){
            //服务器返回所有结果
            if(xhr.readyState === 4){
            //判断是否成功 2xx
            if(xhr.status >= 200 && xhr.status<300){
				X
            }else{}

            }
        }


X //判断成功后处理返回的结果 行 头 空行 体
//1.响应行
	console.log(xhr.status); //状态码
	console.log(xhr.statusText); //状态字符串ok
	console.log(xhr.getAllResponseHeaders()); //所有响应头
	console.log(xhr.response); //响应体
```

### 设置url参数

```json
xhr.open('GEt','url?参数名=value&参数名2=value2');
```

### post

```json
var xhr = new XMLHttpRequest();
 xhr.open("post","url");
//设置请求头,可设置多个
 xhr.setRequestHeader('name','value');
	xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded'); //Content-Type: text/html; charset=utf-8

//设置参数在方法send()中,也可以不设置参数
	xhr.send('a=100&b=200'); //或者键值对形式 a:100&b:200

	xhr.onreadystatechange = function(){
         if(xhr.readyState==4){
           if(xhr.state>=200 && xhr.state <300){
                        
                     }
               }
            }
        }

//设置请求头信息
	
```





```js
app.all() //接受所有类型的请求信息
```

### 服务端响应JSON数据

```json
//服务器响应数据
    //设置数据
    const data={
        name:"fjisdj",
        age:"14"
    }
    let str = JSON.stringify(data); //转换为字符串形式发送
    response.send(str); //响应端返回数据 

//前端对返回的JSON类型数据处理
  //1.手动转换
	let data = JSON.parse(xhr.response); //返回的字符串转换为JSON类型
	console.log(data);
	box.innerHTML = data.name + data.age ; //获取JSON数据的内容
  //2.自动转换,需要设置xhr.responseType="json"
	这样返回的xhr.response就已经是JSON类型了
	
```

### IE缓存问题

IE浏览器会对ajaxGET请求返回的第一次数据进行缓存,在下一次同一url请求时会将缓存的数据显示,影响时效性

解决

```js
//添加时间戳,让浏览器每次访问都不一样
xhr.open('get','http://127.0.0.1:8000/ie?t'+Date.now());

```

### 请求超时和异常网络处理

```javascript
//设置延时取消
xhr.timeout =2000;

//超时的回调函数
 xhr.ontimeout = function(){
    alert("超时重试");
      }
//网络异常
    xhr.onerror =function(){
         alert("网络异常");
        }


```

### 其他处理

```JS
//取消请求
xhr.abort();

//取消重复请求,取消前一个
加上状态判断 issend = false;
在发送前判断是否为true,为true表示已有,需要 xhr.abort();
在发送后将状态码置位true
在接收数据,xhr.readyState ==4 时 将issending恢复为false;
```

## JQuery_AJAX

```js
//get     
对象.click(function({
            $.get('url',{a:100},function(data){ 
            },'json'), //参数:地址 对象类型参数 回调函数 返回体类型
        }))
        
//post
        对象.click(function({
            $.post('url',{a:100},function(data){
            }) //地址 对象类型参数 回调函数
        }))
        
//通用AJAX方法发送请求
      .click(function({
         $ajax({
            //参数是对象类型设置请求参数
            //地址
            url:'',
            //参数
            data:{a:100,b:100},
            //请求类型
            type:'GET',
            //响应体结果类型
            dataType:'json',
            //成功的回调函数
            success:function(data){},//响应体数据 
            //超时设置
            timeout:2000,
            //失败函数
            error:function(){},
          	//头信息
          headers:{}
         });
        }))
```

## AJAX/axios

```js
//get
            axios.get('http://127.0.0.1:8000/axios',{
                //参数
                params:{
                    id:100,
                    name:'axios',
                    time:Date.now()
                },
                //请求头信息
                headers:{
                    name:'晨灰',
                    age:20,
                }
            }).then(value=>{ //处理返回数据
                console.log(value);
            });

//post  axios#post(url[,data[,config]])
            axios.post('http://127.0.0.1:8000/axios',{
                //data
                user:'name',
                pasw:'www'
            },{//config
                //参数
                params:{
                    id:100,
                    name:'axios',
                    time:Date.now(),
                    type:'post'
                },
                //请求头信息
                headers:{
                    name:'ash',
                    age:20,
                }
            }).then(value=>{
                console.log(value.data);
            });

//通用方式
            axios({
                method:'post',
                url:'http://127.0.0.1:8000/axios',
                params:{
                    name:'chenhiu',
                    pasw:123654
                },
                headers:{
                    name:'header',
                    use:'check'
                },
                //请求体参数
                data:{
                    username:'admin',
                    pas:'password'
                }
            }).then(resoponse =>{
                //处理返回内容
            })
```

## AJAX/fetch

```js
           fetch('http://127.0.0.1:8000/fetch[?p1=1&p2=2]',{
               method:'post',
               headers:{
                   name:'chenhui',
                   way:'request'
               },
               //请求体
               body:'user=123&pass=098'
           }).then(response=>{
               //调用方法显示响应体内容
               return response.text();
           }).then(response=>{
               console.log(response)
           })
```

## 同源策略

协议,端口,域名相同才能访问

### 解决跨域

#### JSONP

通过一些默认支持跨域的标签实现,img,script,只支持get

script src="url"访问,url返回js语句供前端直接解析执行

```js
        const script = document.createElement("script");
        script.scr="url"; //访问的地址:端口
		document.body.append(script); //插入网页,进行访问
```

**jQuery/jsonp**

记得引入jQuery

```js
        $.getJSON('url?callback=?',function(data){
	//处理返回的data数据
        })
        // 后端接收callback
        let cd = response.query.callback;
```

#### CORS

官方的跨域请求方式

后端需要设置响应头

```js
//设置响应头 允许跨域

  response.setHeader('Access-Control-Allow-Origin','*');
response.setHeader('Access-Control-Allow-Method','*');
response.setHeader('Access-Control-Allow-Headers','*');
```

