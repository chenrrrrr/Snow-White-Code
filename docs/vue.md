##　vue配置文件在哪写

vuecli3做了终极精简，webpack配置，需要根目录下新建`vue.config.js`文件，在里面撸

## 本地前后端分离开发

由于vue项目会自己跑在某个端口上，后端服务肯定跑在另外一个端口，所以ajax跨域问题诞生了，需要在`vue.config.js`配置跨域

> 补充，如果部署到服务端，vue项目已经打包成了，dist文件夹下，所以需要用nginx做反向代理，express、java后端服务启一个，nginx启一个(做代理转发)，就O了

```javascript
// 代理3000端口/api接口的全部请求
module.exports = {
  devServer: {
    proxy: 'http://localhost:3000'
  }
}
```

## 引入fontawesome4.7

```bash
npm install font-awesome
# 在main.js里添加
import 'font-awesome/css/font-awesome.css'
```

## vuecli3 别名配置

由于vuecli3里面默认配置了`@`，详情在`/node_modules/@vue/cli-service/lib/config/base.js`

```javascript
module.exports = {
  configureWebpack: {
    resolve: {
      alias: {
        'assets': '@/assets',
        'components': '@/components',
        'views': '@/views',
      }
    }
  }
}
```

## vuecli3 stylus import问题

前面需要加入`~`

```javascript
// 引入/src/assets/css/leftbar.stylus
@import '~assets/css/leftbar.styl'
```