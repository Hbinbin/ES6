### 定义

在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。

代理模式的合理使用，能够很好的体现软件设计原则中的下面两条原则:

* **单一职责原则：SRP**
  面向对象设计中鼓励将不同的职责分布到细粒度的对象中，Proxy 在原对象的基础上进行了功能的衍生而又不影响原对象，符合高内聚低耦合的设计理念。
* **开放-封闭原则：OCP**
  代理可以随时从程序中去掉，而不用对其他部分的代码进行修改，在实际场景中，随着版本的迭代可能会有多种原因不再需要代理，那么就可以容易的将代理对象换成原对象的调用。

```js
var proxy = new Proxy(target, handler);
```

### 应用

缓存代理：

```
// 斐波那契数列，number > 40开始很耗时
const getFib = (number) => {
  return number <= 2 ? 1 : getFib(number - 1) + getFib(number - 2)
}
```

```js
// 创建缓存代理函数
const getCacheProxy = (fn, cache = new Map()) => {
  return new Proxy(fn, {
    // apply方法拦截函数调用
    apply(target, context, args) {
      const argsStr = String(args);
      // 如果有缓存,直接返回缓存数据
      if (cache.has(argsStr)) {
        return cache.get(argsStr);
      }
      const result = fn(...args);
      cache.set(argsStr, result);
      return result;
    }
  })
}
const getFibProxy = getCacheProxy(getFib);

console.time('耗时：');
getFibProxy(40); // 耗时: 1142.31298828125ms
console.timeEnd('耗时：'); 

console.time('耗时：');
getFibProxy(40); // 耗时: 0.037109375ms
console.timeEnd('耗时：');
```

传送门：[Proxy代理模式](https://segmentfault.com/a/1190000015800703)

