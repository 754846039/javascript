# swiper插件
http://www.swiper.com.cn/
## swiper功能特性
- swiper是一个免费的、开源的移动端触摸滑动插件，方便我们快速开发轮播图的
- 主要使用于移动端的网站、网页应用程序（web apps）以及原生的应用程序
- pc端和移动端都可以使用的。
- swiper2兼容到ie7
- swiper3只兼容到ie10，比较适合移动端

## swiper使用方法
- 下载并引入swiper.min.js和swiper.min.css；
  - 如果页面加载了jQuery.js或zepto.js，直接引入swiper.jquery.min.js即可
  - Zepto是一个轻量级的JavaScript库，与jQuery的API类似。会用jQuery就会用zepto
- 布局（直接打开demo复制代码即可）

```html
<!-- HTML -->
<!-- 定义一个容器 -->
<div class="swiper-container">
    <!-- 用来包裹轮播元素 -->
    <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
    <!-- 分页器 -->
    <div class="swiper-pagination"></div>

    <!-- 导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>

    <!-- 滚动条 -->
    <div class="swiper-scrollbar"></div>
</div>
```

- 加样式
```css
/*CSS*/
.swiper-container{
	width: 600px;
	height: 400px;
	border: 1px solid #000;
	margin: 0 auto;
}
```

- 初始化Swiper
```javascript
//JavaScript
// 不同容器类名不同控制
var mySwiper = new Swiper ('.swiper-container', {
    direction: 'vertical',
    loop: true,
    // 如果需要分页器
    pagination: '.swiper-pagination',
    // 如果需要前进后退按钮
    nextButton: '.swiper-button-next',
    prevButton: '.swiper-button-prev',
    // 如果需要滚动条
    scrollbar: '.swiper-scrollbar',
})
```
