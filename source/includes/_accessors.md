# Accessors

> Getters and setters

```javascript
// Good
class Dragon {
  getAge() {
    // ...
  }

  setAge(value) {
    // ...
  }
}

// Bad
class Dragon {
  get age() {
    // ...
  }

  set age(value) {
    // ...
  }
}
```

```javascript--flow
// Good
class Dragon {
  getAge() {
    // ...
  }

  setAge(value) {
    // ...
  }
}

// Bad
class Dragon {
  get age() {
    // ...
  }

  set age(value) {
    // ...
  }
}
```

```typescript
// Good
class Dragon {
  getAge() {
    // ...
  }

  setAge(value) {
    // ...
  }
}

// Bad
class Dragon {
  get age() {
    // ...
  }

  set age(value) {
    // ...
  }
}
```

> Boolean naming

```javascript
// Good
if(!dragon.hasAge()) {
  return false;
}

// Bad
if(!dragon.age()) {
  return false;
}
```

```javascript--flow
// Good
if(!dragon.hasAge()) {
  return false;
}

// Bad
if(!dragon.age()) {
  return false;
}
```

```typescript
// Good
if(!dragon.hasAge()) {
  return false;
}

// Bad
if(!dragon.age()) {
  return false;
}
```

> get() and set() functions

```javascript
class Jedi {
  constructor(options = {}) {
    const lightsaber = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  set(key, val) {
    this[key] = val;
  }

  get(key) {
    return this[key];
  }
}
```

```javascript--flow
class Jedi {
  constructor(options = {}) {
    const lightsaber: string = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  set(key: string, val: string): void {
    this[key] = val;
  }

  get(key: string): string {
    return this[key];
  }
}
```

```typescript
class Jedi {
  constructor(options = {}) {
    const lightsaber: string = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  set(key: string, val: string): void {
    this[key] = val;
  }

  get(key: string): string {
    return this[key];
  }
}
```

* Accessor functions for properties are not required.
* Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use `getVal()` and `setVal('hello')`.
* If the property/method is a boolean, use `isVal()` or `hasVal()`.
* It's okay to create `get()` and `set()` functions, but be consistent.
