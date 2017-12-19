# Classes

## Prototype

> Always use class

```javascript
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

```typescript
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

* Always use class. Avoid manipulating prototype directly.
* Class syntax is more concise and easier to reason about.


## Inheritance

> Inheritance

```javascript
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};

// good
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}
```

```typescript
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};

// good
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}
```

* Use extends for inheritance.
* It is a built-in way to inherit prototype functionality without breaking instanceof.


## Return this

> Return this

```javascript
// bad
Jedi.prototype.jump = function() {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();
luke.jump().setHeight(20);
```

```typescript
// bad
Jedi.prototype.jump = function(): boolean {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function(height: number): void {
  this.height = height;
};

const luke: Jedi = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
  jump(): Jedi {
    this.jumping = true;
    return this;
  }

  setHeight(height: number): Jedi {
    this.height = height;
    return this;
  }
}

const luke: Jedi = new Jedi();
luke.jump().setHeight(20);
```

* Methods can return `this` to help with method chaining.


## Overriding methods

> Overriding methods

```javascript
class Jedi {
  constructor(options = {}) {
    this.name = options.name || 'no name';
  }

  getName() {
    return this.name;
  }

  toString() {
    return `Jedi - ${this.getName()}`;
  }
}
```

```typescript
class Jedi {
  constructor(options = {}) {
    this.name = options.name || 'no name';
  }

  getName() {
    return this.name;
  }

  toString() {
    return `Jedi - ${this.getName()}`;
  }
}
```

* It's okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.


## Empty constructors

> Empty constructors

```javascript
// bad
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}

// good
class Jedi {
  getName() {
    return this.name;
  }
}

// bad - No need to redefine the constructor if empty
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}

// good
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}
```

```typescript
// bad
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}

// good
class Jedi {
  getName() {
    return this.name;
  }
}

// bad - No need to redefine the constructor if empty
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}

// good
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}
```

* Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary. 

### ESLint
`"no-useless-constructor": "error"`


## Duplicates

> Duplicates

```javascript
// bad
class Foo {
  bar() {
    return 1;
  }

  bar() {
    return 2;
  }
}

// good
class Foo {
  foo() {
    return 1;
  }

  bar() {
    return 2;
  }
}
```

```typescript
// bad
class Foo {
  bar() {
    return 1;
  }

  bar() {
    return 2;
  }
}

// good
class Foo {
  foo() {
    return 1;
  }

  bar() {
    return 2;
  }
}
```

> No reassigning of classes

```javascript
// bad
class A { }
A = 0;

// bad
A = 0;
class A { }
```

```typescript
// bad
class A { }
A = 0;

// bad
A = 0;
class A { }
```

* Avoid duplicate class members.
* Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.
* Avoid modifying variables of class declarations.

### ESLint

`"no-dupe-class-members": "error"`

`"no-class-assign": "error"`
