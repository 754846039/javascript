## 使用图片
 > canvas更有意思的一项特性就是图像操作能力。可以用于动态的图像合成或者作为图形的背景，以及游戏界面（Sprites）等等。浏览器支持的任意格式的外部图片都可以使用，比如PNG、GIF或者JPEG。 你甚至可以将同一个页面中其他canvas元素生成的图片作为图片源。

 * 引入图像到canvas里需要以下两步基本操作：
   1. 获得一个指向HTMLImageElement的对象或者另一个canvas元素的引用作为源，也可以通过提供一个URL的方式来使用图片.
   2. 使用drawImage()函数将图片绘制到画布上

 * drawImage(image, x, y) 其中 image 是 image 或者 canvas 对象，x 和 y 是其在目标 canvas 里的起始坐标。
 * drawImage(image, x, y, width, height) 这个方法多了2个参数：width 和 height，这两个参数用来控制 当像canvas画入时应该缩放的大小
 * drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight) 第一个参数和其它的是相同的，都是一个图像或者另一个 canvas 的引用。其它8个参数最好是参照右边的图解，前4个是定义图像源的切片位置和大小，后4个则是定义切片的目标显示位置和大小。

## 变形
* save 和 restore 方法是用来保存和恢复 canvas 状态的，都没有参数。Canvas 的状态就是当前画面应用的所有样式和变形的一个快照。
   * save()
   > Canvas状态存储在栈中，每当save()方法被调用后，当前的状态就被推送到栈中保存。一个绘画状态包括：strokeStyle, fillStyle, globalAlpha, lineWidth, lineCap, lineJoin, miterLimit, shadowOffsetX, shadowOffsetY, shadowBlur, shadowColor, 的值

   * restore() 每一次调用 restore 方法，上一个保存的状态就从栈中弹出，所有设定都恢复

   * translate(x, y) translate 方法接受两个参数。x 是左右偏移量，y 是上下偏移量
   * rotate(angle) 这个方法只接受一个参数：旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值。
   * scale(x, y) scale 方法接受两个参数。x,y 分别是横轴和纵轴的缩放因子，它们都必须是正值。值比 1.0 小表示缩小，比 1.0 大则表示放大，值为 1.0 时什么效果都没有。

## 动画
动画的基本步骤

1. 清空 canvas  除非接下来要画的内容会完全充满 canvas （例如背景图），否则你需要清空所有。最简单的做法就是用 clearRect 方法。
2. 保存 canvas 状态  如果你要改变一些会改变 canvas 状态的设置（样式，变形之类的），又要在每画一帧之时都是原始状态的话，你需要先保存一下。
3. 绘制动画图形（animated shapes） 这一步才是重绘动画帧。
4. 恢复 canvas 状态  如果已经保存了 canvas 的状态，可以先恢复它，然后重绘下一帧。   
