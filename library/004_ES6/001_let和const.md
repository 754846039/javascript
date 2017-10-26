# let和const命令
## let
> ECMAScript 6.0（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。<br>
let不像var那样会发生“变量提升”现象。所以，变量一定要在声明后使用，否则就会报错。

```javascript
console.log(foo);   // undefined
console.log(bar);   // bar is not defined
var foo = 2;
let bar = 2;
```

### let 和 var 的异同
- 相同
  - 都是用来声明变量
  - 声明后未赋值，结果都为undefined
- 不同
  - 变量提升
    - var声明的变量可以再声明前使用，值为undefined
    - let必须在声明后使用，否则会报错
    ```javascript
    console.log(age);   //undefined
    console.log(sex);   //报错 sex is not defined
    var age=12;
    let sex="man";
    ```
  - 重复声明一个变量
    - var 声明的变量重复声明会被覆盖
    - let 声明的变量不能重复声明，否则会报错
    ```javascript
    var age=12;
    let sex="man";

    var age=13;
    let sex="woman";
    //直接报错，脚本不会执行
    ```
  - 变量作用范围不同（作用域）
    - var 声明的变量
    - let 声明的变量
    ```javascript
    for(var i=0;i<5;i++){};
    for(let j=0;j<5;j++){};
    console.log(i); //5
    console.log(j); //报错
    ```

## const命令（es6）
- 声明一个只读常量
- 一旦声明，常量的值就不能改变，改变常量的值会报错
- 只声明不赋值，就会报错,声明的时候必须初始化
- 只在声明所在的块级作用域内有效
- 暂时性死区，只能在声明的位置后面使用
- 不可重复声明  
