用来处理移动端滚动问题
http://iscrolljs.com/
// 默认没有滚动条，实现下拉刷新、上拉刷新的功能
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta>
	<title>iscroll</title>
	<style>
		*{
			margin: 0;
			padding: 0;
		}
		.box{
			width: 100%;
			height: 100px;
			border: 1px solid #000;
			overflow: auto;
		}
		.box ul{
			width: 100%;
			height: auto;
		}
		ul li{
			height: 20px;
		}
		.content{
			width: 100%;
			height: 1000px;
		}
	</style>
</head>
<body>
<div class="box">
	<ul>
		<li>1</li>
		<li>2</li>
		<li>3</li>
		<li>4</li>
		<li>5</li>
		<li>6</li>
		<li>7</li>
		<li>8</li>
		<li>9</li>
		<li>10</li>
	</ul>
</div>
<div class="content">ul内部有滚动条，当页面中也有滚动条时，需要用iscroll解决分别滚动问题</div>
</body>
<script src="iscroll.js"></script>
<script>
	var box=document.querySelector(".box");
	// 默认没有滚动条，实现下拉刷新、上拉刷新的功能
	var myScroll=new IScroll(box)
</script>
</html>
```
