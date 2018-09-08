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

     2.勾选：![](/assets/屏幕快照 2018-09-08 上午11.47.36.png)
```

#### node

V10.8.0

![](/assets/node-v10.8.0-support.png)

## babel：javascript编译器

package.json文件

```
"dependencies":{
     "babel-polyfill": "^6.26.0",
},
"devDependencies":{
    "babel-core": "^6.22.1",
    "babel-register": "^6.22.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-loader": "^7.1.1",
    "babel-eslint": "^7.1.1",
    "babel-plugin-component": "^0.10.1"
}

```





















