# Naming Conventions

## Descriptive

> Be descriptive

```javascript
// bad
const q = 'test';

// good
const query = 'test';
```

```typescript
// bad
const q: string = 'test';

// good
const query: string = 'test';
```

* Avoid single letter names. Be descriptive with your naming.

### ESLint

`"id-length": "error"`


## camelCase

> camelCase

```javascript
// bad
const OBJEcttsssss = {};
const this_is_my_object = {};
const c = () => {}

// good
const thisIsMyObject = {};
const thisIsMyFunction = () => {}
```

```typescript
// bad
const OBJEcttsssss: object = {};
const this_is_my_object: object = {};
const c = () => {}

// good
const thisIsMyObject: object = {};
const thisIsMyFunction = () => {}
```

* Use camelCase when naming objects, functions, and instances. 
* Use camelCase when naming properties unless you need to send an object using another format (ie. an API).

### ESLint

`"camelcase": ["error", {properties: "never"}]`

### TSLint

`"variable-name": [true, "ban-keywords", "check-format"`


## PascalCase

> PascalCase

```javascript
// bad
const user = (options) => {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```

```typescript
// bad
const user = (options: object) => {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// good
class User {
  name: string;

  constructor(options: object) {
    this.name = options.name;
  }
}

const good: User = new User({
  name: 'yup',
});
```

* Use PascalCase only when naming constructors or classes. 

### ESLint

`"new-cap": "error"`


## Underscores

> Underscores

```javascript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';

// good
this.firstName = 'Panda';
```

```typescript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';

// good
this.firstName = 'Panda';
```

* Do not use trailing or leading underscores. 
* JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean "private", in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won't count as breaking, or that tests aren't needed. tl;dr: if you want something to be "private", it must not be observably present.

### ESLint

`"no-underscore-dangle": ["error", {"enforceInMethodNames": true}]`


## this

> this

```javascript
// bad
function foo() {
  const self = this;
  
  return function () {
    console.log(self);
  };
}

// bad
function foo() {
  const that = this;

  return function () {
    console.log(that);
  };
}

// good
function foo() {
  return () => {
    console.log(this);
  };
}
```

```typescript
// bad
function foo() {
  const self = this;
  
  return function () {
    console.log(self);
  };
}

// bad
function foo() {
  const that = this;

  return function () {
    console.log(that);
  };
}

// good
function foo() {
  return () => {
    console.log(this);
  };
}
```

* Don't save references to `this`. Use arrow functions or Function#bind.


## Acronyms

> Acronyms

```javascript
// bad
import SmsContainer from './containers/SmsContainer';

// bad
const HttpRequests = [
  // ...
];

// good
import SMSContainer from './containers/SMSContainer';

// good
const HTTPRequests = [
  // ...
];

// also good
const httpRequests = [
  // ...
];

// best
import TextMessageContainer from './containers/TextMessageContainer';

// best
const requests = [
  // ...
];
```

```typescript
// bad
import SmsContainer from './containers/SmsContainer';

// bad
const HttpRequests = [
  // ...
];

// good
import SMSContainer from './containers/SMSContainer';

// good
const HTTPRequests = [
  // ...
];

// also good
const httpRequests = [
  // ...
];

// best
import TextMessageContainer from './containers/TextMessageContainer';

// best
const requests = [
  // ...
];
```

* Acronyms and initialisms should always be all capitalized, or all lowercased.
* Names are for readability, not to appease a computer algorithm.
