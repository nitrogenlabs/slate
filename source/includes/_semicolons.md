# Semicolons

> Semicolons

```javascript
// bad - raises exception
const luke = {}
const leia = {}
[luke, leia].forEach(jedi => jedi.father = 'vader')

// bad - raises exception
const reaction = 'No! That\'s impossible!'
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())

// bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
const foo = () => {
  return
    'search your feelings, you know it to be foo'
}

// good
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) => jedi.father = 'vader');

// good
const reaction = 'No! That\'s impossible!';
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// good
const foo = () => {
  return 'search your feelings, you know it to be foo';
}
```

```typescript
// bad - raises exception
const luke: JediType = {}
const leia: JediType = {}
[luke, leia].forEach((jedi: JediType) => jedi.father = 'vader')

// bad - raises exception
const reaction: string = 'No! That\'s impossible!'
(async () => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())

// bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
const foo = (): string => {
  return
    'search your feelings, you know it to be foo'
}

// good
const luke: JediType = {};
const leia: JediType = {};
[luke, leia].forEach((jedi: JediType) => jedi.father = 'vader');

// good
const reaction: string = 'No! That\'s impossible!';
(async (): void => {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// good
const foo = (): string => {
  return 'search your feelings, you know it to be foo';
}
```

* Use semicolons.
* When JavaScript encounters a line break without a semicolon, it uses a set of rules called Automatic Semicolon Insertion to determine whether or not it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. These rules will become more complicated as new features become a part of JavaScript. Explicitly terminating your statements and configuring your linter to catch missing semicolons will help prevent you from encountering issues.
* Don't let Automatic Semicolon Insertion determine your semicolons, place them yourself to avoid bugs.
* Bugs will also appear if concatenation of javascript files occur and/or minification.

### ESLint

`"semi": "error"`

`"semi-spacing": "error"`

`"no-extra-semi": "error"`

`"no-unexpected-multiline": "error"`

### TSLint

`"semicolon": [true, "always"]`

`"no-extra-semi": true`

`"no-unexpected-multiline": true`
