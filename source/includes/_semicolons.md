# Semicolons

> Semicolons

```javascript
// Good
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) => jedi.father = 'vader');

// Good
const reaction = 'No! That\'s impossible!';
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// Good
const foo = () => {
  return 'search your feelings, you know it to be foo';
}

// Bad - raises exception
const luke = {}
const leia = {}
[luke, leia].forEach(jedi => jedi.father = 'vader')

// Bad - raises exception
const reaction = 'No! That\'s impossible!'
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())

// Bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
const foo = () => {
  return
    'search your feelings, you know it to be foo'
}
```

```javascript--flow
// Good
const luke: Jedi = {};
const leia: Jedi = {};
[luke, leia].forEach((jedi: Jedi) => jedi.father = 'vader');

// Good
const reaction: string = 'No! That\'s impossible!';
(async (): void => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// Good
const foo = (): string => {
  return 'search your feelings, you know it to be foo';
}

// Bad - raises exception
const luke: Jedi = {}
const leia: Jedi = {}
[luke, leia].forEach((jedi: Jedi) => jedi.father = 'vader')

// Bad - raises exception
const reaction: string = 'No! That\'s impossible!'
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())

// Bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
const foo = (): string => {
  return
    'search your feelings, you know it to be foo'
}
```

```typescript
// Good
const luke: Jedi = {};
const leia: Jedi = {};
[luke, leia].forEach((jedi: Jedi) => jedi.father = 'vader');

// Good
const reaction: string = 'No! That\'s impossible!';
(async (): void => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// Good
const foo = (): string => {
  return 'search your feelings, you know it to be foo';
}

// Bad - raises exception
const luke: Jedi = {}
const leia: Jedi = {}
[luke, leia].forEach((jedi: Jedi) => jedi.father = 'vader')

// Bad - raises exception
const reaction: string = 'No! That\'s impossible!'
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())

// Bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
const foo = (): string => {
  return
    'search your feelings, you know it to be foo'
}
```

* Use semicolons.
* When JavaScript encounters a line break without a semicolon, it uses a set of rules called Automatic Semicolon Insertion to determine whether or not it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. These rules will become more complicated as new features become a part of JavaScript. Explicitly terminating your statements and configuring your linter to catch missing semicolons will help prevent you from encountering issues.
* Don't let Automatic Semicolon Insertion determine your semicolons, place them yourself to avoid bugs.
* Bugs will also appear if concatenation of javascript files occur and/or minification.

> ESLint Rules

```json
{
  "semi": ["error", "always"],
  "semi-spacing": "error",
  "no-extra-semi": "error",
  "no-unexpected-multiline": "error"
}
```
