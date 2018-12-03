## 延迟脚本

HTML 4.01 为`<script>`标签定义了 defer 属性。这个属性的用途是表明脚本在执行时不会影响页 面的构造。也就是说，脚本会被延迟到整个页面都解析完毕后再运行。因此，在`<script>`元素中设置 defer 属性，相当于告诉浏览器立即下载，但延迟执行。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
  </head>
  <body>
    <!-- 这里放内容 -->
  </body>
</html>
```

## 异步脚本

HTML5 为`<script>`元素定义了 async 属性。async 只适用于外部脚本文件，并告诉浏览器立即下载文件。与 defer 不同的是，标记为 async 的脚本并不保证按照指定它们的先后顺序执行

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" async src="example1.js"></script>
    <script type="text/javascript" async src="example2.js"></script>
  </head>
  <body>
    <!--
      在以上代码中，第二个脚本文件可能会在第一个脚本文件之前执行。因此，确保两者之间互不依赖
      非常重要。指定 async 属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。
      为此，建议异步脚本不要在加载期间修改 DOM。
    -->
  </body>
</html>
```

## IE 浏览器兼容

粗暴解决方案:

```html
<!--[if lt IE 9
  ]><p class="kill-ie">微软都放弃了IE，为啥你却还不放弃？</p><!
[endif]-->
```

## 浏览器支持 javascript

包含在`<noscript>`元素中的内容只有在下列情况下才会显示出来：

- 浏览器不支持脚本；
- 浏览器支持脚本，但脚本被禁用。

符合上述任何一个条件，浏览器都会显示`<noscript>`中的内容。而在除此之外的其他情况下，浏览器不会呈现`<noscript>`中的内容。

```html
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
  </head>
  <body>
    <noscript> <p>本页面需要浏览器支持（启用）JavaScript。</p></noscript>
  </body>
</html>
```

## 关于{}

```javascript
// 有效但容易出错，不要使用
if (test) alert(1);
else alert(2);
```

## ECMAScript 数据类型

ECMAScript 变量可能包含两种不同数据类型的值：基本类型值和引用类型值，解析器必须确定这个值是基本类型值还是引用类型值，对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除其属性和方法。但是，我们不能给基本类型的值添加属性，尽管这样做不会导致任何错误。

- 基本类型(变量名和值都存储在栈区)：`Undefined(undefined)`、`Null(null)`、`Boolean`、`Number`、`String`
- 引用类型(变量名在栈区,变量值在堆区)：`Object`

```javascript
var person = new Object();
person.name = 'Nicholas';
alert(person.name); //"Nicholas"
// 对比
var name = 'Nicholas';
name.age = 27;
alert(name.age); //undefined
```

一些看不懂的骚东西

```javascript
var car = null;
typeof car; // "object"
var msg;
msg == null && msg == undefined; // true
// 强转Bollean类型
Boolean(123); // true
Boolean(0); // false
// 浮点数
var floatNum1 = 1; // 小数点后面没有数字——解析为 1
var floatNum2 = 10.0; // 整数——解析为 10
// 进制赋值
var hexNum1 = 0xa; // 十六进制的 10
var hexNum2 = 0x1f; // 十六进制的 31
```

对于那些极大或极小的数值，可以用 e 表示法（即科学计数法）表示的浮点数值表示。用 e 表示法表示的数值等于 e 前面的数值乘以 10 的指数次幂。浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数。例如，0.1 加 0.2 的结果不是 0.3，而是 0.30000000000000004

> 关于浮点数值计算会产生舍入误差的问题，有一点需要明确：这是使用基于
> IEEE754 数值的浮点计算的通病，ECMAScript 并非独此一家；其他使用相同数值格
> 式的语言也存在这个问题。

```javascript
var floatNum1 = 3.125e7; // 等于 31250000
var floatNum1 = 3.125e-2; // 等于 0.03125
```

## 深浅拷贝(待写)

...

## parseInt && parseFloat

在 ECMAScript 5 JavaScript 引擎中，parseInt()已经不具有解析八进制值的能力

```javascript
// 数值转换
parseInt('11.451啊大苏打'); // 11
parseInt('啊大苏打11.451'); // NaN
parseInt('0xA'); // 10（十六进制数）
parseInt('070'); // 70（八进制数）
parseInt('70'); // 70（十进制数）
var num1 = parseInt('10', 2); //2 （按二进制解析）
var num2 = parseInt('10', 8); //8 （按八进制解析）
var num3 = parseInt('10', 10); //10 （按十进制解析）
var num4 = parseInt('10', 16); //16 （按十六进制解析）
```

## string 类型

字符串可以由双引号（"）或单引号（'）表示,与 PHP 中的双引号和单引号会影响对字符串的解释方式不同，ECMAScript 中的这两种语法形式没
有什么区别。

```javascript
var value1 = 10;
var value2 = true;
var value3 = null;
var value4;
alert(String(value1)); // "10"
alert(String(value2)); // "true"
alert(String(value3)); // "null"
alert(String(value4)); // "undefined"
```

## ++ & --

```javascript
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2; // 等于 21
var num4 = num1 + num2; // 等于 21

var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2; // 等于 22
var num4 = num1 + num2; // 等于 21
```

## 隐式转换

```javascript
'' + 5 + 10; // "510"
```

## ==&&===

由于相等和不相等操作符存在类型转换问题，而为了保持代码中数据类型的完整性，我们推荐使用全等(`===`)和不全等(`!==`)操作符。

## 复合操作符

设计这些操作符的主要目的就是简化赋值操作。使用它们`不会`带来任何性能的提升。

## label & 循环

- break：跳出循环
- continue：跳过本轮循环

配合 break 使用，跳出全部循环

```javascript
var num = 0;
outermost: for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      break outermost;
    }
    num++;
  }
}
alert(num); //55
```

配合 continue 使用，跳出内部循环

```javascript
var num = 0;
outermost: for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      continue outermost;
    }
    num++;
  }
}
alert(num); //95
```

## switch

switch 语句在比较值时使用的是全等操作符，因此不会发生类型转换

```javascript
var num = '123';
switch (num) {
  case 123:
    alert('错误的类型');
    break;
  case '1' + 23:
    alert('正确');
    break;
  default:
    alert('没有正确的选项');
}
```

## 重载(伪)

```javascript
function doAdd(num1, num2) {
  if (arguments.length == 1) {
    alert(num1 + 10);
  } else if (arguments.length == 2) {
    alert(arguments[0] + num2);
  }
}
```

## 参数

我对于参数真是一无所知

```javascript
function setName(obj) {
  obj.name = 'Nicholas';
}
var person = new Object();
setName(person);
alert(person.name); // "Nicholas"
```

有很多开发人员错误地认为：在局部作用域中修改的对象会在全局作用域中反映出来，就说明
参数是按引用传递的。为了证明`对象是按值传递的`

```javascript
function setName(obj) {
  obj.name = 'Nicholas';
  console.log(obj); // {age: 18, name: "Nicholas"}
  obj = new Object();
  console.log(obj); // {}
  obj.name = 'Greg';
}
var person = new Object();
person.age = 18;
setName(person);
alert(person.name); // "Nicholas"
```

在把 person 传递给
setName()后，其 name 属性被设置为"Nicholas"。然后，又将一个新对象赋给变量 obj，同时将其 name 属性设置为"Greg"。如果 person 是按引用传递的，那么 person 就会自动被修改为指向其 name 属性值为"Greg"的新对象。但是，当接下来再访问 person.name 时，显示的值仍然是"Nicholas"。这说明即使在函数内部修改了参数的值，但原始的引用仍然保持未变。实际上，当在函数内部重写 obj 时，这个变量引用的就是一个局部对象了。而这个局部对象会在函数执行完毕后立即被销毁。

## 检测数据类型

要检测一个变量是不是基本数据类型，typeof 操作符是最佳的工具

```javascript
var s = 'Nicholas';
var b = true;
var i = 22;
var u;
var n = null;
var o = new Object();
alert(typeof s); //string
alert(typeof i); //number
alert(typeof b); //boolean
alert(typeof u); //undefined
alert(typeof n); //object
alert(typeof o); //object
```

特叔：

> 使用 typeof 操作符检测函数时，该操作符会返回"function"。在 Safari 5 及
> 之前版本和 Chrome 7 及之前版本中使用 typeof 检测正则表达式时，由于规范的原
> 因，这个操作符也返回"function"。ECMA-262 规定任何在内部实现[[Call]]方法
> 的对象都应该在应用 typeof 操作符时返回"function"。由于上述浏览器中的正则
> 表达式也实现了这个方法，因此对正则表达式应用 typeof 会返回"function"。在
> IE 和 Firefox 中，对正则表达式应用 typeof 会返回"object"。

虽然在检测基本数据类型时 typeof 是非常得力的助手，但在检测引用类型的值时，这个操作符的
用处不大。通常，我们并不是想知道某个值是对象，而是想知道它是什么类型的对象。为此，ECMAScript
提供了 instanceof 操作符，其语法如下所示：

- result = variable instanceof constructor

```javascript
alert(person instanceof Object); // 变量 person 是 Object 吗？
alert(colors instanceof Array); // 变量 colors 是 Array 吗？
alert(pattern instanceof RegExp); // 变量 pattern 是 RegExp 吗？
```

根据规定，所有引用类型的值都是 Object 的实例。因此，在检测一个引用类型值和 Object 构造函数时，instanceof 操作符始终会返回 true。当然，如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false，因为基本类型不是对象。

## 作用域链

> 本质就是是一个指向变量对象的指针列表，它只引用但不实际包含变量对象

每个函数都有自己的执行环境，当代码在一个环境中执行时，会创建变量对象的一个作用域链（Web 环境中 window 对象是祖先宿主对象)，当`执行流(看不见的手)`进入一个函数时，函数的环境就会被推入一个环境栈中。
而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。ECMAScript 程序中的执行流
正是由这个方便的机制控制着。每个环境都可以向上搜索作用域链，以查询变量和函数名；但任何环境都不能通过向下搜索作用域链而进入另一个执行环境。函数参数也被当作变量来对待(函数对象可以理解为局部变量)，因此其访问规则与执行环境中的其他变量相同。

```javascript
function aaa(aaa) {
  var bbb = 1;
  return function aa(aa) {
    var bb = 1;
    return function a() {
      return bbb + bb + '=>' + aaa + '-' + aa;
    };
  };
}
aaa(111)(11)(); // 2=>111-11
```

## 没有块级作用域

在 JavaScript 中，if、for 语句中的变量声明会将变量添加到当前的执行环境（在这里是全局环境）

```javascript
if (true) {
  var color = 'blue';
}
alert(color); //"blue"
// 同上
for (var i = 0; i < 10; i++) {
  doSomething(i);
}
alert(i); //10
```

使用 var 声明的变量会自动被添加到最接近的环境中，如果初始化变量时没有使用 var 声明，该变量会自动被添加到全局环境。

> 变量不声明直接初始化的先死个妈，老子反手就是一个'use strict'外加一个巴掌

```javascript
function add(num1, num2) {
  var sum = num1 + num2;
  return sum;
}
var result = add(10, 20); //30
alert(sum); //由于 sum 不是有效的变量，因此会导致错误
// 对比
function add(num1, num2) {
  sum = num1 + num2;
  return sum;
}
var result = add(10, 20); //30
alert(sum); //30
```

## 垃圾回收

探测树状宿主的执行环境、作用域链的各种变量，先标记为"可能有用"，如果`执行流`离开了这个执行环境，翻转这些标记，然后过段时间，就清楚它们

## Object 类

访问对象属性用`[]`、`.`都可以，但是`[]`更强大，里面可以传字符串变量，然而通常，除非必须使用变量来访问属性，否则我们建议使用点表示法

```javascript
var obj = new Object({ 'fisrt name': 'chenrui' });
obj.fisrt name; // 报错
obj["first name"]; // 'chenrui'
```

## Array 类型

如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。为了解决这个问题，ECMAScript 5 新增了 Array.isArray()方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的

```javascript
colors = ['red', 'blue', 'green'];
colors instanceof Array; // true
Array.isArray(colors); // true,推荐使用
```

如果不给 join()方法传入任何值，或者给它传入 undefined，则使用逗号作为分隔符

> 如果数组中的某一项的值是 null 或者 undefined，那么该值在 join()、
> toLocaleString()、toString()和 valueOf()方法返回的结果中以空字符串表示

```javascript
var colors = ['red', 'green', 'blue'];
alert(colors.join(',')); //red,green,blue
var nums = [1, 2, 3];
alert(nums.join('')); //'123'
```

## Array 常用操作

数组排序，有 bug，因为 sort 会把数组转字符串，然后比较，'5'>'15'，一般解决方案

```javascript
// 升序
function compare(value1, value2) {
  return value1 - value2;
}
// 降序
function compare(value1, value2) {
  return value2 - value1;
}
values.sort(compare);
```

数组反转

```javascript
var values = [0, 1, 5, 10, 15];
values.reverse(); // [15,10,5,1,0]
var values2 = ['asd', 'dfg', 'qwe', 'tyu'];
values2.reverse(); // ["tyu", "qwe", "dfg", "asd"]
```

数组合并
Array.concat(value，[1，2，3...]，...)，参数可以是数值，可以是数组，不限个数

```javascript
var colors = ['red', 'green', 'blue']; //red,green,blue
var colors2 = colors.concat('yellow', ['black', 'brown']); //red,green,blue,yellow,black,brown
colors.concat(colors2, 'chenrui'); //  ["red", "green", "blue", "red", "green", "blue", "yellow", "black", "brown", "chenrui"]
```

数组删除、插入、替换=>splice

- `splice(0,2)`会删除数组中的前两项
- `splice(2,0,"red","green")`会从当前数组的位置 2 开始插入字符串"red"和"green"
- `splice (2,1,"red","green")`会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串
  "red"和"green"

```javascript
var colors = ['red', 'green', 'blue'];
var removed = colors.splice(0, 1); // 删除第一项
alert(colors); // green,blue
alert(removed); // red，返回的数组中只包含一项
removed = colors.splice(1, 0, 'yellow', 'orange'); // 从位置 1 开始插入两项
alert(colors); // green,yellow,orange,blue
alert(removed); // 返回的是一个空数组
removed = colors.splice(1, 1, 'red', 'purple'); // 插入两项，删除一项
alert(colors); // green,red,purple,orange,blue
alert(removed); // yellow，返回的数组中只包含一项
```

数组下标查找

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
alert(numbers.indexOf(4)); //3
alert(numbers.indexOf(4444)); //-1
```

数组迭代

- every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
var everyResult = numbers.every(function(item, index, array) {
  return item > 2;
});
alert(everyResult); //false
```

- some()：对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
var someResult = numbers.some(function(item, index, array) {
  return item > 2;
});
alert(someResult); //true
```

- filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
var filterResult = numbers.filter(function(item, index, array) {
  return item > 2;
});
alert(filterResult); //[3,4,5,4,3]
```

- map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
var mapResult = numbers.map(function(item, index, array) {
  return item * 2;
});
alert(mapResult); //[2,4,6,8,10,8,6,4,2]
```

- forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。

```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
numbers.forEach(function(item, index, array) {
  //执行某些操作
});
```

## Date 类型

时间戳

```javascript
var timestamp = new Date().getTime() === Date.now() ? 1 : 0; // 1
```

## RegExp 类型

`var expression = / pattern / flags`

- g：表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止
- i：表示不区分大小写（case-insensitive）模式，即在确定匹配项时忽略模式与字符串的大小写
- m：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项

与其他语言中的正则表达式类似，模式中使用的所有元字符都必须转义。正则表达式中的元字符包括：
`( [ { \ ^ $ | ) ? * + .]}`

## Function 类型

递归

```javascript
function factorial(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * arguments.callee(num - 1);
  }
}
```

> 一定要牢记，函数的名字仅仅是一个包含指针的变量而已。因此，即使是在不同的环境中执行，全局的 sayColor()函数与 o.sayColor()指向的仍然是同一个函数。

```javascript
window.color = 'red';
var o = { color: 'blue' };
function sayColor() {
  alert(this.color);
}
sayColor(); //"red"
o.sayColor = sayColor;
o.sayColor(); //"blue"
```

## call()&apply()

call()(或 apply())扩充作用域，bind()绑定，在这里，sayColor()调用 bind()并传入对象 o，创建了 objectSayColor()函数。objectSayColor()函数的 this 值等于 o，因此即使是在全局作用域中调用这个函数，也会看到"blue"

```javascript
window.color = 'red';
var o = { color: 'blue' };
function sayColor() {
  alert(this.color);
}
sayColor.call(o); // 'blue'
sayColor.bind(o)(); // 'blue'
```

call()和 apply()传参

在使用 call()方法的情况下，callSum()必须明确地传入每一个参数。结果与使用 apply()没有什么不同。至于是使用 apply()还是 call()，完全取决于你采取哪种给函数传递参数的方式最方便。如果你打算直接传入 arguments 对象，或者包含函数中先接收到的也是一个数组，那么使用 apply()肯定更方便

```javascript
function sum(num1, num2) {
  return num1 + num2;
}
function callSum(num1, num2) {
  return sum.call(this, num1, num2);
}

function applySum(num1, num2) {
  return sum.apply(this, arguments);
}
alert(callSum(10, 10)); //20
alert(applySum(10, 10)); //20
```

妙用-apply 比较数组最大值、最小值

```javascript
var values = [1, 2, 3, 4, 5, 6, 7, 8];
var max = Math.max.apply(Math, values); // 8
var min = Math.min.apply(Math, values); // 1
```

## 基本包装类型

`Number`、`String`、`Boolean`是可以是基本类型，也可以是引用类型，最好永远不要使用，太特么操蛋了，拿`String`举例，大致过程如下：

- 创建 String 类型的一个实例；
- 在实例上调用指定的方法；
- 销毁这个实例。

可以将以上三个步骤想象成是执行了下列 ECMAScript 代码：

```javascript
var s1 = new String('some text');
var s2 = s1.substring(2);
s1 = null;
```

```javascript
var numObj = new Number(10);
numObj.name = '数值类型';
typeof numObj === 'object';
alert(numObj); // 10
alert(numObj.name); // '数值类型'
```

## Global 对象

> eval()解析字符串为执行代码，牵扯用户输入慎用，严格模式被 ban

Global（全局）对象可以说是 ECMAScript 中最特别的一个对象了，因为不管你从什么角度上看，这个对象都是不存在的。ECMAScript 中的 Global 对象在某种意义上是作为一个终极的“兜底儿对象”来定义的。换句话说，不属于任何其他对象的属性和方法，最终都是它的属性和方法。事实上，没有全局变量或全局函数；所有在全局作用域中定义的属性和函数，都是 Global 对象的属性。本书前面介绍过的那些函数，诸如 isNaN()、isFinite()、parseInt()以及 parseFloat()，实际上全都是 Global 对象的方法。除此之外，Global 对象还包含其他一些方法。

ECMAScript 虽然没有指出如何直接访问 Global 对象，但 Web 浏览器都是将这个全局对象作 window 对象的一部分加以实现的。因此，在全局作用域中声明的所有变量和函数，就都成为了 `window` 对象的属性，JavaScript 中的 window 对象除了扮演 ECMAScript 规定的 Global 对象的角色外，还承担了很多别的任务

## 面向对象-数据属性

数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有 4 个描述其行为的特性

- `[[Configurable]]`：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
- `[[Enumerable]]`：表示能否通过 for-in 循环返回属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
- `[[Writable]]`：表示能否修改属性的值。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
- `[[Value]]`：包含这个属性的数据值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。这个特性的默认值为 undefined。

> 要修改属性默认的特性，必须使用 ECMAScript 5 的 `Object.defineProperty()`方法。IE8 是第一个实现 Object.defineProperty()方法的浏览器版本，由于实现不彻底，建议读者不要在 IE8 中使用

```javascript
var person = {};
Object.defineProperty(person, 'name', {
  writable: false,
  value: 'Nicholas'
});
alert(person.name); //"Nicholas"
person.name = 'Greg'; // 无法修改
alert(person.name); //"Nicholas"
delete person.name; // 无法删除
alert(person.name); //"Nicholas"
```

## 面向对象-访问器属性

访问器属性不包含数据值；它们包含一对儿 getter 和 setter 函数（不过，这两个函数都不是必需的）。在读取访问器属性时，会调用 getter 函数，这个函数负责返回有效的值；在写入访问器属性时，会调用 setter 函数并传入新值，这个函数负责决定如何处理数据

- `[[Configurable]]`：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性或者能否把属性修改为数据属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
- `[[Enumerable]]`：表示能否通过 for-in 循环返回属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
- `[[Get]]`：在读取属性时调用的函数。默认值为 undefined。
- `[[Set]]`：在写入属性时调用的函数。默认值为 undefined。

```javascript
var book = {
  _year: 2004,
  edition: 1
};
Object.defineProperty(book, 'year', {
  get: function() {
    return this._year;
  },
  set: function(newValue) {
    if (newValue > 2004) {
      this._year = newValue;
      this.edition += newValue - 2004;
    }
  }
});
book.year = 2005;
alert(book.edition); //2
```

> `_year` 和 `edition`。`_year` 前面的下划线是一种常用的记号，用于表示只能通过对象方法访问的属性，通过 `Object.defineProperty(obj,attr,{get:()=>{},set:()=>{})` 遍历设置访问属性

## 面向对象-定义多个对象属性

```javascript
var book = {};
Object.defineProperties(book, {
  _year: {
    value: 2004
  },

  edition: {
    value: 1
  },
  year: {
    get: function() {
      return this._year;
    },
    set: function(newValue) {
      if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004;
      }
    }
  }
});
```

## 面向对象-属性描述器

在 JavaScript 中，可以针对任何对象，包括 DOM 和 BOM 对象，使用 Object.getOwnPropertyDescriptor()方法

```javascript
var book = {};
Object.defineProperties(book, {
  _year: {
    value: 2004
  },
  edition: {
    value: 1
  },
  year: {
    get: function() {
      return this._year;
    },
    set: function(newValue) {
      if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004;
      }
    }
  }
});
var descriptor = Object.getOwnPropertyDescriptor(book, '_year');
alert(descriptor.value); //2004
alert(descriptor.configurable); //false
alert(typeof descriptor.get); //"undefined"
var descriptor = Object.getOwnPropertyDescriptor(book, 'year');
alert(descriptor.value); //undefined
alert(descriptor.enumerable); //false
alert(typeof descriptor.get); //"function"
```

## 造对象-工厂模式

这种模式抽象了创建具体对象的过程

```javascript
function createPerson(name, age, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function() {
    alert(this.name);
  };
  return o;
}
var person1 = createPerson('Nicholas', 29, 'Software Engineer');
var person2 = createPerson('Greg', 27, 'Doctor');
```

## 造对象-构造函数模式

```javascript
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() {
    alert(this.name);
  };
}
var person1 = new Person('Nicholas', 29, 'Software Engineer');
var person2 = new Person('Greg', 27, 'Doctor');
```

## 造对象-原型模式

ECMAScript 5 增加了一个新方法，叫 Object.getPrototypeOf()，在所有支持的实现中，这个
方法返回`[[Prototype]]`的值

```javascript
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
};
var person1 = new Person();
person1.sayName(); //"Nicholas"
var person2 = new Person();
person2.sayName(); //"Nicholas"
alert(person1.sayName == person2.sayName); //true
// Object.getPrototypeOf()
alert(Object.getPrototypeOf(person1) == Person.prototype); //true
alert(Object.getPrototypeOf(person1).name); //"Nicholas"
```

当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性；换句话说，添加这个属性只会阻止我们访问原型中的那个属性，但不会修改那个属性。即使将这个属性设置为 null，也只会在实例中设置这个属性，而不会恢复其指向原型的连接。不过，使用 `delete` 操作符则可以完全删除实例属性，从而让我们能够重新访问原型中的属性，如下所示。

```javascript
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();
person1.name = 'Greg';
alert(person1.name); //"Greg"——来自实例
alert(person2.name); //"Nicholas"——来自原型
delete person1.name;
alert(person1.name); //"Nicholas"——来自原型
```

使用 `hasOwnProperty()`方法可以检测一个属性是存在于实例中，还是存在于原型中。这个方法（不
要忘了它是从 Object 继承来的）只在给定属性存在于对象实例中时，才会返回 true

```javascript
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();
alert(person1.hasOwnProperty('name')); //false
person1.name = 'Greg';
alert(person1.name); //"Greg"——来自实例
alert(person1.hasOwnProperty('name')); //true
alert(person2.name); //"Nicholas"——来自原型
alert(person2.hasOwnProperty('name')); //false
delete person1.name;
alert(person1.name); //"Nicholas"——来自原型
alert(person1.hasOwnProperty('name')); //false
```

由于 in 操作符会在通过对象能够访问给定属性时返回 true，无论该属性存在于实例中还是原型中

```javascript
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();
alert(person1.hasOwnProperty('name')); //false
alert('name' in person1); //true
person1.name = 'Greg';
alert(person1.name); //"Greg" ——来自实例
alert(person1.hasOwnProperty('name')); //true
alert('name' in person1); //true
```

而 `hasOwnProperty()`只在属性存在于实例中时才返回 true
判断属性在原型中还是在实例化对象中，结合 `in` 操作符和 `true，hasOwnProperty()`，就可以判断这个属性是在实例化对象中还是原型中

```javacript
function isPrototypePropery(object, name){
 return !object.hasOwnProperty(name) && (name in object);
}
```

补充：
在使用 for-in 循环时，返回的是所有能够通过对象访问的、可枚举的（enumerated）属性，其中既包括存在于实例中的属性，也包括存在于原型中的属性。屏蔽了原型中不可枚举属性（即将`[[Enumerable]]`标记为 false 的属性）的实例属性也会在 for-in 循环中返回，因为根据规定，所有开发人员定义的属性都是可枚举的

Object.keys()方法：取得对象上所有`可枚举`的实例属性
Object.getOwnPropertyNames()：所有实例属性，`无论它是否可枚举`

```javascript
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
};
var keys = Object.keys(Person.prototype);
alert(keys); //"name,age,job,sayName"
var p1 = new Person();
p1.name = 'Rob';
p1.age = 31;
var p1keys = Object.keys(p1);
alert(p1keys); //"name,age"
var keys2 = Object.getOwnPropertyNames(Person.prototype);
alert(keys2); //"constructor,name,age,job,sayName"
var p1keys2 = Object.getOwnPropertyNames(p1);
alert(p1keys2); //"name,age"
```

原型的动态性：

对原型对象所做的任何修改都能够立即从已实例化的对象上反映出来

```javascript
var friend = new Person();
Person.prototype.sayHi = function() {
  alert('hi');
};
friend.sayHi(); //"hi"（没有问题！）
```

但如果是重写整个原型对象会报错

```javascript
function Person() {}
var friend = new Person();

Person.prototype = {
  constructor: Person,
  name: 'Nicholas',
  age: 29,
  job: 'Software Engineer',
  sayName: function() {
    alert(this.name);
  }
};
friend.sayName(); //error
```

## 造对象-构造函数+原型链-推荐

构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。

```javascript
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ['Shelby', 'Court'];
}
Person.prototype = {
  constructor: Person,
  sayName: function() {
    alert(this.name);
  }
};
var person1 = new Person('Nicholas', 29, 'Software Engineer');
var person2 = new Person('Greg', 27, 'Doctor');
person1.friends.push('Van');
alert(person1.friends); //"Shelby,Count,Van"
alert(person2.friends); //"Shelby,Count"
alert(person1.friends === person2.friends); //false
alert(person1.sayName === person2.sayName); //true
```

## 继承

ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型链来实现的

```javascript
function SuperType() {
  this.property = true;
}
SuperType.prototype.getSuperValue = function() {
  return this.property;
};
function SubType() {
  this.subproperty = false;
}
//继承了 SuperType
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function() {
  return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue()); //true
```

## 继承-组合寄生

```javascript
function inheritPrototype(subType, superType) {
  var prototype = Object(superType.prototype); //创建对象
  prototype.constructor = subType; //增强对象
  subType.prototype = prototype; //指定对象
}
function SuperType(name) {
  this.name = name;
  this.colors = ['red', 'blue', 'green'];
}
SuperType.prototype.sayName = function() {
  alert(this.name);
};
function SubType(name, age) {
  SuperType.call(this, name);
  this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function() {
  alert(this.age);
};
```

## 递归

一个函数通过名字调用自身，arguments.callee 是一个指向正在执行的函数的指针，在编写递归函数时，使用 arguments.callee 总比使用函数名更保险，严格模式下还是用函数名吧

## 闭包

当在函数内部定义了其他函数时，就创建了闭包。闭包有权访问包含函数内部的所有变量，根本原因，就是函数执行流程：创建执行环境=>创建作用域链(由内而外逐级搜索，知道全局)

```javascript
function wrap(prop) {
  var name = 'wrapper';
  return function() {
    console.log(prop);
    return name;
  };
}
wrap('我是外层属性')(); // "wrapper"
```

IE 中如果闭包作用域链中存在着 DOM 对象，那么就无法被销毁，内存也就泄露了

```javascript
function assignHandler() {
  var element = document.getElementById('someElement');
  element.onclick = function() {
    alert(element.id);
  };
}
```

常规解决办法

```javascript
function assignHandler() {
  var element = document.getElementById('someElement');
  var id = element.id;

  element.onclick = function() {
    alert(id);
  };

  element = null;
}
```

## 块级作用于的实现

JavaScript 没有块级作用域的概念

```javascript
function outputNumbers(count) {
  for (var i = 0; i < count; i++) {
    console.log(i); // 0、1、2
  }
  console.log(i); // 3
}
```

如何弄一个私有作用域的方式

```javascript
(function() {
  //这里是块级作用域(私有作用域)
})();
```

解决方案：
这种技术经常在全局作用域中被用在函数外部，从而限制向全局作用域中添加过多的变量和函数。一般来说，我们都应该尽量少向全局作用域中添加变量和函数。在一个由很多开发人员共同参与的大型应用程序中，过多的全局变量和函数很容易导致命名冲突。而通过创建私有作用域，每个开发人员既可以使用自己的变量，又不必担心搞乱全局作用域

```javascript
function outputNumbers(count) {
  (function() {
    for (var i = 0; i < count; i++) {
      alert(i);
    }
  })();

  alert(i); //导致一个错误！
}
```

定义了两个特权方法：getName()和 setName()。这两个方法都可以在构造函数外部使用，而且都有权访问私有变量 name。但在 Person 构造函数外部，没有任何办法访问 name。由于这两个方法是在构造函数内部定义的，它们作为闭包能够通过作用域链访问 name。

```javascript
function Person(name) {
  this.getName = function() {
    return name;
  };
  this.setName = function(value) {
    name = value;
  };
}
var person = new Person('Nicholas');
alert(person.getName()); //"Nicholas"
person.setName('Greg');
alert(person.getName()); //"Greg"
```

## BOM

系统对话框
`alert()、confirm()、prompt()`

位置操作

```javascript
location.assign('http://www.wrox.com');
location.href = 'http://www.wrox.com';
location.reload(); // 有缓存
location.reload(true); // 清缓存;
```

`navigator`对象

```javascript
navigator.language; // 'zh-CN'
navigator.mimeTypes; // 在浏览器中注册的MIME类型数组
navigator.onLine; // 是否连接到了因特网
navigator.userAgent; // 用户代理字符串

//检测插件（在 IE 中无效）
function hasPlugin(name) {
  name = name.toLowerCase();
  for (var i = 0; i < navigator.plugins.length; i++) {
    if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1) {
      return true;
    }
  }
  return false;
}

alert(hasPlugin('Flash'));
alert(hasPlugin('QuickTime'));

//检测 IE 中的插件
function hasIEPlugin(name) {
  try {
    new ActiveXObject(name);
    return true;
  } catch (ex) {
    return false;
  }
}
//检测 Flash
alert(hasIEPlugin('ShockwaveFlash.ShockwaveFlash'));
//检测 QuickTime
alert(hasIEPlugin('QuickTime.QuickTime'));
```

history 对象

```javascript
//后退一页
history.go(-1);
//前进一页
history.go(1);
//前进两页
history.go(2);
```

## DOM

HTML5 添加的 `getElementsByClassName()`方法是最受人欢迎的一个方法
HTML5 规定可以为元素添加非标准的属性，但要添加前缀 data-
对于使用短划线（分隔不同的词汇，例如 background-image）的 CSS 属性名，必须将其转换成驼峰大小写形式

```javascript
el.focus(); // 聚焦
el.hasFocus(); // el是否聚焦
el.outerHTML; // 返回el及其后代节点序列化字符串
if (document.readyState == 'complete') {
  console.log('页面加载完成');
} else if (document.readyState == 'loading') {
  console.log('页面加载中');
}
```

## 事件

冒泡(event bubbling)文档中嵌套层次最深的那个节点接收，然后逐级向上传播
捕获(event capturing)

监听
handle 如果是匿名函数无法被移除，事件处理程序不是以添加它们的顺序执行，而是以相反的顺序被触发

```javascript
// 一般常用冒泡
el.addEventListener('click', handle, false); // 冒泡阶段处理
el.addEventListener('click', handle, true); // 捕获阶段处理
el.removeEventListener('click', handle, false); // 移除
```

```javascript
// 取消事件默认行为
var link = document.getElementById('myLink');
link.onclick = function(event) {
  event.preventDefault();
};

// 立即停止事件在 DOM 层次中的传播
var btn = document.getElementById('myBtn');
btn.onclick = function(event) {
  alert('Clicked');
  event.stopPropagation();
};
document.body.onclick = function(event) {
  alert('Body clicked');
};
```

兼容 IE

```javascript
var e = e || window.event;
```

常用事件

- load：当页面完全加载
- mousewheel：滚轮
- keydown：按下键盘任意键，不放回重复触发
- keyup：释放键盘
  - keyCode：按下的键码
    - Del：46
    - Enter：13
    - Backspace：8
    - Tab：9
    - Esc：27
    - capsLock：20
- beforeunload：关闭网页前弹出对话框
- DOMContentLoaded：在 DOM 树后触发，与 load 不同，允许页面在下载的早期添加事件处理程序

常用事件对象

- e.target || e.srcElement：事件对象
- e.clientX || e.clientY：浏览器视口坐标
- e.screenX || e.scrennY：显示器坐标

## DOM2 变动事件(IE9 & +)

检测出浏览器是否支持变动事件

```javascript
document.implementation.hasFeature('MutationEvents', '2.0');
```

DOMSubtreeModified：在 DOM 结构中发生任何变化时触发。这个事件在其他任何事件触发
后都会触发。

- DOMNodeInserted：在一个节点作为子节点被插入到另一个节点中时触发。
- DOMNodeRemoved：在节点从其父节点中被移除时触发。
- DOMNodeInsertedIntoDocument：在一个节点被直接插入文档或通过子树间接插入文档之后触发。这个事件在 DOMNodeInserted 之后触发。
- DOMNodeRemovedFromDocument：在一个节点被直接从文档中移除或通过子树间接从文档中移除之前触发。这个事件在 DOMNodeRemoved 之后触发。
- DOMAttrModified：在特性被修改之后触发。
- DOMCharacterDataModified：在文本节点的值发生变化时触发。

```html
<! DOCTYPE html>
<html>
<head>
 <title>Node Removal Events Example</title>
</head>
<body>
 <ul id="myList">
 <li>Item 1</li>
 <li>Item 2</li>
 <li>Item 3</li>
 </ul>
</body>
</html>
```

```javascript
window.addEventListener('load', function(event) {
  var list = document.getElementById('myList');

  document.addEventListener('DOMSubtreeModified', function(event) {
    alert(event.type);
    alert(event.target);
  });
  document.addEventListener('DOMNodeRemoved', function(event) {
    alert(event.type);
    alert(event.target);
    alert(event.relatedNode);
  });
  list.firstChild.addEventListener('DOMNodeRemovedFromDocument', function(
    event
  ) {
    alert(event.type);
    alert(event.target);
  });

  list.parentNode.removeChild(list);
});
```

## 事件委托

对“事件处理程序过多”问题的解决方案就是事件委托，。事件委托利用了事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件，最适合采用事件委托技术的事件包括 `click、mousedown、mouseup、keydown、keyup` 和 `keypress`，例如可以委托给 `document` 对象，在页面生命周期任何时间点都阔以。

```javascript
document.addEventListener('click', function(e) {
  var e = e || window.event;
  if (e.target.id === 'dom2-变动事件ie9-amp-')
    alert('成功冒泡到document委托触发click');
});
```

## 事件模拟

可以在 `document` 对象上使用 `createEvent()`方法创建 `event` 对象，初始化 event 对象后，使用 `dispatchEvent()`方法处罚，该事件就跻身“官方事件”之列了

创建一个通用键盘事件

```javascript
var textbox = document.getElementById('myTextbox');
//创建事件对象
var event = document.createEvent('Events');
//初始化事件对象
event.initEvent(type, bubbles, cancelable); // type（字符串）：触发的事件类型，例如"keydown"
event.view = document.defaultView;
event.altKey = false;
event.ctrlKey = false;
event.shiftKey = false;
event.metaKey = false;
event.keyCode = 65;
event.charCode = 65;
//触发事件
textbox.dispatchEvent(event);
```

## 表单

常用属性

- acceptCharset：服务器能够处理的字符集；等价于 HTML 中的 accept-charset 特性。
- action：接受请求的 URL；等价于 HTML 中的 action 特性。
- elements：表单中所有控件的集合（HTMLCollection）。
- enctype：请求的编码类型；等价于 HTML 中的 enctype 特性。
- length：表单中控件的数量。
- method：要发送的 HTTP 请求类型，通常是"get"或"post"；等价于 HTML 的 method 特性。
- name：表单的名称；等价于 HTML 的 name 特性。
- reset()：将所有表单域重置为默认值。
- submit()：提交表单。
- target：用于发送请求和接收响应的窗口名称；等价于 HTML 的 target 特性。

提交表单

使用`<input>`或`<button>`都可以定义提交按钮，只要将其 `type` 特性的值设置为`"submit"`即可，而图像按钮则是通过将`<input>`的 `type` 特性值设置为`"image"`来定义的

```html
<!-- 通用提交按钮 -->
<input type="submit" value="Submit Form" />
<!-- 自定义提交按钮 -->
<button type="submit">Submit Form</button>
<!-- 图像按钮 -->
<input type="image" src="graphic.gif" />
```

或者编程式提交，记得验证表单数据，提交表单时可能出现的最大问题，就是重复提交表单，在第一次提交表单后就禁用提交按钮，或者利用 onsubmit 事件处理程序取消后续的表单提交操作

```javascript
var form = document.getElementById('myForm');
//提交表单
form.submit();
// 侦听 submit 事件，并在该事件发生时禁用提交按钮即可
form.addEventListener('submit', function(event) {
  var e = e || window.event;
  var target = e.srcElement || e.target;
  //取得提交按钮
  var btn = target.elements['submit-btn'];
  //禁用它
  btn.disabled = true;
});
```

获得表单元素

```javascript
// www.taobao.com
var form = i < document.getElementById('J_TSearchForm').elements;
for (var i = 0; form.length; i++) {
  console.log(form.elements[i]);
}
```

常规操作

自动聚焦第一个表单

```javascript
window.addEventListener('load', function(event) {
  document.forms[0].element[0].focus();
});
```

或者 HTML5 新增`autofocus`

```html
<input type="text" autofocus />
```

剪切板

```javascript
var EventUtil = {
  getClipboardText: function(event){
    var clipboardData = (event.clipboardData || window.clipboardData);
    return clipboardData.getData("text");
  },
  setClipboardText: function(event, value){
    if (event.clipboardData){
      return event.clipboardData.setData("text/plain", value);
    } else if (window.clipboardData){
      return window.clipboardData.setData("text", value); // IE
  }
```

富文本

`contenteditable`，即就可以编辑该元素页面中的任何元素

```javascript
var div = document.getElementById('richedit');
div.contentEditable = 'true';
```

操作富文本

`document.execCommand()`：可以对文档执行预定义的命令

- copy：将选择的文本复制到剪贴板
- cut：将选择的文本剪切到剪贴板

## Canvas

使用`<canvas>`元素，必须先设置其 `width` 和 `height` 属性，指定可以绘图的区域大小。

```javascript
var drawing = document.getElementById('drawing');
//确定浏览器支持<canvas>元素
if (drawing.getContext) {
  var context = drawing.getContext('2d');
  //取得图像的数据 URI
  var imgURI = drawing.toDataURL('image/png');
  //显示图像
  var image = document.createElement('img');
  image.src = imgURI;
  document.body.appendChild(image);
}
```

使用 2D 绘图上下文提供的方法，可以绘制简单的 2D 图形，比如矩形、弧线和路径。2D 上下文的坐标开始于`<canvas>`元素的左上角，原点坐标是`(0,0)`

## 跨文档消息传递(Web Messaging)

简称为 XDM，，指的是在来自不同域的页面间传递消息。核心是`postMessage()`方法，XDM 已经作为一个规范独立出来，现在它的名字叫 `Web Messaging`，官方页面是`http://dev.w3.org/html5/postmsg/`

```javascript
// 注意：所有支持 XDM 的浏览器也支持 iframe 的 contentWindow 属性
var iframeWindow = document.getElementById('myframe').contentWindow;
// 向内嵌框架中发送一条消息，指定框架中的文档必须来源于"http://www.wrox.com"域
iframeWindow.postMessage('A secret', 'http://www.wrox.com');
// 回执消息
window.addEventListener('message', function(event) {
  if (event.origin == 'http://www.wrox.com') {
    //处理接收到的数据
    processMessage(event.data);
    //可选：向来源窗口发送回执
    event.source.postMessage('Received!', 'http://p2p.wrox.com');
  }
});
```

接收到 XDM 消息时，会触发 `window` 对象的 `message` 事件。这个事件是以异步形式触发的

## 媒体元素

`<video>`和`<audio>`元素都提供了完善的 JavaScript 接口，这两个媒体元素还可以触发很多事件

```html
<!-- 嵌入视频 -->
<video id="myVideo">
  <source src="conference.webm" type="video/webm; codecs='vp8, vorbis'" />
  <source src="conference.ogv" type="video/ogg; codecs='theora, vorbis'" />
  <source src="conference.mpg" />
  Video player not available.
</video>
<!-- 嵌入音频 -->
<audio id="myAudio">
  <source src="song.ogg" type="audio/ogg" />
  <source src="song.mp3" type="audio/mpeg" />
  Audio player not available.
</audio>
```

## try-catch

```javascript
try {
  // 可能会导致错误的代码
} catch (error) {
  // 在错误发生时怎么处理
} finally {
  // 无论如何都会执行
}

// 抛异常
function process(value) {
  if (values instanceof Array) {
    return 1;
  } else {
    throw new Error('Something bad happened.');
  }
}
function use() {
  try {
    console.log(process(1));
  } catch (err) {
    console.log(err.message); // 控制台打印 Something bad happened.
  }
}
```

## JSON

JSON.stringify()除了要序列化的 JavaScript 对象外，还可以接收另外两个参数，这两个参数用于指定以不同的方式序列化 JavaScript 对象。第一个参数是个过滤器，可以是一个数组，也可以是一个函数；第二个参数是一个选项，表示是否在 JSON 字符串中保留缩进。

```javascript
// JSON.stringify()数组过滤器
var book = {
  title: 'Professional JavaScript',
  authors: ['Nicholas C. Zakas'],
  edition: 3,
  year: 2011
};
var jsonText = JSON.stringify(book, ['title', 'edition']);
// JSON.stringify()函数过滤器
var book = {
  title: 'Professional JavaScript',
  authors: ['Nicholas C. Zakas'],
  edition: 3,
  year: 2011
};
var jsonText = JSON.stringify(book, function(key, value) {
  switch (key) {
    case 'authors':
      return value.join(',');
    case 'year':
      return 5000;
    case 'edition':
      return undefined;
    default:
      return value;
  }
});
// 是否保留缩进
var book = {
  title: 'Professional JavaScript',
  authors: ['Nicholas C. Zakas'],
  edition: 3,
  year: 2011
};
var jsonText = JSON.stringify(book, null, 4);
/*
  // 返回
  {
    "title": "Professional JavaScript",
    "authors": [
    "Nicholas C. Zakas"
    ],
    "edition": 3,
    "year": 2011
  }

*/
```

## Ajax

Ajax 技术的核心是 XMLHttpRequest 对象（简称 XHR）

get 请求

```javascript
function addURLParam(url, name, value) {
  url += url.indexOf('?') == -1 ? '?' : '&';
  url += encodeURIComponent(name) + '=' + encodeURIComponent(value);
  return url;
}
// 接口地址
var url = 'example.php';
// 添加参数
url = addURLParam(url, 'name', 'Nicholas');
url = addURLParam(url, 'book', 'Professional JavaScript');
// 初始化请求
xhr.open('get', url, false);
```

## 跨域

JSONP 是 JSON with padding（填充式 JSON 或参数式 JSON）的简写，是应用 JSON 的一种新方法，是通过动态`<script>`元素(`<script>`元素有能力不受限制地从其他域加载资源)

```javascript
function handleResponse(response) {
  alert(
    'You’re at IP address ' +
      response.ip +
      ', which is in ' +
      response.city +
      ', ' +
      response.region_name
  );
}
var script = document.createElement('script');
script.src = 'http://freegeoip.net/json/?callback=handleResponse';
document.body.insertBefore(script, document.body.firstChild);
```

## Comet To WebSocket

Comet 是一种更高级的 Ajax 技术（经常也有人称为“服务器推送”）。Ajax 是一种从页面向服务器请求数据的技术，而 Comet 则是一种服务器向页面推送数据的技术。但是容易出错，衍生出`Web Socket`

Web Sockets 使用了自定义的协议，所以 URL 模式也略有不同。未加密的连接不再是 http://，而是 ws://；加密的连接也不是 https://，而是 wss://。

要创建 Web Socket，先实例一个 WebSocket 对象并传入要连接的 URL：

```javascript
// 同源策略对 Web Sockets 不适用，因此可以通过它打开到任何站点的连接，通过握手信息就可以知道请求来自何方
var socket = new WebSocket('ws://www.example.com/server.php');
```

WebSocket 也有一个 readyState 类似 readystatechange

- WebSocket.OPENING (0)：正在建立连接。
- WebSocket.OPEN (1)：已经建立连接。
- WebSocket.CLOSING (2)：正在关闭连接。
- WebSocket.CLOSE (3)：已经关闭连接。

关闭 WebSocket 连接

```javascript
socket.close(); // 可以在任何时候调用
```

发送消息

```javascript
var socket = new WebSocket('ws://www.example.com/server.php');
socket.send('Hello world!'); // 单纯文本
socket.send(JSON.stringify({ name: 'grey' })); // 序列化对象
```

当服务器向客户端发来消息时，WebSocket 对象就会触发 message 事件，把返回的数据保存在 event.data 属性中

```javascript
socket.onmessage = function(event) {
  var data = event.data;
};
```

## 对象防篡改

不可扩展对象

```javascript
var person = { name: 'Nicholas' };
Object.preventExtensions(person);
person.age = 29;
alert(person.age); //undefined
```

密封对象

```javascript
var person = { name: 'Nicholas' };
Object.seal(person);
person.age = 29;
alert(person.age); //undefined
delete person.name;
alert(person.name); //"Nicholas"
```

冻结对象

```javascript
var person = { name: 'Nicholas' };
Object.freeze(person);
person.age = 29;
alert(person.age); //undefined
delete person.name;
alert(person.name); //"Nicholas"
person.name = 'Greg';
alert(person.name); //"Nicholas"
```

## 重复的定时器

`setInterval`或者使用链式`setTimeout()`，这个模式链式调用了 setTimeout()，每次函数执行的时候都会创建一个新的定时器。第二个 setTimeout()调用使用了 arguments.callee 来获取对当前执行的函数的引用，并为其设置另外一个定时器。这样做的好处是，在前一个定时器代码执行完之前，不会向队列插入新的定时器代码，确保不会有任何缺失的间隔。

```javascript
setTimeout(function() {
  //处理中
  setTimeout(arguments.callee, interval);
}, interval);
```

## 离线应用

检测是否离线：`navigator.onLine`

## 应用缓存

HTML5 的应用缓存（application cache），或者简称为 appcache，是专门为开发离线 Web 应用而设计的。Appcache 就是从浏览器的缓存中分出来的一块缓存区。要想在这个缓存中保存数据，可以使用一个描述文件（manifest file），核心是`applicationCache`对象，这个对象有一个 `status` 属性，以及很多事件

```xml
CACHE MANIFEST
#Comment
file.js
file.css
```
