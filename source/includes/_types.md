# Types

## Primitives

> Primatives

```javascript
const foo = 1;
let bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

When you access a primitive type you work directly on its value.

* string
* number
* boolean
* null
* undefined
* symbol

<aside class="notice">
Symbols cannot be faithfully polyfilled, so they should not be used when targeting browsers/environments that don't support them natively.</aside>

## Complex

> Complex

```javascript
const foo = [1, 2];
const bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

When you access a complex type you work on a reference to its value.

* object
* array
* function
