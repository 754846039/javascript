# 画板标签

[canvas MDN教程](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)  
## canvas简介
- canvas 元素用于图形的绘制，通过脚本(通常是JavaScript)来完成。canvas标签只是
图形容器，您必须使用脚本来绘制图形。你可以通过多种方法使用Canva绘制路径，盒、圆、字符以及添加图像。
- 有默认大小  300*150
- 不能在css中设置大小，在行内设置width、height（如果CSS的尺寸与初始画布的比例不一致，它会出现扭曲)
- 浏览器版本过低时在会显示标签中的字
- 使用一个JavaScript上下文对象，它能动态创建图像。

## 渲染上下文
- canvas元素的 getContext() 方法用来获得渲染上下文和它的绘画功能
- getContext()只有一个参数，上下文的格式。

```html
<canvas id="myCanvas" width="200" height="100"
        style="border:1px solid #000000;">
    您的浏览器不支持画布
</canvas>
<script type="text/javascript">
    var canvas=document.querySelector("#myCanvas");
    if(canvas.getContext){
      var ctx=canvas.getContext("2d");//得到画笔对象
    }
</script>
```     
