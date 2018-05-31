# Functions

## Arrow functions

> Arrow functions

```javascript
// Best
[1, 2, 3].map((x) => x * (x + 1));

// Good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// Bad
[1, 2, 3].map(function(x) {
  const y = x + 1;
  return x * y;
});
```

```javascript--flow
// Best
[1, 2, 3].map((x: number) => x * (x + 1));

// Good
[1, 2, 3].map((x: number) => {
  const y: number = x + 1;
  return x * y;
});

// Bad
[1, 2, 3].map(function(x: number) {
  const y: number = x + 1;
  return x * y;
});
```

```typescript
// Best
[1, 2, 3].map((x: number) => x * (x + 1));

// Good
[1, 2, 3].map((x: number) => {
  const y: number = x + 1;
  return x * y;
});

// Bad
[1, 2, 3].map(function(x: number) {
  const y: number = x + 1;
  return x * y;
});
```

> Confusing arrow

```javascript
// Best
const itemHeight = (item) => {
  const {height, largeSize, smallSize} = item;
  return height > 256 ? largeSize : smallSize;
};

// Good
const itemHeight = (item) => (item.height > 256 ? item.largeSize : item.smallSize);

// Bad
const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

// Bad
const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;
```

```javascript--flow
// Best
const itemHeight: number = (item) => {
  const {height, largeSize, smallSize} = item;
  return height > 256 ? largeSize : smallSize;
};

// Good
const itemHeight: number = (item) => (item.height > 256 ? item.largeSize : item.smallSize);

// Bad
const itemHeight: number = item => item.height > 256 ? item.largeSize : item.smallSize;

// Bad
const itemHeight: number = (item) => item.height > 256 ? item.largeSize : item.smallSize;
```

```typescript
// Best
const itemHeight: number = (item) => {
  const {height, largeSize, smallSize} = item;
  return height > 256 ? largeSize : smallSize;
};

// Good
const itemHeight: number = (item) => (item.height > 256 ? item.largeSize : item.smallSize);

// Bad
const itemHeight: number = item => item.height > 256 ? item.largeSize : item.smallSize;

// Bad
const itemHeight: number = (item) => item.height > 256 ? item.largeSize : item.smallSize;
```

* When you must use an anonymous function (as when passing an inline callback), use arrow function notation.
* It creates a version of the function that executes in the context of this, which is usually what you want, and is a more concise syntax.
* If you have a fairly complicated function, you might move the `this` logic out into its own named function expression.
* Avoid confusing arrow function syntax (=>) with comparison operators (<=, >=). 

> ESLint Rules

```json
{
  "prefer-arrow-callback": "error",
  "arrow-spacing": "error",
  "no-confusing-arrow": ["error", {"allowParens": true}]
}
```

## Named function expressions

> Named function expressions

```javascript
// Good
const foo = () => {
  // ...
};

// Bad
function foo() {
  // ...
}

// Bad
const foo = function() {
  // ...
};
```

```javascript--flow
// Good
const foo = () => {
  // ...
};

// Bad
function foo() {
  // ...
}

// Bad
const foo = function() {
  // ...
};
```

```typescript
// Good
const foo = () => {
  // ...
};

// Bad
function foo() {
  // ...
}

// Bad
const foo = function() {
  // ...
};
```

* Use named function expressions instead of function declarations. 
* Any time an anonymous function expression appears on the right-hand side of something like an assignment or initialization, the resulting function will have a name (foo, in the examples).

> ESLint Rules

```json
{
  "func-style": ["error", "expression", {"allowArrowFunctions": true}]
}
```

## Single line

> Single line

```javascript
// Best
[1, 2, 3].map((value) => `A string containing the ${value + 1}.`);

// Good - returns an array with strings
[1, 2, 3].map((value) => `A string containing the ${value}.`);

// Good
[1, 2, 3].map((value) => {
  const nextNumber = value + 1;
  return `A string containing the ${nextNumber}.`;
});

// Good
[1, 2, 3].map((value, index) => ({[index]: value}));

// Bad - returns an array with 3 undefines
[1, 2, 3].map((value) => {
  const nextNumber = value + 1;
  `A string containing the ${nextNumber}.`;
});

// No implicit return with side effects
const foo = (callback) => {
  const val = callback();

  if(val === true) {
    // Do something if callback returns true
  }
};

let bool = false;

// Good - returns a boolean
foo(() => {
  bool = true;
  return bool;
});

// Bad - returns undefined to the callback
foo(() => bool = true);
```

```javascript--flow
// Best
[1, 2, 3].map((value: number) => `A string containing the ${value + 1}.`);

// Good - returns an array with strings
[1, 2, 3].map((value: number): string => `A string containing the ${value}.`);

// Good
[1, 2, 3].map((value: number): string => {
  const nextNumber: number = value + 1;
  return `A string containing the ${nextNumber}.`;
});

// Good
[1, 2, 3].map((value: number, index: number) => ({[index]: value}));

// Bad - returns an array with 3 undefines
[1, 2, 3].map((value: number): void => {
  const nextNumber: number = value + 1;
  `A string containing the ${nextNumber}.`;
});

// No implicit return with side effects
const foo = (callback: () => boolean) => {
  const val: boolean = callback();

  if(val === true) {
    // Do something if callback returns true
  }
};

let bool: boolean = false;

// Good - returns a boolean
foo(() => {
  bool = true;
  return bool;
});

// Bad - returns undefined to the callback
foo(() => bool = true);
```

```typescript
// Best
[1, 2, 3].map((value: number) => `A string containing the ${value + 1}.`);

// Good - returns an array with strings
[1, 2, 3].map((value: number): string => `A string containing the ${value}.`);

// Good
[1, 2, 3].map((value: number): string => {
  const nextNumber: number = value + 1;
  return `A string containing the ${nextNumber}.`;
});

// Good
[1, 2, 3].map((value: number, index: number) => ({[index]: value}));

// Bad - returns an array with 3 undefines
[1, 2, 3].map((value: number): void => {
  const nextNumber: number = value + 1;
  `A string containing the ${nextNumber}.`;
});

// No implicit return with side effects
const foo = (callback: () => boolean) => {
  const val: boolean = callback();

  if(val === true) {
    // Do something if callback returns true
  }
};

let bool: boolean = false;

// Good - returns a boolean
foo(() => {
  bool = true;
  return bool;
});

// Bad - returns undefined to the callback
foo(() => bool = true);
```

* If the function body consists of a single statement returning an expression without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a return statement.
* Syntactic sugar. It reads well when multiple functions are chained together.

> ESLint Rules

```json
{
  "arrow-parens": ["error", "always"],
  "arrow-body-style": ["error", "as-needed"]
}
```

## Multiline

> Multiline

```javascript
// Good
['get', 'post', 'put'].map(httpMethod => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));

// Bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);
```

```javascript--flow
// Good
['get', 'post', 'put'].map(httpMethod => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));

// Bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);
```

```typescript
// Good
['get', 'post', 'put'].map(httpMethod => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));

// Bad
['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);
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

```javascript--flow
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

* Wrap immediately invoked function expressions in parentheses.
* An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

> ESLint Rules

```json
{
  "wrap-iife": ["error", "outside"]
}
```


## Non-function block

* Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears. 

> ESLint Rules

```json
{
  "no-loop-func": "warn"
}
```


## Block definition

> Block definition

```javascript
// Good
let test;

if(currentUser) {
  test = () => {
    console.log('Yup.');
  };
}

// Bad
if(currentUser) {
  let test = () => {
    console.log('Nope.');
  };
}
```

```javascript--flow
// Good
let test;

if(currentUser) {
  test = () => {
    console.log('Yup.');
  };
}

// Bad
if(currentUser) {
  let test = () => {
    console.log('Nope.');
  };
}
```

```typescript
// Good
let test;

if(currentUser) {
  test = () => {
    console.log('Yup.');
  };
}

// Bad
if(currentUser) {
  let test = () => {
    console.log('Nope.');
  };
}
```

* ECMA-262 defines a block as a list of statements. A function declaration is not a statement.

## Arguments

> Parentheses

```javascript
// Good
[1, 2, 3].map((x) => x * x);

// Bad
[1, 2, 3].map(x => x * x);
```

```javascript--flow
// Good
[1, 2, 3].map((x: number) => x * x);

// Bad
[1, 2, 3].map(x => x * x);
```

```typescript
// Good
[1, 2, 3].map((x: number) => x * x);

// Bad
[1, 2, 3].map(x => x * x);
```

> Parameter names

```javascript
// Good
const foo = (name, options, args) => {
  // ...
}

// Bad
const foo = (name, options, arguments) => {
  // ...
}
```

```javascript--flow
// Good
const foo = (name: string, options: object, args) => {
  // ...
}

// Bad
const foo = (name: string, options: object, arguments) => {
  // ...
}
```

```typescript
// Good
const foo = (name: string, options: object, args) => {
  // ...
}

// Bad
const foo = (name: string, options: object, arguments) => {
  // ...
}
```

> Rest params syntax

```javascript
// Good
const concatenateAll = (...args) => {
  return args.join('');
};

// Bad
const concatenateAll = () => {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
};
```

```javascript--flow
// Good
const concatenateAll = (...args) => {
  return args.join('');
};

// Bad
const concatenateAll = () => {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
};
```

```typescript
// Good
const concatenateAll = (...args) => {
  return args.join('');
};

// Bad
const concatenateAll = () => {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
};
```

* Always include parentheses around arguments for clarity and consistency.
* Parentheses do not need to be added later if arguments are added.
* Easier transition when using typings.
* Never name a parameter arguments. This will take precedence over the arguments object that is given to every function scope.
* Never use arguments, opt to use rest syntax `...` instead.
* ... is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like arguments.

> ESLint Rules

```json
{
  "arrow-parens": ["error", "always"],
  "prefer-rest-params": "error"
}
```

## Default parameters

> Default parameters

```javascript
// Good
handleThings = (opts = {}) => {
  // ...
}

// Really bad
handleThings = (opts) => {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// Still bad
handleThings = (opts) => {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}
```

```javascript--flow
// Good
handleThings = (opts: object = {}) => {
  // ...
}

// Really bad
handleThings = (opts: object) => {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// Still bad
handleThings = (opts: object) => {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}
```

```typescript
// Good
handleThings = (opts: object = {}) => {
  // ...
}

// Really bad
handleThings = (opts: object) => {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// Still bad
handleThings = (opts: object) => {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}
```

* Use default parameter syntax rather than mutating function arguments.

> Default parameters last

```javascript
// Good
const handleThings = (name, opts = {}) => {
  // ...
};

// Bad
const handleThings = (opts = {}, name) => {
  // ...
};
```

```javascript--flow
// Good
const handleThings = (name: string, opts: object = {}) => {
  // ...
};

// Bad
const handleThings = (opts: object = {}, name: string) => {
  // ...
};
```

```typescript
// Good
const handleThings = (name: string, opts: object = {}) => {
  // ...
};

// Bad
const handleThings = (opts: object = {}, name: string) => {
  // ...
};
```

* Always put default parameters last.

## Side effects

> Side effects

```javascript
var b = 1;

// Bad
const count = (a = b++) => {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

```javascript--flow
var b: number = 1;

// Bad
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

// Bad
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
// Good
const x = (a, b) => {
  // ...
  return a + b;
};

// Bad
const add = new Function('a', 'b', 'return a + b');

// Still bad
const subtract = Function('a', 'b', 'return a - b');
```

```javascript--flow
// Good
const x = (a: number, b: number): number => {
  // ...
  return a + b;
};

// Bad
const add = new Function('a', 'b', 'return a + b');

// Still bad
const subtract = Function('a', 'b', 'return a - b');
```

```typescript
// Good
const x = (a: number, b: number): number => {
  // ...
  return a + b;
};

// Bad
const add = new Function('a', 'b', 'return a + b');

// Still bad
const subtract = Function('a', 'b', 'return a - b');
```

* Never use the Function constructor to create a new function. 
* Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

> ESLint Rules

```json
{
  "no-new-func": "error"
}
```

## Mutate params 

> Mutate params

```javascript
// Best
import {default as cloneDeep} from 'lodash/cloneDeep';

const f1 = (obj) => {
  const updatedObj = {...cloneDeep(obj), key: 1}; // using lodash for a deep clone
}

// Good
const f1 = (obj) => {
  const updatedObj = {...obj, key: 1}; // shallow clone
}

// Bad
const f1 = (obj) => {
  obj.key = 1;
}
```

```javascript--flow
// Best
import {default as cloneDeep} from 'lodash/cloneDeep';

const f1 = (obj: object) => {
  const updatedObj: object = {...cloneDeep(obj), key: 1}; // using lodash for a deep clone
}

// Good
const f1 = (obj: object) => {
  const updatedObj: object = {...obj, key: 1}; // shallow clone
}

// Bad
function f1(obj: object) {
  obj.key = 1;
}
```

```typescript
// Best
import {default as cloneDeep} from 'lodash/cloneDeep';

const f1 = (obj: object) => {
  const updatedObj: object = {...cloneDeep(obj), key: 1}; // using lodash for a deep clone
}

// Good
const f1 = (obj: object) => {
  const updatedObj: object = {...obj, key: 1}; // shallow clone
}

// Bad
function f1(obj: object) {
  obj.key = 1;
}
```

> Reassign parameters

```javascript
// Good
const f4 = (a = 1) => {
  // ...
}

// Bad
const f1 = (a) => {
  a = 1;
  // ...
}

// Bad
const f2 = (a) => {
  if (!a) {a = 1;}
  // ...
}
```

```javascript--flow
// Good
const f4 = (a: number = 1) => {
  // ...
}

// Bad
const f1 = (a: number) => {
  a = 1;
  // ...
}

// Bad
const f2 = (a: number) => {
  if (!a) {a = 1;}
  // ...
}
```

```typescript
// Good
const f4 = (a: number = 1) => {
  // ...
}

// Bad
const f1 = (a: number) => {
  a = 1;
  // ...
}

// Bad
const f2 = (a: number) => {
  if (!a) {a = 1;}
  // ...
}
```

* Never mutate parameters.
* Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.
* It will alter the variable being passed in.
* Never reassign parameters. 
* Reassigning parameters can lead to unexpected behavior, especially when accessing the arguments object. It can also cause optimization issues, especially in V8.

> ESLint Rules

```json
{
  "no-param-reassign": "error"
}
```

## Spread operator

> Spread operator

```javascript
// Good
const x = [1, 2, 3, 4, 5];
console.log(...x);

// Good
new Date(...[2018, 8, 5]);

// Bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// Bad
new (Function.prototype.bind.apply(Date, [null, 2018, 8, 5]));
```

```javascript--flow
// Good
const x: number[] = [1, 2, 3, 4, 5];
console.log(...x);

// Good
new Date(...[2018, 8, 5]);

// Bad
const x: number[] = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// Bad
new (Function.prototype.bind.apply(Date, [null, 2018, 8, 5]));
```

```typescript
// Good
const x: number[] = [1, 2, 3, 4, 5];
console.log(...x);

// Good
new Date(...[2018, 8, 5]);

// Bad
const x: number[] = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// Bad
new (Function.prototype.bind.apply(Date, [null, 2018, 8, 5]));
```

* Prefer the use of the spread operator ... to call variadic functions. 
* It's cleaner, you don't need to supply a context, and you can not easily compose new with apply.

> ESLint Rules

```json
{
  "prefer-spread": "error"
}
```

## Returns

> Returns

```javascript
// Good
const doSomething(condition) {
  if(condition) {
    return true;
  }

  return false;
}

// Bad
const doSomething(condition) {
  if(condition) {
    return true;
  }
}
```

```javascript--flow
// Good
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }

  return false;
}

// Bad
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }
}
```

```typescript
// Good
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }

  return false;
}

// Bad
const doSomething(condition): boolean {
  if(condition) {
    return true;
  }
}
```

* Unless a function returns undefined, always return.
* Unlike statically-typed languages which enforce that a function returns a specified type of value, JavaScript allows different code paths in a function to return different types of values.

> ESLint Rules

```json
{
  "consistent-return": "warn"
}
