# canvas
>  canvas 是 HTML5 新增的元素，可使用JavaScript脚本来绘制图形。例如：画图，合成照片，创建动画甚至实时视频处理与渲染。

* canvas起初是空白的。为了展示，首先脚本需要找到渲染上下文，然后在它的上面绘制。canvas>元素有一个做 getContext() 的方法，这个方法是用来获得渲染上下文和它的绘画功能。getContext()只有一个参数，上下文的格式。

```JavaScript
 var canvas = document.getElementById('canvas');
 var ctx = canvas.getContext('2d');
```

## 绘制形状
> HTML中的元素canvas只支持一种原生的图形绘制：矩形。所有其他的图形的绘制都至少需要生成一条路径。

 * 绘制矩形的三种方法
    * fillRect(x, y, width, height) 绘制一个填充的矩形
    * strokeRect(x, y, width, height)绘制一个矩形的边框
    * clearRect(x, y, width, height)清除指定矩形区域，让清除部分完全透明。

 >上面提供的方法之中每一个都包含了相同的参数。x与y指定了在canvas画布上所绘制的矩形的左上角（相对于原点）的坐标。width和height设置矩形的尺寸。    

## 绘制路径
 > 图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。使用路径绘制图形需要一些额外的步骤。

    * 首先，你需要创建路径起始点。
    * 然后你使用画图命令去画出路径。
    * 之后你把路径封闭。
    * 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。
  * 绘制路径所需要的方法      

|方法|含义|
|:----:|:----:|
|beginPath() |新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。|
|moveTo(x, y)|将笔触移动到指定的坐标x以及y上。|
|lineTo(x, y)| 绘制一条从当前位置到指定x以及y位置的直线。|
| closePath()| 闭合路径之后图形绘制命令又重新指向到上下文中。|
|stroke()| 通过线条来绘制图形轮廓。|
|fill()| 通过填充路径的内容区域生成实心的图形。|
|rect(x, y, width, height)|绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。|
|arc(x, y, radius, startAngle, endAngle, anticlockwise)|圆心坐标，半径，起始角度，结束角度，顺、逆时针|
|bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)|绘制二次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。|
> 生成路径的第一步叫做beginPath()。本质上，路径是由很多子路径构成，这些子路径都是在一个列表中，所有的子路径（线、弧形、等等）构成图形。而每次这个方法调用之后，列表清空重置，然后我们就可以重新绘制新的图形。

## 样式和颜色
> 到目前为止，我们只看到过绘制内容的方法。如果我们想要给图形上色，有两个重要的属性可以做到：fillStyle 和 strokeStyle。

 * fillStyle = color 设置图形的填充颜色
 * strokeStyle = color设置图形轮廓的颜色。
 > color 可以是表示 CSS 颜色值的字符串，渐变对象或者图案对象。    

## 线型
> 可以通过一系列属性来设置线的样式。

  * lineWidth = value 设置线条宽度。
  * lineCap = type 设置线条末端样式。
  > 属性 lineCap 的值决定了线段端点显示的样子。它可以为下面的三种的其中之一：butt，round 和 square。

  * lineJoin = type设定线条与线条间接合处的样式。
  > lineJoin 的属性值决定了图形中两线段连接处所显示的样子。它可以是这三种之一：round, bevel 和 miter。默认是 miter。


  * miterLimit = value限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。
  * getLineDash()返回一个包含当前虚线样式，长度为非负偶数的数组。
  * setLineDash(segments)设置当前虚线样式。
  * lineDashOffset = value 设置虚线样式的起始偏移量。

## 渐变
> 就好像一般的绘图软件一样，我们可以用线性或者径向的渐变来填充或描边。我们用下面的方法新建一个 canvasGradient 对象，并且赋给图形的 fillStyle 或 strokeStyle 属性。

* createLinearGradient(x1, y1, x2, y2) createLinearGradient 方法接受 4 个参数，表示渐变的起点 (x1,y1) 与终点 (x2,y2)。  
* createRadialGradient(x1, y1, r1, x2, y2, r2) createRadialGradient 方法接受 6 个参数，前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆。
* gradient.addColorStop(position, color)
>addColorStop 方法接受 2 个参数，position 参数必须是一个 0.0 与 1.0 之间的数值，表示渐变中颜色所在的相对位置。例如，0.5 表示颜色会出现在正中间。color 参数必须是一个有效的 CSS 颜色值（如 #FFF， rgba(0,0,0,1)，等等）。

## 阴影
  * shadowOffsetX = float shadowOffsetY = float
  > shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。

  * shadowBlur 用于设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵的影响，默认为 0。
  * shadowColor = color shadowColor 是标准的 CSS 颜色值，用于设定阴影颜色效果，默认是全透明的黑色。

## 绘制文本
   * fillText(text, x, y [, maxWidth]) 在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的.
   * strokeText(text, x, y [, maxWidth])在指定的(x,y)位置绘制文本边框，绘制的最大宽度是可选的.
   * font = value 当前我们用来绘制文本的样式. 这个字符串使用和 CSS font 属性相同的语法. 默认的字体是 10px sans-serif。
   * textAlign = value 文本对齐选项. 可选的值包括：start, end, left, right or center. 默认值是 start。
   * textBaseline = value 基线对齐选项. 可选的值包括：top, hanging, middle, alphabetic, ideographic, bottom。默认值是 alphabetic
   * direction = value 文本方向。可能的值包括：ltr, rtl, inherit。默认值是 inherit。
