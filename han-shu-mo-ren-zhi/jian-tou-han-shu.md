只需要记住以下三点：

1.函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。

栗子：

```js
HTML:
<button id="btn" >long long ago</button>
//以前
btn.onclick = function() {
    var self = this;
    setTimeout(function() {
        console.log(self.textContent);
    });
}
//现在：this指向btn这个元素
btn.onclick = function() {
    setTimeout(() => {
        console.log(this.textContent);
    });
}
// 下面的this指向window
btn.onclick = () => {
    setTimeout(() => {
        console.log(this.textContent);
    });
}
```

2.不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。

栗子：

```
// wrong code
const Utils = (name, age, work) => {
    this.name = name;
    this.age = age;
    this.work = work;
}
let utils = new Utils();

```

3.不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

栗子：

```
const foo = (...args) =>{
    console.log(args);
    console.log(arguments);
}

```

  


