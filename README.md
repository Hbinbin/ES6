## 什么是ES6

一般将ES2015之后的版本，如ES2015、ES2016、ES2017、ES2018称为ES6。ES6泛指“下一代 JavaScript 语言”。每年的6月份，TC39 委员会都会发布ECMAScript的新版标准。

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

### ![](/assets/ES6+.png)node

V10.8.0

![](/assets/node-v10.8.0-support.png)传送门：[node官网](https://nodejs.org/zh-cn/)

## babel：javascript编译器

package.json文件

```js
"dependencies":{
     //"babel-polyfill": "^6.26.0",
     "babel-runtime":"6.26.0"
},
"devDependencies":{
    "babel-core": "^6.22.1",
    "babel-register": "^6.22.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-loader": "^7.1.1",
    //"babel-eslint": "^7.1.1",
    //"babel-plugin-component": "^0.10.1"
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

