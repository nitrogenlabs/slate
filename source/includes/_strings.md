#Strings

## Single Quotes

> Single quotes

```javascript
// Good
const name = 'Capt. Janeway';
const name = '<div class="test"/>';

// Bad
const name = "Capt. Janeway";
const name = "<div class=\"test\"/>";

// Bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;
```

```javascript--flow
// Good
const name: string = 'Capt. Janeway';
const name: string = '<div class="test"/>';

// Bad
const name: string = "Capt. Janeway";
const name: string = "<div class=\"test\"/>";

// Bad - template literals should contain interpolation or newlines
const name: string = `Capt. Janeway`;
```

```typescript
// Good
const name: string = 'Capt. Janeway';
const name: string = '<div class="test"/>';

// Bad
const name: string = "Capt. Janeway";
const name: string = "<div class=\"test\"/>";

// Bad - template literals should contain interpolation or newlines
const name: string = `Capt. Janeway`;
```

* Use single quotes '' for strings. 
* Maintains consistency. There are more scenarios in which a single quote must be escaped than a double. Best example is when using HTML elements.
* Single quotes is used in a wider range of Javascript projects. Double quotes are usually found in Java and C language strings.

> ESLint Rules

```json
{
  "quotes": ["error", "single"]
}
```

## Long strings

> Long strings

```javascript
// Good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// Bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// Bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';
```

```javascript--flow
// Good
const errorMessage: string = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// Bad
const errorMessage: string = 'This is a super long error that was thrown \
because of Batman. When you stop to think about how Batman had anything \
to do with this, you would get nowhere fast.';

// Bad
const errorMessage: string = 'This is a super long error that was thrown ' +
  'because of Batman. When you stop to think about how Batman had anything ' +
  'to do with this, you would get nowhere fast.';
```

```typescript
// Good
const errorMessage: string = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// Bad
const errorMessage: string = 'This is a super long error that was thrown \
because of Batman. When you stop to think about how Batman had anything \
to do with this, you would get nowhere fast.';

// Bad
const errorMessage: string = 'This is a super long error that was thrown ' +
  'because of Batman. When you stop to think about how Batman had anything ' +
  'to do with this, you would get nowhere fast.';
```

Strings that cause the line to go over 120 characters should not be written across multiple lines using string concatenation.

* Long strings are usually not logic so would not need to be a priority when reviewing code.
* Broken strings are painful to work with and make code less searchable.


## Template strings

> Template strings

```javascript
// Good
const sayHi = (name) => {
  return `How are you, ${name}?`;
}

// Bad
const sayHi = (name) => {
  return 'How are you, ' + name + '?';
}

// Bad
const sayHi = (name) => {
  return ['How are you, ', name, '?'].join();
}

// Bad
const sayHi = (name) => {
  return `How are you, ${ name }?`;
}
```

```javascript--flow
// Good
const sayHi: string = (name) => {
  return `How are you, ${name}?`;
}

// Bad
const sayHi: string = (name) => {
  return 'How are you, ' + name + '?';
}

// Bad
const sayHi: string = (name) => {
  return ['How are you, ', name, '?'].join();
}

// Bad
const sayHi: string = (name) => {
  return `How are you, ${ name }?`;
}
```

```typescript
// Good
const sayHi: string = (name) => {
  return `How are you, ${name}?`;
}

// Bad
const sayHi: string = (name) => {
  return 'How are you, ' + name + '?';
}

// Bad
const sayHi: string = (name) => {
  return ['How are you, ', name, '?'].join();
}

// Bad
const sayHi: string = (name) => {
  return `How are you, ${ name }?`;
}
```

* When programmatically building up strings, use template strings instead of concatenation.
* Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

> ESLint Rules

```json
{
  "prefer-template":  "error",
  "no-useless-concat": "error",
  "template-curly-spacing": ["error", "never"]
}
```

## eval

Never use eval() on a string, it opens too many vulnerabilities.

> ESLint Rules

```json
{
  "no-eval": "warn"
}
```

## Unnecessary escape characters

> Unnecessary escape characters

```javascript
// Good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;

// Bad
const foo = '\'this\' \i\s \"quoted\"';
```

```javascript--flow
// Good
const foo: string = '\'this\' is "quoted"';
const foo: string = `my name is '${name}'`;

// Bad
const foo: string = '\'this\' \i\s \"quoted\"';
```

```typescript
// Good
const foo: string = '\'this\' is "quoted"';
const foo: string = `my name is '${name}'`;

// Bad
const foo: string = '\'this\' \i\s \"quoted\"';
```

* Do not unnecessarily escape characters in strings.
* Backslashes harm readability, thus they should only be present when necessary.

> ESLint Rules

```json
{
  "no-useless-escape": "error"
}
```
