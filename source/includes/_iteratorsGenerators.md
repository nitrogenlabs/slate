## Iterators and Generators

> Do not use iterators

```javascript
const numbers = [1, 2, 3, 4, 5];

// Best (use the functional force)
const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;

// Best (keeping it functional)
const increasedByOne = numbers.map(num => num + 1);

// Good
let sum = 0;
numbers.forEach((num) => sum += num);
sum === 15;

// Good
const increasedByOne = [];
numbers.forEach((num) => increasedByOne.push(num + 1));

// Bad
let sum = 0;

for(let num of numbers) {
  sum += num;
}

sum === 15;

// Bad
const increasedByOne = [];

for(let i = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}
```

```javascript--flow
const numbers: number[] = [1, 2, 3, 4, 5];

// Best (use the functional force)
const sum: number = numbers.reduce((total, num) => total + num, 0);
sum === 15;

// Best (keeping it functional)
const increasedByOne: number[] = numbers.map((num: number) => num + 1);

// Good
let sum: number = 0;
numbers.forEach((num: number) => sum += num);
sum === 15;

// Good
const increasedByOne: number[] = [];
numbers.forEach((num: number) => increasedByOne.push(num + 1));

// Bad
let sum: number = 0;

for(let num: number of numbers) {
  sum += num;
}

sum === 15;

// Bad
const increasedByOne: number[] = [];

for(let i: number = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}
```

```typescript
const numbers: number[] = [1, 2, 3, 4, 5];

// Best (use the functional force)
const sum: number = numbers.reduce((total, num) => total + num, 0);
sum === 15;

// Best (keeping it functional)
const increasedByOne: number[] = numbers.map((num: number) => num + 1);

// Good
let sum: number = 0;
numbers.forEach((num: number) => sum += num);
sum === 15;

// Good
const increasedByOne: number[] = [];
numbers.forEach((num: number) => increasedByOne.push(num + 1));

// Bad
let sum: number = 0;

for(let num: number of numbers) {
  sum += num;
}

sum === 15;

// Bad
const increasedByOne: number[] = [];

for(let i: number = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}
```

* Don't use iterators. 
* Prefer JavaScript"s higher-order functions instead of loops like for-in or for-of.
* This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side effects.
* Use map() / every() / filter() / find() / findIndex() / reduce() / some() / ... to iterate over arrays, and Object.keys() / Object.values() / Object.entries() to produce arrays so you can iterate over objects.

> ESLint Rules

```json
{
  "no-iterator": "error",
  "no-restricted-syntax": [
    "error",
    "FunctionExpression",
    "WithStatement",
    "BinaryExpression[operator='in']"
  ]
}
```

* Don't use generators for now.
* They don't transpile well to ES5.
