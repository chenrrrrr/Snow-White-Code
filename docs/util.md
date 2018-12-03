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
