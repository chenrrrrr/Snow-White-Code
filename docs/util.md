## 简化 console.log

```javascript
var log = console.log.bind(console);
log(1, 2, 3, 4, 5); // 1 2 3 4 5
```

## 倒计时

ES6 实现

```javascript
var log = console.log.bind(console);
class Countdown {
  constructor(startNum, endNum, interval) {
    [this.startNum, this.endNum, this.interval] = [startNum, endNum, interval];
  }
  execute() {
    var timer = setTimeout(() => {
      if (this.startNum >= this.endNum) {
        log(this.startNum);
        this.startNum -= 1;
        this.execute();
      } else {
        clearTimeout(timer);
      }
    }, this.interval);
  }
}
// 实例化调用
var countdown = new Countdown(5, 0, 1000).execute();
```

ES5 实现

```javascript
var log = console.log.bind(console);
function countdown(startNum, endNum, interval) {
  var timer = setTimeout(function() {
    if (startNum >= endNum) {
      log(startNum);
      startNum -= 1;
      countdown(startNum, endNum, interval);
    } else {
      clearTimeout(timer);
    }
  }, interval);
}
// 调用
countdown(5, 0, 1000);
```

## 范围随机数

```javascript
function getRandomRangeNum(min, max) {
  return min + Math.floor(Math.random() * (max - min));
}
```

## 随机渐变背景

```javascript
function getRandomRangeNum(min, max) {
  return min + Math.floor(Math.random() * (max - min));
}

function setRandomBg(el) {
  var left = getRandomRangeNum(0, 255);
  var bottom = getRandomRangeNum(0, 255);
  var css = ['linear-gradient(to left bottom,hsl(', left, ', 100%, 85%) 0%,hsl(', bottom, ', 100%, 85%) 100%)'];
  el.style.background = css.join('');
}
```

## ul 下 li 居中

```html
<!--外层包个div/section block元素 -->
<div>
  <ul class="clearfix">
    <li>1</li>
    <li>2</li>
  </ul>
</div>
```

```css
div{
  text-align: center
}
ul{
  display: inline-block
}
li{
  display: inline
  float: left
}
```

## 获取当前月的天数

```javascript
function getCurMonthDays() {
  return new Date(new Date().getFullYear(), new Date().getMonth() + 1, 0).getDate();
}
```

## 常用 js 正则

- Email 地址:`^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$`
- 域名:`[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(/.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+/.?`
- InternetURL:`[a-zA-z]+://[^\\s]* 或 ^http://([\\w-]+\\.)+[\\w-]+(/[\\w-./?%&=]*)?$`
- 电话号码(“XXX-XXXXXXX”、”XXXX-XXXXXXXX”、”XXX-XXXXXXX”、”XXX-XXXXXXXX”、”XXXXXXX”和”XXXXXXXX):`^(\\(\\d{3,4}-)|\\d{3.4}-)?\\d{7,8}$`
- 国内电话：`\\d{3}-\\d{8}|\\d{4}-\\d{7}`
- 身份证号(15 位、18 位数字)：`^\\d{15}|\\d{18}$`
- 短身份证号码：`^([0-9]){7,18}(x|X)?$`或`^\\d{8,18}|[0-9x]{8,18}|[0-9X]{8,18}?$`
- 帐号是否合法(字母开头，允许 5-16 字节，允许字母数字下划线):`^[a-zA-Z][a-zA-Z0-9_]{4,15}$`
- 密码(以字母开头，长度在 6~18 之间，只能包含字母、数字和下划线)：`^[a-zA-Z]\\w{5,17}$`
- 强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在 8-10 之间)：`^(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$`
- 日期格式：`^\\d{4}-\\d{1,2}-\\d{1,2}`
- 一年的 12 个月(01 ～ 09 和 1 ～ 12)：`^(0?[1-9]|1[0-2])$`
- 一个月的 31 天(01 ～ 09 和 1 ～ 31)：`^((0?[1-9])|((1|2)[0-9])|30|31)$`
- 手机：`/^1\d{10}$/`
- 腾讯 QQ 号：`[1-9][0-9]{4,}`(腾讯 QQ 号从 10000 开始)
- 中国邮政编码：`[1-9]\\d{5}(?!\\d)`(中国邮政编码为 6 位数字)
- IP 地址：`\\d+\\.\\d+\\.\\d+\\.\\d+`(提取 IP 地址时有用)
- 空白行的正则表达式：`\ \\s*\\r`
- 车牌：`/^[京津沪渝冀豫云辽黑湘皖鲁新苏浙赣鄂桂甘晋蒙陕吉闽贵粤青藏川宁琼使领A-Z]{1}[A-Z]{1}[A-Z0-9]{4}[A-Z0-9挂学警港澳]{1}$/`
- 验证码：`/^\d{6}$/`
- 中文：`/^[\u4E00-\u9FA5]{2,6}$/`
- 数字：`^[0-9]*$`
- n 位数字：`^\\d{n}$`
- 至少 n 位数字：`^\\d{n,}$`
- m-n 位的数字：`^\\d{m,n}$`
- 零和非零开头的数字：`1^(0|[1-9][0-9]*)$`
- 非零开头的最多带两位小数的数字：`^([1-9][0-9]*)+(.[0-9]{1,2})?$`
- 带 1-2 位小数的正数或负数：`^(\\-)?\\d+(\\.\\d{1,2})?$`
- 正数、负数、和小数：`^(\\-|\\+)?\\d+(\\.\\d+)?$`
- 有两位小数的正实数：`^[0-9]+(.[0-9]{2})?$`
- 有 1~3 位小数的正实数：`^[0-9]+(.[0-9]{1,3})?$`
- 非零的正整数：`^[1-9]\\d*$或 ^([1-9][0-9]*){1,3}$或 ^\\+?[1-9][0-9]*$`
- 非零的负整数：`^\\-[1-9][]0-9\"*$或^-[1-9]\\d*$`
- 非负整数：`^\\d+$ 或 ^[1-9]\\d*|0$`
- 非正整数：`^-[1-9]\\d*|0$ 或 ^((-\\d+)|(0+))$`
- 非负浮点数：`^\\d+(\\.\\d+)?$ 或 ^[1-9]\\d*\\.\\d*|0\\.\\d*[1-9]\\d*|0?\\.0+|0$`
- 非正浮点数：`^((-\\d+(\\.\\d+)?)|(0+(\\.0+)?))$ 或^(-([1-9]\\d*\\.\\d*|0\\.\\d*[1-9]\\d*))|0?\\.0+|0$`
- 正浮点数：`^[1-9]\\d*\\.\\d*|0\\.\\d*[1-9]\\d*$ 或 ^(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*))$`
- 负浮点数：`^-([1-9]\\d*\\.\\d*|0\\.\\d*[1-9]\\d*)$或 ^(-(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*)))$`
- 浮点数：`^(-?\\d+)(\\.\\d+)?$ 或 ^-?([1-9]\\d*\\.\\d*|0\\.\\d*[1-9]\\d*|0?\\.0+|0)$`
- 汉字：`^[\\u4e00-\\u9fa5]{0,}\$`
- 英文和数字：`^[A-Za-z0-9]+$ 或^[A-Za-z0-9]{4,40}$`
- 长度为 3-20 的所有字符：`^.{3,20}\$`
- 由 26 个英文字母组成的字符串：`^[A-Za-z]+\$`
- 由 26 个大写英文字母组成的字符串：`^[A-Z]+\$`
- 由 26 个小写英文字母组成的字符串：`^[a-z]+\$`
- 由数字和 26 个英文字母组成的字符串：`^[A-Za-z0-9]+\$`
- 由数字、26 个英文字母或者下划线组成的字符串：`^\\w+$ 或 ^\\w{3,20}$`
- 中文、英文、数字包括下划线：`^[\\u4E00-\\u9FA5A-Za-z0-9_]+\$`
- 中文、英文、数字但不包括下划线等符号：`^[\\u4E00-\\u9FA5A-Za-z0-9]+$ 或 ^[\\u4E00-\\u9FA5A-Za-z0-9]{2,20}$`
- 可以输入含有^%&',;=?\$\\\"等字符：`[^%&',;=?$\\x22]+ 12`
- 禁止输入含有~的字符：`[^~\\x22]+`
- 身份证：

```javascript
export const isID = n => {
  var checkCode = function(val) {
    var p = /^[1-9]\d{5}(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
    var factor = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
    var parity = [1, 0, 'X', 9, 8, 7, 6, 5, 4, 3, 2];
    var code = val.substring(17);
    if (p.test(val)) {
      var sum = 0;
      for (var i = 0; i < 17; i++) {
        sum += val[i] * factor[i];
      }
      if (parity[sum % 11] === code.toUpperCase()) {
        return true;
      }
    }
    return false;
  };
  var checkDate = function(val) {
    var pattern = /^(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)$/;
    if (pattern.test(val)) {
      var year = val.substring(0, 4);
      var month = val.substring(4, 6);
      var date = val.substring(6, 8);
      var date2 = new Date(year + '-' + month + '-' + date);
      if (date2 && date2.getMonth() === parseInt(month) - 1) {
        return true;
      }
    }
    return false;
  };
  var checkProv = function(val) {
    var pattern = /^[1-9][0-9]/;
    var provs = {
      11: '北京',
      12: '天津',
      13: '河北',
      14: '山西',
      15: '内蒙古',
      21: '辽宁',
      22: '吉林',
      23: '黑龙江 ',
      31: '上海',
      32: '江苏',
      33: '浙江',
      34: '安徽',
      35: '福建',
      36: '江西',
      37: '山东',
      41: '河南',
      42: '湖北 ',
      43: '湖南',
      44: '广东',
      45: '广西',
      46: '海南',
      50: '重庆',
      51: '四川',
      52: '贵州',
      53: '云南',
      54: '西藏 ',
      61: '陕西',
      62: '甘肃',
      63: '青海',
      64: '宁夏',
      65: '新疆',
      71: '台湾',
      81: '香港',
      82: '澳门',
    };
    if (pattern.test(val)) {
      if (provs[val]) {
        return true;
      }
    }
    return false;
  };
  var checkID = function(val) {
    if (checkCode(val)) {
      var date = val.substring(6, 14);
      if (checkDate(date)) {
        if (checkProv(val.substring(0, 2))) {
          return true;
        }
      }
    }
    return false;
  };

  if (n === undefined) {
    return false;
  }
  return checkID(n);
};
```

## 类型检测

Q：使用`typeof foo === "object"`检测`foo`是否为对象有什么缺点？如何避免？

A：用 `typeof` 是否能准确判断一个对象变量，答案是否定的，`null` 的结果也是 `object`，`Array` 的结果也是 `object`，有时候我们需要的是 "纯粹" 的 `object` 对象

```js
Object.prototype.toString.call(obj) === '[object Object]';
```
