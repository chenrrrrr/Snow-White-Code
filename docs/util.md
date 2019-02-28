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

- 手机：`/^1\d{10}$/`
- 车牌：`/^[京津沪渝冀豫云辽黑湘皖鲁新苏浙赣鄂桂甘晋蒙陕吉闽贵粤青藏川宁琼使领A-Z]{1}[A-Z]{1}[A-Z0-9]{4}[A-Z0-9挂学警港澳]{1}$/`
- 验证码：`/^\d{6}$/`
- 中文：`/^[\u4E00-\u9FA5]{2,6}$/`
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
