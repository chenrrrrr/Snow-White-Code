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
  var css = [
    'linear-gradient(to left bottom,hsl(',
    left,
    ', 100%, 85%) 0%,hsl(',
    bottom,
    ', 100%, 85%) 100%)'
  ];
  el.style.background = css.join('');
}
```
## ul下li居中

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
function getCurMonthDays(){
  return new Date(new Date().getFullYear(), new Date().getMonth()+1, 0).getDate();
}
```