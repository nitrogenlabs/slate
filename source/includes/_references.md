# References

## const

> Using const

```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

```typescript
// bad
var a = 1;
var b = 2;

// good
const a: number = 1;
const b: number = 2;
```

* Use `const` for all references; avoid using `var`.
* This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.

### ESLint

`"prefer-const": "error"`

`"no-const-assign": "error"`

### TSLint

`"prefer-const": true`


## let

> Using let

```javascript
// bad
var count = 1;

if (true) {
  count += 1;
}

// good, use the let.
let count = 1;

if (true) {
  count += 1;
}
```

```typescript
// bad
var count = 1;

if (true) {
  count += 1;
}

// good, use the let.
let count: number = 1;

if (true) {
  count += 1;
}
```

> const and let only exist in the blocks they are defined in.

```javascript
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
```

```typescript
{
  let a: number = 1;
  const b: number = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
```

* If you must reassign references, use `let` instead of `var`.
* `let` is block-scoped rather than function-scoped like `var`.
* Note that both `let` and `const` are block-scoped.

### ESLint

`no-var: "error"`

### TSLint

`"no-var-keyword": true`
