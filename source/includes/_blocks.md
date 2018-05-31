# Blocks

## Brackets

> Brackets

```javascript
// Good
if(test) {
  return false;
}

// Good
const bar = () => {
  return false;
}

// Bad
if(test)
  return false;

// Bad
if(test) return false;

// Bad
const foo = () => { return false; }
```

```javascript--flow
// Good
if(test) {
  return false;
}

// Good
const bar = () => {
  return false;
}

// Bad
if(test)
  return false;

// Bad
if(test) return false;

// Bad
const foo = () => { return false; }
```

```typescript
// Good
if(test) {
  return false;
}

// Good
const bar = () => {
  return false;
}

// Bad
if(test)
  return false;

// Bad
if(test) return false;

// Bad
const foo = () => { return false; }
```

* Use braces with all blocks.
* All blocks should be multiline. This makes it easier to spot conditionals and nested functions when reviewing or adding to the block.

> ESLint Rules

```json
{
  "curly": "error"
}
```

## Else

> Else if and else

```javascript
// Good
if(test) {
  thing1();
  thing2();
} else if(another) {
  thing3();
} else {
  thing4();
}

// Bad
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
```

```javascript--flow
// Good
if(test) {
  thing1();
  thing2();
} else if(another) {
  thing3();
} else {
  thing4();
}

// Bad
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
```

```typescript
// Good
if(test) {
  thing1();
  thing2();
} else if(another) {
  thing3();
} else {
  thing4();
}

// Bad
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
```

* If using multiline blocks with `if`, `else if`, and `else`, put `else if` and `else` on the same line as your block's closing brace.

> ESLint Rules

```json
{
  "brace-style": [
    "error",
    "1tbs",
    {
      "allowSingleLine": false
    }
  ]
}
```

## Return statement

> Return statement

```javascript
// Good
const foo = () => {
  if(x) {
    return x;
  }

  return y;
};

// Good - consolidate if possible. Explicitly return null.
const cats = () => {
  if(x) {
    return x;
  } else if(y) {
    return y;
  }

  return null;
};

// Good - combine condition if possible
const dogs = (x) => {
  if(x || z) {
    return y;
  }

  return z;
};

// Bad
const foo = () => {
  if(x) {
    return x;
  } else {
    return y;
  }
};

// Bad
const cats () => {
  if(x) {
    return x;
  }

  if(y) {
    return y;
  }
};

// Bad
const cats = () => {
  if(x) {
    return x;
  } else {
    if(y) {
      return y;
    }
  }
}

// Bad
const dogs = (x) => {
  if(x) {
    if(z) {
      return y;
    }
  } else {
    return z;
  }
};
```

```javascript--flow
// Good
const foo = (): string => {
  if(x) {
    return x;
  }

  return y;
};

// Good - consolidate if possible. Explicitly return null.
const cats = (): string => {
  if(x) {
    return x;
  } else if(y) {
    return y;
  }

  return null;
};

// Good - combine condition if possible
const dogs = (x: string): string => {
  if(x || z) {
    return y;
  }

  return z;
};

// Bad
const foo = (): string => {
  if(x) {
    return x;
  } else {
    return y;
  }
};

// Bad
const cats (): string => {
  if(x) {
    return x;
  }

  if(y) {
    return y;
  }
};

// Bad
const cats = (): string => {
  if(x) {
    return x;
  } else {
    if(y) {
      return y;
    }
  }
}

// Bad
const dogs = (x: string): string => {
  if(x) {
    if(z) {
      return y;
    }
  } else {
    return z;
  }
};
```

```typescript
// Good
const foo = (): string => {
  if(x) {
    return x;
  }

  return y;
};

// Good - consolidate if possible. Explicitly return null.
const cats = (): string => {
  if(x) {
    return x;
  } else if(y) {
    return y;
  }

  return null;
};

// Good - combine condition if possible
const dogs = (x: string): string => {
  if(x || z) {
    return y;
  }

  return z;
};

// Bad
const foo = (): string => {
  if(x) {
    return x;
  } else {
    return y;
  }
};

// Bad
const cats (): string => {
  if(x) {
    return x;
  }

  if(y) {
    return y;
  }
};

// Bad
const cats = (): string => {
  if(x) {
    return x;
  } else {
    if(y) {
      return y;
    }
  }
}

// Bad
const dogs = (x: string): string => {
  if(x) {
    if(z) {
      return y;
    }
  } else {
    return z;
  }
};
```

* If an if block always executes a return statement, the subsequent else block is unnecessary.
* A return in an else if block following an if block that contains a return can be separated into multiple if blocks. 
* Always return. The end of a block should return a variable or null unless the block returns void. 

> ESLint Rules

```json
{
  "no-else-return": "error"
}
```
