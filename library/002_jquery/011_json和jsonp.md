# json和jsonp
## json
是一种数据的结构化写法，用于前后台数据交互的一种数据格式
```javascript
var jsonData=[
  {name:"zhangsan",age:"14"},
  {name:"wangwu",age:"23"},
  {name:"lisi",age:"13"}
]
```
·
## jsonp  （json with padding包裹）
- 前后台交互的一种数据传输方式
- 解决跨域问题；ajax不能跨域请求（同源策略，一般只能请求位于同一域名下的数据，协议+主机名+端口号必须都一致才是同源。也有例外，比如天气api就允许ajax跨域访问数据）
```
http://www.xxx.com
https://www.xxx.com
http://www.xxx.com:80
http://www.aa.xxx.com
http://www.xxx.com/aa/bb  和第一个同源
```

#### jsonp获取数据原理
- ajax获取不了跨域资源，但是script标签可以
- 通过script标签去加载资源的时候，是没有跨域问题的，但是获取的资源只能看，不能获取到使用
- 先声明一个函数a，然后用php输出函数的调用"echo ‘a()’;"
- 用webstorm打开访问wrmp的www目录下的文件
###### html
```html
<script>
  function aa(data){
    console.log(data);
  }
</script>
<script src="localhost/jsonp/a.php?callback=aa"></script>
<!-- 别的域下的文件路径，把函数的定义传到php，php输出函数的调用 -->

```
###### php
```php
<?php  
  $file=file_get_contents("city.json");
  $cb=$_GET['callback'];
  echo $cb."(".$file.")";     传出 aa()
?>
```

#### 封装jsonp
```javascript
function jsonp(option){
  var url=option.url;
  var data=opation.data||"";
  var jsonp=option.jsonp||"callback";
  // 只是一个函数名，在当前环境被调用，函数名为了防止冲突，意外调用其他函数所以使用时间戳
  var jspnpCallback=option.jsonpCallback||"j"+new Date().getTime();
  // 如果有data url?a=b&callback=ss
  if(data!=""){
    url+="?"+data+"&"+jsonp+"="+jsonpCallback;
  }else{
    url+="?"+jsonp+"="+jsonpCallback;
  }
  // 创建script标签
  var script=document.createElement("script");
  script.src=url;
  document.head.appendChild(script);
  // 不写这个方法，会报错  因为函数还没声明就调用
  window[jsonpCallback]=function(r){
    console.log("函数会调用执行");
    option.success(r);
    delete window[jsonpCallback];
    document.head.removeChild(script);
  }
}
jsonp({
  url:"http://localhost/...../demo.php",
  data:"aa=1",
  jsonp:"callback", //用于php接收
  jsonpCallback:"aa",//发送到php的函数名
  success:function(r){
    console.log(r); //跨域数据取回
  }
})
```
