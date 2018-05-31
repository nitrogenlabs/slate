# Modules

## Prefer modules

> Prefer modules

```javascript
// Good
import {es6} from './StyleGuideJS';
export {es6};

// Bad
const StyleGuideJS = require('./StyleGuide');
module.exports = StyleGuideJS.es6;
```

```javascript--flow
// Good
import {es6} from './StyleGuideJS';
export {es6};

// Bad
const StyleGuideJS = require('./StyleGuideJS');
module.exports = StyleGuideJS.es6;
```

```typescript
// Good
import {es6} from './StyleGuideJS';
export {es6};

// Bad
const StyleGuideJS = require('./StyleGuideJS');
module.exports = StyleGuideJS.es6;
```

* Always use modules (import/export) over a non-standard module system. 
* You can always transpile to your preferred module system.
* Modules are the future, let"s start using the future now.

## Wildcards

> Wildcards

```javascript
// Good
import {StyleGuideJS} from './StyleGuideJS';

// Bad
import * as StyleGuideJS from './StyleGuideJS';
```

```javascript--flow
// Good
import {StyleGuideJS} from './StyleGuideJS';

// Bad
import * as StyleGuideJS from './StyleGuideJS';
```

```typescript
// Good
import {StyleGuideJS} from './StyleGuideJS';

// Bad
import * as StyleGuideJS from './StyleGuideJS';
```

* Do not use wildcard imports, make sure you explicitly import and export.

## Defaults

> Defaults

```javascript
// Good
import {StyleGuide} from './StyleGuide';

// Bad
import StyleGuide from './StyleGuide';
```

```javascript--flow
// Good
import {StyleGuide} from './StyleGuide';

// Bad
import StyleGuide from './StyleGuide';
```

```typescript
// Good
import {StyleGuide} from './StyleGuide';

// Bad
import StyleGuide from './StyleGuide';
```

* Do not export defaults, make sure you explicitly name your exports.
* If you refactor `Foo` in foo.ts it will not rename it in bar.ts
* If you end up needing to export more stuff from foo.ts (which is what many of your files will have) then you have to juggle the import syntax.

## Exporting

> Exporting

```javascript
// Good
import {es6} from './StyleGuide';
export {es6};

// Bad
export {es6} from './StyleGuide';
```

```javascript--flow
// Good
import {es6} from './StyleGuide';
export {es6};

// Bad
export {es6} from './StyleGuide';
```

```typescript
// Good
import {es6} from './StyleGuide';
export {es6};

// Bad
export {es6} from './StyleGuide';
```

* And do not export directly from an import.
* Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

> ESLint Rules

```json
{
  "import/prefer-default-export": 0
}
```

## Duplicate imports

> Duplicate imports

```javascript
// Good
import {foo, named1, named2} from 'foo';

// Bad
import {foo} from 'foo';
import {named1, named2} from 'foo';
```

```javascript--flow
// Good
import {foo, named1, named2} from 'foo';

// Bad
import {foo} from 'foo';
import {named1, named2} from 'foo';
```

```typescript
// Good
import {foo, named1, named2} from 'foo';

// Bad
import {foo} from 'foo';
import {named1, named2} from 'foo';
```

* Only import from a path in one place.
* Having multiple lines that import from the same path can make code harder to maintain.

> ESLint Rules

```json
{
  "no-duplicate-imports": "error"
}
```

## Mutable bindings

> Mutable bindings

```javascript
// Good
export const foo = 3;

// Bad
export let foo = 3;
```

```javascript--flow
// Good
export const foo: number = 3;

// Bad
export let foo: number = 3;
```

```typescript
// Good
export const foo: number = 3;

// Bad
export let foo: number = 3;
```

* Do not export mutable bindings. 
* Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

> ESLint Rules

```json
{
  "import/no-mutable-exports": "error"
}
```


## Ordering

> Ordering

```javascript
// Good
import {foo} from 'foo';
import {bar} from 'bar';

foo.init();

// Bad
import {foo} from 'foo';
foo.init();

import {bar} from 'bar';
```

```javascript--flow
// Good
import {foo} from 'foo';
import {bar} from 'bar';

foo.init();

// Bad
import {foo} from 'foo';
foo.init();

import {bar} from 'bar';
```

```typescript
// Good
import {foo} from 'foo';
import {bar} from 'bar';

foo.init();

// Bad
import {foo} from 'foo';
foo.init();

import {bar} from 'bar';
```

* Put all imports above non-import statements.
* Since imports are hoisted, keeping them all at the top prevents surprising behavior.

> ESLint Rules

```json
{
  "import/first": "error",
  "import/order": [
    "error",
    {
      "newlines-between": "always"
    }
  ]
}
```


## Indent

> Indent

```javascript
// Good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE
} from 'foo';
```

```javascript--flow
// Good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE
} from 'foo';
```

```typescript
// Good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE
} from 'foo';
```

* Multiline imports should be indented just like multiline array and object literals.
* The curly braces follow the same indentation rules as every other curly brace block in the style guide, as has the no trailing comma rule.
