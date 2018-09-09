```js
export default class Utils {
    /**
     * 深克隆
     * @static
     * @param {Object|Array} obj - 引用类型Object、Array
     * @returns {Object|Array}
     * @memberof Utils
     */
    static deepClone(obj) {
      let clone = Object.assign({}, obj) // 浅克隆
      Object.keys(obj).forEach(key => {
        clone[key] = typeof obj[key] === 'object' ? this.deepClone(obj[key]) : obj[key]
      })
      return Array.isArray(obj) ? (clone.length = obj.length) && Array.from(clone) : clone
    }

    /**
     * url添加参数
     * @static
     * @param {string} url - 需要添加参数的url
     * @param {object} params - 添加的参数，参数是'key:value'形式
     * @param {boolean} [isEncode=false] - 传入的url是否被编码过
     * @param {boolean} [needEncode=false] - 返回的url是否需要编码
     * @returns {string}
     * @memberof Utils
     */
    static addParams({ url = '', params = {}, isEncode = false, needEncode = false } = {}) {
      url = isEncode ? decodeURIComponent(url) : url;
      if (url.indexOf('?') > -1) {
        let oldParams = {};
        url.split('?')[1].split('&').forEach(val => {
          let newVal = val.split('=');
          oldParams[newVal[0]] = newVal[1];
        });
        // 合并、去重参数
        params = { ...oldParams, ...params };
      }
      let [paramsStr, i] = ['', 1];
      for (let [key, val] of Object.entries(params)) {
        paramsStr += i > 1 ? `&${key}=${val}` : `${key}=${val}`;
        i++;
      }
      return needEncode ? encodeURIComponent(`${url.split('?')[0]}?${paramsStr}`) : `${url.split('?')[0]}?${paramsStr}`;
  }
}
```



