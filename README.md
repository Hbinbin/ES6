## 什么是ES6

一般将ES2015之后的版本，如ES2015、ES2016、ES2017、ES2018称为ES6。ES6泛指“下一代 JavaScript 语言”。每年的6月份，TC39 委员会都会发布ECMAScript的新版标准。

传送门：[阮一峰ES6教程](http://es6.ruanyifeng.com/?search=import&x=0&y=0#README)

## 各种环境的ES6支持率

#### chrome

版本 69.0.3497.81（正式版本）

![](/assets/chrome-ES6-support.png)

注：ES6支持率查看:[http://ruanyf.github.io/es-checker/](http://ruanyf.github.io/es-checker/)

注：开启chrome的ES6支持：

```
 1.打开：chrome://flags/
 2.勾选：Experimental JavaScript为enable
```

![](/assets/ES6+.png)传送门：[ES6](http://es6.ruanyifeng.com/?search=import&x=0&y=0#README)

### node

V10.8.0

![](/assets/node-v10.8.0-support.png)传送门：[node官网](https://nodejs.org/zh-cn/)

## babel：javascript编译器

package.json文件

```js
"dependencies":{
     "babel-polyfill": "^6.26.0",// 提供浏览器不支持的ES新功能
     "babel-runtime":"6.26.0" // 运行时编译
},
"devDependencies":{
    "babel-core": "^6.22.1", // 使用babel的api转换代码
    "babel-register": "^6.22.0",
    "babel-preset-env": "^1.3.2", // 编译ES2015+版本
    "babel-preset-stage-2": "^6.22.0", // 编译处于草案阶段的语法
    "babel-plugin-transform-runtime": "^6.22.0",//运行时编译
    "babel-loader": "^7.1.1", // 配置需要转码的js文件
    //"babel-eslint": "^7.1.1", // 用eslint检查babel代码
    //"babel-plugin-component": "^0.10.1" // element ui模块化引入插件
}
```

在浏览器中使用：

```js
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<script type="text/babel">
    // ES6 code
</script>
```

传送门：[babel中文网](https://www.babeljs.cn/docs/setup/)

