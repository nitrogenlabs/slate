# Comments

## Multiline

> Multiline

```javascript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag) => {
  // ...
  return element;
}

// good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
}
```

```typescript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag: TagType): Element => {
  // ...
  return element;
}

// good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: TagType): Element => {
  // ...
  return element;
}
```

* Use `/** ... */` for multi-line comments.


## Single line

> Single line

```javascript
// bad
const active = true;  // is current tab

// good
// is current tab
const active = true;

// bad
const getType = () => {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};

// good
const getType = () => {
  console.log('fetching type...');

  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};

// also good
const getType = () => {
  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};
```

```typescript
// bad
const active: boolean = true;  // is current tab

// good
// is current tab
const active: boolean = true;

// bad
const getType = (): string => {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// good
const getType = (): string => {
  console.log('fetching type...');

  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// also good
const getType = (): string => {
  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};
```

* Use `//` for single line comments. 
* Place single line comments on a newline above the subject of the comment. 
* Put an empty line before the comment unless it's on the first line of a block.

## Prefix

> Space prefix

```javascript
// bad
//is current tab
const active = true;

// good
// is current tab
const active = true;

// bad
/**
  *make() returns a new element
  *based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
};

// good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
};
```

```typescript
// bad
//is current tab
const active: boolean = true;

// good
// is current tab
const active: boolean = true;

// bad
/**
  *make() returns a new element
  *based on the passed-in tag name
  */
const make = (tag: string): Element => {
  // ...
  return element;
};

// good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: string): Element => {
  // ...
  return element;
};
```

> Use // FIXME: to annotate problems.

```javascript
class Calculator extends Abacus {
  constructor() {
    super();

    // FIXME: shouldn't use a global here
    total = 0;
  }
}
```

```typescript
class Calculator extends Abacus {
  constructor() {
    super();

    // FIXME: shouldn't use a global here
    total = 0;
  }
}
```

> Use // TODO: to annotate solutions to problems.

```javascript
class Calculator extends Abacus {
  constructor() {
    super();

    // TODO: total should be configurable by an options param
    this.total = 0;
  }
}
```

```typescript
class Calculator extends Abacus {
  private total: number;
  
  constructor() {
    super();

    // TODO: total should be configurable by an options param
    this.total = 0;
  }
}
```

* Start all comments with a space to make it easier to read. 
* Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.
* Adding an eslint warning will remind you what needs to be tended to.

### ESLint
`"spaced-comment": ["error", "always", { "exceptions": ["-", "+"] }]`

`"no-warning-comments": ["warn", {"terms": ["fixme", "todo"], "location": "anywhere"}]`

### TSLint
`"comment-format": [true, "check-space"]`
