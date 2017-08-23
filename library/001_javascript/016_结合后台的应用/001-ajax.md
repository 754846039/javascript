# ajax
> AJAX全称为“Asynchronous JavaScript and XML”（异步JavaScript和XML），是一种创建交互式网页应用的网页开发技术

## 特点
  * 使用XHTML+CSS来标准化呈现
  * 使用XML和XSLT进行数据交换及相关操作
  * 使用XMLHttpRequest对象与Web服务器进行异步数据通信
  * 使用Javascript操作Document Object Model进行动态显示及交互
  * 使用JavaScript绑定和处理所有数据

## 与传统的web应用比较
  传统的Web应用交互由用户触发一个HTTP请求到服务器,服务器对其进行处理后再返回一个新的HTHL页到客户端, 每当服务器处理客户端提交的请求时,客户都只能空闲等待,并且哪怕只是一次很小的交互、只需从服务器端得到很简单的一个数据,都要返回一个完整的HTML页,而用户每次都要浪费时间和带宽去重新读取整个页面。这个做法浪费了许多带宽，由于每次应用的交互都需要向服务器发送请求，应用的响应时间就依赖于服务器的响应时间。这导致了用户界面的响应比本地应用慢得多。
  与此不同，AJAX应用可以仅向服务器发送并取回必需的数据，它使用SOAP或其它一些基于XML的Web Service接口，并在客户端采用JavaScript处理来自服务器的响应。因为在服务器和浏览器之间交换的数据大量减少，结果我们就能看到响应更快的应用。同时很多的处理工作可以在发出请求的客户端机器上完成，所以Web服务器的处理时间也减少了。

## ajax的工作原理
Ajax的工作原理相当于在用户和服务器之间加了—个中间层(AJAX引擎),使用户操作与服务器响应异步化。并不是所有的用户请求都提交给服务器,像—些数据验证和数据处理等都交给Ajax引擎自己来做, 只有确定需要从服务器读取新数据时再由Ajax引擎代为向服务器提交请求。<br>

Ajax其核心有JavaScript、XMLHTTPRequest、DOM对象组成，通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用JavaScript来操作DOM而更新页面。
## XMLHttpRequest对象
  1. 实例化ajax对象 new XMLHttpRequest()
  2. open() 用于配置请求

|参数|值|
|:----:|:----:|
|request-type|发送请求的类型,典型的值是 get 或 post|
|url|要连接的 URL|
|asynch|如果希望使用异步连接则为 true，否则为 false。该参数是可选的，默认为 true|
|username|如果需要身份验证，则可以在此指定用户名。该可选参数没有默认值|
|password|如果需要身份验证，则可以在此指定口令。该可选参数没有默认值|
  3. send() 用于发送请求
   * 如果请求是以get方式配置的,用 URL 发送数据要容易得多。如果需要发送安全信息或 XML，可能要考虑使用send()发送内容。如果不需要通过 send() 传递数据，则只要传递 null 作为该方法的参数即可，将传递的数据放在url地址后面进行传递。用 URL 发送数据要容易得多。如果需要发送安全信息或 XML，可能要考虑使用 send() 发送内容。如果不需要通过 send() 传递数据，则只要传递 null作为该方法的参数即可，将传递的数据放在url地址后面进行传递
   * 如果请求是以post方式配置的,需要先设置请求头信息，然后将需要发送的数据放到send()的参数中进行发送。
```javascript
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send(data);
```
 4. onreadystatechange
  * 当XMLHttpRequest 的readyState属性每一次发生改变时触发的事件
  * readyState的值
  |值|含义|
  |:----:|:----:|
  |0|（未初始化）还没有调用send()方法|
  |1|（载入）已调用send()方法，正在发送请求|
  |2|（载入完成）send()方法执行完成，已经接收到全部响应内容 |
  |3|（交互）正在解析响应内容 |
  |4|（完成）响应内容解析完成，可以在客户端调用了|
5. status
 > 正如我们前面看到的当readyState 的值为4的时候，说明我们和服务器的
    交互是成功的，但是如何判断页面返回的数据是成功的呢？我们需要再
    来检测一下状态码，他保存XMLHttpRequest 的一个简单属性status 这
    个上面

  |值|含义|
  |:----:|:----:|
  |200|OK 一切正常|
  |304|Not Modified 客户端有缓冲的文档并发出了一个条件性的请求（一般是提供If-Modified-Since头表示客户只想比指定日期更新的文档）。服务器告诉客户，原来缓冲的文档还可以继续使用|
  |404|Not Found 无法找到指定位置的资源|
  |5xx|服务器错误|

 6. 响应
     * response 响应实体的类型由 responseType 来指定， 可以是 ArrayBuffer， Blob， Document， JavaScript 对象 (即 "json")， 或者是字符串。如果请求未完成或失败，则该值为 null。
     * responesType 设置该值能够改变响应类型。就是告诉服务器你期望的响应格式。
     * responseText 此次请求的响应为文本，或是当请求未成功或还未发送时为 null。
     * responseXML 本次请求的响应是一个 Document 对象，如果是以下情况则值为 null：请求未成功，请求未发送，或响应无法被解析成 XML 或 HTML。当响应为text/xml 流时会被解析。

 7.  upload
 可以在 upload 上添加一个事件监听来跟踪上传过程。

> ajax对象和upload对象拥有相同的事件

|事件|含义|
|:----:|:-----:|
|onabort|当发生中止事件时触发的事件|
|onerror|当发生加载错误是触发的事件|
|onload|当加载结束后触发的事件，不论成功与否|
|onloadend|加载结束后触发的事件|
|onloadstart|当加载开始时触发的事件|
|onprogress|在加载过程中不断触发的事件|
|ontimeout|加载超时后执行的事件|

```javascript
 xhr.upload.onprogress=function(e){
 //获取当前上传进度传递到progress中显示
 progress.value=parseInt(e.loaded/e.total*100)
}
```
## get和post的区别
* get是从服务器上获取数据，post是向服务器传送数据。
* get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
* 对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据。
* get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。

*  get安全性非常低，post安全性较高。
*  HTTP 定义了与服务器交互的不同方法，最基本的方法是 GET 和 POST。事实上 GET 适用于多数请求，而保留 POST 仅用于更新站点。根据 HTTP 规范，GET 用于信息获取，而且应该是 安全的和幂等的。所谓安全的意味着该操作用于获取信息而非修改信息。换句话说，GET 请求一般不应产生副作用。幂等的意味着对同一 URL 的多个请求应该返回同样的结果。完整的定义并不像看起来那样严格。从根本上讲，其目标是当用户打开一个链接时，她可以确信从自身的角度来看没有改变资源。 比如，新闻站点的头版不断更新。虽然第二次请求会返回不同的一批新闻，该操作仍然被认为是安全的和幂等的，因为它总是返回当前的新闻。反之亦然。POST 请求就不那么轻松了。POST 表示可能改变服务器上的资源的请求。仍然以新闻站点为例，读者对文章的注解应该通过 POST 请求实现，因为在注解提交之后站点已经不同
*  在FORM提交的时候，如果不指定Method，则默认为GET请求，Form中提交的数据将会附加在url之后，以?分开与url分开。字母数字字符原 样发送，但空格转换为“+“号，其它符号转换为%XX,其中XX为该符号以16进制表示的ASCII（或ISO Latin-1）值。GET请求请提交的数据放置在HTTP请求协议头中，而POST提交的数据则放在实体数据中；GET方式提交的数据最多只能有1024字节，而POST则没有此限制。

## 同步和异步的区别
   * 同步：提交请求->等待服务器处理->处理完毕返回 这个期间客户端浏览器不能干任何事
   * 异步: 请求通过事件触发->服务器处理（这是浏览器仍然可以作其他事情）->处理完毕
