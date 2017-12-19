# Properties

## Access property

> Access property

```javascript
const luke = {
  jedi: true,
  age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;

// better
const {jedi: isJedi} = luke;
```

```typescript
const luke: Jedi = {
  jedi: true,
  age: 28,
};

// bad
const isJedi: boolean = luke['jedi'];

// good
const isJedi: boolean = luke.jedi;

// better
const {jedi: isJedi} = luke;
```

* Deconstruct properties when accessing properties. This way we traverse the object once and write fewer lines of code.
* If deconstructing is not possible, use dot notation. 

### ESLint

`"dot-notation": "error"`


## Braket Notation

> Braket Notation

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

```typescript
const luke: Jedi = {
  jedi: true,
  age: 28
};

const getProp = (prop: string) => {
  return luke[prop];
};

const isJedi: boolean = getProp('jedi') as boolean;
```

* Use bracket notation `[]` when accessing properties with a variable.


## Exponentiation operator

> Exponentiation operator

```javascript
// bad
const binary = Math.pow(2, 10);

// good
const binary = 2 ** 10;
```

```typescript
// bad
const binary: number = Math.pow(2, 10);

// good
const binary: number = 2 ** 10;
```

* Use exponentiation operator `**` when calculating exponentiations. 

### ESLint

`"no-restricted-properties": ["error", {"object": "Object", "property": "assign", "message": "Please use spread, {...obj}"}]`
