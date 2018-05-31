# Naming Conventions

## Descriptive

> Be descriptive

```javascript
// Good
const query = 'test';

// Bad
const q = 'test';
```

```javascript--flow
// Good
const query: string = 'test';

// Bad
const q: string = 'test';
```

```typescript
// Good
const query: string = 'test';

// Bad
const q: string = 'test';
```

* Avoid single letter names. Be descriptive with your naming.
* Minimum of at least 2 characters. This prevents single letter names but does not exclude names such as 'id'.

> ESLint Rules

```json
{
  "id-length": ["error", 2]
}
```

## camelCase

> camelCase

```javascript
// Good
const thisIsMyObject = {};
const thisIsMyFunction = () => {}

// Bad
const OBJEcttsssss = {};
const this_is_my_object = {};
const c = () => {}
```

```javascript--flow
// Good
const thisIsMyObject: object = {};
const thisIsMyFunction = () => {}

// Bad
const OBJEcttsssss: object = {};
const this_is_my_object: object = {};
const c = () => {}
```

```typescript
// Good
const thisIsMyObject: object = {};
const thisIsMyFunction = () => {}

// Bad
const OBJEcttsssss: object = {};
const this_is_my_object: object = {};
const c = () => {}
```

* Use camelCase when naming objects, functions, and instances. 
* Use camelCase when naming properties unless you need to send an object using another format (ie. an API).

> ESLint Rules

```json
{
  "camelcase": ["error", {"properties": "never"}]
}
```

## PascalCase

> PascalCase

```javascript
// Good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});

// Bad
const user = (options) => {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});
```

```javascript--flow
// Good
class User {
  name: string;

  constructor(options: object) {
    this.name = options.name;
  }
}

const good: User = new User({
  name: 'yup',
});

// Bad
const user = (options: object) => {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});
```

```typescript
// Good
class User {
  name: string;

  constructor(options: object) {
    this.name = options.name;
  }
}

const good: User = new User({
  name: 'yup',
});

// Bad
const user = (options: object) => {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});
```

* Use PascalCase only when naming constructors or classes.

> ESLint Rules

```json
{
  "new-cap": "error"
}
```

## Underscores

> Underscores

```javascript
// Good
this.firstName = 'Panda';

// Bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';
```

```javascript--flow
// Good
this.firstName = 'Panda';

// Bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';
```

```typescript
// Good
this.firstName = 'Panda';

// Bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';
```

* Do not use trailing or leading underscores. 
* JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean "private", in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won't count as breaking, or that tests aren't needed. tl;dr: if you want something to be "private", it must not be observably present.

> ESLint Rules

```json
{
  "no-underscore-dangle": ["error", {"enforceInMethodNames": true}]
}
```

## this

> this

```javascript
// Good
function foo() {
  return () => {
    console.log(this);
  };
}

// Bad
function foo() {
  const self = this;

  return function () {
    console.log(self);
  };
}

// Bad
function foo() {
  const that = this;

  return function () {
    console.log(that);
  };
}
```

```javascript--flow
// Good
function foo() {
  return () => {
    console.log(this);
  };
}

// Bad
function foo() {
  const self = this;

  return function () {
    console.log(self);
  };
}

// Bad
function foo() {
  const that = this;

  return function () {
    console.log(that);
  };
}
```

```typescript
// Good
function foo() {
  return () => {
    console.log(this);
  };
}

// Bad
function foo() {
  const self = this;

  return function () {
    console.log(self);
  };
}

// Bad
function foo() {
  const that = this;

  return function () {
    console.log(that);
  };
}
```

* Don't save references to `this`. Use arrow functions or Function#bind.

## Acronyms

> Acronyms

```javascript
// Best
import TextMessageContainer from './containers/TextMessageContainer';

// Best
const requests = [
  // ...
];

// Good
import SMSContainer from './containers/SMSContainer';

// Good
const HTTPRequests = [
  // ...
];

// Good
const httpRequests = [
  // ...
];

// Bad
import SmsContainer from './containers/SmsContainer';

// Bad
const HttpRequests = [
  // ...
];
```

```javascript--flow
// Best
import TextMessageContainer from './containers/TextMessageContainer';

// Best
const requests = [
  // ...
];

// Good
import SMSContainer from './containers/SMSContainer';

// Good
const HTTPRequests = [
  // ...
];

// Good
const httpRequests = [
  // ...
];

// Bad
import SmsContainer from './containers/SmsContainer';

// Bad
const HttpRequests = [
  // ...
];
```

```typescript
// Best
import TextMessageContainer from './containers/TextMessageContainer';

// Best
const requests = [
  // ...
];

// Good
import SMSContainer from './containers/SMSContainer';

// Good
const HTTPRequests = [
  // ...
];

// Good
const httpRequests = [
  // ...
];

// Bad
import SmsContainer from './containers/SmsContainer';

// Bad
const HttpRequests = [
  // ...
];
```

* Acronyms and initials should always be all capitalized, or all lowercase.
* Names are for readability, not to appease a computer algorithm.
