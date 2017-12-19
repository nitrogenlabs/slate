# Type Casting

Perform type coercion at the beginning of the statement.

## Strings

> Strings

```javascript
// => this.reviewScore = 9;

// bad
const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// bad
const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// bad
const totalScore = this.reviewScore.toString(); // isn't guaranteed to return a string

// good
const totalScore = String(this.reviewScore);
```

```typescript
// => this.reviewScore = 9;

// bad
const totalScore: string = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// bad
const totalScore: string = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// bad
const totalScore: string = this.reviewScore.toString(); // isn't guaranteed to return a string

// good
const totalScore: string = String(this.reviewScore);
```

* Use String for parsing strings.

### ESLint

`"no-new-wrappers": "error"`


## Numbers

> Numbers

```javascript
const inputValue = '4';

// bad
const val = new Number(inputValue);

// bad
const val = +inputValue;

// bad
const val = inputValue >> 0;

// bad
const val = parseInt(inputValue);

// good
const val = Number(inputValue);

// good
const val = parseInt(inputValue, 10);
```

```typescript
const inputValue: string = '4';

// bad
const val: number = new Number(inputValue);

// bad
const val: number = +inputValue;

// bad
const val: number = inputValue >> 0;

// bad
const val: number = parseInt(inputValue);

// good
const val: number = Number(inputValue);

// good
const val: number = parseInt(inputValue, 10);
```

* Use Number for type casting and parseInt always with a radix for parsing strings. 
* If for whatever reason you are doing something wild and parseInt is your bottleneck and need to use Bitshift for performance reasons, leave a comment explaining why and what you're doing.

### ESLint

`"radix no-new-wrappers"`

### TSLint

`"no-construct": true`


> Explaining bitshift

```javascript
// good
/**
* parseInt was the reason my code was slow.
* Bitshifting the String to coerce it to a
* Number made it a lot faster.
*/
const val = inputValue >> 0;
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

// bad
const hasAge = new Boolean(age);

// good
const hasAge = Boolean(age);

// best
const hasAge = !!age;
```

```typescript
const age: number = 0;

// bad
const hasAge: boolean = new Boolean(age);

// good
const hasAge: boolean = Boolean(age);

// best
const hasAge: boolean = !!age;
```

* Use Boolean for parsing strings.
* Use of 'not not' is better.

### ESLint

`"no-new-wrappers"`

### TSLint

`"no-construct": true`
