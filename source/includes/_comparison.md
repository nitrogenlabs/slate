# Comparison Operators

## eqeqeq

> eqeqeq

```javascript
// bad
if(x != y && x == z) {
  console.log('test');
}

// good
if(x !== y && x === z) {
  console.log('test');
}
```

```typescript
// bad
if(x != y && x == z) {
  console.log('test');
}

// good
if(x !== y && x === z) {
  console.log('test');
}
```

* Use `===` and `!==` over `==` and `!=`. 

### ESLint

`"eqeqeq": ["error", "always"]`

`"no-eq-null": "error"`

### TSLint

`"triple-equals": true`


## Coercion

> Coercion

```javascript
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
// bad
if(isValid === true) {
  // ...
}

// good
if(isValid) {
  // ...
}

// bad
const name = '';

if(name) {
  // ...
}

// good - Checks if name is empty string, null or undefined
const name = '';

if(!!name) {
  // ...
}

// better - Only checks for empty string
const name = '';

if(name !== '') {
  // ...
}

// bad
if(collection.length) {
  // ...
}

// good - Checks for zero length, null or undefined
if(!!collection.length) {
  // ...
}

// better - Checks for zero length
if(collection.length > 0) {
  // ...
}
```

```typescript
// bad
if(isValid === true) {
  // ...
}

// good
if(isValid) {
  // ...
}

// bad
const name = '';

if(name) {
  // ...
}

// good - Checks if name is empty string, null or undefined
const name = '';

if(!!name) {
  // ...
}

// better - Only checks for empty string
const name = '';

if(name !== '') {
  // ...
}

// bad
if(collection.length) {
  // ...
}

// good - Checks for zero length, null or undefined
if(!!collection.length) {
  // ...
}

// better - Checks for zero length
if(collection.length > 0) {
  // ...
}
```

* Use shortcuts for booleans, but explicit comparisons for strings and numbers.
* Use 'not not' operator, `!!` to explicitly change type to a boolean. Note empty strings convert to a falsey.


## Case blocks

> Create blocks

```javascript
// bad
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

// good
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
    function f() {
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
```

```typescript
// bad
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

// good
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
    function f() {
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
```

* Use braces to create blocks in case and default clauses that contain lexical declarations (e.g. let, const, function, and class). 
* Lexical declarations are visible in the entire switch block but only get initialized when assigned, which only happens when its case is reached. This causes problems when multiple case clauses attempt to define the same thing.
* Makes it easier to use frameworks which rely heavily on switch blocks (ie. ArkhamJS and Redux). Reduces the amount of unique variable names.

### ESLint
`"no-case-declarations": "error"`


## Ternaries

> Nested ternaries

```javascript
// bad
const foo = maybe1 > maybe2
  ? 'bar'
  : value1 > value2 ? 'baz' : null;

// split into 2 separated ternary expressions
const maybeNull = value1 > value2 ? 'baz' : null;

// better
const foo = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// best
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

```typescript
// bad
const foo: string = maybe1 > maybe2
  ? 'bar'
  : value1 > value2 ? 'baz' : null;

// split into 2 separated ternary expressions
const maybeNull: string = value1 > value2 ? 'baz' : null;

// better
const foo: string = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// best
const foo: string = maybe1 > maybe2 ? 'bar' : maybeNull;
```

> Avoid unneeded ternary

```javascript
// bad
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;

// good
const foo = a || b;
const bar = !!c;
const baz = !c;
```

```typescript
// bad
const foo: boolean = a ? a : b;
const bar: boolean = c ? true : false;
const baz: boolean = c ? false : true;

// good
const foo: boolean = a || b;
const bar: boolean = !!c;
const baz: boolean = !c;
```

> Enclose operators in parentheses

```javascript
// bad
const foo = a && b < 0 || c > 0 || d + 1 === 0;

// bad
const bar = a ** b - 5 % d;

// bad
// one may be confused into thinking (a || b) && c 
if(a || b && c) {
  return d;
}

// good
const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

// good
const bar = (a ** b) - (5 % d);

// good
if(a || (b && c)) {
  return d;
}

// good
const bar = a + b / c * d;
```

```typescript
// bad
const foo: boolean = a && b < 0 || c > 0 || d + 1 === 0;

// bad
const bar: number = a ** b - 5 % d;

// bad
// one may be confused into thinking (a || b) && c 
if(a || b && c) {
  return d;
}

// good
const foo: boolean = (a && b < 0) || c > 0 || (d + 1 === 0);

// good
const bar: number = (a ** b) - (5 % d);

// good
if(a || (b && c)) {
  return d;
}

// good
const bar: number = a + b / c * d;
```

* Ternaries should not be nested and generally be single line expressions. 
* Avoid unneeded ternary statements.
* Enclose operators in parentheses when they are mixed in a statement. When mixing arithmetic operators, do not mix ** and % with themselves or with +, -, *, & /.
* This improves readability and clarifies the developer's intention.

### ESLint
`"no-nested-ternary": "error"`

`"no-unneeded-ternary": "error"`

`"no-mixed-operators": "error"`
