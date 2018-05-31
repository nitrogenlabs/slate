# Destructuring

## Object destructuring

> Object destructuring

```javascript
// Best
const getFullName = ({firstName, lastName}) => `${firstName} ${lastName}`;

// Good
const getFullName = user => {
  const {firstName, lastName} = user;
  return `${firstName} ${lastName}`;
};

// Bad
const getFullName = user => {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
};
```

```javascript--flow
interface UserType {
  +firstName: string;
  +lastName: string;
}

// Best
const getFullName = ({firstName, lastName}: UserType): string => {
  return `${firstName} ${lastName}`;
};

// Good
const getFullName = (user: UserType): string => {
  const {firstName, lastName} = user;
  return `${firstName} ${lastName}`;
};

// Bad
const getFullName = (user: UserType): string => {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
};
```

```typescript
interface UserType {
  readonly firstName: string;
  readonly lastName: string;
}

// Best
const getFullName = ({firstName, lastName}: UserType): string => {
  return `${firstName} ${lastName}`;
};

// Good
const getFullName = (user: UserType): string => {
  const {firstName, lastName} = user;
  return `${firstName} ${lastName}`;
};

// Bad
const getFullName = (user: UserType): string => {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
};
```

> Array destructuring

```javascript
const arr = [1, 2, 3, 4];

// Good
const [first, second] = arr;

// Bad
const first = arr[0];
const second = arr[1];
```

```javascript--flow
const arr: number[] = [1, 2, 3, 4];

// Good
const [first, second] = arr;

// Bad
const first: number = arr[0];
const second: number = arr[1];
```

```typescript
const arr: number[] = [1, 2, 3, 4];

// Good
const [first, second] = arr;

// Bad
const first: number = arr[0];
const second: number = arr[1];
```

> Multiple return values

```javascript
// Good
const processInput = input => {
  // then a miracle occurs
  return {left, right, top, bottom};
};

// the caller selects only the data they need
const {left, top} = processInput(input);

// Bad
const processInput = input => {
  // then a miracle occurs
  return [left, right, top, bottom];
};

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);
```

```javascript--flow
// Good
const processInput = (input): object => {
  // then a miracle occurs
  return {left, right, top, bottom};
};

// the caller selects only the data they need
const {left, top} = processInput(input);

// Bad
const processInput = (input): object => {
  // then a miracle occurs
  return [left, right, top, bottom];
};

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);
```

```typescript
// Good
const processInput = (input): object => {
  // then a miracle occurs
  return {left, right, top, bottom};
};

// the caller selects only the data they need
const {left, top} = processInput(input);

// Bad
const processInput = (input): object => {
  // then a miracle occurs
  return [left, right, top, bottom];
};

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);
```

* Use object destructuring when accessing and using multiple properties of an object.
* Destructuring saves you from creating temporary references for those properties.
* Use array destructuring.
* Use object destructuring for multiple return values, not array destructuring.
* You can add new properties over time or change the order of things without breaking call sites.

> ESLint Rules

```json
{
  "prefer-destructuring": [
    "error",
    {
      "array": true,
      "object": true
    },
    {
      "enforceForRenamedProperties": false
    }
  ]
}
```
