# Conditional Statements

## Maximum length

> Max length

```javascript
// bad
if((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// bad
if(foo === 123 &&
  bar === 'abc') {
  thing1();
}

// bad
if(foo === 123
  && bar === 'abc') {
  thing1();
}

// bad
if(
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}

// good
if(
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// good
if(
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// good
if(foo === 123 && bar === 'abc') {
  thing1();
}
```

```typescript
// bad
if((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// bad
if(foo === 123 &&
  bar === 'abc') {
  thing1();
}

// bad
if(foo === 123
  && bar === 'abc') {
  thing1();
}

// bad
if(
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}

// good
if(
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// good
if(
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// good
if(foo === 123 && bar === 'abc') {
  thing1();
}
```

* In case your control statement (if, while etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. 
* The logical operator should begin the line.
* Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.
