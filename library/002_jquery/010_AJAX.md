# ajax
## ajax请求
#### $.ajax()
添加到jQuery本身的方法
```javascript
// 方式一
$.ajax(url,{
  data:{key:value},
  dataType:"text",
  async:true,
  success:function(res){

  }
})
//data:{"aa":"bb","cc":"dd"}自动转为"aa==bb&cc==dd"

//方式二
$.ajax({
  url:"login.php",
  type:"POST",
  data:{key:value},
  dataType:"text",
  async:true,
  success:function(res){

  }
})
```

#### $.get("url",{data:val},callback,"type")
#### $.post("url",{data:val},callback,"type")
#### $.getScript("url",callback)
在需要的时候通过 HTTP GET 请求载入并执行一个 JavaScript 文件
#### $.getJSON("url",callback)
通过 HTTP GET 请求载入 JSON 数据（可以跨域）

#### serialize()
序列表表格内容为字符串。
返回值："zhanghao=admin&mima=123456"字符串


## 天气API
- 和风天气
- 说明文档--接口说明
```javascript
$.ajax({
  url:"https://free-api.heweather.com/v5/weather",
  data:{
    city:"太原",
    key:"24eb76b76750468dbaf21403366d5e1b"
  },
  success:function(res){
    console.log(res);
  }
})
```

## ajax事件（只能加到document对象上）
#### ajaxComplete(callback)
- 参数1：e 事件对象
- 参数2：jQuery对象
- 参数3：当前请求配置对象

#### ajaxError(callback)
#### ajaxSend(callback)
#### ajaxStart(callback)
#### ajaxStop(callback)
#### ajaxSuccess(callback)
