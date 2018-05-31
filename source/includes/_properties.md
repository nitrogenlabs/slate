# Properties

## Access property

> Access property

```javascript
const luke = {
  jedi: true,
  age: 28,
};

// Best
const {jedi: isJedi} = luke;

// Good
const isJedi = luke.jedi;

// Bad
const isJedi = luke['jedi'];
```

```javascript--flow
interface Jedi {
  +jedi: boolean;
  +age: number;
}

const luke: Jedi = {
  jedi: true,
  age: 28,
};

// Best
const {jedi: isJedi} = luke;

// Good
const isJedi: boolean = luke.jedi;

// Bad
const isJedi: boolean = luke['jedi'];
```

```typescript
interface Jedi {
  readonly jedi: boolean;
  readonly age: number;
}

const luke: Jedi = {
  jedi: true,
  age: 28,
};

// Best
const {jedi: isJedi} = luke;

// Good
const isJedi: boolean = luke.jedi;

// Bad
const isJedi: boolean = luke['jedi'];
```

* Deconstruct properties when accessing properties. This way we traverse the object once and write fewer lines of code.
* If deconstructing is not possible, use dot notation. 

> ESLint Rules

```json
{
  "dot-notation": "error"
}
```


## Bracket Notation

> Bracket Notation

```javascript
const luke = {
  jedi: true,
  age: 28
};

const getProp = (prop) => {
  return luke[prop];
};

const isJedi = getProp('jedi');
```

```javascript--flow
interface Jedi {
  +jedi: boolean;
  +age: number;
}

const luke: Jedi = {
  jedi: true,
  age: 28
};

const getProp = (prop: string): any => {
  return luke[prop];
};

const isJedi: boolean = getProp('jedi') as boolean;
```

```typescript
interface Jedi {
  readonly jedi: boolean;
  readonly age: number;
}

const luke: Jedi = {
  jedi: true,
  age: 28
};

const getProp = (prop: string): any => {
  return luke[prop];
};

const isJedi: boolean = getProp('jedi') as boolean;
```

* Use bracket notation `[]` when accessing properties with a variable.

## Exponentiation operator

> Exponentiation operator

```javascript
// Good
const binary = 2 ** 10;

// Bad
const binary = Math.pow(2, 10);
```

```javascript--flow
// Good
const binary: number = 2 ** 10;

// Bad
const binary: number = Math.pow(2, 10);
```

```typescript
// Good
const binary: number = 2 ** 10;

// Bad
const binary: number = Math.pow(2, 10);
```

* Use exponentiation operator `**` when calculating exponentiations.

## Spreads

> Spreads

```javascript
// Good
const father = {...vader};

// Bad
const father = Object.spread({}, vader);
```

```javascript--flow
// Good
const father: Jedi = {...vader};

// Bad
const father: Jedi = Object.spread({}, vader);
```

```typescript
// Good
const father: Jedi = {...vader};

// Bad
const father: Jedi = Object.spread({}, vader);
```

> ESLint Rules

```json
{
  "no-restricted-properties": [
    "error",
    {
      "object": "Object",
      "property": "assign",
      "message": "Please use spread, {...obj}"
    }
  ]
}
```
