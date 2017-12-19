#Strings

## Single Quotes

> Single quotes

```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// bad
const name = "<div class=\"test\"/>";

// good
const name = 'Capt. Janeway';

// good
const name = '<div class="test"/>';
```

```typescript
// bad
const name: string = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name: string = `Capt. Janeway`;

// bad
const name: string = "<div class=\"test\"/>";

// good
const name: string = 'Capt. Janeway';

// good
const name: string = '<div class="test"/>';
```

* Use single quotes '' for strings. 
* Maintains consistency. There are more scenarios in which a single quote must be escaped than a double. Best example is when using HTML elements.
* Single quotes is used in a wider range of Javascript projects. Double quotes are usually found in Java and C language strings.

### ESLint

`"quotes": ["error", "single"]`

### TSLint

`"quotemark": [true, "single", "jsx-double", "avoid-template"]`


## Long strings

> Long strings

```javascript
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

```typescript
// bad
const errorMessage: string = 'This is a super long error that was thrown \
because of Batman. When you stop to think about how Batman had anything \
to do with this, you would get nowhere fast.';

// bad
const errorMessage: string = 'This is a super long error that was thrown ' +
  'because of Batman. When you stop to think about how Batman had anything ' +
  'to do with this, you would get nowhere fast.';

// good
const errorMessage: string = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

Strings that cause the line to go over 120 characters should not be written across multiple lines using string concatenation.

* Long strings are usually not logic so would not need to be a priority when reviewing code.
* Broken strings are painful to work with and make code less searchable.


## Template strings

> Template strings

```javascript
// bad
const sayHi = (name) => {
  return 'How are you, ' + name + '?';
}

// bad
const sayHi = (name) => {
  return ['How are you, ', name, '?'].join();
}

// bad
const sayHi = (name) => {
  return `How are you, ${ name }?`;
}

// good
const sayHi = (name) => {
  return `How are you, ${name}?`;
}
```

```typescript
// bad
const sayHi: string = (name) => {
  return 'How are you, ' + name + '?';
}

// bad
const sayHi: string = (name) => {
  return ['How are you, ', name, '?'].join();
}

// bad
const sayHi: string = (name) => {
  return `How are you, ${ name }?`;
}

// good
const sayHi: string = (name) => {
  return `How are you, ${name}?`;
}
```

* When programmatically building up strings, use template strings instead of concatenation.
* Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

### ESLint

`"prefer-template":  "error"`

`"no-useless-concat": "error"`

`"template-curly-spacing": "error"`


## eval
Never use eval() on a string, it opens too many vulnerabilities.

### ESLint

`"no-eval": "error"`

### TSLint

`"no-eval": true`


## Unnecessary escape characters

> Unnecessary escape characters

```javascript
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

```typescript
// bad
const foo: string = '\'this\' \i\s \"quoted\"';

// good
const foo: string = '\'this\' is "quoted"';
const foo: string = `my name is '${name}'`;
```

* Do not unnecessarily escape characters in strings.
* Backslashes harm readability, thus they should only be present when necessary.

### ESLint

`"no-useless-escape": "error"`
