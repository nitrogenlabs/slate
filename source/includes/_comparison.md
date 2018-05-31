# Comparison Operators

## eqeqeq

> eqeqeq

```javascript
// Good
if(x !== y && x === z) {
  console.log('test');
}

// Bad
if(x != y && x == z) {
  console.log('test');
}
```

```javascript--flow
// Good
if(x !== y && x === z) {
  console.log('test');
}

// Bad
if(x != y && x == z) {
  console.log('test');
}
```

```typescript
// Good
if(x !== y && x === z) {
  console.log('test');
}

// Bad
if(x != y && x == z) {
  console.log('test');
}
```

* Use `===` and `!==` over `==` and `!=`. 

> ESLint Rules

```json
{
  "eqeqeq": ["error", "always"],
  "no-eq-null": "error"
}
```

## Coercion

> Coercion

```javascript
if([0] && []) {
  // true
  // an array (even an empty one) is an object, objects will evaluate to true
}
```

```javascript--flow
if([0] && []) {
  // true
  // an array (even an empty one) is an object, objects will evaluate to true
}
```

```typescript
if([0] && []) {
  // true
  // an array (even an empty one) is an object, objects will evaluate to true
}
```

* Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules:
  * Objects evaluate to true
  * Undefined evaluates to false
  * Null evaluates to false
  * Booleans evaluate to the value of the boolean
  * Numbers evaluate to false if +0, -0, or NaN, otherwise true
  * Strings evaluate to false if an empty string '', otherwise true

## Shortcut booleans

> Shortcut booleans

```javascript
// Best - Only checks for empty string
const name = '';

if(name !== '') {
  // ...
}

// Best - Checks for zero length
if(collection.length > 0) {
  // ...
}

// Good
if(isValid) {
  // ...
}

// Good - Checks if name is empty string, null or undefined
const name = '';

if(!!name) {
  // ...
}

// Good - Checks for zero length, null or undefined
if(!!collection.length) {
  // ...
}

// Bad
if(isValid === true) {
  // ...
}

// Bad
const name = '';

if(name) {
  // ...
}

// Bad
if(collection.length) {
  // ...
}
```

```javascript--flow
// Best - Only checks for empty string
const name: string = '';

if(name !== '') {
  // ...
}

// Best - Checks for zero length
if(collection.length > 0) {
  // ...
}

// Good
if(isValid) {
  // ...
}

// Good - Checks if name is empty string, null or undefined
const name: string = '';

if(!!name) {
  // ...
}

// Good - Checks for zero length, null or undefined
if(!!collection.length) {
  // ...
}

// Bad
if(isValid === true) {
  // ...
}

// Bad
const name: string = '';

if(name) {
  // ...
}

// Bad
if(collection.length) {
  // ...
}
```

```typescript
// Best - Only checks for empty string
const name: string = '';

if(name !== '') {
  // ...
}

// Best - Checks for zero length
if(collection.length > 0) {
  // ...
}

// Good
if(isValid) {
  // ...
}

// Good - Checks if name is empty string, null or undefined
const name: string = '';

if(!!name) {
  // ...
}

// Good - Checks for zero length, null or undefined
if(!!collection.length) {
  // ...
}

// Bad
if(isValid === true) {
  // ...
}

// Bad
const name: string = '';

if(name) {
  // ...
}

// Bad
if(collection.length) {
  // ...
}
```

* Use shortcuts for booleans, but explicit comparisons for strings and numbers.
* Use 'not not' operator, `!!` to explicitly change type to a boolean. Note empty strings convert to a falsey.

## Case blocks

> Create blocks

```javascript
// Good
switch(foo) {
  case 1: {
    let x = 1;
    break;
  }
  case 2: {
    const x = 2;
    break;
  }
  case 3: {
    const f = () => {
      // ...
    }

    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}

// Bad
switch(foo) {
  case 1:
    let x = 1;
    break;
  case 2:
    // Throws an error since x is already declared
    const x = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}
```

```javascript--flow
// Good
switch(foo) {
  case 1: {
    let x: number = 1;
    break;
  }
  case 2: {
    const x: number = 2;
    break;
  }
  case 3: {
    const f = () => {
      // ...
    }

    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}

// Bad
switch(foo) {
  case 1:
    let x: number = 1;
    break;
  case 2:
    // Throws an error since x is already declared
    const x: number = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}
```

```typescript
// Good
switch(foo) {
  case 1: {
    let x: number = 1;
    break;
  }
  case 2: {
    const x: number = 2;
    break;
  }
  case 3: {
    const f = () => {
      // ...
    }

    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}

// Bad
switch(foo) {
  case 1:
    let x: number = 1;
    break;
  case 2:
    // Throws an error since x is already declared
    const x: number = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}
```

* Use braces to create blocks in case and default clauses that contain lexical declarations (e.g. let, const, function, and class).
* Lexical declarations are visible in the entire switch block but only get initialized when assigned, which only happens when its case is reached. This causes problems when multiple case clauses attempt to define the same thing.
* Makes it easier to use frameworks which rely heavily on switch blocks (ie. [ArkhamJS](https://arkhamjs.io) and Redux). Reduces the amount of unique variable names.

> ESLint Rules

```json
{
  "no-case-declarations": "error"
}
```

## Ternaries

> Nested ternaries

```javascript
// Split into 2 separated ternary expressions
const maybeNull = value1 > value2 ? 'baz' : null;

// Best
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;

// Good
const foo = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// Bad
const foo = maybe1 > maybe2
  ? 'bar'
  : value1 > value2 ? 'baz' : null;
```

```javascript--flow
// Split into 2 separated ternary expressions
const maybeNull: string = value1 > value2 ? 'baz' : null;

// Best
const foo: string = maybe1 > maybe2 ? 'bar' : maybeNull;

// Good
const foo: string = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// Bad
const foo: string = maybe1 > maybe2
  ? 'bar'
  : value1 > value2 ? 'baz' : null;
```

```typescript
// Split into 2 separated ternary expressions
const maybeNull: string = value1 > value2 ? 'baz' : null;

// Best
const foo: string = maybe1 > maybe2 ? 'bar' : maybeNull;

// Good
const foo: string = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// Bad
const foo: string = maybe1 > maybe2
  ? 'bar'
  : value1 > value2 ? 'baz' : null;
```

> Avoid unneeded ternary

```javascript
// Good
const foo = a || b;
const bar = !!c;
const baz = !c;

// Bad
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;
```

```javascript--flow
// Good
const foo: boolean = a || b;
const bar: boolean = !!c;
const baz: boolean = !c;

// Bad
const foo: boolean = a ? a : b;
const bar: boolean = c ? true : false;
const baz: boolean = c ? false : true;
```

```typescript
// Good
const foo: boolean = a || b;
const bar: boolean = !!c;
const baz: boolean = !c;

// Bad
const foo: boolean = a ? a : b;
const bar: boolean = c ? true : false;
const baz: boolean = c ? false : true;
```

> Enclose operators in parentheses

```javascript
// Good
const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

// Good
const bar = (a ** b) - (5 % d);

// Good
if(a || (b && c)) {
  return d;
}

// Good
const bar = a + b / c * d;

// Bad
const foo = a && b < 0 || c > 0 || d + 1 === 0;

// Bad
const bar = a ** b - 5 % d;

// Bad
// one may be confused into thinking (a || b) && c 
if(a || b && c) {
  return d;
}
```

```javascript--flow
// Good
const foo: boolean = (a && b < 0) || c > 0 || (d + 1 === 0);

// Good
const bar: number = (a ** b) - (5 % d);

// Good
if(a || (b && c)) {
  return d;
}

// Good
const bar: number = a + b / c * d;

// Bad
const foo: boolean = a && b < 0 || c > 0 || d + 1 === 0;

// Bad
const bar: number = a ** b - 5 % d;

// Bad
// one may be confused into thinking (a || b) && c 
if(a || b && c) {
  return d;
}
```

```typescript
// Good
const foo: boolean = (a && b < 0) || c > 0 || (d + 1 === 0);

// Good
const bar: number = (a ** b) - (5 % d);

// Good
if(a || (b && c)) {
  return d;
}

// Good
const bar: number = a + b / c * d;

// Bad
const foo: boolean = a && b < 0 || c > 0 || d + 1 === 0;

// Bad
const bar: number = a ** b - 5 % d;

// Bad
// one may be confused into thinking (a || b) && c 
if(a || b && c) {
  return d;
}
```

* Ternaries should not be nested and generally be single line expressions.
* Avoid unneeded ternary statements.
* Enclose operators in parentheses when they are mixed in a statement. When mixing arithmetic operators, do not mix ** and % with themselves or with +, -, *, & /.
* This improves readability and clarifies the developer's intention.

> ESLint Rules

```json
{
  "no-nested-ternary": "error",
  "no-unneeded-ternary": "error",
  "no-mixed-operators": "error"
}
```
