# javascript Object

## 常用方法

### Object.create()
>该方法可以创建一个拥有指定原型和若干个指定属性的对象。<br/>
>Object.create(proto, [ propertiesObject ]) 是ES5中提出的一种新的对象创建方式，第一个参数是要继承的原型，如果不是一个子函数，可以传一个null，第二个参数是对象的属性描述符，这个参数是可选的。
* 数据属性:
  * writable:是否可任意写
  * configurable：是否能够删除
  * enumerable：是否能用 for in 枚举
  * value：值
* 访问属性:
  * get(): 访问
  * set(): 设置

  **实例：**
  ```javascript
  var obj = {
    a: 100,
    b: function(){
      console.log(100);
    }
  }
  var newObj = {};
  newObj = Object.create(obj,{
      t1: {
          value:'yupeng',
          writable:false
      },
      t2: {
          configurable: false,
          get: function() { return t2; },
          set: function(value) { t2 = value }
      }
  })
  console.log(newObj.t1);   //yupeng
  newObj.t1='yupeng1';
  console.log(newObj.t1);   //yupeng

  newObj.t2=201;
  delete newObj.t2;
  console.log(newObj.t2);  //201

  for(var i in newObj){
    console.log(i);      // t1 a b
  }
  ```

### Object.is()
>它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。不同之处只有两个：一是+0不等于-0，二是NaN等于自身。

  ```javascript
  //不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
  console.log(+0 === -0) //true
  console.log(NaN === NaN) // false
  console.log(Object.is(+0, -0)) // false
  console.log(Object.is(NaN, NaN)) // true
  ```

### Object.assign()
* 基本用法
 >Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
 >Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。

  ```javascript
  var target = { a: 1 };
  var source1 = { b: 2 };
  var source2 = { c: 3 };
  Object.assign(target, source1, source2);
  console.log(target) // {a:1, b:2, c:3}
  ```

* 如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

  ```javascript
  var target = { a: 1, b: 1 };
  var source1 = { b: 2, c: 2 };
  var source2 = { c: 3 };
  Object.assign(target, source1, source2);
  console.log(target) // {a:1, b:2, c:3}
  ```

* 如果只有一个参数，Object.assign会直接返回该参数。

  ```javascript
  var obj = {a: 1};
  Object.assign(obj) === obj // true
  ```

* 如果该参数不是对象，则会先转成对象，然后返回。

  ```javascript
  typeof Object.assign(2) // "object"
  ```

* 由于undefined和null无法转成对象，所以如果它们作为参数，就会报错。

  ```javascript
  Object.assign(undefined) // 报错
  Object.assign(null) // 报错
  ```

* Object.assign方法实行的是浅拷贝，而不是深拷贝。

  ```javascript
  var obj1 = {a: {b: 1}};
  var obj2 = Object.assign({}, obj1);
  obj1.a.b = 2;
  console.log(obj2.a.b)      // 2
  ```

### Object.getOwnPropertyDescriptors()
>返回某个对象属性的描述对象。

  ```javascript
  var obj = { a: 'b' };
  Object.getOwnPropertyDescriptor(obj, 'a');   // a的描述对象
  // Object {
  //   value: "b",
  //   writable: true,
  //   enumerable: true,
  //   configurable: true
  // }
  ```

## 属性的遍历（Object对象方法的使用）

### 属性的可枚举性
>对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。<br/>
Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象。<br/>
描述对象的enumerable属性，称为"可枚举性"，如果该属性为false，就表示某些操作会忽略当前属性。

  * for...in循环：只遍历对象自身的和继承的可枚举的属性。
  * Object.keys()：返回对象自身的所有可枚举的属性的键名。
  * JSON.stringify()：只串行化对象自身的可枚举的属性。
  * Object.assign()：只拷贝对象自身的可枚举的属性。

### 遍历的方式
>ES6一共有5种方法可以遍历对象的属性。

* for...in
>for...in循环遍历对象自身的和继承的可枚举属性（不含Symbol属性）。

* Object.keys(obj)
>Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含Symbol属性）。

* Object.getOwnPropertyNames(obj)
>Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性）。

* Object.getOwnPropertySymbols(obj)
>Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol属性。

* Reflect.ownKeys(obj)
>Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管是属性名是Symbol或字符串，也不管是否可枚举。

* 以上的5种方法遍历对象的属性，都遵守同样的属性遍历的次序规则。
 * 首先遍历所有属性名为数值的属性，按照数字排序。
 * 其次遍历所有属性名为字符串的属性，按照生成时间排序。
 * 最后遍历所有属性名为Symbol值的属性，按照生成时间排序。
