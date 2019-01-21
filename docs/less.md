## 变量

LESS 中的变量为完全的 '常量' ，所以只能定义一次

```css
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header { color: @light-blue; }
```
输出

```css
#header { color: #6c94be; }
```

## 混合

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

使用

```css
#menu a {
  color: #111;
  .bordered;
}
.post a {
  color: red;
  .bordered;
}
```

带参

```css
.border-radius (@radius) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
```

#header {
  .border-radius(4px);
}

`@arguments`变量，包含了所有传递进来的参数. 如果你不想单独处理每一个参数

```css
.box-shadow (@x: 0, @y: 0, @blur: 1px, @color: #000) {
  box-shadow: @arguments;
  -moz-box-shadow: @arguments;
  -webkit-box-shadow: @arguments;
}
.box-shadow(2px, 5px);
```

无参

```css
.wrap () {
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}

pre { .wrap }
```

## Color 函数
```css
@color-base: #3bafdA;
@color-hover:lighten(@color-primary,10%);
@color-focus:darken(@color-primary,10%);
```


## JavaScript 表达式

```css
@var: `"hello".toUpperCase() + '!'`;
@height: `document.body.clientHeight`;
```

## 父选择器
@只能代表父元素，不能代表父亲的父辈元素，施加改性类或伪类
```css
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```

## 重复父类名
```css
.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
```