# Objects

## Object creation

> Object creation

```javascript
// Good
const item = {};

// Bad
const item = new Object();
```

```javascript--flow
// Good
const item: object = {};

// Bad
const item: object = new Object();
```

```typescript
// Good
const item: object = {};

// Bad
const item: object = new Object();
```

* Use the literal syntax for object creation.

> ESLint Rules

```json
{
  "no-new-object": "error"
}
```

## Computed property names

> Computed property names

```javascript
const getKey = k => `a key named ${k}`;

// Good
const obj = {
  id: 5,
  name: 'Chicago',
  [getKey('enabled)]: true
};

// Bad
const obj = {
  id: 5,
  name: 'Chicago'
};
obj[getKey('enabled')] = true;
```

```javascript--flow
const getKey = (k: string): string => `a key named ${k}`;

// Good
const obj: object = {
  id: 5,
  name: 'Chicago',
  [getKey('enabled')]: true
};

// Bad
const obj: object = {
  id: 5,
  name: 'Chicago'
};
obj[getKey('enabled')] = true;
```

```typescript
const getKey = (k: string): string => `a key named ${k}`;

// Good
const obj: object = {
  id: 5,
  name: 'Chicago',
  [getKey('enabled')]: true
};

// Bad
const obj: object = {
  id: 5,
  name: 'Chicago'
};
obj[getKey('enabled')] = true;
```

* Use computed property names when creating objects with dynamic property names.
* They allow you to define all the properties of an object in one place.

## Shorthand

> Object method shorthand

```javascript
// Good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  }
};

// Bad
const atom = {
  value: 1,

  addValue: value => {
    return atom.value + value;
  }
};
```

```javascript--flow
// Good
const atom: object = {
  value: 1,

  addValue(value: string): string {
    return atom.value + value;
  }
};

// Bad
const atom: object = {
  value: 1,

  addValue: (value: string): string => {
    return atom.value + value;
  }
};
```

```typescript
// Good
const atom: object = {
  value: 1,

  addValue(value: string): string {
    return atom.value + value;
  }
};

// Bad
const atom: object = {
  value: 1,

  addValue: (value: string): string => {
    return atom.value + value;
  }
};
```

> Object property shorthand

```javascript
const lukeSkywalker = 'Luke Skywalker';

// Good
const obj = {
  lukeSkywalker
};

// Bad
const obj = {
  lukeSkywalker: lukeSkywalker
};
```

```javascript--flow
const lukeSkywalker: string = 'Luke Skywalker';

// Good
const obj: object = {
  lukeSkywalker
};

// Bad
const obj: object = {
  lukeSkywalker: lukeSkywalker
};
```

```typescript
const lukeSkywalker: string = 'Luke Skywalker';

// Good
const obj: object = {
  lukeSkywalker
};

// Bad
const obj: object = {
  lukeSkywalker: lukeSkywalker
};
```

> Group shorthand properties at the begninning

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// Good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};

// Bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};
```

```javascript--flow
const anakinSkywalker: string = 'Anakin Skywalker';
const lukeSkywalker: string = 'Luke Skywalker';

// Good
const obj: object = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};

// Bad
const obj: object = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};
```

```typescript
const anakinSkywalker: string = 'Anakin Skywalker';
const lukeSkywalker: string = 'Luke Skywalker';

// Good
const obj: object = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};

// Bad
const obj: object = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};
```

> Only quote invalid identifiers

```javascript
// Good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};

// Bad
const bad = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};
```

```javascript--flow
// Good
const good: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};

// Bad
const bad: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};
```

```typescript
// Good
const good: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};

// Bad
const bad: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};
```

> Do not call prototype methods directly

```javascript
// Best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));

// Good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// Bad
console.log(object.hasOwnProperty(key));
```

```javascript--flow
// Best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));

// Good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// Bad
console.log(object.hasOwnProperty(key));
```

```typescript
// Best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));

// Good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// Bad
console.log(object.hasOwnProperty(key));
```

> Use object spreads

```javascript
// Good
const original = {a: 1, b: 2};
const copy = {...original, c: 3}; // copy => {a: 1, b: 2, c: 3}

const {a, ...noA} = copy; // noA => {b: 2, c: 3}

// Bad
const original = {a: 1, b: 2};
const copy = Object.assign({}, original, {c: 3}); // copy => {a: 1, b: 2, c: 3}

// Very bad
const original = {a: 1, b: 2};
const copy = Object.assign(original, {c: 3}); // this mutates `original`
delete copy.a; // so does this
```

```javascript--flow
// Good
const original: object = {a: 1, b: 2};
const copy: object = {...original, c: 3}; // copy => {a: 1, b: 2, c: 3}

const {a, ...noA} = copy; // noA => {b: 2, c: 3}

// Bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign({}, original, {c: 3}); // copy => {a: 1, b: 2, c: 3}

// Very bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign(original, {c: 3}); // this mutates `original`
delete copy.a; // so does this
```

```typescript
// Good
const original: object = {a: 1, b: 2};
const copy: object = {...original, c: 3}; // copy => {a: 1, b: 2, c: 3}

const {a, ...noA} = copy; // noA => {b: 2, c: 3}

// Bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign({}, original, {c: 3}); // copy => {a: 1, b: 2, c: 3}

// Very bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign(original, {c: 3}); // this mutates `original`
delete copy.a; // so does this
```

* Use object method shorthand.
* Use property value shorthand.
* It is shorter to write and descriptive.
* Group your shorthand properties at the beginning of your object declaration.
* It's easier to tell which properties are using shorthand.
* Only quote properties that are invalid identifiers. 
* In general we consider it subjectively easier to read, improves syntax highlighting, and easily optimized by many JS engines.
* Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.
* These methods may be shadowed by properties on the object in question - consider `{hasOwnProperty: false}` - or, the object may be a null object `(Object.create(null))`.
* Prefer the object spread operator over `Object.assign` to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

> ESLint Rules

```json
{
  "object-shorthand": "warn",
  "quote-props": ["error", "as-needed"]
}
