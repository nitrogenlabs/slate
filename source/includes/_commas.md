# Commas

## Leading commas

> Leading commas

```javascript
// bad
const story = [
    once
  , upon
  , aTime
];

// good
const story = [
  once,
  upon,
  aTime,
];

// bad
const hero = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};

// good
const hero = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers',
};
```

```typescript
// bad
const story: StoryType = [
    once
  , upon
  , aTime
];

// good
const story: StoryType = [
  once,
  upon,
  aTime,
];

// bad
const hero: HeroType = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};

// good
const hero: HeroType = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers',
};
```

* No leading commas.

### ESLint
`"comma-style": ["error", "last"]`


## Trailing comma

> Additional trailing commas

```javascript
// bad
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];

// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes = [
  'Batman',
  'Superman'
];

// bad
const createHero = (
  firstName,
  lastName,
  inventorOf,
) => {
  // does nothing
}

// good
const createHero = (
  firstName,
  lastName,
  inventorOf
) => {
  // does nothing
}

// good (note that a comma must not appear after a "rest" element)
const createHero = (
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
) => {
  // does nothing
}

// bad
createHero(
  firstName,
  lastName,
  inventorOf,
);

// good
createHero(
  firstName,
  lastName,
  inventorOf
);

// good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);
```

```typescript
// bad
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];

// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes = [
  'Batman',
  'Superman'
];

// bad
const createHero = (
  firstName,
  lastName,
  inventorOf,
) => {
  // does nothing
}

// good
const createHero = (
  firstName,
  lastName,
  inventorOf
) => {
  // does nothing
}

// good (note that a comma must not appear after a "rest" element)
const createHero = (
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
) => {
  // does nothing
}

// bad
createHero(
  firstName,
  lastName,
  inventorOf,
);

// good
createHero(
  firstName,
  lastName,
  inventorOf
);

// good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);
```

* No trailing commas.
* Creates extra work when switching from multiline lists to single.
* Trailing commas cause problems in legacy browsers.
* Stays consistent with JSON formatting
* Although transpilers, like Babel, will remove the additional trailing comma in the transpiled code, we should write better code and not rely on transpilers fixing incorrect code.
* Git diffs may increase but our philosophy is better code, not smaller commits/reviews.

### ESLint
`"comma-dangle": ["error", "never"]`

### TSLint
`"trailing-comma": [true, {"multiline": "never", "singleline": "never", "esSpecCompliant": true}]`
