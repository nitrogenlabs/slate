# Blocks

## Brackets

> Brackets

```javascript
// bad
if(test)
  return false;

// bad
if(test) return false;

// good
if(test) {
  return false;
}

// bad
const foo = () => { return false; }

// good
const bar = () => {
  return false;
}
```

```typescript
// bad
if(test)
  return false;

// bad
if(test) return false;

// good
if(test) {
  return false;
}

// bad
const foo = () => { return false; }

// good
const bar = () => {
  return false;
}
```

* Use braces with all blocks. 
* All blocks should be multiline. This makes it easier to spot conditionals and nested functions when reviewing or adding to the block.

### ESLint
`"curly": "error"`

### TSLint
`"curly": true`


## Else

> Else if and else

```javascript
// bad
if(test) {
  thing1();
  thing2();
}
else if(another) {
  thing3();
}
else {
  thing4();
}

// good
if(test) {
  thing1();
  thing2();
} else if(another) {
  thing3();
} else {
  thing4();
}
```

```typescript
// bad
if(test) {
  thing1();
  thing2();
}
else if(another) {
  thing3();
}
else {
  thing4();
}

// good
if(test) {
  thing1();
  thing2();
} else if(another) {
  thing3();
} else {
  thing4();
}
```

* If using multiline blocks with `if`, `else if`, and `else`, put `else if` and `else` on the same line as your block's closing brace.

### ESLint
`"brace-style": ["error", "1tbs", {"allowSingleLine": false}]`

### TSLint
`"brace-style": [true, "1tbs", {"allowSingleLine": false}]`


## Return statement

> Return statement

```javascript
// bad
const foo = () => {
  if(x) {
    return x;
  } else {
    return y;
  }
};

// good
const foo = () => {
  if(x) {
    return x;
  }

  return y;
};

// bad
const cats () => {
  if(x) {
    return x;
  }

  if(y) {
    return y;
  }
};

// bad
const cats = () => {
  if(x) {
    return x;
  } else {
    if(y) {
      return y;
    }
  }
}

// good - consolidate if possible. Explicitly return null.
const cats = () => {
  if(x) {
    return x;
  } else if(y) {
    return y;
  }

  return null;
};

// bad
const dogs = (x) => {
  if(x) {
    if(z) {
      return y;
    }
  } else {
    return z;
  }
};

// good - combine condition if possible
const dogs = (x) => {
  if(x || z) {
    return y;
  }

  return z;
};
```

```typescript
// bad
const foo = (): string => {
  if(x) {
    return x;
  } else {
    return y;
  }
};

// good
const foo = (): string => {
  if(x) {
    return x;
  }

  return y;
};

// bad
const cats (): string => {
  if(x) {
    return x;
  }

  if(y) {
    return y;
  }
};

// bad
const cats = (): string => {
  if(x) {
    return x;
  } else {
    if(y) {
      return y;
    }
  }
}

// good - consolidate if possible. Explicitly return null.
const cats = (): string => {
  if(x) {
    return x;
  } else if(y) {
    return y;
  }

  return null;
};

// bad
const dogs = (x: string): string => {
  if(x) {
    if(z) {
      return y;
    }
  } else {
    return z;
  }
};

// good - combine condition if possible
const dogs = (x: string): string => {
  if(x || z) {
    return y;
  }

  return z;
};
```

* If an if block always executes a return statement, the subsequent else block is unnecessary.
* A return in an else if block following an if block that contains a return can be separated into multiple if blocks. 
* Always return. The end of a block should return a variable or null unless the block returns void. 

### ESLint
`"no-else-return": "error"`
