## @touchmove 和 catchtouchmove

在`android`环境下测试了两者，`wepy`自带的`@touchmove`需要添加`.stop`，效果等同于`catchtouchmove`，如果不添加`.stop`，小程序动画效果在`android`机上会非常卡顿


## view-model覆盖的问题

WePY中的组件都是静态组件，是以组件ID作为唯一标识的，每一个ID都对应一个组件实例。当页面引入两个相同ID的组件时，这两个组件共用同一个实例与数据，当其中一个组件数据变化时，另外一个也会一起变化。如需避免这个问题，则需要分配多个组件ID和实例

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
            anotherchild: Child
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
    import Child from '../components/child';    // 引入child组件文件

    export default class Index extends wepy.component {
        components = {
            child: Child
        }

        data = {
            list: [{id: 1, title: 'title1'}, {id: 2, title: 'title2'}]
        }
    }
</script>
```

## 父子组件双向绑定

```