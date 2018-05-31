# Commas

## Leading commas

> Leading commas

```javascript
// Good
const story = [
  once,
  upon,
  aTime
];

// Good
const hero = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers'
};

// Bad
const story = [
    once
  , upon
  , aTime
];

// Bad
const hero = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};
```

```javascript--flow
// Good
const story: StoryType = [
  once,
  upon,
  aTime
];

// Good
const hero: HeroType = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers'
};

// Bad
const story: StoryType = [
    once
  , upon
  , aTime
];

// Bad
const hero: HeroType = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};
```

```typescript
// Good
const story: StoryType = [
  once,
  upon,
  aTime
];

// Good
const hero: HeroType = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers'
};

// Bad
const story: StoryType = [
    once
  , upon
  , aTime
];

// Bad
const hero: HeroType = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};
```

* No leading commas.

> ESLint Rules

```json
{
  "comma-style": ["error", "last"]
}
```


## Trailing comma

> Additional trailing commas

```javascript
// Good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes = [
  'Batman',
  'Superman'
];

// Good
const createHero = (
  firstName,
  lastName,
  inventorOf
) => {
  // does nothing
}

// Good (note that a comma must not appear after a "rest" element)
const createHero = (
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
) => {
  // does nothing
}

// Good
createHero(
  firstName,
  lastName,
  inventorOf
);

// Good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);

// Bad
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];

// Bad
const createHero = (
  firstName,
  lastName,
  inventorOf,
) => {
  // does nothing
}

// Bad
createHero(
  firstName,
  lastName,
  inventorOf,
);
```

```javascript--flow
interface Hero {
  +firstName: string;
  +lastName: string;
}

// Good
const hero: Hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes: string[] = [
  'Batman',
  'Superman'
];

// Good
const createHero = (
  firstName,
  lastName,
  inventorOf
): Hero => {
  // does nothing
}

// Good (note that a comma must not appear after a "rest" element)
const createHero = (
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
): Hero => {
  // does nothing
}

// Good
createHero(
  firstName,
  lastName,
  inventorOf
);

// Good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);

// Bad
const hero: Hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes: string[] = [
  'Batman',
  'Superman',
];

// Bad
const createHero = (
  firstName,
  lastName,
  inventorOf,
): Hero => {
  // does nothing
}

// Bad
createHero(
  firstName,
  lastName,
  inventorOf,
);
```

```typescript
interface Hero {
  readonly firstName: string;
  readonly lastName: string;
}

// Good
const hero: Hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes: string[] = [
  'Batman',
  'Superman'
];

// Good
const createHero = (
  firstName,
  lastName,
  inventorOf
): Hero => {
  // does nothing
}

// Good (note that a comma must not appear after a "rest" element)
const createHero = (
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
): Hero => {
  // does nothing
}

// Good
createHero(
  firstName,
  lastName,
  inventorOf
);

// Good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);

// Bad
const hero: Hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes: string[] = [
  'Batman',
  'Superman',
];

// Bad
const createHero = (
  firstName,
  lastName,
  inventorOf,
): Hero => {
  // does nothing
}

// Bad
createHero(
  firstName,
  lastName,
  inventorOf,
);
```

* No trailing commas.
* Creates extra work when switching from multiline lists to single.
* Trailing commas cause problems in legacy browsers.
* Stays consistent with JSON formatting
* Although transpilers, like Babel, will remove the additional trailing comma in the transpiled code, we should write better code and not rely on transpilers fixing incorrect code.
* Git diffs may increase but our philosophy is better code, not smaller commits/reviews.

> ESLint Rules

```json
{
  "comma-dangle": ["error", "never"]
}
```
