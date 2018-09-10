简介

JS的异步：定时器、事件、HTTP请求。

promise和async await的目的就是让异步流程，用同步的方式表达，避免回调地狱。

原理：

```js
class Promise{
  constructor(executor){
    this.state = 'pending';
    this.value = undefined;
    this.reason = undefined;
    this.onResolvedCallbacks = [];
    this.onRejectedCallbacks = [];
    let resolve = value => {
      if (this.state === 'pending') {
        this.state = 'fulfilled';
        this.value = value;
        this.onResolvedCallbacks.forEach(fn=>fn());
      }
    };
    let reject = reason => {
      if (this.state === 'pending') {
        this.state = 'rejected';
        this.reason = reason;
        this.onRejectedCallbacks.forEach(fn=>fn());
      }
    };
    try{
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }
  then(onFulfilled,onRejected) {
    // onFulfilled如果不是函数，就忽略onFulfilled，直接返回value
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : value => value;
    // onRejected如果不是函数，就忽略onRejected，直接扔出错误
    onRejected = typeof onRejected === 'function' ? onRejected : err => { throw err };
    let promise2 = new Promise((resolve, reject) => {
      if (this.state === 'fulfilled') {
        // 异步
        setTimeout(() => {
          try {
            let x = onFulfilled(this.value);
            resolvePromise(promise2, x, resolve, reject);
          } catch (e) {
            reject(e);
          }
        }, 0);
      };
      if (this.state === 'rejected') {
        // 异步
        setTimeout(() => {
          // 如果报错
          try {
            let x = onRejected(this.reason);
            resolvePromise(promise2, x, resolve, reject);
          } catch (e) {
            reject(e);
          }
        }, 0);
      };
      if (this.state === 'pending') {
        this.onResolvedCallbacks.push(() => {
          // 异步
          setTimeout(() => {
            try {
              let x = onFulfilled(this.value);
              resolvePromise(promise2, x, resolve, reject);
            } catch (e) {
              reject(e);
            }
          }, 0);
        });
        this.onRejectedCallbacks.push(() => {
          // 异步
          setTimeout(() => {
            try {
              let x = onRejected(this.reason);
              resolvePromise(promise2, x, resolve, reject);
            } catch (e) {
              reject(e);
            }
          }, 0)
        });
      };
    });
    // 返回promise，完成链式
    return promise2;
  }
  _resolvePromise(promise2, x, resolve, reject){
    // 循环引用报错
    if(x === promise2){
      // reject报错
      return reject(new TypeError('Chaining cycle detected for promise'));
    }
    // 防止多次调用
    let called;
    // x不是null 且x是对象或者函数
    if (x != null && (typeof x === 'object' || typeof x === 'function')) {
      try {
        // A+规定，声明then = x的then方法
        let then = x.then;
        // 如果then是函数，就默认是promise了
        if (typeof then === 'function') { 
          // 就让then执行 第一个参数是this   后面是成功的回调 和 失败的回调
          then.call(x, y => {
            // 成功和失败只能调用一个
            if (called) return;
            called = true;
            // resolve的结果依旧是promise 那就继续解析
            resolvePromise(promise2, y, resolve, reject);
          }, err => {
            // 成功和失败只能调用一个
            if (called) return;
            called = true;
            reject(err);// 失败了就失败了
          })
        } else {
          resolve(x); // 直接成功即可
        }
      } catch (e) {
        // 也属于失败
        if (called) return;
        called = true;
        // 取then出错了那就不要在继续执行了
        reject(e); 
      }
    } else {
      resolve(x);
    }
  }
}
```

总结：  
p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'PingFang SC Semibold'; color: \#000000; -webkit-text-stroke: \#000000}  
p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: \#000000; -webkit-text-stroke: \#000000}  
p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'PingFang SC'; color: \#000000; -webkit-text-stroke: \#000000}  
span.s1 {font: 12.0px 'PingFang SC'; font-kerning: none}  
span.s2 {font-kerning: none}  
span.s3 {font: 12.0px 'Helvetica Neue'; font-kerning: none}  


**总结：**

1.then、catch、finally可随意组合。

2.Promise对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获（catch）为止。catch总会捕捉到之前的错误，不管是promise/then/catch/finally的错误。

catch中的错误可在后面的catch捕捉。

3.Promise内部的错误不会影响到Promise外部的代码，不会退出进程、终止脚本执行。

4.finally方法用于指定不管Promise对象最后状态如何，都会执行的操作。

finally中的代码总会执行，不管是之前的promise内部，还是then，还是catch中发生错误。

传送门：[Promises/A+](https://promisesaplus.com/)、[手写promise教程](https://juejin.im/post/5b2f02cd5188252b937548ab)

