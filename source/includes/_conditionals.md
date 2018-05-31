# Conditional Statements

## Maximum length

> Max length

```javascript
// Good
if(
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// Good
if(
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// Good
if(foo === 123 && bar === 'abc') {
  thing1();
}

// Bad
if((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// Bad
if(foo === 123 &&
  bar === 'abc') {
  thing1();
}

// Bad
if(foo === 123
  && bar === 'abc') {
  thing1();
}

// Bad
if(
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}
```

```javascript--flow
// Good
if(
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// Good
if(
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// Good
if(foo === 123 && bar === 'abc') {
  thing1();
}

// Bad
if((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// Bad
if(foo === 123 &&
  bar === 'abc') {
  thing1();
}

// Bad
if(foo === 123
  && bar === 'abc') {
  thing1();
}

// Bad
if(
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}
```

```typescript
// Good
if(
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// Good
if(
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// Good
if(foo === 123 && bar === 'abc') {
  thing1();
}

// Bad
if((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// Bad
if(foo === 123 &&
  bar === 'abc') {
  thing1();
}

// Bad
if(foo === 123
  && bar === 'abc') {
  thing1();
}

// Bad
if(
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}
```

* In case your control statement (if, while etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line.
* The logical operator should begin the line.
* Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.
