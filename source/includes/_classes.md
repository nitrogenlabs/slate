# Classes

## Prototype

> Always use class

```javascript
// Good
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

// Bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};
```

```javascript--flow
// Good
class Queue {
  constructor(contents = []) {
    this.queue: string[] = [...contents];
  }
  pop(): string {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}

// Bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};
```

```typescript
// Good
class Queue {
  constructor(contents = []) {
    this.queue: string[] = [...contents];
  }
  pop(): string {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}

// Bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};
```

* Always use class. Avoid manipulating prototype directly.
* Class syntax is more concise and easier to reason about.


## Inheritance

> Inheritance

```javascript
// Good
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}

// Bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};
```

```javascript--flow
// Good
class PeekableQueue extends Queue {
  peek(): string {
    return this.queue[0];
  }
}

// Bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};
```

```typescript
// Good
class PeekableQueue extends Queue {
  peek(): string {
    return this.queue[0];
  }
}

// Bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};
```

* Use extends for inheritance.
* It is a built-in way to inherit prototype functionality without breaking instanceof.


## Return this

> Return this

```javascript
// Good
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

// Bad
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
```

```javascript--flow
// Good
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

// Bad
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
```

```typescript
// Good
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

// Bad
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

```javascript--flow
class Jedi {
  constructor(options = {}) {
    this.name = options.name || 'no name';
  }

  getName(): string {
    return this.name;
  }

  toString(): string {
    return `Jedi - ${this.getName()}`;
  }
}
```

```typescript
class Jedi {
  constructor(options = {}) {
    this.name = options.name || 'no name';
  }

  getName(): string {
    return this.name;
  }

  toString(): string {
    return `Jedi - ${this.getName()}`;
  }
}
```

* It's okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.

## Empty constructors

> Empty constructors

```javascript
// Good
class Jedi {
  getName() {
    return this.name;
  }
}

// Good
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}

// Bad
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}

// Bad - No need to redefine the constructor if empty
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}
```

```javascript--flow
// Good
class Jedi {
  getName() {
    return this.name;
  }
}

// Good
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}

// Bad
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}

// Bad - No need to redefine the constructor if empty
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}
```

```typescript
// Good
class Jedi {
  getName() {
    return this.name;
  }
}

// Good
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}

// Bad
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}

// Bad - No need to redefine the constructor if empty
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}
```

* Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary.

> ESLint Rules

```json
{
  "no-useless-constructor": "error"
}
```

## Duplicates

> Duplicates

```javascript
// Good
class Foo {
  foo() {
    return 1;
  }

  bar() {
    return 2;
  }
}

// Bad
class Foo {
  bar() {
    return 1;
  }

  bar() {
    return 2;
  }
}
```

```javascript--flow
// Good
class Foo {
  foo(): number {
    return 1;
  }

  bar(): number {
    return 2;
  }
}

// Bad
class Foo {
  bar(): number {
    return 1;
  }

  bar(): number {
    return 2;
  }
}
```

```typescript
// Good
class Foo {
  foo(): number {
    return 1;
  }

  bar(): number {
    return 2;
  }
}

// Bad
class Foo {
  bar(): number {
    return 1;
  }

  bar(): number {
    return 2;
  }
}
```

> No reassigning of classes

```javascript
// Bad
class A { }
A = 0;

// Bad
A = 0;
class A { }
```

```javascript--flow
// Bad
class A { }
A = 0;

// Bad
A = 0;
class A { }
```

```typescript
// Bad
class A { }
A = 0;

// Bad
A = 0;
class A { }
```

* Avoid duplicate class members.
* Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.
* Avoid modifying variables of class declarations.

> ESLint Rules

```json
{
  "no-class-assign": "error",
  "no-dupe-class-members": "error"
}
```
