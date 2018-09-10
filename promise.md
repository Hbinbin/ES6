### 简介

JS的异步：定时器、事件、HTTP请求。

promise和async await的目的就是让异步流程，用同步的方式表达，避免回调地狱。

原理：发布订阅模式 + 回调

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
    // 声明返回的promise2
    let promise2 = new Promise((resolve, reject)=>{
      if (this.state === 'fulfilled') {
        let x = onFulfilled(this.value);
        // resolvePromise函数，处理自己return的promise和默认的promise2的关系
        resolvePromise(promise2, x, resolve, reject);
      };
      if (this.state === 'rejected') {
        let x = onRejected(this.reason);
        resolvePromise(promise2, x, resolve, reject);
      };
      if (this.state === 'pending') {
        this.onResolvedCallbacks.push(()=>{
          let x = onFulfilled(this.value);
          resolvePromise(promise2, x, resolve, reject);
        })
        this.onRejectedCallbacks.push(()=>{
          let x = onRejected(this.reason);
          resolvePromise(promise2, x, resolve, reject);
        })
      }
    });
    // 返回promise，完成链式
    return promise2;
  }
}

作者：卡姆爱卡姆
链接：https://juejin.im/post/5b2f02cd5188252b937548ab
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



