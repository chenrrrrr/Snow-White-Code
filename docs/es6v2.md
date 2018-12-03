## babel

Babel 的配置文件是 .babelrc ，存放在项目的根目录下

babel-cli 工具

```bash
# 全局安装
$ npm install --global babel-cli
# 项目安装
$ npm install --save-dev babel-cli
```

命令

```bash
# 转码结果输出到标准输出
$ babel example.js
# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js
# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib
# -s 参数生成source map文件
$ babel src -d lib -s
```

babel cdn

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standa
lone/6.4.4/babel.min.js"></script>
<script type="text/babel">
  // Your ES6 code
</script>
```

## ESLint

```bash
$ npm install --save-dev eslint babel-eslint
```

## let 和 const 命令

`let` 命令所在的代码块内有效，for 循环的计数器，就很合适使用 `let` 命令，更重要的是，`let`明确了块级作用域，外层作用域无法读取内层作用于的变量，ES5 声明私有作用域的`(function(){}())`

```javascript
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i); // abc *3
}
console.log(i); //  k is not defined
```

在代码块内，使用 let 命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）

```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError
  let tmp; // TDZ结束
  console.log(tmp); // undefined
  tmp = 123;
  console.log(tmp); // 123
}
```

const 命令

```javascript
const a = 5;
a = 6; //报错
const obj = {};
obj.name = '陈睿'; // OK
obj = {}; // 报错
```

const 只是让指针不能改变，但是映射的内存对象是可以变化的，obj 实际存储的是一个地址，所以赋值新的{}给 obj 会报错，因为新的{}的内存地址变了

冻结对象

```javascript
const foo = Object.freeze({});
foo.prop = 123;
```

## ES6 声明变量

操蛋的事情，顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一

```javascript
window.a = 1;
a; // 1
a = 2;
window.a; // 2
```

ES6 为了改变这一点，一方面规定，为了保持兼容性， var 命令和 function 命令声明的全局变量，依旧是顶层对象的属性；另一方面规定， let 命令、 const 命令、 class 命令声明的全局变量，不属于顶层对象的属性

## 变量解构赋值

```javascript
// before
let a = 1;
let b = 2;
let c = 3;
// now
let [a, b, c] = [1, 2, 3];
let [foo, [[bar], baz]] = [1, [[2], 3]];
let [head, ...tail] = [1, 2, 3, 4]; //  head = 1、tail = [2, 3, 4]
// 对象解构
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
```

解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数）、那么解构赋值拷贝的是这个值的引用，而不是这个值的副本

```javascript
let obj = { a: { b: 1 } };
let { ...x } = obj;
obj.a.b = 2;
x.a.b; // 2
obj.a = null;
x.a; // { b:1 }
```

## 字符串扩展

```javascript
'x'.repeat(3); // 'xxx'
'hello'.repeat(2); //'hellohello'
'x'.padStart(5, 'ab'); // 'ababx'
'x'.padEnd(5, 'ab'); // 'xabab'
```

模板字符串，用` `` `包裹标识

```javascript
$('#result').append(`
There are <b>${basket.count}</b> items
in your basket, <em>${basket.onSale}</em>
are on sale!
`);
```

模板字符串中`变量`或者`函数`用`${}`包裹，如果模板字符串中出现`，\转义

## 正则

正则表达式使用圆括号进行组匹配

```javascript
const RE_DATE = /(\d{4})-(\d{2})-(\d{2})/;
```

上面代码中，正则表达式里面有三组圆括号。使用 exec 方法，就可以将这三组匹配结果提取出来

```javascript
const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj[1]; // 1999
const month = matchObj[2]; // 12
const day = matchObj[3]; // 31
```

## 箭头函数

箭头函数里面根本没有自己的 this ，而是引用外层的 this，，所以不能用 call() 、 apply() 、 bind() 这些方法去改变 this 的指向

不可以当作构造函数，不可以使用 new 命令

箭头函数中没有`arguments`对象

```javascript
var jiantou = (x, y, z) => {
  console.log(arguments);
};
function putong(x, y, z) {
  console.log(arguments);
}

jiantou(1, 2, 3); // 报错
putong(1, 2, 3); //Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

## 尾调用

尾递归的实现，往往需要改写递归函数，确保最后一步只调用自身。做到这一点的方法，就是把所有用到的内部变量改写成函数的参数。

## 扩展运算符

合并数组

```javascript
var arr1 = [1, 2];
var arr2 = [3, 4];
var arr3 = [5];
// ES5
arr1.concat(arr2, arr3);
// ES6
[...arr1, ...arr2, ...arr3];
```

拆分字符串

```javascript
[...'hello']; // ["h", "e", "l", "l", "o"]
```

## 数组

ES6 提供三个新的方法—— entries() ， keys() 和 values() ——用于遍历数组。

```javascript
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1
for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

ES6,Array.prototype.includes 方法返回一个布尔值，表示某个数组是否包含给定的值

```javascript
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
```

兼容写法判断数组是否存在某个元素

```javascript
const contains = (() =>
  Array.prototype.includes
    ? (arr, value) => arr.includes(value)
    : (arr, value) => arr.some(el => el === value))();
contains(['foo', 'bar'], 'baz'); // => false
```

## Object.assign()

`Object.assign()` 方法用于对象的合并(浅拷贝)，将源对象（source）的所有可枚举属性，复制到目标对象（target）

> 如果 source 中的某个属性的值是对象，那么只是拷贝了引用

```javascript
var target = { a: 1 };
var source1 = { b: 2 };
var source2 = { c: 3 };
Object.assign(target, source1, source2);
target; // {a:1, b:2, c:3}

// 合并多个到一个新对象，并返回
var merge = (target, ...sources) => Object.assign({}, ...sources);
```

为类添加属性

```javascript
class Point {
  constructor(x, y) {
    Object.assign(this, { x, y });
  }
}
```

## 对象属性遍历

ES6 一共有 5 种方法可以遍历对象的属性。

- `for...in`
  for...in 循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。
- `Object.keys(obj)`
  Object.keys 返回一个数组，包括对象自身的（不含继承的）所有可枚举属性
  （不含 Symbol 属性）。
- `Object.getOwnPropertyNames(obj)`
  Object.getOwnPropertyNames 返回一个数组，包含对象自身的所有属性（不含
  Symbol 属性，但是包括不可枚举属性）。
- `Object.getOwnPropertySymbols(obj)`
  Object.getOwnPropertySymbols 返回一个数组，包含对象自身的所有 Symbol
  属性。
- `Reflect.ownKeys(obj)`
  Reflect.ownKeys 返回一个数组，包含对象自身的所有属性，不管属性名是
  Symbol 或字符串，也不管是否可枚举。

## 对象转 map

`Object.entries` 的基本用途是遍历对象的属性

```javascript
let obj = { one: 1, two: 2 };
for (let [k, v] of Object.entries(obj)) {
  console.log(`${JSON.stringify(k)}: ${JSON.stringify(v)}`);
}
// "one": 1
// "two": 2
```

转 map

```javascript
var obj = { foo: 'bar', baz: 42 };
var map = new Map(Object.entries(obj));
map; // Map { foo: "bar", baz: 42 }
```

手动模拟`Object.entries`

```javascript
// Generator函数的版本
function* entries(obj) {
  for (let key of Object.keys(obj)) {
    yield [key, obj[key]];
  }
}
// 非Generator函数的版本
function entries(obj) {
  let arr = [];
  for (let key of Object.keys(obj)) {
    arr.push([key, obj[key]]);
  }
  return arr;
}
```

## Symbol

ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，。它是 JavaScript
语言的第七种数据类型，前六种是： undefined 、 null 、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）

注意，Symbol 值作为对象属性名时，不能用点运算符，该属性还是公开属性，不是私有属性，该属性不会出现在 for...in 、 for...of 循环中，也不会被 Object.keys() 、 Object.getOwnPropertyNames() 、 JSON.stringify()返回

```javascript
var mySymbol = Symbol();
var a = {};
a.mySymbol = 'Hello!'; // 这里的mySymbol是字符串
a[mySymbol]; // undefined
a['mySymbol']; // "Hello!"
```

## Set & WeakSet

类似于数组，成员的值都是唯一的，没有重复，Set 函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数

- `.size()`：长度
- `.add(value)`：添加某个值，返回 Set()
- `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功
- `has(value)` ：返回一个布尔值，表示该值是否为 Set 的成员。
- `clear()` ：清除所有成员，没有返回值。

```javascript
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

数组去重

> Array.from 方法可以将 Set 结构转为数组

```javascript
[...new Set(array)];
```

WeakSet 结构与 Set 类似，成员只能是对象，即垃圾回收机制不考虑 WeakSet 对该对象的引用，，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存

## Map

传统 Object，Key 只能是字符串，Map 的 Key 也可以是 Object
