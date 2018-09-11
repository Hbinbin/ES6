### 简介

使用`async/await`, 搭配`promise，` 可以通过编写同步的代码方式来处理异步流程, 提高代码的简洁性和可读性。

async/await是基于Promise，Promise是基于回调函数。

async/await是为了简化多个Promise的同步操作，Promise是为了解决回调地狱的问题。

### 基本用法

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

    // 定义接口api
    const APIKey = {
      USERINFO: Symbol('userinfo'),
      SHIPINFO: Symbol('shipinfo'),
      ORDERDETAIL: Symbol('orderdetail'),
    }
    const API = {
      [APIKey.USERINFO]: {
        url: '/user/userinfo',
        params: {uid: ''}
      },
      [APIKey.SHIPINFO]: {
        url: '/user/shipinfo',
        params: {sid: '',date: ''}
      },
      [APIKey.ORDERDETAIL]: {
        url: '/user/orderdetail',
        params: {oid: ''}
      }
    }
    // 定义async函数
    async function getDetail() {
      let userinfo = await fetch(API[APIKey.USERINFO].url);
      let shipinfo = await fetch(API[APIKey.SHIPINFO].url, {
        method: 'POST'
        body: `sid=${userinfo.sid}&date=${userinfo.date}`
      });
      console.log('我在这里最后执行');
      return shipinfo;
    }
    // 调用
    getDetail().then().catch().finally();

### 注意事项

并发执行和顺序执行

```py
const fetchArr = [fetch(url1), fetch(url2), fetch(url3)];
```

```js
// 顺序执行异步操作
async function getData() {
    let dataArr = [];
    for (let i = 0 ; i < fetchArr.length; i++) {
        dataArr.push(await fetchArr[i]);
    }
}
```

```js
//并发执行
async function getData() {
    return fetchArr.map( async fetchData => {
        let data = await fetchData;
        return data;
    });
}
// 相当于
async function getData() {
    for (..) {
        async ... await ... 
    }
}
```

错误处理

```
async function myFunction() {
  try {
    await fetch(url);
  } catch (err) {
    console.error(err);
  }
}

// 另一种写法
async function myFunction() {
  await fetch()
  .catch(function (err) {
    console.error(err);
  });
}
```

传送门：[Fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)

