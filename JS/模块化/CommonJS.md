# CommonJS

CommonJS是服务器端模块的规范，由于Node.js被广泛认知。

```js
  //file1.js
  moudle.exports = {
    a: 1
  };

  //file2.js
  var f1 = require('./file1');
  var v = f1.a + 2;
  module.exports = {
    v: v
  };
```

CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作。像Node.js主要用于服务器的编程，服务端模块存放在本地硬盘，读取速度不是问题，但客户端浏览器大多数模块都放在服务端，等待时间取决于网络的快慢，会出现浏览器假死。因为相对于_同步加载_出现了_异步加载_。这就是AMD规范诞生的背景。

CommonJS是服务器端模块的规范，由于Node.js被广泛认知。

```js
//file1.js
moudle.exports = {
  a: 1
};

//file2.js
var f1 = require('./file1');
var v = f1.a + 2;
module.exports = {
  v: v
};
```

CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作。像Node.js主要用于服务器的编程，服务端模块存放在本地硬盘，读取速度不是问题，但客户端浏览器大多数模块都放在服务端，等待时间取决于网络的快慢，会出现浏览器假死。因为相对于_同步加载_出现了_异步加载_。这就是AMD规范诞生的背景。