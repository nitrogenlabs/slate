# Type Casting

Perform type coercion at the beginning of the statement.

## Strings

> Strings

```javascript
// => this.reviewScore = 9;

// Good
const totalScore = String(this.reviewScore);

// Bad
const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// Bad
const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// Bad
const totalScore = this.reviewScore.toString(); // isn't guaranteed to return a string
```

```javascript--flow
// => this.reviewScore = 9;

// Good
const totalScore: string = String(this.reviewScore);

// Bad
const totalScore: string = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// Bad
const totalScore: string = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// Bad
const totalScore: string = this.reviewScore.toString(); // isn't guaranteed to return a string
```

```typescript
// => this.reviewScore = 9;

// Good
const totalScore: string = String(this.reviewScore);

// Bad
const totalScore: string = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// Bad
const totalScore: string = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// Bad
const totalScore: string = this.reviewScore.toString(); // isn't guaranteed to return a string
```

* Use String for parsing strings.

> ESLint Rules

```json
{
  "no-new-wrappers": "error"
}
```

## Numbers

> Numbers

```javascript
const inputValue = '4';

// Good
const val = Number(inputValue);

// Good
const val = parseInt(inputValue, 10);

// Bad
const val = new Number(inputValue);

// Bad
const val = +inputValue;

// Bad
const val = inputValue >> 0;

// Bad
const val = parseInt(inputValue);
```

```javascript--flow
const inputValue: string = '4';

// Good
const val: number = Number(inputValue);

// Good
const val: number = parseInt(inputValue, 10);

// Bad
const val: number = new Number(inputValue);

// Bad
const val: number = +inputValue;

// Bad
const val: number = inputValue >> 0;

// Bad
const val: number = parseInt(inputValue);
```

```typescript
const inputValue: string = '4';

// Good
const val: number = Number(inputValue);

// Good
const val: number = parseInt(inputValue, 10);

// Bad
const val: number = new Number(inputValue);

// Bad
const val: number = +inputValue;

// Bad
const val: number = inputValue >> 0;

// Bad
const val: number = parseInt(inputValue);
```

* Use Number for type casting and parseInt always with a radix for parsing strings. 
* If for whatever reason you are doing something wild and parseInt is your bottleneck and need to use Bitshift for performance reasons, leave a comment explaining why and what you're doing.

> ESLint Rules

```json
{
  "radix": ["error", "as-needed"]
}
```

> Explaining bitshift

```javascript
// Good
/**
* parseInt was the reason my code was slow.
* Bitshifting the String to coerce it to a
* Number made it a lot faster.
*/
const val = inputValue >> 0;
```

```javascript--flow
// Good
/**
* parseInt was the reason my code was slow.
* Bitshifting the String to coerce it to a
* Number made it a lot faster.
*/
const val: number = inputValue >> 0;
```

```typescript
// Good
/**
* parseInt was the reason my code was slow.
* Bitshifting the String to coerce it to a
* Number made it a lot faster.
*/
const val: number = inputValue >> 0;
```

<aside>
Note: Be careful when using bitshift operations. Numbers are represented as 64-bit values, but bitshift operations always return a 32-bit integer (source). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. Discussion. Largest signed 32-bit Int is 2,147,483,647:
2147483647 >> 0; // => 2147483647
2147483648 >> 0; // => -2147483648
2147483649 >> 0; // => -2147483647
</aside>

## Booleans

> Booleans

```javascript
const age = 0;

// Best
const hasAge = !!age;

// Good
const hasAge = Boolean(age);

// Bad
const hasAge = new Boolean(age);
```

```javascript--flow
const age: number = 0;

// Best
const hasAge: boolean = !!age;

// Good
const hasAge: boolean = Boolean(age);

// Bad
const hasAge: boolean = new Boolean(age);
```

```typescript
const age: number = 0;

// Best
const hasAge: boolean = !!age;

// Good
const hasAge: boolean = Boolean(age);

// Bad
const hasAge: boolean = new Boolean(age);
```

* Use Boolean for parsing strings.
* Use of 'not not' is better.

> ESLint Rules

```json
{
  "no-new-wrappers": "error"
}
```
