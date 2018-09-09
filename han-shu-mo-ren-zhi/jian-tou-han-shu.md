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
let utils = new Utils(); // 报错：Uncaught TypeError: Utils is not a constructor
```

3.不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

栗子：

```
const foo = (...args) =>{
    console.log(args); // [1,2,3]
    console.log(arguments); // 报错：Uncaught ReferenceError: arguments is not defined
}
foo(1,2,3);
```

### 在Vue和React中

##### vue中：

在选项中：如钩子函数、methods、watch等使用箭头函数，this不会像预期指向Vue实例，而只是一个简单的‘当前定义时所在的对象’。在.vue文件中：

```js
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '我是this'
    }
  },
  methods: {
    mth1: () => {
      console.log(this.a.methods)
    },
    mth2 () {
      console.log(this)
    }

  },
  created: () => {
    console.log(this)
  }
}
```

mth1 && created![](/assets/mth1.png)

