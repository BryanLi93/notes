# Object

## Computed property names

> Allowing you to put an expression in brackets [], that will be computed and used as the property name.

```js
    var param = 'size';
    var config = {
      [param]: 12,
      ['mobile' + param.charAt(0).toUpperCase() + param.slice(1)]: 4
    };
    console.log(config); // {size: 12, mobileSize: 4}
```