# hammer.js
Hammer.js是一个开源的，轻量级的，专门用于控制、定制手势的javascript库，它可以识别出常见的触摸、拖动、长按、缩放等等，移动端的事件库。

http://hammerjs.github.io/
http://hammerjs.github.io/getting-started/
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>hammer</title>
</head>
<body>
	<div class="demo"></div>
</body>
<script src="hammer.min.js"></script>
<script>
	var demo=document.querySelector(".demo");
	var myHammer=new Hammer(demo);
	myHammer.on("tap",function(){
		console.log("单击");
	})
</script>
</html>
```
