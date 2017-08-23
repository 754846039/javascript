# fullpage全屏滚动插件
http://www.dowebok.com/77.html
http://www.jq22.com/jquery-info1124

- 引入jQuery.js和jQuery.fullpage.js
- 引入jQuery.fullpage.css
- 启动fullpage即可

```html
<!-- HTML -->
<div class="container">
  <div class="session">
    <div id="menu">

    </div>
  </div>
  <div class="session"></div>
  <div class="session"></div>
</div>
<!-- 每一个session都是相对定位的 -->
```

```javascript
//JavaScript
$("container").fullpage({
  anchors:["page1","page2","page3"],  //锚点，把每一屏幕的信息保存在地址栏,需要在a连接中写入“#page1”，数量同页面布局
  sessionsColor:["red","green","blue"],//背景颜色
  controlArrows:false,  //箭头
  scrollSpeed:700,//滚动速度，默认700
  loopBottom:true,//滚动到底部时滚动到顶部
  loopTop:true,//滚动到顶部时滚动到顶部
  continuesVertical:true,//无缝轮播
  fixedElements:"#menu",//设置谁需要固定定位
  menu:"#menu",
  afterRender:function(){
      //加载完成之后执行函数
  },
  afterload:function(anchorLink,index){
     //anchorLink==锚链接
     if(index==1){

     }else if(index==2){

     }
  },
  onLeave:function(index,nextIndex,direction){

  }
})
$.fn.fullpage.moveSessionDown(); //往下走
$.fn.fullpage.moveTo(1);        //回到顶部

```
