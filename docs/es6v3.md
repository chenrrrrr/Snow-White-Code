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

## Reflect

Reflect 对象的设计目的有这样几个。

- 将 Object 对象的一些明显属于语言内部的方法（比
  如 `Object.defineProperty` ），放到 Reflect 对象上。现阶段，某些方法同时
  在 Object 和 Reflect 对象上部署，未来的新方法将只部署在 Reflect 对象
  上。也就是说，从 Reflect 对象上可以拿到语言内部的方法。
- 修改某些 Object 方法的返回结果，让其变得更合理。比
  如， `Object.defineProperty(obj, name, desc)` 在无法定义属性时，会抛出一
  个错误，而 `Reflect.defineProperty(obj, name, desc)` 则会返回 false 。

```javascript
// 老写法
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}
// 新写法
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```

## Promise

Promise 是异步编程的一种解决方案，有三种状态： pending （进行中）、 fulfilled （已成功）和 rejected （已失败），通常用`resolved`代表成功，`rejected`代表失败

```javascript
var promise = new Promise(function(resolve, reject) {
// ... some code
if (/* 异步操作成功 */){
resolve(value);
} else {
reject(error);
}
});
```

Promise 实例生成以后，可以用 then 方法分别指定 resolved 状态和 rejected 状态的回调函数，Promise 新建后就会立即执行

```javascript
promise.then(
  function(value) {
    // success
  },
  function(error) {
    // failure
  }
);
```

Promise 实现 Ajax

```javascript
var getJSON = function(url) {
  var promise = new Promise(function(resolve, reject) {
    var client = new XMLHttpRequest();
    client.open('GET', url);
    client.onreadystatechange = handler;
    client.responseType = 'json';
    client.setRequestHeader('Accept', 'application/json');
    client.send();
    function handler() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    }
  });
  return promise;
};
getJSON('/posts.json').then(
  function(json) {
    console.log('Contents: ' + json);
  },
  function(error) {
    console.error('出错了', error);
  }
);
```

调用 resolve 或 reject 并不会终结 Promise 的参数函数的执行，因为立即 resolved 的 Promise 是在本轮事件循环的末尾执行，总是晚于本轮循环的同步任务

```javascript
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});
// 2
// 1
```

一般来说，调用 resolve 或 reject 以后，Promise 的使命就完成了，后继操作应该放到 then 方法里面

```javascript
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
});
```

抛出错误

```javascript
var promise = new Promise(function(resolve, reject) {
  reject(new Error('test'));
});
promise.catch(function(error) {
  console.log(error);
});
```

一般来说，不要在 then 方法里面定义 Reject 状态的回调函数（即 then 的第二个参数），总是使用 catch 方法

```javascript
// bad
promise.then(
  function(data) {
    // success
  },
  function(err) {
    // error
  }
);
// good
promise
  .then(function(data) {
    //cb
    // success
  })
  .catch(function(err) {
    // error
  });
```

catch 方法返回的还是一个 Promise 对象，因此后面还可以接着调用 then 方法，如果没有报错，则会跳过 catch 方法

```javascript
var someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // 下面一行会报错，因为 x 没有声明
    resolve(x + 2);
  });
};
someAsyncThing()
  .catch(function(error) {
    console.log('oh no', error);
  })
  .then(function() {
    console.log('carry on');
  });
// oh no [ReferenceError: x is not defined]
// carry on
```

Promise.all()
只有 p1 、 p2 、 p3 的状态都变成 fulfilled ， p 的状态才会变成 fulfilled

```javascript
var p = Promise.all([p1, p2, p3]);
```

Promise.resolve()
将现有对象转为 Promise 对象

```javascript
var jsPromise = Promise.resolve($.ajax('/whatever.json'));
```

done()
Promise 对象的回调链，不管以 then 方法或 catch 方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为 Promise 内部的错误不会冒泡到全局）。因此，我们可以提供一个 done 方法，总是处于回调链的尾端，保证抛出任何可能出现的错误。

```javascript
// 注入原型
Promise.prototype.done = function(onFulfilled, onRejected) {
  this.then(onFulfilled, onRejected).catch(function(reason) {
    // 抛出一个全局错误
    setTimeout(() => {
      throw reason;
    }, 0);
  });
};
// 使用done
asyncFunc()
  .then(f1)
  .catch(r1)
  .then(f2)
  .done();
```

finally()
finally 方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。它与 done 方法的最大区别，它接受一个普通的回调函数作为参数，该函数不管怎样都必须执行。

```javascript
// 注入原型
Promise.prototype.finally = function(callback) {
  let P = this.constructor;
  return this.then(
    value => P.resolve(callback()).then(() => value),
    reason =>
      P.resolve(callback()).then(() => {
        throw reason;
      })
  );
};
// 使用finally
server
  .listen(0)
  .then(function() {
    // run test
  })
  .finally(server.stop);
```

Promise.try()

不知道或者不想区分，函数 f 是同步函数还是异步操作，但是想用 Promise 来处理它

```javascript
const f = () => console.log('now');
Promise.resolve().then(f);
console.log('next');
// next
// now
```

上面代码中，函数 f 是同步的，但是用 Promise 包装了以后，就变成异步执行了。那么有没有一种方法，让同步函数同步执行，异步函数异步执行，并且让它们具有统一的 API 呢？

```javascript
Promise.try(f);
console.log('next');
```

假设现在`database.users.get({id: userId})`是一个连接数据库，请求数据的的方法，你不知道是否存在异常

```javascript
Promise.try(database.users.get({id: userId}))
.then(...)
.catch(...)

```

## Generator 函数

yield 只能用在 Generator 函数里面，不能用于普通函数(例如：`forEach`)，遇到 yield 表达式，就暂停执行后面的操作，并将紧跟在 yield 后面的那个表达式的值，作为返回的对象的 value 属性值。

```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}
var hw = helloWorldGenerator();

hw.next(); // { value: 'hello', done: false }

hw.next(); // { value: 'world', done: false }

hw.next(); // { value: 'ending', done: true }

hw.next(); // { value: undefined, done: true }
```

co 模块

[co 模块](https://github.com/tj/co)是著名程序员 TJ Holowaychuk 于 2013 年 6 月发布的一个小工具，函数返回一个 Promise 对象，因此可以用 then 方法添加回调函数

```javascript
var gen = function*() {
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
var co = require('co');
co(gen).then(function() {
  console.log('Generator 函数执行完成');
});
```

## async

ES2017 标准引入了 async 函数，就是 Generator 函数的语法糖，当函数执行的时候，一旦遇到 await 就会先返回，等到异步操作完成，再接着执行函数体内后面的语句

```javascript
var asyncReadFile = async function() {
  var f1 = await readFile('/etc/fstab');
  var f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

async 函数返回一个 Promise 对象，可以使用 then 方法添加回调函数。

```javascript
async function f() {
  return 'hello world';
}
f().then(v => console.log(v));
// "hello world"
```

async 函数内部抛出错误，会导致返回的 Promise 对象变为 reject 状态。抛出的错误对象会被 catch 方法回调函数接收到。

```javascript
async function f() {
  throw new Error('出错了');
}
f().then(v => console.log(v), e => console.log(e));
// Error: 出错了
```

async 函数返回的 Promise 对象，必须等到内部所有 await 命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到 return 语句或者抛出错误。也就是说，只有 async 函数内部的异步操作执行完，才会执行 then 方法指定的回调函数

```javascript
async function getTitle(url) {
  let response = await fetch(url);
  let html = await response.text();
  return html.match(/<title>([\s\S]+)<\/title>/i)[1];
}
getTitle('https://tc39.github.io/ecma262/').then(console.log);
// "ECMAScript 2017 Language Specification"
```

await 命令后面是一个 Promise 对象。如果不是，会被转成一个立即 resolve 的 Promise 对象

```javascript
async function f() {
  return await 123;
}
f().then(v => console.log(v));
// 123
```

await 命令后面的 Promise 对象如果变为 reject 状态，则 reject 的参数会被 catch 方法的回调函数接收到

```javascript
async function f() {
  await Promise.reject('出错了');
}
f()
  .then(v => console.log(v))
  .catch(e => console.log(e));
// 出错了
```

希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个 await 放在 try...catch 结构里面，这样不管这个异步操作是否成功，第二个 await 都会执行

```javascript
async function f() {
  try {
    await Promise.reject('出错了');
  } catch (e) {}
  return await Promise.resolve('hello world');
}
f().then(v => console.log(v));
// hello world
```

另一种方法是 await 后面的 Promise 对象再跟一个 catch 方法，处理前面可能出现的错误

```javascript
async function f() {
  await Promise.reject('出错了').catch(e => console.log(e));
  return await Promise.resolve('hello world');
}
f().then(v => console.log(v));
// 出错了
// hello world
```

await 命令后面的 Promise 对象，运行结果可能是 rejected，所以最好把 await 命令放在 try...catch 代码块中

```javascript
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}
```

此外，多个 await 命令后面的异步操作，如果不存在继发关系，最好让它们同时触发

```javascript
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);
// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```

按顺序完成异步操作，依次远程读取一组 URL，然后按照读取的顺序输出结果

Promise 的写法如下

```javascript
function logInOrder(urls) {
  // 远程读取所有URL
  const textPromises = urls.map(url => {
    return fetch(url).then(response => response.text());
  });
  // 按次序输出
  textPromises.reduce((chain, textPromise) => {
    return chain.then(() => textPromise).then(text => console.log(text));
  }, Promise.resolve());
}
```

async 继发实现

```javascript
async function logInOrder(urls) {
  for (const url of urls) {
    const response = await fetch(url);
    console.log(await response.text());
  }
}
```

async 并发实现

```javascript
async function logInOrder(urls) {
  // 并发读取远程URL
  const textPromises = urls.map(async url => {
    const response = await fetch(url);
    return response.text();
  });
  // 按次序输出
  for (const textPromise of textPromises) {
    console.log(await textPromise);
  }
}
```

## Class

类不存在变量提升

```javascript
//定义类
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

事实上，类的所有方法都定义在类的 prototype 属性上面，类的内部所有定义的方法，都是不可枚举的（non-enumerable）

```javascript
class Point {
  constructor() {
    // ...
  }
  toString() {
    // ...
  }
  toValue() {
    // ...
  }
}
// 等同于
Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {}
};
```

由于类的方法都定义在 prototype 对象上面，所以类的新方法可以添加在 prototype 对象上面。 Object.assign 方法可以很方便地一次向类添加多个方法。

```javascript
class Point {
  constructor() {
    // ...
  }
}
Object.assign(Point.prototype, {
  toString() {},
  toValue() {}
});
```

this 指向，下面代码中， printName 方法中的 this ，默认指向 Logger 类的实例。但是，
如果将这个方法提取出来单独使用， this 会指向该方法运行时所在的环境，因为找不到 print 方法而导致报错

```javascript
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }
  print(text) {
    console.log(text);
  }
}
const logger = new Logger();
const { printName } = logger;
printName(); // TypeError: Cannot read property 'print' of undef
ined;
```

解决方案，构造方法里 `bind(this)`，或者使用箭头函数

```javascript
// bind(this)
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }
  // ...
}

// 箭头函数
class Logger {
  constructor() {
    this.printName = (name = 'there') => {
      this.print(`Hello ${name}`);
    };
  }
  // ...
}
```

`static`静态方法，可以被子类继承

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}
Foo.classMethod(); // 'hello'
var foo = new Foo();
foo.classMethod();
// TypeError: foo.classMethod is not a function
```

## 类修饰器@

> 目前，Babel 转码器已经支持 Decorator

[core-decorators.js](https://github.com/jayphelps/core-decorators)是一个第三方模块，提供了几个常见的修饰器，通过它可以更好地理解修饰器

`autobind` 修饰器使得方法中的 `this` 对象，绑定原始对象

```javascript
import { autobind } from 'core-decorators';
class Person {
  @autobind
  getPerson() {
    return this;
  }
}
let person = new Person();
let getPerson = person.getPerson;
getPerson() === person;
// true
```

`readonly` 修饰器使得属性或方法不可写。

```javascript
import { readonly } from 'core-decorators';
class Meal {
  @readonly
  entree = 'steak';
}
var dinner = new Meal();
dinner.entree = 'salmon';
// Cannot assign to read only property 'entree' of [object Object]
```

## Module 语法

模块功能主要由两个命令构成： export 和 import，一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取，import 和 export 命令只能在模块的顶层

- `export` 命令用于规定模块的对外接口，
- `import` 命令用于输入其他模块提供的功能

如果你希望外部能够读取模块内部的某个变量，就必须使用 export 关键字输出该变量

```javascript
// profile.js(比较捞)
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;

// 推荐
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;
export { firstName, lastName, year };
```

实际上`export`必须声明对外的接口，`{firstName}`代表一个对象`{firstname:fisrtName}`

```javascript
// 写法一
export var m = 1;
// 写法二
var m = 1;
export {m};
// 写法三
var n = 1;
export {n as m};
// 函数写法一
export function f() {};
// 函数写法二
function f() {}
export {f};
```

使用 `export` 命令定义了模块的对外接口以后，其他 JS 文件就可以通过 `import` 命令加载这个模块。

```javascript
// main.js
import { firstName, lastName, year } from './profile';
function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

as 重命名接口变量`.js`可以省略

```javascript
import { lastName as surname } from './profile';
```

模块的整体加载

```javascript
// circle.js
export function area(radius) {
  return Math.PI * radius * radius;
}
export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```

```javascript
import * as circle from './circle';
console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));
```

`export default`命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此 `export default`命令只能使用一次

```javascript
// 第一组
export default function crc32() {
  // ...
}
import crc32 from 'crc32'; // 输入
// 第二组
export function crc32() {
  // ...
}
import { crc32 } from 'crc32'; // 输入
```

因为 `export default` 命令其实只是输出一个叫做 `default` 的变量，所以它后面不能跟变量声明语句

```javascript
// 正确
export var a = 1;
// 正确
var a = 1;
export default a;
// 错误
export default var a = 1;
// MyClass.js
export default class { ... }
// main.js
import MyClass from 'MyClass';
let o = new MyClass();

```

跨模块常量

```javascript
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;
// test1.js 模块
import * as constants from './constants';
console.log(constants.A); // 1
console.log(constants.B); // 3
// test2.js 模块
import { A, B } from './constants';
console.log(A); // 1
console.log(B); // 3
```

如果要使用的常量非常多，可以建一个专门的 constants 目录，将各种常量写在不同的文件里面

```javascript
// constants/db.js
export const db = {
  url: 'http://my.couchdbserver.local:5984',
  admin_username: 'admin',
  admin_password: 'admin password'
};
// constants/user.js
export const users = ['root', 'admin', 'staff', 'ceo', 'chief', 'moderator'];
```

然后，将这些文件输出的常量，合并在 index.js 里面

```javascript
// constants/index.js
export { db } from './db';
export { users } from './users';
```

使用的时候，直接加载 index.js 就可以了。

```javascript
// script.js
import { db, users } from './index';
```

## ES6 模块与 CommonJS 模块差异

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口

CommonJS 模块输出的是值的拷贝，，模块内部的变化就影响不到这个值

```javascript
// lib.js
var counter = 3;
function incCounter() {
  counter++;
}
module.exports = {
  counter: counter,
  incCounter: incCounter
};
```

```javascript
// main.js
var mod = require('./lib');
console.log(mod.counter); // 3
mod.incCounter();
console.log(mod.counter); // 3
```

CommonJS 解决方案

```javascript
// lib.js
var counter = 3;
function incCounter() {
  counter++;
}
module.exports = {
  get counter() {
    return counter;
  },
  incCounter: incCounter
};
```

## Node 加载

Node 采用 CommonJS 模块格式，模块的输出都定义在 module.exports 这个属性上面

```javascript
// a.js
module.exports = {
  foo: 'hello',
  bar: 'world'
};
// 等同于
export default {
  foo: 'hello',
  bar: 'world'
};
```

## ES6 编码风格

let 取代 var

```javascript
'use strict';
if (true) {
  let x = 'hello';
}
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号

```javascript
// bad
const a = 'foobar';
const b = 'foo' + a + 'bar';
// acceptable
const c = `foobar`;
// good
const a = 'foobar';
const b = `foo${a}bar`;
const c = 'foobar';
```

函数的参数如果是对象的成员，优先使用解构赋值

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
}
// good
function getFullName(obj) {
  const { firstName, lastName } = obj;
}
// best
function getFullName({ firstName, lastName }) {}
```

函数返回多个值，优先使用对象的解构赋值

```javascript
// bad
function processInput(input) {
  return [left, right, top, bottom];
}
// good
function processInput(input) {
  return { left, right, top, bottom };
}
const { left, right } = processInput(input);
```

对象尽量静态化

```javascript
// bad
const a = {};
a.x = 3;
// if reshape unavoidable
const a = {};
Object.assign(a, { x: 3 });
// good
const a = { x: null };
a.x = 3;
```

如果对象的属性名是动态的

```javascript
// bad
const obj = {
  id: 5,
  name: 'San Francisco'
};
obj[getKey('enabled')] = true;
// good
const obj = {
  id: 5,
  name: 'San Francisco',
  ['say' + 'Something']() {
    return 'hello word';
  }
};
```

对象的属性和方法，尽量采用简洁表达法

```javascript
var ref = 'some value';
// bad
const atom = {
  ref: ref,
  value: 1,
  addValue: function(value) {
    return atom.value + value;
  }
};
// good
const atom = {
  ref,
  value: 1,
  addValue(value) {
    return atom.value + value;
  }
};
```

使用扩展运算符（...）拷贝数组

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}
// good
const itemsCopy = [...items];
```

使用 Array.from 方法，将类似数组的对象转为数组

```javascript
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

立即执行函数数可以写成箭头函数

```javascript
(() => {
  console.log('Welcome to the Internet.');
})();
```

箭头函数取代 Function.prototype.bind ，不应再用 self/\_this/that 绑定 this

```javascript
// bad
const self = this;
const boundMethod = function(...params) {
  return method.apply(self, params);
};
// acceptable
const boundMethod = method.bind(this);
// best
const boundMethod = (...params) => method.apply(this, params);
```

Module 语法是 JavaScript 模块的标准写法，坚持使用这种写法。使用 import 取代 require

```javascript
// bad
const moduleA = require('moduleA');
const func1 = moduleA.func1;
const func2 = moduleA.func2;
// good
import { func1, func2 } from 'moduleA';
```

不要在模块输入中使用通配符，如果模块默认输出一个对象，对象名的首字母应该大写

```javascript
const StyleGuide = {
  es6: {}
};
export default StyleGuide;
```

## ESLint

ESLint 是一个语法规则和代码风格的检查工具，可以用来保证写出语法正确、风格统一的代码

```bash
npm i -g eslint
```

安装 Airbnb 语法规则

```bash
npm i -g eslint-config-airbnb
```

最后，在项目的根目录下新建一个 .eslintrc 文件，配置 ESLint

```json
{
  "extends": "eslint-config-airbnb"
}
```

使用 ESLint 检查`index.js`

```bash
eslint index.js
```
