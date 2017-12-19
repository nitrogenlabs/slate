# Variables

## Const/Let

> const/let

```javascript
// bad
superPower = new SuperPower();

// good
let superPower = new SuperPower();

// better
const superPower = new SuperPower();
```

```typescript
// bad
superPower = new SuperPower();

// good
let superPower: SuperPower = new SuperPower();

// better
const superPower: SuperPower = new SuperPower();
```

* Always use const or let to declare variables. Not doing so will result in global variables. 
* We want to avoid polluting the global namespace. Captain Planet warned us of that.

### ESLint

`"no-undef": "error"`

`"prefer-const": "error"`

### TSLint

`"prefer-const": true`


## Single use

> Single use

```javascript
// bad
const items = getItems(),
  goSportsTeam = true,
  dragonball = 'z';

// bad
// (compare to above, and try to spot the mistake)
const items = getItems(),
  goSportsTeam = true;
  dragonball = 'z';

// good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

```typescript
// bad
const items: Items[] = getItems(),
  goSportsTeam: boolean = true,
  dragonball: string = 'z';

// bad
// (compare to above, and try to spot the mistake)
const items: Items[] = getItems(),
  goSportsTeam: boolean = true;
  dragonball: string = 'z';

// good
const items: Items[] = getItems();
const goSportsTeam: boolean = true;
const dragonball: string = 'z';
```

* Use one `const` or `let` declaration per variable.
* It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

### ESLint
`"one-var": ["error", "never"]`

### TSLint

`"one-variable-per-declaration": false`


## Unused

> Unused

```javascript
// bad
const foo = (amount) => {
  const percent = 0.3;
  const ratio = (120 * 0.5) * percent;
  const total = amount * percent;

  return `$ ${total}`;
};

// good
const foo = (amount) => {
  const percent = 0.3;
  const total = amount * percent;

  return `$ ${total}`;
};
```

```typescript
// bad
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const ratio: number = (120 * 0.5) * percent;
  const total: number = amount * percent;

  return `$ ${total}`;
};

// good
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const total: number = amount * percent;

  return `$ ${total}`;
};
```

* Maintains clean code.
* Quite often, a developer will optimize a snippet of code but leave remnants behind. These often confuse other developers working on the same codebase.

### ESLint

`"no-unused-vars": ["error", {"ignoreRestSiblings": true}]`

### TSLint

`"no-unused-variable": true`


## Grouping

> Grouping

```javascript
// bad
let i, len, dragonball,
  items = getItems(),
  goSportsTeam = true;

// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

```typescript
// bad
let i: number, len: number, dragonball: DragonBall,
  items: Items[] = getItems(),
  goSportsTeam: boolean = true;

// bad
let i: number;
const items: Items[] = getItems();
let dragonball: DragonBall;
const goSportsTeam: boolean = true;
let len: number;

// good
const goSportsTeam: boolean = true;
const items: Items[] = getItems();
let dragonball: DragonBall;
let i: number;
let length: number;
```

* Group all your `const` and then group all your `let`.
* This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.


## Naming

> Avoid abbreviations

```javascript
// bad
const lat: number = 41.8781;
const lon: number = 87.6298;

// good
const latitude: number = 41.8781;
const longitude: number = 87.6298;
```

```typescript
// bad
const lat: number = 41.8781;
const lon: number = 87.6298;

// good
const latitude: number = 41.8781;
const longitude: number = 87.6298;
```

* Try to avoid abbreviations when all possible. 
* Make sure variables are well explained in the name to help other developers identify and follow data.


## Placement

> Placement

```javascript
// bad - unnecessary function call
const checkName = (hasName) => {
  const name = getName();

  if(hasName) {
    return null;
  }

  if(name === 'test') {
    this.setName('');
    return null;
  }

  return name;
};

// good
const checkName = (hasName) => {
  if(hasName) {
    return null;
  }

  const name = getName();

  if(name === 'test') {
    this.setName('');
    return null;
  }

  return name;
};
```

```typescript
// bad - unnecessary function call
const checkName = (hasName: boolean): string => {
  const name: string = getName();

  if(hasName) {
    return null;
  }

  if(name === 'test') {
    this.setName('');
    return null;
  }

  return name;
};

// good
const checkName = (hasName: boolean): string => {
  if(hasName) {
    return false;
  }

  const name: string = getName();

  if(name === 'test') {
    this.setName('');
    return null;
  }

  return name;
};
```

* Assign variables where you need them, but place them in a reasonable place.
* `let` and `const` are block scoped and not function scoped.

### ESLint

`"no-use-before-define": ["error", {"functions": false, "classes": false}]`

### TSLint

`"no-use-before-declare": true`


## Chain

> Chaining

```javascript
// bad
(() => {
  // JavaScript interprets this as
  // let a = ( b = ( c = 1 ) );
  // The let keyword only applies to variable a; variables b and c become
  // global variables.
  let a = b = c = 1;
}());

console.log(a); // throws ReferenceError
console.log(b); // 1
console.log(c); // 1

// good
(() => {
  let a = 1;
  let b = a;
  let c = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`
```

```typescript
// bad
(() => {
  // JavaScript interprets this as
  // let a = ( b = ( c = 1 ) );
  // The let keyword only applies to variable a; variables b and c become
  // global variables.
  let a: number = b = c = 1;
}());

console.log(a); // throws ReferenceError
console.log(b); // 1
console.log(c); // 1

// good
(() => {
  let a: number = 1;
  let b: number = a;
  let c: number = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`
```

* Don't chain variable assignments.
* Chaining variable assignments creates implicit global variables.

### ESLint
`"no-multi-assign": "error"`


## Unary increments/decrements

> Unary increments/decrements

```javascript
// bad
const array = [1, 2, 3];
let num = 1;
num++;
--num;
let sum = 0;
let truthyCount = 0;

for(let i = 0; i < array.length; i++) {
  let value = array[i];
  sum += value;

  if(value) {
    truthyCount++;
  }
}

// good
const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;
```

```typescript
// bad
const array: number[] = [1, 2, 3];
let num: number = 1;
num++;
--num;
let sum: number = 0;
let truthyCount: number = 0;

for(let i: number = 0; i < array.length; i++) {
  let value: number = array[i];
  sum += value;

  if(value) {
    truthyCount++;
  }
}

// good
const array: number[] = [1, 2, 3];
let num: number = 1;
num += 1;
num -= 1;

const sum: number = array.reduce((a, b) => a + b, 0);
const truthyCount: number = array.filter(Boolean).length;
```

* Avoid using unary increments and decrements (`++`, `--`).
* Per the eslint documentation, unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like `num += 1` instead of `num++` or `num ++`. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.

### ESLint

`"no-plusplus": "error"`
