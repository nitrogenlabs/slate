# Arrays

## Array creation

> Array creation

```javascript
// Good
const items = [];
const colors = ['red', 'blue'];

// Bad
const items = new Array();
const colors = ['red',, 'blue'];
```

```javascript--flow
// Good
const items: any[] = [];
const colors: string[] = ['red', 'blue'];

// Bad
const items: any[] = new Array();
const colors: string[] = ['red',, 'blue'];
```

```typescript
// Good
const items: any[] = [];
const colors: string[] = ['red', 'blue'];

// Bad
const items: any[] = new Array();
const colors: string[] = ['red',, 'blue'];
```

* Use the literal syntax for array creation.
* No sparse arrays. Arrays containing empty slots, most frequently due to multiple commas being used in an array literal.
* TypeScript should enforce the use of, `T[]` instead of `Array<T>` for all types `T`.

> ESLint Rules

```json
{
  "no-array-constructor": "error",
  "no-sparse-arrays": "error"
}
```

## Add items

> Use push to add items

```javascript
const someStack = [];

// Good
someStack.push('abracadabra');

// Bad
someStack[someStack.length] = 'abracadabra';
```

```javascript--flow
const someStack: string[] = [];

// Good
someStack.push('abracadabra');

// Bad
someStack[someStack.length] = 'abracadabra';
```

```typescript
const someStack: string[] = [];

// Good
someStack.push('abracadabra');

// Bad
someStack[someStack.length] = 'abracadabra';
```

* Use Array#push instead of direct assignment to add items to an array.

> Use spreads

```javascript
// Good
const itemsCopy: any[] = [...items];

// Bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}
```

```javascript--flow
// Good
const itemsCopy: any[] = [...items];

// Bad
const len: number = items.length;
const itemsCopy: any[] = [];
let i: number;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}
```

```typescript
// Good
const itemsCopy: any[] = [...items];

// Bad
const len: number = items.length;
const itemsCopy: any[] = [];
let i: number;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}
```

* Use array spreads `...` to copy arrays.

## Convert to array

> Convert from array-like to array

```javascript
const foo = document.querySelectorAll('.foo');

// Best
const nodes = [...foo];

// Good
const nodes = Array.from(foo);
```

```javascript--flow
const foo: any[] = document.querySelectorAll('.foo');

// Best
const nodes: any[] = [...foo];

// Good
const nodes: any[] = Array.from(foo);
```

```typescript
const foo: any[] = document.querySelectorAll('.foo');

// Best
const nodes: any[] = [...foo];

// Good
const nodes: any[] = Array.from(foo);
```

* To convert an array-like object to an array, use spreads `...` instead of Array.from.

> Mapping over iterables

```javascript
// Good
const baz = Array.from(foo, bar);

// Bad
const baz = [...foo].map(bar);
```

```javascript--flow
// Good
const baz: any[] = Array.from(foo, bar);

// Bad
const baz: any[] = [...foo].map(bar);
```

```typescript
// Good
const baz: any[] = Array.from(foo, bar);

// Bad
const baz: any[] = [...foo].map(bar);
```

* Use `Array.from` instead of spread `...` for mapping over iterables, because it avoids creating an intermediate array.

> Return statements

```javascript
// Good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});

// Good
[1, 2, 3].map((x) => x + 1);

// Good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// Good
inbox.filter((msg) => {
  const { subject, author } = msg;

  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});

// Bad - no returned value means `memo` becomes undefined after the first
iteration [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// Bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});
```

```javascript--flow
// Good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});

// Good
[1, 2, 3].map((x) => x + 1);


// Good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// Bad - no returned value means `memo` becomes undefined after the first
iteration [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// Good
inbox.filter((msg) => {
  const { subject, author } = msg;

  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});

// Bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});
```

```typescript
// Good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});

// Good
[1, 2, 3].map((x) => x + 1);


// Good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// Bad - no returned value means `memo` becomes undefined after the first
iteration [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// Good
inbox.filter((msg) => {
  const { subject, author } = msg;

  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});

// Bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});
```

* Use return statements in array method callbacks. It's ok to omit the return if the function body consists of a single statement returning an expression without side effects.

> ESLint Rules

```json
{
  "array-callback-return": "error"
}
```

## Line breaks

> Line breaks

```javascript
// Good
const arr = [[0, 1], [2, 3], [4, 5]];
const objectInArray = [{id: 1}, {id: 2}];
const numberInArray = [1, 2];

// Bad
const arr = [[0, 1], [2, 3], [4, 5]];
const objectInArray = [{id: 1}, {id: 2}];
const numberInArray = [1, 2];
```

```javascript--flow
// Good
const arr = [
  [0, 1],
  [2, 3],
  [4, 5]
];

const objectInArray = [
  {id: 1},
  {id: 2}
];

const numberInArray: number[] = [
  1,
  2
];

// Bad
const arr: number[] = [
  [0, 1], [2, 3], [4, 5]
];

const objectInArray: object[] = [{
  id: 1
}, {
    id: 2
}];

const numberInArray number[] = [
  1, 2
];
```

```typescript
// Good
const arr = [
  [0, 1],
  [2, 3],
  [4, 5]
];

const objectInArray = [
  {id: 1},
  {id: 2}
];

const numberInArray: number[] = [
  1,
  2
];

// Bad
const arr: number[] = [
  [0, 1], [2, 3], [4, 5]
];

const objectInArray: object[] = [{
  id: 1
}, {
    id: 2
}];

const numberInArray number[] = [
  1, 2
];
```

* Use line breaks after open and before close array brackets if an array has multiple lines
