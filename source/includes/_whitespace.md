# Whitespace

## Tabs 

> Tabs

```javascript
// Good
const baz = () => {
∙∙let name;
}

// Bad
const foo = () => {
∙∙∙∙let name;
}

// Bad
const bar = () => {
∙let name;
}
```

```javascript--flow
// Good
const baz = () => {
∙∙let name: string;
}

// Bad
const foo = () => {
∙∙∙∙let name: string;
}

// Bad
const bar = () => {
∙let name: string;
}
```

```typescript
// Good
const baz = () => {
∙∙let name: string;
}

// Bad
const foo = () => {
∙∙∙∙let name: string;
}

// Bad
const bar = () => {
∙let name: string;
}
```

* Use soft tabs, space character instead of an actual tab.
* Set to 2 spaces.
* This eases readability when reviewing code online and via diff clients.

> ESLint Rules

```json
{
  "indent": ["error", 2, {"SwitchCase": 1}],
  "no-mixed-spaces-and-tabs": "error"
}
```

## Lines

> Lines

```javascript
// Good
export class es6 {↵
  // ...↵
  ↵
  ↵
  /// ...
}↵
↵

// Bad - more than 2 consecutive newline characters and more than 1 at the EOF
export class es6 {↵
  // ...↵
  ↵
  ↵
  ↵
  /// ...
}↵
↵
↵
```

```javascript-flow
// Good
export class es6 {↵
  // ...↵
  ↵
  ↵
  /// ...
}↵
↵

// Bad - more than 2 consecutive newline characters and more than 1 at the EOF
export class es6 {↵
  // ...↵
  ↵
  ↵
  ↵
  /// ...
}↵
↵
↵
```

```typescript
// Good
export class es6 {↵
  // ...↵
  ↵
  ↵
  /// ...
}↵
↵

// Bad - more than 2 consecutive newline characters and more than 1 at the EOF
export class es6 {↵
  // ...↵
  ↵
  ↵
  ↵
  /// ...
}↵
↵
↵
```

* Excess whitespace takes up more of the screen.
* Helps maintain a readable style in your codebase.

> ESLint Rules

```json
{
  "no-multiple-empty-lines": [
    "error",
    {"max": 2, "maxEOF": 1}
  ]
}
```

## Trailing

> Trailing

```javascript
// Good
let foo = 0;
let baz = 5;

// Bad
let foo = 0;//•••••
let baz = 5;//••
//•••••
```

```javascript--flow
// Good
let foo: number = 0;
let baz: number = 5;

// Bad
let foo: number = 0;//•••••
let baz: number = 5;//••
//•••••
```

```typescript
// Good
let foo: number = 0;
let baz: number = 5;

// Bad
let foo: number = 0;//•••••
let baz: number = 5;//••
//•••••
```

* These white spaces offer no benefit.
* Can be picked up by source control systems and flagged as diffs, causing frustration for developers.

> ESLint Rules

```json
{
  "no-trailing-spaces": "error"
}
```

## Leading brace

> Leading brace

```javascript
// Good
const test = () => {
  console.log('test');
}

// Good
if(isJedi) {
  console.log('May the force be with you!');
}

// Good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// Bad
const test = ()=>{
  console.log('test');
}

// Bad
if(isJedi){
  console.log('May the force be with you!');
}

// Bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

```javascript--flow
// Good
const test = () => {
  console.log('test');
}

// Good
if(isJedi) {
  console.log('test');
}

// Good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// Bad
const test = ()=>{
  console.log('test');
}

// Bad
if(isJedi){
  console.log('test');
}

// Bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

```typescript
// Good
const test = () => {
  console.log('test');
}

// Good
if(isJedi) {
  console.log('test');
}

// Good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// Bad
const test = ()=>{
  console.log('test');
}

// Bad
if(isJedi){
  console.log('test');
}

// Bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

* Place 1 space before the leading brace.

> ESLint Rules

```json
{
  "space-before-blocks": ["error", "always"]
}
```


## Opening parenthesis

> Opening parenthesis

```javascript
// Good
if (isJedi) {
  fight();
}

// Good
const fight = () => {
  console.log('Swooosh!');
}

// Bad
if(isJedi) {
  fight ();
}

// Bad
const fight =() => {
  console.log ('Swooosh!');
}
```

```javascript--flow
// Good
if(isJedi) {
  fight();
}

// Good
const fight = () => {
  console.log('Swooosh!');
}

// Bad
if (isJedi) {
  fight ();
}

// Bad
const fight =() => {
  console.log ('Swooosh!');
}
```

```typescript
// Good
if(isJedi) {
  fight();
}

// Good
const fight = () => {
  console.log('Swooosh!');
}

// Bad
if (isJedi) {
  fight ();
}

// Bad
const fight =() => {
  console.log ('Swooosh!');
}
```

* No spaces before the opening parenthesis.
* This rule will maintain consistency through all scenarios including control statements (if, while etc.), functional calls, and argument lists.
* Our philosophy is to not have exceptions. All rules should maintain consistency throughout the code. If no space before an opening parenthesis and function call, then no space between control statement and opening parenthesis.

> ESLint Rules
```json
{
  "keyword-spacing": [
    "error", 
    {
      "overrides": {
        "if": {
          "after": false
        },
        "for": {
          "after": false
        },
        "while": {
          "after": false
        },
        "switch": {
          "after": false
        },
        "catch": {
          "after": false
        }
      }
    }
  ]
}
```

## Operators

> Operators

```javascript
// Good
const x = y + 5;

// Bad
const x=y+5;
```

```javascript--flow
// Good
const x: number = y + 5;

// Bad
const x: number=y+5;
```

```typescript
// Good
const x: number = y + 5;

// Bad
const x: number=y+5;
```

* Set off operators with spaces.

> ESLint Rules

```json
{
  "space-infix-ops": "error"
}
```

## EOF

> End files with newline character

```javascript
// Good a single newline character at the end
export class es6 {↵
  // ...↵
}↵

// Bad - no newline character at the end
export class es6 {↵
  // ...↵
}

// Bad - more than a single newline character
export class es6 {↵
  // ...↵
}↵
↵
```

```javascript--flow
// Good a single newline character at the end
export class es6 {↵
  // ...↵
}↵

// Bad - no newline character at the end
export class es6 {↵
  // ...↵
}

// Bad - more than a single newline character
export class es6 {↵
  // ...↵
}↵
↵
```

```typescript
// Good a single newline character at the end
export class es6 {↵
  // ...↵
}↵

// Bad - no newline character at the end
export class es6 {↵
  // ...↵
}

// Bad - more than a single newline character
export class es6 {↵
  // ...↵
}↵
↵
```

* End files with a single newline character.

> ESLint Rules

```json
{
  "eol-last": ["error", "always"]
}
```

## Long chains

> Long chains

```javascript
// Good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// Good
const leds = stage.selectAll('.led')
  .data(data)
  .enter()
  .append('svg:svg')
  .classed('led', true)
  .attr('width', (radius + margin) * 2)
  .append('svg:g')
  .attr('transform', `translate(${radius + margin},${radius + margin})`)
  .call(tron.led);

// Good
const leds = stage.selectAll('.led').data(data);

// Bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// Bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// Bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);
```

```javascript--flow
// Good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// Good
const leds = stage.selectAll('.led')
  .data(data)
  .enter()
  .append('svg:svg')
  .classed('led', true)
  .attr('width', (radius + margin) * 2)
  .append('svg:g')
  .attr('transform', `translate(${radius + margin},${radius + margin})`)
  .call(tron.led);

// Good
const leds = stage.selectAll('.led').data(data);

// Bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// Bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// Bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);
```

```typescript
// Good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// Good
const leds = stage.selectAll('.led')
  .data(data)
  .enter()
  .append('svg:svg')
  .classed('led', true)
  .attr('width', (radius + margin) * 2)
  .append('svg:g')
  .attr('transform', `translate(${radius + margin},${radius + margin})`)
  .call(tron.led);

// Good
const leds = stage.selectAll('.led').data(data);

// Bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// Bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// Bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);
```

* Use indentation when using a method chain with more than 2.
* Use a leading dot, which emphasizes that the line is a method call, not a new statement.

> ESLint Rules

```json
{
  "newline-per-chained-call": [
    "error",
    {"ignoreChainWithDepth": 2 }
  ],
  "no-whitespace-before-property": "error"
}
```

## Block statements

> Block statements

```javascript
// Good
const isJedi = true;

if(isJedi) {
  return bar;
}

return baz;

// Good
const obj = {
  foo() {
  },

  bar() {
  }
};

return obj;

// Bad
const isJedi = true;
if(isJedi) {
  return bar;
}
return baz;

// Bad
const obj = {
  foo() {
  },
  bar() {
  },
};
return obj;
```

```javascript--flow
// Good
const isJedi: boolean = true;

if(isJedi) {
  return bar;
}

return baz;

// Good
class obj {
  foo() {
  },

  bar() {
  }
}

export obj;

// Bad
const isJedi: boolean = true;
if(isJedi) {
  return bar;
}
return baz;

// Bad
class obj {
  foo() {
  },
  bar() {
  },
}
export obj;
```

```typescript
// Good
const isJedi: boolean = true;

if(isJedi) {
  return bar;
}

return baz;

// Good
class obj {
  foo() {
  },

  bar() {
  }
}

export obj;

// Bad
const isJedi: boolean = true;
if(isJedi) {
  return bar;
}
return baz;

// Bad
class obj {
  foo() {
  },
  bar() {
  },
}
export obj;
```

* A blank line should come before a block statement. This makes it easier to spot conditionals and nested functions.
* Leave a blank line after blocks and before the next statement.

## Padding Blocks

> Padding

```javascript
// Good
const bar = () => {
  console.log(foo);
}

// Good
if(baz) {
  console.log(qux);
} else {
  console.log(foo);
}

// Good
class Foo {
  constructor(bar) {
    console.log(bar);
  }
}

// Bad
const bar = () => {

  console.log(foo);

}

// Bad
if(baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// Bad
class Foo {

  constructor(bar) {
    console.log(bar);
  }
}
```

```javascript--flow
// Good
const bar = () => {
  console.log(foo);
}

// Good
if(baz) {
  console.log(qux);
} else {
  console.log(foo);
}

// Good
class Foo {
  constructor(bar) {
    console.log(bar);
  }
}

// Bad
const bar = () => {

  console.log(foo);

}

// Bad
if(baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// Bad
class Foo {

  constructor(bar) {
    console.log(bar);
  }
}
```

```typescript
// Good
const bar = () => {
  console.log(foo);
}

// Good
if(baz) {
  console.log(qux);
} else {
  console.log(foo);
}

// Good
class Foo {
  constructor(bar) {
    console.log(bar);
  }
}

// Bad
const bar = () => {

  console.log(foo);

}

// Bad
if(baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// Bad
class Foo {

  constructor(bar) {
    console.log(bar);
  }
}
```

* Do not pad your blocks with blank lines.

> ESLint Rules

```json
{
  "padded-blocks": ["error", "never"]
}
```

## Parentheses spacing

> Parentheses spacing

```javascript
// Good
const bar = (foo) => {
  return foo;
}

// Bad
const bar = ( foo ) => {
  return foo;
}

// Good
if(isJedi) {
  console.log(isJedi);
}

// Bad
if( isJedi ) {
  console.log(isJedi);
}
```

```javascript--flow
// Good
const bar = (foo: string): string => {
  return foo;
}

// Good
if(isJedi) {
  console.log(isJedi);
}

// Bad
const bar = ( foo: string ): string => {
  return foo;
}

// Bad
if( isJedi ) {
  console.log( isJedi );
}
```

```typescript
// Good
const bar = (foo: string): string => {
  return foo;
}

// Good
if(isJedi) {
  console.log(isJedi);
}

// Bad
const bar = ( foo: string ): string => {
  return foo;
}

// Bad
if( isJedi ) {
  console.log( isJedi );
}
```

* Do not add spaces inside parentheses. 

> ESLint Rules

```json
{
  "space-in-parens": ["error", "never"]
}
```

## Bracket spaces

> Bracket spaces

```javascript
// Good
const foo = [1, 2, 3];
console.log(foo[0]);

// Bad
const foo = [ 1, 2, 3 ];
console.log(foo[ 0 ]);
```

```javascript--flow
// Good
const foo: number[] = [1, 2, 3];
console.log(foo[0]);

// Bad
const foo: number[] = [ 1, 2, 3 ];
console.log(foo[ 0 ]);
```

```typescript
// Good
const foo: number[] = [1, 2, 3];
console.log(foo[0]);

// Bad
const foo: number[] = [ 1, 2, 3 ];
console.log(foo[ 0 ]);
```

* Do not add spaces inside brackets.

> ESLint Rules

```json
{
  "array-bracket-spacing": ["error", "never"],
  "computed-property-spacing": ["error", "never"]
}
```

## Curly braces

> Curly braces

```javascript
// Good
const foo = {clark: 'kent'};

// Bad
const foo = { clark: 'kent' };
```

```typescript
// Good
const foo: object = {clark: 'kent'};

// Bad
const foo: object = { clark: 'kent' };
```

* Do not add spaces inside curly braces.

> ESLint Rules

```json
{
  "object-curly-spacing": ["error", "never"]
}
```

## Long lines

> Long lines

```javascript
// Best - consolidate lines if fit
ApiUtils.ajax({method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' }})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Good
const foo = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// Good
ApiUtils.ajax({
  method: 'POST',
  url: 'https://nitrogenlabs.com/',
  data: { name: 'John' }
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Bad
const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// Bad
ApiUtils.ajax({ method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));
```

```javascript--flow
// Best - consolidate lines if fit
ApiUtils.ajax({method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' }})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Good
const foo: boolean = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// Good
ApiUtils.ajax({
  method: 'POST',
  url: 'https://nitrogenlabs.com/',
  data: { name: 'John' }
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Bad
const foo: boolean = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// Bad
ApiUtils.ajax({ method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));
```

```typescript
// Best - consolidate lines if fit
ApiUtils.ajax({method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' }})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Good
const foo: boolean = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// Good
ApiUtils.ajax({
  method: 'POST',
  url: 'https://nitrogenlabs.com/',
  data: { name: 'John' }
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// Bad
const foo: boolean = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// Bad
ApiUtils.ajax({ method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));
```

* Avoid having lines of code that are longer than 120 characters (including whitespace).
* Do not breakdown to multiline if not necessary.
* This ensures readability and maintainability.
* Long lines may be unseen when reviewing code and can be easily overseen.
* Eliminates the need to scroll horizontally when reviewing code in editors and online clients (ie. GitHub).

> ESLint Rules

```json
{
  "max-len": [
    "error", {
      "code": 120,
      "ignoreRegExpLiterals": true,
      "ignoreStrings": true,
      "ignoreTemplateLiterals": true,
      "ignoreUrls": true,
      "tabWidth": 2
    }
  ]
}
```

## Block

```javascript
// Good
const x = function () {};
const y = function a() {};

// Bad
const f = function(){};
const g = function (){};
const h = function() {};
```

```typescript
// Good
const x = function () {};
const y = function a() {};

// Bad
const f = (){};
const g = function (){};
const h = function() {};
```

* Spacing in a function signature.
* Maintain consistency.

> ESLint Rules

```json
{
  "space-before-function-paren": [
    "error",
    {
      "anonymous": "never",
      "asyncArrow": "always",
      "named": "never",
    }
  ],
  "space-before-blocks": ["error", "always"]
}
```

## Multiline signatures

```javascript
// Good
const foo = (
  bar,
  baz,
  quux
) => {
  // ...
}

// Good
console.log(
  foo,
  bar,
  baz
);

// Bad
const foo = (bar,
              baz,
              quux) => {
  // ...
}

// Bad
console.log(foo,
  bar,
  baz);
```

```javascript--flow
// Good
const foo = (
  bar,
  baz,
  quux
) => {
  // ...
}

// Good
console.log(
  foo,
  bar,
  baz
);

// Bad
const foo = (bar,
              baz,
              quux) => {
  // ...
}

// Bad
console.log(foo,
  bar,
  baz);
```

```typescript
// Good
const foo = (
  bar,
  baz,
  quux
) => {
  // ...
}

// Good
console.log(
  foo,
  bar,
  baz
);

// Bad
const foo = (bar,
              baz,
              quux) => {
  // ...
}

// Bad
console.log(foo,
  bar,
  baz);
```

* Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item.
