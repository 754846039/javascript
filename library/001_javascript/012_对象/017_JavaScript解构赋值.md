# ES6解构赋值和类

## 解构赋值
### 对象的解构赋值
* 对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
```javascript
var {b,a} = {a:"aaa",b:"bbb"};
console.log(a) // "aaa"
console.log(b) // "bbb"

var {c} = {a:"aaa",b:"bbb"};
console.log(c) // undefined
```

* 如果变量名与属性名不一致
```javascript
var {a:c} = {a:"aaa",b:"bbb"};
console.log(c) // "aaa"
console.log(a) // a is not defined

// 上面代码中，a是匹配的模式，c才是变量。真正被赋值的是变量c，而不是模式a。
```

* 采用解构赋值时，变量的声明和赋值是一体的。对于let和const来说，变量不能重新声明，所以一旦赋值的变量以前声明过，就会报错。

* 圆括号
  ```javascript
  let foo;
  ({foo} = {foo: 1}); // 1 成功

  let baz;
  ({bar: baz} = {bar: 1}); // 1 成功
  ```
let命令下面一行的圆括号是必须的，否则会报错。因为解析器会将起首的大括号，理解成一个代码块，而不是赋值语句。

### 字符串的解构赋值
  * 字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
  ```javascript
  const [a, b, c, d, e] = 'hello';
  console.log(a) // "h"
  console.log(b) // "e"
  console.log(c) // "l"
  console.log(d) // "l"
  console.log(e) // "o"
  ```

  * 类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。
  ```javascript
  let {length : len} = 'hello';
  console.log(len) // 5
  ```

### 数值的解构赋值
  解构赋值时，如果等号右边是数值，则会先转为对象。
  ```javascript
  let {toString: s} = 123;
  s === Number.prototype.toString // true
  ```

### 布尔值的解构赋值
  数值和布尔值的包装对象都有toString属性，因此变量s都能取到值。
  ```javascript
  let {toString: s} = true;
  s === Boolean.prototype.toString // true
  ```

### null和undefined的解构赋值
  解构赋值的规则是，只要等号右边的值不是对象，就先将其转为对象。<br/>
  由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
  ```javascript
  let { prop: x } = undefined; // 报错
  let { prop: y } = null; // 报错
  ```

### 函数参数的解构赋值
* 函数的参数也可以使用解构赋值。
  ```javascript
  function add([x, y]){
      return x + y;
  }
  add([1, 2]); // 3
  ```
  上面代码中，函数add的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量x和y。对于函数内部的代码来说，它们能感受到的参数就是x和y。

* 默认值
 ```javascript
 function move1({x = 0, y = 0} = {}) {
     return [x, y];
 }
 console.log(move1({x: 3, y: 8})); // [3, 8]
 console.log(move1({x: 3}));       // [3, 0]
 console.log(move1({}));           // [0, 0]
 console.log(move1());             // [0, 0]

 function move2({x, y} = { x: 0, y: 0 }) {
     return [x, y];
 }
 console.log(move2({x: 3, y: 8})); // [3, 8]
 console.log(move2({x: 3}));       // [3, undefined]  {x,y}={x:3}
 console.log(move2({}));           // [undefined, undefined]  {x,y}={}
 console.log(move2());             // [0, 0]
 ```

### 圆括号的问题
>解构赋值虽然很方便，但是解析起来并不容易。对于编译器来说，一个式子到底是模式，还是表达式，没有办法从一开始就知道，必须解析到（或解析不到）等号才能知道。

* 以下三种解构赋值不得使用圆括号。
 * 变量声明语句中，不能带有圆括号。
 * 函数参数中，模式不能带有圆括号。
 * 赋值语句中，不能将整个模式，或嵌套模式中的一层，放在圆括号之中。

### 解构赋值的用途
* 交换变量的值
>写法不仅简洁，而且易读，语义非常清晰

  ```javascript
   [x,y] = [y,x];
  ```

* 从函数返回多个值
>函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。

  ```javascript
  // 返回一个数组
  function example1() {
     return [1, 2, 3];
  }
  var [a, b, c] = example1();
  console.log(a, b, c);//1 2 3

  // 返回一个对象
  function example2() {
     return {
         first: 1,
         second: 2
     };
  }
  var {first, second} = example2();
  console.log(first, second)
  ```

* 函数参数的定义
>解构赋值可以方便地将一组参数与变量名对应起来。

  ```javascript
  // 参数是一组有次序的值
  function f([x, y, z]) { ... }
  f([1, 2, 3]);
  // 参数是一组无次序的值
  function f({x, y, z}) { ... }
  f({z: 3, y: 2, x: 1});
  ```
* 提取JSON数据
>解构赋值对提取JSON对象中的数据，尤其有用。

  ```javascript
  var jsonData = {
     id: 42,
     status: "OK",
     data: [401, 402]
  };
  let { id, status, data: number } = jsonData;
  console.log(id, status, number);  // 42, "OK", [401, 402]
```
* 输入模块的指定方法
>加载模块时，往往需要指定输入那些方法。解构赋值使得输入语句非常清晰。

  ```javascript
  const { SourceMapConsumer, SourceNode } = require("source-map");
  ```
