## @touchmove 和 catchtouchmove

在`android`环境下测试了两者，`wepy`自带的`@touchmove`需要添加`.stop`，效果等同于`catchtouchmove`，如果不添加`.stop`，小程序动画效果在`android`机上会非常卡顿

## view-model 覆盖的问题

WePY 中的组件都是静态组件，是以组件 ID 作为唯一标识的，每一个 ID 都对应一个组件实例。当页面引入两个相同 ID 的组件时，这两个组件共用同一个实例与数据，当其中一个组件数据变化时，另外一个也会一起变化。如需避免这个问题，则需要分配多个组件 ID 和实例

```vue
<template>
  <view class="child1">
    <child></child>
  </view>

  <view class="child2">
    <anotherchild></anotherchild>
  </view>
</template>

<script>
import wepy from 'wepy';
import Child from '../components/child';

export default class Index extends wepy.component {
  components = {
    //为两个相同组件的不同实例分配不同的组件ID，从而避免数据同步变化的问题
    child: Child,
    anotherchild: Child,
  };
}
</script>
```

## 组件循环渲染

```vue
<template>
  <!-- 注意，使用for属性，而不是使用wx:for属性 -->
  <repeat for="{{list}}" key="index" index="index" item="item">
    <!-- 插入<script>脚本部分所声明的child组件，同时传入item -->
    <child :item="item"></child>
  </repeat>
</template>

<script>
import wepy from 'wepy';
import Child from '../components/child'; // 引入child组件文件

export default class Index extends wepy.component {
  components = {
    child: Child,
  };

  data = {
    list: [{ id: 1, title: 'title1' }, { id: 2, title: 'title2' }],
  };
}
</script>
```

## 小程序点击 e.target & e.currentTarget

    - `e.target`指向触发事件监听的对象
    - `e.currentTarget`指向添加监听事件的对象

点击一个 cell，考虑到用户操作精确度问题，通常我们是给整个 cell 都绑定点击事件，如果是 cell 是通过`vm`循环出的，通常做法如下

```html
<view class="cell" data-index="{{index}}" wx:for="{{cellList}}" wx:for-item="item" wx:key="index" wx:for-index="index" @tap="handleClick">
  <label>{{item.alias}}</label>
  <label>></label>
</view>
```

```less
.cell {
  display: flex;
  justify-content: space-between;
}
```

```javascript
data:{
    cellList:[
        {
            alias:'最新消息',
        },
        {
            alias:'我的钱包',
        }
    ]
}
methods:{
    handleClick(e){
        console.log(`${e.currentTarget.dataset.index} ----  ${e.target.dataset.index}`)
    }
}
```

如果是`e.target.dataset.index`，当点击到`label:first-child`元素的时候，会打印`undifined`，而`e.currentTarget.dataset.index`则返回对应的`dataset.index`，也就实现了捕获

MDN 中对 target 的解释为，一个触发事件的对象的引用， 当事件处理程序在事件的冒泡或捕获阶段被调用时，而对于 currentTarget，它指的是当事件遍历 DOM 时，标识事件的当前目标。它总是引用事件处理程序附加到的元素，而不是 event.target，它标识事件发生的元素

## 全局消息提示

项目框架选用 wepy，需要跨页面做全局的消息提醒，已经显示过的消息，跨页面时，不显示，思路

- `app.wpy > globalData`注入全局消息对象例如`msgList`
- `mixins` 加入对象`msgListAcceptor = this.$parent.globalData.msgList`
- 页面`wx:for={{msgListAcceptor}} wx:for-item="item"`
- 根据`item`里面的属性，例如`hasShow`判断是否显示过了，给个样式`show`控制显示/隐藏，`class="{{item.hasShow ? 'show' : ''}}"`

## 双向绑定

动态传值是指父组件向子组件传递动态数据内容，父子组件数据完全独立互不干扰。

- 可以通过使用`.sync`修饰符来达到父组件数据绑定至子组件的效果
- 也可以通过设置子组件`props`的`twoWay: true`来达到子组件数据绑定至父组件的效果
- 父使用`.sync`修饰符，子组件`props`中添加的`twoWay: true`时，就可以实现数据的双向绑定了。

## 滚动弹出层(穿透)解决方案

`common.css`

```css
.noscroll {
  height: 100%;
  overflow: hidden;
}
```

`调用.wpy`

`{{isShow?'noscroll':''}}`加酌情判断加在`<page>`节点或者`<scroll-view>`

```html
<template class="{{isShow?'noscroll':''}}">
  <scroll-view scroll-y class="page-wrapper">
    <view class="list-item>
      ...
    </view>
  </scroll-view>
  <!-- 调用popup组件 -->
  <popup :isShow.sync="isShow"></popup>
</template>

```

`popup.wpy`

```js
// 样式style省略
<template>
  <view class="mask"><!-- 灰色蒙层 -->
    <slot name="popup-content"><!-- 或者slot -->
      ...
    </slot>
  </view>
</template>

export default class Index extends wepy.component {
  props = {
    isShow: {
      type: Boolean,
      default: false,
      twoWay: true
    }
  }
}
```

## wpy 模板快速生成

`ctrl+shift+p` => `配置用户代码片段` => `vue.json` 加入

```js
  "Print to console": {
    "prefix": "wpy",
    "body": ["<!-- $0 -->", "<style lang='less' scoped>", "</style>", "<template>", "<view class='page-wrapper'>", "index", "</view>", "</template>", "", "<script>", "import wepy from 'wepy'", "export default class Index extends wepy.page {", "config = {", "navigationBarTitleText: 'index'", "}", "components = {}", "data = {}", "computed = {}", "methods = {}", "events = {}", "initFun() {}", "onLoad() {", "this.initFun()", "}", "}", "</script>", ""],
    "description": "Log output to console"
  }
```

## common.less

```less
/* --------- page --------- */
page {
  font-size: 14px;
  height: 100%;
  .page-wrapper {
    background-color: #f4f4f4;
    box-sizing: border-box;
  }
}

/* --------- hover-class:"hover" --------- */
.hover {
  background: rgba(121, 121, 121, 0.1) !important;
}

/* --------- 超出省略 ... --------- */
.ellipsis {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* --------- bg color --------- */

@blue: #1e9fff; // tech-bgc
@black: #393d49; // nav
@mint: #5fb878; // isSelected
@teal: #009688; // button decoration
@orange: #ffb800; // notice
@red: #ff5722; // awesome
@blue-1: #01aaed; // text、link
@bar: #2f4056; // footer、siderbar

/* --------- grey series --------- */

@grey: #c2c2c2;
@grey-1: #d2d2d2;
@grey-2: #dddddd;
@grey-3: #e2e2e2;
@grey-4: #eeeeee;
@grey-5: #f2f2f2;
@grey-6: #f0f0f0;

/* --------- ellipsis --------- */
.ellipsis {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* --------- flex --------- */

.flex(@jc:center,@ai:center) {
  display: flex;
  justify-content: @jc;
  align-items: @ai;
}

/* --------- padding --------- */
.pd(@a,@b,@c,@d) {
  padding: @arguments;
}

/* --------- margin --------- */
.mar(@a,@b,@c,@d) {
  margin: @arguments;
}

/* --------- position --------- */

.pr() {
  position: relative;
}

.pa() {
  position: absolute;
}

.pcc(@l,@t,@style:absolute) {
  position: @style;
  top: 50%;
  left: 50%;
  margin-left: -@l / 2;
  margin-top: -@t / 2;
}
/* --------- width-height --------- */

.wh(@w:auto,@h:auto) {
  width: @w;
  height: @h;
}

.lh(@h:1) {
  line-height: @h;
}

/* --------- font --------- */

.font(@fz:14px,@color:#333,@align:left) {
  font-size: @fz;
  color: @color;
  text-align: @align;
  .lh();
}

/* --------- bg --------- */

.bg(@color:@grey-3) {
  background: @color;
}

/* --------- br --------- */

.br(@br:2px) {
  border-radius: @br;
}

/* --------- button --------- */

.btn-lg {
}

.btn-md {
}

.btn-sm {
}
```
