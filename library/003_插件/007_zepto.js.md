# zepto.js
http://www.css88.com/doc/zeptojs_api/
http://www.zeptojs.cn/

## zepto.js简介
Zepto是一个轻量级的JavaScript库，与jQuery的API类似。会用jQuery就会用zepto

### touch事件
#### 移动端默认事件
- touchstart
- touchmove
- touchend

#### touch
touch不是默认的事件，需要在github中打开复制js代码

- tap
  - 移动端点击事件，不要用click
- singleTap 单击（如果没有双击事件，用tap即可）
- doubleTap 双击
- longTap 长按
- swipe 滑动
- swipeLeft
- swipeRight
- swipeUp
- swipeDown

```JavaScript
$(".box").tap(function(){
  console.log("点击");
})
$(".box").on("tap",function(){
  console.log("点击");
})
```











移动端js
swiper
hammer
iscroll
