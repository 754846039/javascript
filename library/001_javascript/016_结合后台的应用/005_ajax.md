# AJAX
利用JavaScript异步机制来和数据进行交互（页面不刷新不跳转可以对数据来进行操作）

1. 应用场景：
  - 单页面应用
  - 涉及到复杂的数据操作、多次增删改查
2. 缺点
  - 对搜索引擎不太友好
  - 不能够应对大批量页面的载入，造成内存无法回收（所有的操作都在一个页面中）
3. 优点
  - 无跳转，提供连续流畅的用户体验

## 工具 wamp
- w windows系统   Linux系统
- a Apache 服务器
- m MySQL 数据库
- p php

#### 安装需注意
- 不要装到C盘
- 路径中不要出现汉字
- 图标绿色正常
- 右击可以选择语言
- 安装后打不开的情况
  - 缺少 msvcr110.dll
    - 解决：拷贝这个文件到 c->windows下
  - 出现错误0xc000007b  DirectX 文件损坏  
    - 解决：下载安装或修复DirectX，或者安装vc
- 图标为黄色 sql  apache  
  - 解决：iis tomcat关闭软件   
  - 计算机管理->服务和应用程序->需要关闭服务world wide web 、 iis、 sql关闭服务
- 关闭防火墙

## AJAX简介
#### 什么是AJAX  单线程异步机制的语言
- AJAX Asynchronous Javascript and XML 异步JavaScript和可扩展标记语言
- AJAX并非缩写词，而是由Jesse James Gaiiett创造的名词，是指一种创建交互式网页应用的网页开发技术。
- 在页面不刷新的情况下实现前台和后台的数据交互的一种技术，用js去获取数据，用DOM的方法操作文档的内容，通过xhr对象完成数据的发送，XML是数据发送时的一种格式
- 核心是JavaScript
- xml/json/text/html/md是数据发送时的有一种格式   标签语言的鼻祖，html是XML的扩展，XML专门用来存储数据，html展示数据
>在www文件中新建项目<br>
访问：localhost(本地域名)==127.0.0.1<br>
localhost/ajax/login.html

- 单页面，大量数据增删改查适合用ajax

#### 单线程异步机制
- 单线程，一次只能做一件事
- 异步
  - 正常线程代码执行完毕空闲下来的时候再去执行的代码为异步执行的代码
  - 模拟多线程，多线程不足：边打饭边收钱效率低，所以派10个收银员，成本增大
  - 一切需要耗费时间（时间函数）或者不确定执行（事件函数）的代码都是异步的
- 可以解决很多多线程解决不了的事情
- 单线程优势：
  - 把耗时的事情放到恰当时机去做
  - 打饭，吃饭完人少了再收款
  - setTimeout
  - 一切需要耗费时间或者不确定执行的代码都是异步的
- 单页面的处理，单线程异步需要等待正常代码执行，但是这点时间忽略不计，因为运行速度非常快
#### AJAX应用场景
1. 表单异步验证
  - 用来异步验证用户名是否存在等！
2. 深层次导航
	- 深层次的级联菜单（树）的遍历是一项非常复杂的任务，使用JavaScript来控制显示逻辑，使用Ajax延迟加载更深层次的数据可以有效的减轻服务器的负担
  - 比如智联上的地区选择
3. 快速的用户与用户间的交流响应
	- 可以实时显示用户交互状态
4. 类似投票系统
  - 能够在不刷新的前提下，得到投票后的结果
5. 普通的文本输入提示和自动完成的场景
  - 在文本框等输入表单中给予输入提示，或者自动完成，可以有效的改善用户体验，尤其是那些自动完成的数据可能来自于服务器端的场合，Ajax是很好的选择。   

## 进程和线程
- 进程
  - 每开启一个软件就是一个进程，进程的多少和CPU有关，开辟通道
  - QQ会开启多个进程，钉钉会开启8个进程
  - 河流，一条河无法承载水流量，所以需要再开辟一条河流来分流
- 线程
  - 一个进程可以开辟多个线程，推荐使用进程
  - 在河流的基础上开辟小溪

## 异步和同步
- 同步：按照顺序依次执行，在同一时间只能做一件事情（代码执行顺序与书写顺序一致）
  - 支付
  - php模拟网络延时，然后点击发送，请求未完成时不能点击
- 异步：同一时间可以处理多个问题
  - php模拟网络延时，然后多次点击发送，查看network的时间轴，看到同时执行

## b/s架构  c/s架构
- b/s 基于浏览器  数据的传递、交互需要不断发http请求
  - 无需下载更新
- c/s 基于电脑、客户端
  - QQ 更新
希望基于b/s架构的软件像基于c/s架构的软件一样操作方便

## 前后台交互模式
#### 传统的前后台交互模式
- form表单实现交互
- 前台提交数据 --> 后台接收数据处理返回数据 --> 刷新显示一个新的html页面（重定向）
- 案例
###### login.html
```html
<!-- html -->
<form method="get" action="login.php">
    <label for="account">账号：</label>
    <input type="text" name="account" value="" id="account">
    <label for="account">密码：</label>
    <input type="password" name="password" value="" id="password">
    <input type="submit" name="submit" value="提交">
<form>
```
###### login.php
>php识别html语法，可以直接写html<br>
>php中可以任意换行，一个语句结束必须写;分号。js中换行表示一条语句的结束
>{}后可不加分号

- 方式一
```html
<body>
<?php
  echo "hello world!";
  $account=$_GET("account");
  $password=$_GET("password");
  if($account=="admin"&&$password=="123456"){
    echo "登陆成功";
  }else{
    echo "登录失败";
  }
?>
</body>
```
- 方式二
```php
<?php
    $account=$_GET("account");
    $password=$_GET("password");
?>
```

#### AJAX 实现交互
- 网页不用刷新
- 所有的发送接收操作都通过XMLHTTPRequest对象来完成
- 操作DOM

##### 1. 创建AJAX / xhr对象的操作
- 大部分浏览器
```javascript
var xhr=new XMLHTTPRequest();
```
- IE6
```javascript
var xhr=new ActiveXObject("MicrosoftHTTP")
```
- 兼容
```javascript
var xhr=window.XMLHTTPRequest ? new XMLHTTPRequest : new ActiveXObject("MicrosoftHTTP");
```

##### 2. 配置请求
```javascript
xhr.open(requestType,url);
```
- 参数一：发送方式 requestType
  - get 传输数据量比较小，速度比较快，安全性比较低（把数据连接到地址栏的后面发送）
  - post 传输数据量比较大，速度比较慢，安全性相对较高（把数据插入到请求头信息里面发送）
- 参数二：发送地址 url
  - get方式：发送的内容要连接到地址的后面
- 参数三：asynch
  - true 异步连接（默认）
  - false 同步连接
- 参数四：username（如果需要身份验证，则可以在此指定用户名。该可选参数没有默认值。）
password：如果需要身份验证，则可以在此指定口令。该可选参数没有默认值

  ```javascript
  xhr.open("get","login.php?account=admin&password=123456")
  // ?查询字符串
  ```

  - post方式：只写地址
  ```javascript
  xhr.open("post","login.php")
  ```

##### 3. 发送请求
- get方式
```javascript
xhr.send([null])
```
- post方式
```javascript
// 设置头信息
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.setRequestHeader("Content-Type")
// 发送数据
xhr.send("account=admin&password=123456")
```
##### 4. 建立监听函数(异步)
>监听客户端和服务器交互的状态，即监听请求是否完成<br>
>接收响应

```javascript
/* 方法一 */
// ajax状态发生改变时触发
xhr.onreadystatechange=function(){
  // 响应完成
  if(xhr.readyState==4){
    // 响应成功
    if(xhr.status==200){
      // 接收数据
      var data=xhr.response;
    }
  }
}

/* 方法二 */
xhr.onload=function(){
  var data=xhr.response;
}
```
- `xhr.readyState` 检测HTTP就绪状态 (响应是否完成)

状态码 | 描述
---|---
0|请求没有发出（在调用 open() 之前）。
1|请求已经建立但还没有发出（调用 send() 之前）。
2|请求已经发出正在处理之中（这里通常可以从响应得到内容头部）。
3|请求已经处理，响应中通常有部分数据可用，但是服务器还没有完成响应。
4|响应已完成，可以访问服务器响应并使用它。
【注意】一定要放到send()之前

-  `xhr.status` 检测http状态码(响应是否成功)

状态码 | 描述
---|---
200|交易成功(OK)
201|提示知道新文件的URL(Created)
202|接受和处理、但处理未完成(Accepted)
203|返回信息不确定或不完整(Non-Authoritative Information)
404|页面未找到

- 接收服务器传回的信息 xhr.response

#### AJAX常用属性和方法
属性|描述
---|---
readyState|检测HTTP就绪状态（是否完成响应）
status|检测HTTP状态码（响应是否成功）
onreadystatechange|监听请求是否完成
responseType|指定接收数据格式 text/json/document 通过arrayBuffer形式接收
response|接收响应
responseText|接收文本格式的数据
responseXML|接收XML格式的数据（DOM对象）
方法|描述
---|---
open() |打开请求
send() |发送请求
abort() |   停止当前请求
getAllResponseHeaders() |返回完整的HTTP响应头信息。
getResponseHeader("headerLabel")| 返回指定名称的HTTP响应头信息。
setRequestHeader("label", "value")| 设置发送请求的request头信息。

###### login.html
```html
<form method="" action="">
    <label for="account">账号：</label>
    <input type="text" name="account" value="" id="account">
    <label for="account">密码：</label>
    <input type="password" name="password" value="" id="password">
    <input type="button" name="submit" value="提交">
<form>
```  
###### login.js
```javascript
var account=document.querySelector("[name='account']").value;
var password=document.querySelector("[name='password']").value;
var submit=document.querySelector("[name='submit']");
var xhr=new XMLHttpRequest();
xhr.open("post","login.php");
xhr.send("account="+account+"&password="+password);
xhr.onload=function(){
  var res=xhr.response;
  ...
}
```
###### login.php
```php
<?php
    sleep(5);//模拟网络延时
    $account=$_GET["account"];
    $password=$_GET["password"];
    if($account=="admin"&&$password=="123456"){
      echo 1;
    }else{
      echo 0;
    }
?>
```
#### 传统交互和AJAX的区别
- ajax可是无刷新实现交互，传统的form不行
- ajax是异步的，传统交互是同步

## AJAX乱码问题
#### 原因
- xtmlhttp 返回的数据默认的字符编码是utf-8，如果前台页面是gb2312或者其它编码数据就会产生乱码
- post方法提交数据默认的字符编码是utf-8，如果后台是gb2312或其他编码数据就会产生乱码
- get方式提交中文乱码

#### 解决
- 前台后台都用utf-8编码
- 编码转换
```
header('Content-Type:text/html;charset=GB2312');
iconv("gbk","utf-8","优逸客");
```
