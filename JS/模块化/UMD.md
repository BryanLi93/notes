# UMD （Universal Module Definition - 通用模块定义）

UMD是AMD和CommonJS的一个糅合。AMD是浏览器优先，异步加载；CommonJS是服务器优先，同步加载。

## 实现原理

UMD的实现很简单：

1. 先判断是否支持Node.js模块格式（exports是否存在），存在则使用Node.js模块格式。
2. 再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块。
3. 前两个都不存在，则将模块公开到全局（window或global）。

```js
  // if the module has no dependencies, the above pattern can be simplified to
  (function (root, factory) {
    if (typeof define === 'function' && define.amd) {
      // AMD. Register as an anonymous module.
      define([], factory);
    } else if (typeof exports === 'object') {
      // Node. Does not work with strict CommonJS, but
      // only CommonJS-like environments that support module.exports,
      // like Node.
      module.exports = factory();
    } else {
      // Browser globals (root is window)
      root.returnExports = factory();
    }
  }(this, function () {
    //do something... 这里是真正的函数体
  }));
```