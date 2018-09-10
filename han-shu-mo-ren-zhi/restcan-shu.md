举个栗子：

函数柯里华实现累加

```js
const accumulation = (...args1) => {
  // 以前
  // let allArgs = [].slice.call(arguments);
  // 现在
  let allArgs = args1;
  const _fn = (...args2) => {
    allArgs = [...allArgs,...args2];
    // allArgs = allArgs.concat([].slice.call(arguments));
    return _fn;
  }
  _fn.toString = () => {
    return allArgs.reduce((a, b) => a + b);
  }
  return _fn;
}
accumulation(1);
accumulation(1,2,3);
accumulation(1)(2)(3)(4);
accumulation(1,2,3)(4)(5);
accumulation(1,2,3)(4)(5,6,7)(8);
```



