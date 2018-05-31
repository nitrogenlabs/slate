# Variables

## Const/Let

> const/let

```javascript
// Best
const superPower = new SuperPower();

// Good
let superPower = new SuperPower();

// Bad
superPower = new SuperPower();
```

```javascript--flow
// Best
const superPower: SuperPower = new SuperPower();

// Good
let superPower: SuperPower = new SuperPower();

// Bad
superPower = new SuperPower();
```

```typescript
// Best
const superPower: SuperPower = new SuperPower();

// Good
let superPower: SuperPower = new SuperPower();

// Bad
superPower = new SuperPower();
```

* Always use const or let to declare variables. Not doing so will result in global variables. 
* We want to avoid polluting the global namespace. Captain Planet warned us of that.

> ESLint Rules

```json
{
  "no-undef-init": "error",
  "prefer-const": "error"
}
```

## Single use

> Single use

```javascript
// Good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';

// Bad
const items = getItems(),
  goSportsTeam = true,
  dragonball = 'z';

// Bad
// (compare to above, and try to spot the mistake)
const items = getItems(),
  goSportsTeam = true;
  dragonball = 'z';
```

```javascript--flow
// Good
const items: Items[] = getItems();
const goSportsTeam: boolean = true;
const dragonball: string = 'z';

// Bad
const items: Items[] = getItems(),
  goSportsTeam: boolean = true,
  dragonball: string = 'z';

// Bad
// (compare to above, and try to spot the mistake)
const items: Items[] = getItems(),
  goSportsTeam: boolean = true;
  dragonball: string = 'z';
```

```typescript
// Good
const items: Items[] = getItems();
const goSportsTeam: boolean = true;
const dragonball: string = 'z';

// Bad
const items: Items[] = getItems(),
  goSportsTeam: boolean = true,
  dragonball: string = 'z';

// Bad
// (compare to above, and try to spot the mistake)
const items: Items[] = getItems(),
  goSportsTeam: boolean = true;
  dragonball: string = 'z';
```

* Use one `const` or `let` declaration per variable.
* It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

> ESLint Rules

```json
{
  "one-var": ["error", "never"]
}
```

## Unused

> Unused

```javascript
// Good
const foo = (amount) => {
  const percent = 0.3;
  const total = amount * percent;

  return `$ ${total}`;
};

// Bad
const foo = (amount) => {
  const percent = 0.3;
  const ratio = (120 * 0.5) * percent;
  const total = amount * percent;

  return `$ ${total}`;
};
```

```javascript--flow
// Good
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const total: number = amount * percent;

  return `$ ${total}`;
};

// Bad
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const ratio: number = (120 * 0.5) * percent;
  const total: number = amount * percent;

  return `$ ${total}`;
};
```

```typescript
// Good
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const total: number = amount * percent;

  return `$ ${total}`;
};

// Bad
const foo = (amount: number): string => {
  const percent: number = 0.3;
  const ratio: number = (120 * 0.5) * percent;
  const total: number = amount * percent;

  return `$ ${total}`;
};
```

* Maintains clean code.
* Quite often, a developer will optimize a snippet of code but leave remnants behind. These often confuse other developers working on the same codebase.

> ESLint Rules

```json
{
  "no-unused-vars": ["error", {"ignoreRestSiblings": true}]
}
```

## Grouping

> Grouping

```javascript
// Good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;

// Bad
let i, len, dragonball,
  items = getItems(),
  goSportsTeam = true;

// Bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;
```

```javascript--flow
// Good
const goSportsTeam: boolean = true;
const items: Items[] = getItems();
let dragonball: DragonBall;
let i: number;
let length: number;

// Bad
let i: number, len: number, dragonball: DragonBall,
  items: Items[] = getItems(),
  goSportsTeam: boolean = true;

// Bad
let i: number;
const items: Items[] = getItems();
let dragonball: DragonBall;
const goSportsTeam: boolean = true;
let len: number;
```

```typescript
// Good
const goSportsTeam: boolean = true;
const items: Items[] = getItems();
let dragonball: DragonBall;
let i: number;
let length: number;

// Bad
let i: number, len: number, dragonball: DragonBall,
  items: Items[] = getItems(),
  goSportsTeam: boolean = true;

// Bad
let i: number;
const items: Items[] = getItems();
let dragonball: DragonBall;
const goSportsTeam: boolean = true;
let len: number;
```

* Group all your `const` and then group all your `let`.
* This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

## Naming

> Avoid abbreviations

```javascript
// Good
const latitude = 41.8781;
const longitude = 87.6298;

// Bad
const lat = 41.8781;
const lon = 87.6298;
```

```javascript--flow
// Good
const latitude: number = 41.8781;
const longitude: number = 87.6298;

// Bad
const lat: number = 41.8781;
const lon: number = 87.6298;
```

```typescript
// Good
const latitude: number = 41.8781;
const longitude: number = 87.6298;

// Bad
const lat: number = 41.8781;
const lon: number = 87.6298;
```

* Try to avoid abbreviations when all possible. 
* Make sure variables are well explained in the name to help other developers identify and follow data.


## Placement

> Placement

```javascript
// Good
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

// Bad - unnecessary function call
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
```

```javascript--flow
// Good
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

// Bad - unnecessary function call
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
```

```typescript
// Good
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

// Bad - unnecessary function call
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
```

* Assign variables where you need them, but place them in a reasonable place.
* `let` and `const` are block scoped and not function scoped.

> ESLint Rules

```json
{
  "no-use-before-define": ["error", {"functions": false, "classes": false}]
}
```

## Chain

> Chaining

```javascript
// Good
(() => {
  let a = 1;
  let b = a;
  let c = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`

// Bad
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
```

```javascript--flow
// Good
(() => {
  let a: number = 1;
  let b: number = a;
  let c: number = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`

// Bad
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
```

```typescript
// Good
(() => {
  let a: number = 1;
  let b: number = a;
  let c: number = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`

// Bad
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
```

* Don't chain variable assignments.
* Chaining variable assignments creates implicit global variables.

> ESLint Rules

```json
{
  "no-multi-assign": "error"
}
```

## Unary increments/decrements

> Unary increments/decrements

```javascript
// Good
const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;

// Bad
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
```

```javascript--flow
// Good
const array: number[] = [1, 2, 3];
let num: number = 1;
num += 1;
num -= 1;

const sum: number = array.reduce((a, b) => a + b, 0);
const truthyCount: number = array.filter(Boolean).length;

// Bad
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
```

```typescript
// Good
const array: number[] = [1, 2, 3];
let num: number = 1;
num += 1;
num -= 1;

const sum: number = array.reduce((a, b) => a + b, 0);
const truthyCount: number = array.filter(Boolean).length;

// Bad
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
```

* Avoid using unary increments and decrements (`++`, `--`).
* Per the eslint documentation, unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like `num += 1` instead of `num++` or `num ++`. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.

> ESLint Rules

```json
{
  "no-plusplus": "error"
}
```
