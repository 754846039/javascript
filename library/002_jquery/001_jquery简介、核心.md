# jQuery简介
>从获取元素、操作样式、添加事件三方面讲

## 下载
[jQuery:http://jquery.com/](http://jquery.com/)
[jQuery bootcdn:http://www.bootcdn.cn/jquery/](http://www.bootcdn.cn/jquery/)
[jQuery在线：https://code.jquery.com/](https://code.jquery.com/)
- Download the compressed, production jQuery 3.2.1  
  - 生产版本
- Download the uncompressed, development jQuery 3.2.1
  - 开发版本

## 插件
[jQuery插件：www.jq22.com](www.jq22.com)

## 什么是jQuery     
1. jQuery是一个快速，轻量级，功能丰富的js库、框架（从版本2开始不再考虑ie6、ie7、ie8，版本3 改进了对h5、css3的支持 ）
2. JQuery核心理念：write less,do more!
3. jQuery的核心功能都是通过$函数实现的，jQuery的一切都基于$函数，$函数是jQuery的入口
4. 特性
  - 通用性
  - 可扩展性
  - 链式调用（每次都会返回一个JQuery对象）
  - 隐式循环（each）
  - 无兼容性
  - 跨平台  

## jQuery原理

```javascript
// jQuery原理
function Jquery(selector){
  var obj=this.get(selector);
  this.length=obj.length;
  for(let i=0;i<obj.length;i++){
    this[i]=obj[i];
  }
}
Jquery.prototype={
  get:function(selector){
    return document.querySelectAll(selector);
  },
  each:function(callback){
    for(let i=0;i<this.length;i++){
      callback(this[i],i);
    }
  },
  html:function(html){
    this.each(function(ele,index){
      ele.innerHTML=html;
    });
    return this;
  },
  css:function(attr,value){
    this.each(function(ele,index){
      ele.style[attr]=value;
    })
    return this;
  },
  click:function(callback){
    this.each(function(ele,index){
      ele.onclick=function(){
        callback();
      }
    })
    return this;//链式调用
  }
}

function $(selector){
  return new Jquery(selector);
}

$("div").html("html");
```

## $===jQuery
#### $可传的参数：
- 字符串：选择器字符串
- 原生对象（DOM对象）：会把DOM对象打包成jQuery对象
- html标签字符串
- 回调函数

#### window.onload=function(){} 和 $(function(){})的区别
- 两者功能相同，但是$通过事件绑定添加的,可以添加多次
- $(function(){})文档结构加载完成后就执行，而window.onload是等文档结构和内容（资源）全部加载完成后才执行<br>
  `$(function(){}) 默认执行的是 document.addEventListener("DOMContentloaded",function(){})  ？？？？`

```html
<script>
  // 按执行顺序排列
	$(function(){
		console.log("$()");
	})
	document.addEventListener("DOMContentLoaded",function(){
		console.log("DOMContentLoaded");
	})
	window.onload=function(){
		console.log("window.onload")
	}
</script>
```

#### $(function(){})是$(document).ready(function(){}) 的简写      

## jQuery核心（用在jQuery内部）
#### $([selector,[context]])
- 用来匹配一些元素
- 返回值为jquery对象的集合
- jquery对象转DOM对象：加下标或get([index])
- DOM对象（原生对象）转为jQuery对象：用$(document)包起来即可；
- context是上下文的意思，提高检索效率
```javascript
$("div",".box");  //在box中检索div元素
```

#### $(html,[创建DOM元素所在的文档])
- 动态创建由jQuery对象包装的DOM元素(即jQuery对象)。同时设置一系列的属性、事件等。

```javascript
// 方法一
$("<div class='one'>我是新创建的div</div>").appendTo($(docunment.body));
// 方法二
$("<div>", {
  "class": "test",
  text: "Click me!",
  click: function(){
    $(this).toggleClass("test");
  }
}).appendTo("body");
```

#### $(callback)
    参数：下标、DOM对象
【eg】$(function(index,dom){})

  4、size()\length  返回值为jQuery对象中元素的个数（所有的子元素）。
区别：size()是方法，length是属性

  5、get([index])
传参数：把指定下标的jQuery对象转换成DOM对象并返回
不传参数：把整个jQuery对象转换成DOM对象集合并返回

  6、index()
参数：jQuery对象，jQuery集合，DOM集合
返回值：不传参数：默认输出当前元素元素在其同辈元素集合里的索引值
	传参数：当前元素在当前集合里的索引值
	如果找不到匹配的元素，则返回-1。

  7、data([attr],[value])
数据缓存到jQuery对象身上，不会缓存到DOM对象上（即给每一个jQuery对象添加一个attr属性，值为value）
默认访问第一个jQuery对象的index属性的值
参数也可以传一个对象
  8、多库共存
function和jQuery中的$共存，  释放对于$的使用权，则可用function里面的$
方法一、Conflict冲突
  jQuery.noConflict()
  jQuery(".box").click()
```javascript
// 为了防止与其他框架的$冲突
(function($){
  $("div")....
})(jQuery)
```

方法二、
  var aa=jQuery.noConflict()   把$的使用权交给aa
  aa(".box").click...

#### 插件（扩展功能）
>fullpage全屏滚动/jq22网 /直接搜jquery插件，在页面中引入，修改配置项，调用就好了

- jQuery.fn.extend()===jQuery.prototype.extend()  
  - 扩展到jQuery原型身上，可以被继承
  ```javascript
  $.fn.extend({
      play:function(){
          alert("play");
      }
  })
  $("div").play();
  ```

- jQuery.extend()   
  - 添加到jQuery本身，只能jQuery本身调用，不能用jQuery实例化对象调用
  ```javascript
  $.extend({
      play:function(){
          alert("play");
      }
  })
  $.play();
  ```

#### 队列
- queue(e,[q])  
  - 不传参数返回数组（添加一个动画就会在队列中添加一个动作，并且）
  ```javascript
  $(".box").slideUp(500).slideDown(500).fadeOut(500).fadeOut(500);//动画依次执行，原理是队列控制
  $(".box").queue();//返回队列数组
  ```
  - 传参数（一旦使用的queue方法，在queue函数外再添加队列的话添加不上，所以dequeue）
  ```javascript
  // 情况一
  $(".box").slideUp(500).slideDown(500).fadeOut(500).fadeOut(500).css({color:"red"});//颜色会在最开始就变化，不等动画完成

  // 情况二
  $(".box").slideUp(500).slideDown(500).fadeOut(500).fadeIn(500).queue(function(){
    // 加入队列之后会按顺序依次执行
    $(this).css({color:"red"}).dequeue();
  })
  $(".box").click(function(){
    console.log(1);     //1
    $(this).fadeOut();  //动画不会执行，因为一旦使用的queue方法，在queue函数外再添加队列的话添加不上，所以需要dequeue
  })
  ```

- dequeue([queueName])
- clearQueue([queueName])
清空队列


##### 队列分为3种
- 内部自运行的队列 animate
```javascript
$("div").animate({width:500},1000);
$("div").animate({height:500},1000);
```
- fx队列
  - 仅次于animate的队列
  - 先进先出（列头进，列尾出）

```javascript
$("div").queue(["fx",]function(){
  alert(1);
  $("div").dequeue(["fx"]);
})
$("div").queue(["fx"],function(){
  alert(2);
  $("div").dequeue(["fx"]);
})
```

- 自定义队列
  - 不会自己出队，需要手动出队(执行调用)

```javascript
$("div").queue("aa",function(){
  alert(1);
  $("div").dequeue("aa");
})
$("div").queue("aa",function(){
  alert(1);
  $("div").dequeue("aa");
})
$("div").dequeue("aa"); //需要手动出队
```

##### 队列和栈的区别
- 队列：先进先出fx（列头进，列尾出）
- 栈：先进后出（只能从栈顶进出，栈底不能）

### 语法特点
- 换行不影响执行
