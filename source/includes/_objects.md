# Objects

## Object creation

> Object creation

```javascript
// bad
const item = new Object();

// good
const item = {};
```

```typescript
// bad
const item: object = new Object();

// good
const item: object = {};
```

* Use the literal syntax for object creation.

### ESLint

`"no-new-object": "error"`


## Computed property names

> Computed property names

```javascript
const getKey = k => `a key named ${k}`;

// bad
const obj = {
  id: 5,
  name: 'Chicago'
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'Chicago',
  [getKey('enabled)]: true
};
```

```typescript
const getKey = (k: string): string => `a key named ${k}`;

// bad
const obj: object = {
  id: 5,
  name: 'Chicago'
};
obj[getKey('enabled')] = true;

// good
const obj: object = {
  id: 5,
  name: 'Chicago',
  [getKey('enabled')]: true
};
```

* Use computed property names when creating objects with dynamic property names.
* They allow you to define all the properties of an object in one place.

## Shorthand

> Object method shorthand

```javascript
// bad
const atom = {
  value: 1,

  addValue: value => {
    return atom.value + value;
  }
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  }
};
```

```typescript
// bad
const atom: object = {
  value: 1,

  addValue: (value: string): string => {
    return atom.value + value;
  }
};

// good
const atom: object = {
  value: 1,

  addValue(value: string): string {
    return atom.value + value;
  }
};
```

> Object property shorthand

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker
};

// good
const obj = {
  lukeSkywalker
};
```

```typescript
const lukeSkywalker: string = 'Luke Skywalker';

// bad
const obj: object = {
  lukeSkywalker: lukeSkywalker
};

// good
const obj: object = {
  lukeSkywalker
};
```

> Group shorthand properties at the begninning

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};

// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};
```

```typescript
const anakinSkywalker: string = 'Anakin Skywalker';
const lukeSkywalker: string = 'Luke Skywalker';

// bad
const obj: object = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};

// good
const obj: object = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};
```

> Only quote invalid identifiers

```javascript
// bad
const bad = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};
```

```typescript
// bad
const bad: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};

// good
const good: object = {
  foo: 3,
  bar: 4,
  'data-blah': 5
};
```

> Do not call prototype methods directly

```javascript
// bad
console.log(object.hasOwnProperty(key));

// good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));
```

```typescript
// bad
console.log(object.hasOwnProperty(key));

// good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));
```

> Use object spreads

```javascript
// very bad
const original = {a: 1, b: 2};
const copy = Object.assign(original, {c: 3}); // this mutates `original`
delete copy.a; // so does this

// bad
const original = {a: 1, b: 2};
const copy = Object.assign({}, original, {c: 3}); // copy => {a: 1, b: 2, c: 3}

// good
const original = {a: 1, b: 2};
const copy = {...original, c: 3}; // copy => {a: 1, b: 2, c: 3}

const {a, ...noA} = copy; // noA => {b: 2, c: 3}
```

```typescript
// very bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign(original, {c: 3}); // this mutates `original`
delete copy.a; // so does this

// bad
const original: object = {a: 1, b: 2};
const copy: object = Object.assign({}, original, {c: 3}); // copy => {a: 1, b: 2, c: 3}

// good
const original: object = {a: 1, b: 2};
const copy: object = {...original, c: 3}; // copy => {a: 1, b: 2, c: 3}

const {a, ...noA} = copy; // noA => {b: 2, c: 3}
```

* Use object method shorthand.
* Use property value shorthand.
* It is shorter to write and descriptive.
* Group your shorthand properties at the beginning of your object declaration.
* It's easier to tell which properties are using shorthand.
* Only quote properties that are invalid identifiers. 
* In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.
* Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.
* These methods may be shadowed by properties on the object in question - consider `{hasOwnProperty: false}` - or, the object may be a null object `(Object.create(null))`.
* Prefer the object spread operator over `Object.assign` to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

### ESLint

`"object-shorthand": "error"`

`"quote-props": ["error", "as-needed"]`

### TSLint

`"object-literal-shorthand": true`

`"object-literal-key-quotes": [true, "as-needed"]`
