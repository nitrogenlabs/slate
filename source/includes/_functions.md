# Functions

## Arrow functions

> Arrow functions

```javascript
// bad
[1, 2, 3].map(function(x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// better
[1, 2, 3].map((x) => x * (x + 1));
```

```typescript
// bad
[1, 2, 3].map(function(x: number) {
  const y: number = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x: number) => {
  const y: number = x + 1;
  return x * y;
});

// better
[1, 2, 3].map((x: number) => x * (x + 1));
```

> Confusing arrow

```javascript
// bad
const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = (item) => (item.height > 256 ? item.largeSize : item.smallSize);

// better
const itemHeight = (item) => {
  const {height, largeSize, smallSize} = item;
  return height > 256 ? largeSize : smallSize;
};
```

```typescript
// bad
const itemHeight: number = item => item.height > 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight: number = (item) => item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight: number = (item) => (item.height > 256 ? item.largeSize : item.smallSize);

// better
const itemHeight: number = (item) => {
  const {height, largeSize, smallSize} = item;
  return height > 256 ? largeSize : smallSize;
};
```

* When you must use an anonymous function (as when passing an inline callback), use arrow function notation.
* It creates a version of the function that executes in the context of this, which is usually what you want, and is a more concise syntax.
* If you have a fairly complicated function, you might move the `this` logic out into its own named function expression.
* Avoid confusing arrow function syntax (=>) with comparison operators (<=, >=). 

### ESLint
`"prefer-arrow-callback": "error"`

`"arrow-spacing": "error"`

`"no-confusing-arrow": ["error", {"allowParens": true}]`

### TSLint

`"only-arrow-functions": true`

`"ter-prefer-arrow-callback": [true, {"allowNamedFunctions": false, "allowUnboundThis": false}]`

`"ter-arrow-spacing": [true]`


## Named function expressions

> Named function expressions

```javascript
// bad
function foo() {
  // ...
}

// bad
const foo = function() {
  // ...
};

// good
const foo = () => {
  // ...
};
```

```typescript
// bad
function foo() {
  // ...
}

// bad
const foo = function() {
  // ...
};

// good
const foo = () => {
  // ...
};
```
* Use named function expressions instead of function declarations. 
* Any time an anonymous function expression appears on the right-hand side of something like an assignment or initialization, the resulting function will have a name (foo, in the examples).

### ESLint
`"func-style": ["error", "expression", {"allowArrowFunctions": true}]`


## Single line

> Single line

```javascript
// bad - returns an array with 3 undefines
[1, 2, 3].map((value) => {
  const nextNumber = value + 1;
  `A string containing the ${nextNumber}.`;
});

// good - returns an array with strings
[1, 2, 3].map((value) => `A string containing the ${value}.`);

// good
[1, 2, 3].map((value) => {
  const nextNumber = value + 1;
  return `A string containing the ${nextNumber}.`;
});

// better
[1, 2, 3].map((value) => `A string containing the ${value + 1}.`);

// good
[1, 2, 3].map((value, index) => ({[index]: value}));

// No implicit return with side effects
const foo = (callback) => {
  const val = callback();
  
  if(val === true) {
    // Do something if callback returns true
  }
};

let bool = false;

// bad - returns undefined to the callback
foo(() => bool = true);

// good - returns a boolean
foo(() => {
  bool = true;
  return bool;
});
```

```typescript
// bad - returns an array with 3 undefines
[1, 2, 3].map((value: number): void => {
  const nextNumber: number = value + 1;
  `A string containing the ${nextNumber}.`;
});

// good - returns an array with strings
[1, 2, 3].map((value: number): string => `A string containing the ${value}.`);

// good
[1, 2, 3].map((value: number): string => {
  const nextNumber: number = value + 1;
  return `A string containing the ${nextNumber}.`;
});

// better
[1, 2, 3].map((value: number) => `A string containing the ${value + 1}.`);

// good
[1, 2, 3].map((value: number, index: number) => ({[index]: value}));

// No implicit return with side effects
const foo = (callback: () => boolean) => {
  const val: boolean = callback();
  
  if(val === true) {
    // Do something if callback returns true
  }
};

let bool: boolean = false;

// bad - returns undefined to the callback
foo(() => bool = true);

// good - returns a boolean
foo(() => {
  bool = true;
  return bool;
});
```

* If the function body consists of a single statement returning an expression without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a return statement.
* Syntactic sugar. It reads well when multiple functions are chained together.

### ESLint

`"arrow-parens": ["error", "as-needed"]`

`"arrow-body-style": ["error", "as-needed"]`

### TSLint

`"arrow-parens": true`

`"arrow-return-shorthand": true`

`"ter-arrow-body-style": [true, "as-needed", {"requireReturnForObjectLiteral": false}]`


## Multiline

> Multiline

```javascript
// bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);

// good
['get', 'post', 'put'].map(httpMethod => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));
```

```typescript
// bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);

// good
['get', 'post', 'put'].map(httpMethod => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));
```

* In case the expression spans over multiple lines, wrap it in parentheses for better readability.
* It shows clearly where the function starts and ends.


## Wrapping functions

> Wrapping

```javascript
// immediately-invoked function expression (IIFE)
(() => {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

```typescript
// immediately-invoked function expression (IIFE)
(() => {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

* Wrap immediately invoked function expressions in parentheses. eslint: wrap-iife jscs: requireParenthesesAroundIIFE
* An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

### ESLint

`"wrap-iife": ["error", "outside"]`


## Non-function block

* Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears. 

### ESLint

`"no-loop-func": "error"`


## Block definition

> Block definition

```javascript
// bad
if(currentUser) {
  let test = () => {
    console.log('Nope.');
  };
}

// good
let test;

if(currentUser) {
  test = () => {
    console.log('Yup.');
  };
}
```

```typescript
// bad
if(currentUser) {
  let test = () => {
    console.log('Nope.');
  };
}

// good
let test;

if(currentUser) {
  test = () => {
    console.log('Yup.');
  };
}
```

* ECMA-262 defines a block as a list of statements. A function declaration is not a statement.


## Arguments

> Parentheses

```javascript
// bad
[1, 2, 3].map(x => x * x);

// good
[1, 2, 3].map((x) => x * x);
```

```typescript
// bad
[1, 2, 3].map(x => x * x);

// good
[1, 2, 3].map((x: number) => x * x);
```

> Parameter names

```javascript
// bad
const foo = (name, options, arguments) => {
  // ...
}

// good
const foo = (name, options, args) => {
  // ...
}
```

```typescript
// bad
const foo = (name: string, options: object, arguments) => {
  // ...
}

// good
const foo = (name: string, options: object, args) => {
  // ...
}
```

> Rest params syntax

```javascript
// bad
const concatenateAll = () => {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
};

// good
const concatenateAll = (...args) => {
  return args.join('');
};
```

```typescript
// bad
const concatenateAll = () => {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
};

// good
const concatenateAll = (...args) => {
  return args.join('');
};
```

* Always include parentheses around arguments for clarity and consistency.
* Parentheses do not need to be added later if arguments are added.
* Easier transition when using typings.
* Never name a parameter arguments. This will take precedence over the arguments object that is given to every function scope.
* Never use arguments, opt to use rest syntax `...` instead. 
* ... is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like arguments.

### ESLint

`"arrow-parens": ["error", "as-needed"]`

`"prefer-rest-params": "error"`

### TSLint

`"arrow-parens": true`

`"ter-func-call-spacing": [true]`


## Default parameters

> Default parameters

```javascript
// really bad
handleThings = (opts) => {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
handleThings = (opts) => {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
handleThings = (opts = {}) => {
  // ...
}
```

```typescript
// really bad
handleThings = (opts: object) => {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
handleThings = (opts: object) => {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
handleThings = (opts: object = {}) => {
  // ...
}
```

* Use default parameter syntax rather than mutating function arguments.

> Default parameters last

```javascript
// bad
const handleThings = (opts = {}, name) => {
  // ...
};

// good
const handleThings = (name, opts = {}) => {
  // ...
};
```


```typescript
// bad
const handleThings = (opts: object = {}, name: string) => {
  // ...
};

// good
const handleThings = (name: string, opts: object = {}) => {
  // ...
};
```

* Always put default parameters last.


## Side effects

> Side effects

```javascript
var b = 1;

// bad
const count = (a = b++) => {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

```typescript
var b: number = 1;

// bad
const count = (a = b++) => {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

* Avoid side effects with default parameters.
* They are confusing to reason about.


## New functions

> New functions

```javascript
// bad
const add = new Function('a', 'b', 'return a + b');

// still bad
const subtract = Function('a', 'b', 'return a - b');

// good
const x = (a, b) => {
  // ...
  return a + b;
};
```

```typescript
// bad
const add = new Function('a', 'b', 'return a + b');

// still bad
const subtract = Function('a', 'b', 'return a - b');

// good
const x = (a: number, b: number): number => {
  // ...
  return a + b;
};
```

* Never use the Function constructor to create a new function. 
* Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

### ESLint

`"no-new-func": "error"`


## Mutate params 

> Mutate params

```javascript
// bad
const f1 = (obj) => {
  obj.key = 1;
}

// good
const f1 = (obj) => {
  const updatedObj = {...obj, key: 1}; // shallow clone
}

// better
import {default as cloneDeep} from 'lodash/cloneDeep';

const f1 = (obj) => {
  const updatedObj = {...cloneDeep(obj), key: 1}; // using lodash for a deep clone
}
```

```typescript
// bad
function f1(obj: object) {
  obj.key = 1;
}

// good
const f1 = (obj: object) => {
  const updatedObj: object = {...obj, key: 1}; // shallow clone
}

// better
import {default as cloneDeep} from 'lodash/cloneDeep';

const f1 = (obj: object) => {
  const updatedObj: object = {...cloneDeep(obj), key: 1}; // using lodash for a deep clone
}
```

> Reassign parameters

```javascript
// bad
const f1 = (a) => {
  a = 1;
  // ...
}

// bad
const f2 = (a) => {
  if (!a) {a = 1;}
  // ...
}

// good
const f4 = (a = 1) => {
  // ...
}
```

```typescript
// bad
const f1 = (a: number) => {
  a = 1;
  // ...
}

// bad
const f2 = (a: number) => {
  if (!a) {a = 1;}
  // ...
}

// good
const f4 = (a: number = 1) => {
  // ...
}
```

* Never mutate parameters.
* Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.
* It will alter the variable being passed in.
* Never reassign parameters. 
* Reassigning parameters can lead to unexpected behavior, especially when accessing the arguments object. It can also cause optimization issues, especially in V8.

### ESLint

`"no-param-reassign": "error"`


## Spread operator

> Spread operator

```javascript
// bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// good
const x = [1, 2, 3, 4, 5];
console.log(...x);

// bad
new (Function.prototype.bind.apply(Date, [null, 2018, 8, 5]));

// good
new Date(...[2018, 8, 5]);
```

```typescript
// bad
const x: number[] = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// good
const x: number[] = [1, 2, 3, 4, 5];
console.log(...x);

// bad
new (Function.prototype.bind.apply(Date, [null, 2018, 8, 5]));

// good
new Date(...[2018, 8, 5]);
```

* Prefer the use of the spread operator ... to call variadic functions. 
* It's cleaner, you don't need to supply a context, and you can not easily compose new with apply.

### ESLint

`"prefer-spread": "error"`


## Returns

> Returns

```javascript
// bad
const doSomething(condition) {
  if(condition) {
    return true;
  }
}

// good
const doSomething(condition) {
  if(condition) {
    return true;
  }

  return false;
}
```

```typescript
// bad
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }
}

// good
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }

  return false;
}
```

* Unless a function returns undefined, always return.
* Unlike statically-typed languages which enforce that a function returns a specified type of value, JavaScript allows different code paths in a function to return different types of values.

### ESLint

`"consistent-return": "error"`
