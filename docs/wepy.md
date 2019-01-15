## @touchmove 和 catchtouchmove

在`android`环境下测试了两者，`wepy`自带的`@touchmove`需要添加`.stop`，效果等同于`catchtouchmove`，如果不添加`.stop`，小程序动画效果在`android`机上会非常卡顿
