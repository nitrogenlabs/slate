# Whitespace

## Tabs 

> Tabs

```javascript
// bad
const foo = () => {
∙∙∙∙let name;
}

// bad
const bar = () => {
∙let name;
}

// good
const baz = () => {
∙∙let name;
}
```

```typescript
// bad
const foo = () => {
∙∙∙∙let name: string;
}

// bad
const bar = () => {
∙let name: string;
}

// good
const baz = () => {
∙∙let name: string;
}
```

* Use soft tabs, space character instead of an actual tab.
* Set to 2 spaces. 
* This eases readability when reviewing code online and via diff clients.

### ESLint

`"indent": ["error", 2, {"SwitchCase": 1}]`

`"no-mixed-spaces-and-tabs": "error"`

### TSLint

`"indent": [true, "spaces", 2]`

`"ter-indent": [true, 2, {"SwitchCase": 1}]`


## Lines

> Lines

```javascript
// bad - more than 2 consecutive newline characters and more than 1 at the EOF
export class es6 {↵
  // ...↵
  ↵
  ↵
  ↵
  /// ...
}↵
↵
↵

// good
export class es6 {↵
  // ...↵
  ↵
  ↵
  /// ...
}↵
↵
```

```typescript
// bad - more than 2 consecutive newline characters and more than 1 at the EOF
export class es6 {↵
  // ...↵
  ↵
  ↵
  ↵
  /// ...
}↵
↵
↵

// good
export class es6 {↵
  // ...↵
  ↵
  ↵
  /// ...
}↵
↵
```

* Excess whitespace takes up more of the screen.
* Helps maintain a readable style in your codebase.

### ESLint

`"no-multiple-empty-lines": ["error", {"max": 2, "maxEOF": 1}]`

### TSLint

`"no-consecutive-blank-lines": [true, 2]`


## Trailing

> Trailing

``` javascript
// bad
let foo = 0;//•••••
let baz = 5;//••
//•••••

// good
let foo = 0;
let baz = 5;
```

``` typescript
// bad
let foo: number = 0;//•••••
let baz: number = 5;//••
//•••••

// good
let foo: number = 0;
let baz: number = 5;
```

* These white spaces offer no benefit.
* Can be picked up by source control systems and flagged as diffs, causing frustration for developers.

### ESLint

`"no-trailing-spaces": "error"`

### TSLint

`"no-trailing-whitespace": true`


## Leading brace

> Leading brace

```javascript
// bad
const test = ()=>{
  console.log('test');
}

// good
const test = () => {
  console.log('test');
}

// bad
if(isJedi){
  console.log('May the force be with you!');
}

// good
if(isJedi) {
  console.log('May the force be with you!');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

```typescript
// bad
const test = ()=>{
  console.log('test');
}

// good
const test = () => {
  console.log('test');
}

// bad
if(isJedi){
  console.log('test');
}

// good
if(isJedi) {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

* Place 1 space before the leading brace. 

### ESLint

`"space-before-blocks": ["error", "always"]`


## Opening parenthesis

> Opening parenthesis

```javascript
// bad
if(isJedi) {
  fight ();
}

// good
if (isJedi) {
  fight();
}

// bad
const fight =() => {
  console.log ('Swooosh!');
}

// good
const fight = () => {
  console.log('Swooosh!');
}
```

```typescript
// bad
if (isJedi) {
  fight ();
}

// good
if(isJedi) {
  fight();
}

// bad
const fight =() => {
  console.log ('Swooosh!');
}

// good
const fight = () => {
  console.log('Swooosh!');
}
```

* No spaces before the opening parenthesis.
* This rule will maintain consistency through all scenarios including control statements (if, while etc.), functional calls, and argument lists.
* Our philosophy is to not have exceptions. All rules should maintain consistency throughout the code. If no space before an opening parenthesis and function call, then no space between control statement and opening parenthesis.

### ESLint
`"keyword-spacing": ["error", {"before": true}]`


## Operators

> Operators

```javascript
// bad
const x=y+5;

// good
const x = y + 5;
```

```typescript
// bad
const x: number=y+5;

// good
const x: number = y + 5;
```

* Set off operators with spaces. 

### ESLint
`"space-infix-ops": "error"`


## EOF

> End files with newline character

```javascript
// bad - no newline character at the end
export class es6 {↵
  // ...↵
}

// bad - more than a single newline character
export class es6 {↵
  // ...↵
}↵
↵

// good a single newline character at the end
export class es6 {↵
  // ...↵
}↵
```

```typescript
// bad - no newline character at the end
export class es6 {↵
  // ...↵
}

// bad - more than a single newline character
export class es6 {↵
  // ...↵
}↵
↵

// good a single newline character at the end
export class es6 {↵
  // ...↵
}↵
```

* End files with a single newline character. 

### ESLint
`"eol-last": ["error", "always"]`

### TSLint

`"eofline": true`


## Long chains

> Long chains

```javascript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led')
  .data(data)
  .enter()
  .append('svg:svg')
  .classed('led', true)
  .attr('width', (radius + margin) * 2)
  .append('svg:g')
  .attr('transform', `translate(${radius + margin},${radius + margin})`)
  .call(tron.led);

// good
const leds = stage.selectAll('.led').data(data);
```

```typescript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led')
  .data(data)
  .enter()
  .append('svg:svg')
  .classed('led', true)
  .attr('width', (radius + margin) * 2)
  .append('svg:g')
  .attr('transform', `translate(${radius + margin},${radius + margin})`)
  .call(tron.led);

// good
const leds = stage.selectAll('.led').data(data);
```

* Use indentation when using a method chain with more than 2. 
* Use a leading dot, which emphasizes that the line is a method call, not a new statement. 

### ESLint

`"newline-per-chained-call": ["error", { "ignoreChainWithDepth": 2 }]`

`"no-whitespace-before-property": "error"`


## Block statements

> Block statements

```javascript
// bad
const isJedi = true;
if(isJedi) {
  return bar;
}
return baz;

// good
const isJedi = true;

if(isJedi) {
  return bar;
}

return baz;

// bad
const obj = {
  foo() {
  },
  bar() {
  },
};
return obj;

// good
const obj = {
  foo() {
  },

  bar() {
  },
};

return obj;
```

```typescript
// bad
const isJedi: boolean = true;
if(isJedi) {
  return bar;
}
return baz;

// good
const isJedi: boolean = true;

if(isJedi) {
  return bar;
}

return baz;

// bad
class obj {
  foo() {
  },
  bar() {
  },
}
export obj;

// good
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
// bad
const bar = () => {

  console.log(foo);

}

// bad
if(baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// bad
class Foo {

  constructor(bar) {
    console.log(bar);
  }
}

// good
const bar = () => {
  console.log(foo);
}

// good
if(baz) {
  console.log(qux);
} else {
  console.log(foo);
}

// good
class Foo {
  constructor(bar) {
    console.log(bar);
  }
}
```

```typescript
// bad
const bar = () => {

  console.log(foo);

}

// bad
if(baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// bad
class Foo {

  constructor(bar) {
    console.log(bar);
  }
}

// good
const bar = () => {
  console.log(foo);
}

// good
if(baz) {
  console.log(qux);
} else {
  console.log(foo);
}

// good
class Foo {
  constructor(bar) {
    console.log(bar);
  }
}
```

* Do not pad your blocks with blank lines. 

### ESLint
`"padded-blocks": ["error", "never"]`


## Parentheses spacing

> Parentheses spacing

```javascript
// bad
const bar = ( foo ) => {
  return foo;
}

// good
const bar = (foo) => {
  return foo;
}

// bad
if( isJedi ) {
  console.log(isJedi);
}

// good
if(isJedi) {
  console.log(isJedi);
}
```

```typescript
// bad
const bar = ( foo: string ) => {
  return foo;
}

// good
const bar = (foo: string) => {
  return foo;
}

// bad
if( isJedi ) {
  console.log( isJedi );
}

// good
if(isJedi) {
  console.log(isJedi);
}
```

* Do not add spaces inside parentheses. 

### ESLint

`"space-in-parens": ["error", "never"]`


## Bracket spaces

> Bracket spaces

```javascript
// bad
const foo = [ 1, 2, 3 ];
console.log(foo[ 0 ]);

// good
const foo = [1, 2, 3];
console.log(foo[0]);
```

```typescript
// bad
const foo: number[] = [ 1, 2, 3 ];
console.log(foo[ 0 ]);

// good
const foo: number[] = [1, 2, 3];
console.log(foo[0]);
```

* Do not add spaces inside brackets. 

### ESLint

`"array-bracket-spacing": ["error", "never"]`

`"computed-property-spacing": ["error", "never"]`

### TSLint

`"array-bracket-spacing": [true, "never"]`

`"ter-computed-property-spacing": [true, "never"]`


## Curly braces

> Curly braces

```javascript
// bad
const foo = { clark: 'kent' };

// good
const foo = {clark: 'kent'};
```

```typescript
// bad
const foo: object = { clark: 'kent' };

// good
const foo: object = {clark: 'kent'};
```

* Do not add spaces inside curly braces.

### ESLint

`"object-curly-spacing"`

### TSLint

`"object-curly-spacing": [true, "never"]`


## Long lines

> Long lines

```javascript
// bad
const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// bad
ApiUtils.ajax({ method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

// good
const foo = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// good
ApiUtils.ajax({
  method: 'POST',
  url: 'https://nitrogenlabs.com/',
  data: { name: 'John' }
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// better - consolidate lines if fit
ApiUtils.ajax({method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' }})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));
```

```typescript
// bad
const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// bad
ApiUtils.ajax({ method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

// good
const foo = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// good
ApiUtils.ajax({
  method: 'POST',
  url: 'https://nitrogenlabs.com/',
  data: { name: 'John' }
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));

// better - consolidate lines if fit
ApiUtils.ajax({method: 'POST', url: 'https://nitrogenlabs.com/', data: { name: 'John' }})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));
```

* Avoid having lines of code that are longer than 120 characters (including whitespace).
* Do not breakdown to multiline if not necessary.
* This ensures readability and maintainability.
* Long lines may be unseen when reviewing code and can be easily overseen.
* Eliminates the need to scroll horizontally when reviewing code in editors and online clients (ie. GitHub).

### ESLint
`"max-len": ["error", {"code": 120, "ignoreRegExpLiterals": true, "ignoreStrings": true, "ignoreTemplateLiterals": true, "ignoreUrls": true, "tabWidth": 2}]`

### TSLint

`"ter-max-len": [true, {"code": 120, "ignoreRegExpLiterals": true, "ignoreStrings": true, "ignoreTemplateLiterals": true,"ignoreUrls": true, "tabWidth": 2}]`


## Block

```javascript
// bad
const f = function(){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

```typescript
// bad
const f = (){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

* Spacing in a function signature. 
* Maintain consistency.

### ESLint
`"space-before-function-paren": ["error", "never"]`

`"space-before-blocks": ["error", "always"]`

### TSLint

`"whitespace": [true, "check-decl", "check-operator", "check-preblock", "check-type", "check-typecast", "check-separator"]`


## Multiline signatures

```javascript
// bad
const foo = (bar,
              baz,
              quux) => {
  // ...
}

// good
const foo = (
  bar,
  baz,
  quux,
) => {
  // ...
}

// bad
console.log(foo,
  bar,
  baz);

// good
console.log(
  foo,
  bar,
  baz,
);
```

```typescript
// bad
const foo = (bar,
              baz,
              quux) => {
  // ...
}

// good
const foo = (
  bar,
  baz,
  quux,
) => {
  // ...
}

// bad
console.log(foo,
  bar,
  baz);

// good
console.log(
  foo,
  bar,
  baz,
);
```

* Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item.

### TSLint

`"align": [true, "elements", "members"]`
