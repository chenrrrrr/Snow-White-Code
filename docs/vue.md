##　 vue 配置文件在哪写

vuecli3 做了终极精简，webpack 配置，需要根目录下新建`vue.config.js`文件，在里面撸

## 本地前后端分离开发

由于 vue 项目会自己跑在某个端口上，后端服务肯定跑在另外一个端口，所以 ajax 跨域问题诞生了，需要在`vue.config.js`配置跨域

> 补充，如果部署到服务端，vue 项目已经打包成了，dist 文件夹下，所以需要用 nginx 做反向代理，express、java 后端服务启一个，nginx 启一个(做代理转发)，就 O 了

```javascript
// 代理3000端口/api接口的全部请求
module.exports = {
  devServer: {
    proxy: 'http://localhost:3000',
  },
};
```

## 引入 fontawesome4.7

```bash
npm install font-awesome
# 在main.js里添加
import 'font-awesome/css/font-awesome.css'
```

## vuecli3 别名配置

由于 vuecli3 里面默认配置了`@`，详情在`/node_modules/@vue/cli-service/lib/config/base.js`

```javascript
module.exports = {
  configureWebpack: {
    resolve: {
      alias: {
        assets: '@/assets',
        components: '@/components',
        views: '@/views',
      },
    },
  },
};
```

## vuecli3 stylus import 问题

前面需要加入`~`

```javascript
// 引入/src/assets/css/leftbar.stylus
@import '~assets/css/leftbar.styl'
```

## v-on 传参(\$event)

```javascript
<tempalte>
   <button @blur="leave($event)">点击</button>
</template>
<script>
export default {
  methods:{
    leave(e) {
      console.log(e)
      // 当前点击的元素
      e.target
      // 绑定事件的元素
      e.currentTarget
      // 获得点击元素的前一个元素
      e.currentTarget.previousElementSibling.innerHTML
      // 获得点击元素的第一个子元素
      e.currentTarget.firstElementChild
      // 获得点击元素的下一个元素
      e.currentTarget.nextElementSibling
      // 获得点击元素中id为string的元素
      e.currentTarget.getElementById("string")
      // 获得点击元素的string属性
      e.currentTarget.getAttributeNode('string')
      // 获得点击元素的父级元素
      e.currentTarget.parentElement
      // 获得点击元素的前一个元素的第一个子元素的HTML值
      e.currentTarget.previousElementSibling.firstElementChild.innerHTML
    },
  }
}
```

## 路由跳转

this.\$router.push()
跳转到不同的 url，但这个方法会向 history 栈添加一个记录，点击后退会返回到上一个页面

```javascript
// 字符串
router.push('home');
// 对象
router.push({ path: 'home' });
// 命名路由
router.push({ name: 'user', params: { userId: 123 } });
// 带查询参数
router.push({ path: 'register', query: { plan: 'private' } });
```

this.\$router.replace()
同样是跳转到指定的 url，但是这个方法不会向 history 里面添加新的记录，点击返回，会跳转到上上一个页面。上一个记录是不存在的

this.\$router.go(n)
相对于当前页面向前或向后跳转多少个页面,类似 window.history.go(n)。n 可为正数可为负数。正数返回上一个页面

## wpy vscode 快捷模板

`ctrl+shift+p` => `配置用户代码片段` => `vue.json` 加入

```js
  "Print to console": {
    "prefix": "vue",
    "body": ["<!-- $0 -->", "<template>", "  <div></div>", "</template>", "", "<script>", "export default {", "  data () {", "    return {", "    };", "  }", "}", "</script>", "", "<style lang='less' scoped>", "</style>"],
    "description": "Log output to console"
  },
```
