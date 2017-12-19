# Arrays

## Array creation

> Array creation

```javascript
// bad
const items = new Array();

// good
const items = [];

// bad
const colors = ['red',, 'blue'];

// good
const colors = ['red', 'blue'];
```

```typescript
// bad
const items: any[] = new Array();

// good
const items: any[] = [];

// bad
const colors: string[] = ['red',, 'blue'];

// good
const colors: string[] = ['red', 'blue'];
```

* Use the literal syntax for array creation.
* No sparse arrays. Arrays containing empty slots, most frequently due to multiple commas being used in an array literal.
* TypeScript should enforce the use of, `T[]` instead of `Array<T>` for all types `T`.

### ESLint

`"no-array-constructor": "error"`

`"no-sparse-arrays": "error"`

### TSLint

`"array-type": [true, "array"]`


## Add items

> Use push to add items

```javascript
const someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

```typescript
const someStack: string[] = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

* Use Array#push instead of direct assignment to add items to an array.

> Use spreads

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy: any[] = [...items];
```

```typescript
// bad
const len: number = items.length;
const itemsCopy: any[] = [];
let i: number;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy: any[] = [...items];
```

* Use array spreads `...` to copy arrays.

## Convert to array

> Convert from array-like to array

```javascript
const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```

```typescript
const foo: any[] = document.querySelectorAll('.foo');

// good
const nodes: any[] = Array.from(foo);

// best
const nodes: any[] = [...foo];
```

* To convert an array-like object to an array, use spreads `...` instead of Array.from.

> Mapping over iterables

```javascript
// bad
const baz = [...foo].map(bar);

// good
const baz = Array.from(foo, bar);
```

```typescript
// bad
const baz: any[] = [...foo].map(bar);

// good
const baz: any[] = Array.from(foo, bar);
```

* Use `Array.from` instead of spread `...` for mapping over iterables, because it avoids creating an intermediate array.

> Return statements

```javascript
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});

// good
[1, 2, 3].map((x) => x + 1);

// bad - no returned value means `memo` becomes undefined after the first
iteration [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

// good
inbox.filter((msg) => {
  const { subject, author } = msg;

  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

```typescript
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});

// good
[1, 2, 3].map((x) => x + 1);

// bad - no returned value means `memo` becomes undefined after the first
iteration [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

// good
inbox.filter((msg) => {
  const { subject, author } = msg;

  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

* Use return statements in array method callbacks. It's ok to omit the return if the function body consists of a single statement returning an expression without side effects.

### ESLint

`"array-callback-return": "error"`


## Line breaks

> Line breaks

```javascript
// bad
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [{id: 1}, {id: 2}];

const numberInArray = [1, 2];

// good
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [{id: 1}, {id: 2}];

const numberInArray = [1, 2];
```

```typescript
// bad
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

// good
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
```

* Use line breaks after open and before close array brackets if an array has multiple lines
