# this

`this`关键词是JavaScript中最令人疑惑的机制之一。`this`是非常特殊的关键词标识符，在每个函数的作用域中被自动创建，但它到底指向什么（对象），很多人弄不清。
当函数被调用，一个activation record（即 execution context）被创建。这个record包涵信息：函数在哪调用（call-stack），函数怎么调用的，参数等等。record的一个属性就是`this`，指向函数执行期间的`this`对象。

- `this`不是author-time binding，而是 runtime binding。
- `this`的上下文基于函数调用的情况。和函数在哪定义无关，而和函数怎么调用有关。

## 1.1 `this`在具体情况下的分析

## 1.1.1 Global context

在全局上下文（任何函数以外），this指向全局对象。
`console.log(this === window); // true`

## 1.1.2 Function context

在函数内部时，this由函数怎么调用来确定。

## 1.1.2.1 Simple call

简单调用，即独立函数调用。由于`this`没有通过`call`来指定，且`this`必须指向对象，那么默认就指向全局对象。

```js
  function f1(){
    return this;
  }
  f1() === window; // global object
```

在严格模式下，`this`保持进入execution context时被设置的值。如果没有设置，那么默认是`undefined`。它可以被设置为任意值（包括`null/undefined/1`等等基础值，不会被转换成对象）。

```js
  function f2(){
    "use strict"; // see strict mode
    return this;
  }

  f2() === undefined;
```

## 1.1.2.2 Arrow functions

在箭头函数中，`this`由词法/静态作用域设置（set lexically）。它被设置为包含它的execution context的`this`，并且不再被调用方式影响（call/apply/bind）。

```js
  var globalObject = this;
  var foo = (() => this);
  console.log(foo() === globalObject); // true

  // Call as a method of a object
  var obj = {foo: foo};
  console.log(obj.foo() === globalObject); // true

  // Attempt to set this using call
  console.log(foo.call(obj) === globalObject); // true

  // Attempt to set this using bind
  foo = foo.bind(obj);
  console.log(foo() === globalObject); // true
```

## 1.1.2.3 As an object method

当函数作为对象方法调用时，`this`指向该对象。

```js
    var o = {
      prop: 37,
      f: function() {
        return this.prop;
      }
    };
    console.log(o.f()); // logs 37
```

*this on the object's prototype chain*
原型链上的方法根对象方法一样，作为对象方法调用时this指向该对象。

## 1.1.2.4 构造函数

在构造函数（函数用`new`调用）中，`this`指向要被constructed的新对象。

## 1.1.2.5 call和apply

`Function.prototype`上的`call`和`apply`可以指定函数运行时的`this`。

```js
  function add(c, d){
    return this.a + this.b + c + d;
  }

  var o = {a:1, b:3};
  add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
  add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

注意，当用`call`和`apply`而传进去作为`this`的不是对象时，将会调用内置的`ToObject`操作转换成对象。所以`4`将会装换成`new Number(4)`，\*而\*`null/undefined`/由于无法转换成对象，全局对象将作为/`this`。

## 1.1.2.6 bind

ES5引进了`Function.prototype.bind`。`f.bind(someObject`)会创建新的函数（函数体和作用域与原函数一致），但`this`被永久绑定到`someObject`，不论你怎么调用。

## 1.1.2.7 As a DOM event handler

`this`自动设置为触发事件的dom元素。