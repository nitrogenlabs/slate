# Comments

## Multiline

> Multiline

```javascript
// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
}

// Bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag) => {
  // ...
  return element;
}
```

```javascript
// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: TagType): Element => {
  // ...
  return element;
}

// Bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag: TagType): Element => {
  // ...
  return element;
}
```

```javascript--flow
// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: TagType): Element => {
  // ...
  return element;
}

// Bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag: TagType): Element => {
  // ...
  return element;
}
```

```typescript
// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: TagType): Element => {
  // ...
  return element;
}

// Bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
const make = (tag: TagType): Element => {
  // ...
  return element;
}
```

* Use `/** ... */` for multi-line comments.

## Single line

> Single line

```javascript
// Good
// Is current tab
const active = true;


// Good
const getType = () => {
  console.log('fetching type...');

  // Set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};

// Good
const getType = () => {
  // Set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};

// Bad
const active = true;  // is current tab

// Bad
const getType = () => {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};

// Bad
const getType = () => {

  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
};
```

```javascript--flow
// Good
// Is current tab
const active: boolean = true;


// Good
const getType = (): string => {
  console.log('fetching type...');

  // Set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Good
const getType = (): string => {
  // Set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Bad
const active: boolean = true;  // is current tab

// Bad
const getType = (): string => {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Bad
const getType = (): string => {

  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};
```

```typescript
// Good
// Is current tab
const active: boolean = true;


// Good
const getType = (): string => {
  console.log('fetching type...');

  // Set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Good
const getType = (): string => {
  // Set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Bad
const active: boolean = true;  // is current tab

// Bad
const getType = (): string => {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type: string = this.type || 'no type';

  return type;
};

// Bad
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
// Good
// Is current tab
const active = true;

// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
};

// Bad
//is current tab
const active = true;

// Bad
/**
  *make() returns a new element
  *based on the passed-in tag name
  */
const make = (tag) => {
  // ...
  return element;
};
```

```javascript--flow
// Good
// is current tab
const active: boolean = true;

// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: string): Element => {
  // ...
  return element;
};

// Bad
//is current tab
const active: boolean = true;

// Bad
/**
  *make() returns a new element
  *based on the passed-in tag name
  */
const make = (tag: string): Element => {
  // ...
  return element;
};
```

```typescript
// Good
// is current tab
const active: boolean = true;

// Good
/**
  * make() returns a new element
  * based on the passed-in tag name
  */
const make = (tag: string): Element => {
  // ...
  return element;
};

// Bad
//is current tab
const active: boolean = true;

// Bad
/**
  *make() returns a new element
  *based on the passed-in tag name
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

```javascript--flow
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

```javascript--flow
class Calculator extends Abacus {
  private total: number;
  
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

> ESLint Rules

```json
{
  "spaced-comment": [
    "error",
    "always",
    {
      "exceptions": ["-", "+"]
    }
  ],
  "no-warning-comments": [
    "warn",
    {
      "terms": ["fixme", "todo"],
      "location": "anywhere"
    }
  ]
}
```
