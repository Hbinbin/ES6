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
//现在
btn.onclick = function() {
    setTimeout(() => {
        console.log(this.textContent);
    });
}

```

3.不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

