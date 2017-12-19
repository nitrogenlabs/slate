# Modules

## Prefer modules

> Prefer modules

```javascript
// bad
const StyleGuide = require('./StyleGuide');
module.exports = StyleGuide.es6;

// best
import {es6} from './StyleGuide';
export {es6};
```

```typescript
// bad
const StyleGuide = require('./StyleGuide');
module.exports = StyleGuide.es6;

// best
import {es6} from './StyleGuide';
export {es6};
```

* Always use modules (import/export) over a non-standard module system. 
* You can always transpile to your preferred module system.
* Modules are the future, let"s start using the future now.


## Wildcards

> Wildcards

```javascript
// bad
import * as StyleGuide from './StyleGuide';

// good
import {StyleGuide} from './StyleGuide';
```

```typescript
// bad
import * as StyleGuide from './StyleGuide';

// good
import {StyleGuide} from './StyleGuide';
```

* Do not use wildcard imports, make sure you explicitly export.


## Defaults

> Defaults

```javascript
// bad
import StyleGuide from './StyleGuide';

// good
import {StyleGuide} from './StyleGuide';
```

```typescript
// bad
import StyleGuide from './StyleGuide';

// good
import {StyleGuide} from './StyleGuide';
```

* Do not export defaults, make sure you explicitly name your exports.
* If you refactor `Foo` in foo.ts it will not rename it in bar.ts
* If you end up needing to export more stuff from foo.ts (which is what many of your files will have) then you have to juggle the import syntax.

### ESLint

`"import/prefer-default-export"`


## Exporting

> Exporting

```javascript
// bad
// filename es6.js
export {es6} from './StyleGuide';

// good
// filename es6.js
import {es6} from './StyleGuide';
export {es6};
```

```typescript
// bad
// filename es6.js
export {es6} from './StyleGuide';

// good
// filename es6.js
import {es6} from './StyleGuide';
export {es6};
```

* And do not export directly from an import.
* Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.


## Duplicate imports

> Duplicate imports

```javascript
// bad
import {foo} from 'foo';
// … some other imports … //
import {named1, named2} from 'foo';

// good
import {foo, named1, named2} from 'foo';

// good
import {
  foo,
  named1,
  named2,
} from 'foo';
```

```typescript
// bad
import {foo} from 'foo';
// … some other imports … //
import {named1, named2} from 'foo';

// good
import {foo, named1, named2} from 'foo';

// good
import {
  foo,
  named1,
  named2,
} from 'foo';
```

* Only import from a path in one place.
* Having multiple lines that import from the same path can make code harder to maintain.

### ESLint

`"no-duplicate-imports": "error"`


## Mutable bindings

> Mutable bindings

```javascript
// bad
export let foo = 3;

// good
export const foo = 3;
```

```typescript
// bad
export let foo: number = 3;

// good
export const foo: number = 3;
```

* Do not export mutable bindings. 
* Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

### ESLint

`"import/no-mutable-exports": "error"`


## Ordering

> Ordering

```javascript
// bad
import {foo} from 'foo';
foo.init();

import {bar} from 'bar';

// good
import {foo} from 'foo';
import {bar} from 'bar';

foo.init();
```

```typescript
// bad
import {foo} from 'foo';
foo.init();

import {bar} from 'bar';

// good
import {foo} from 'foo';
import {bar} from 'bar';

foo.init();
```

* Put all imports above non-import statements.
* Since imports are hoisted, keeping them all at the top prevents surprising behavior.

### ESLint

`"import/first": "error"`


## Indent

> Indent

```javascript
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'foo';

// good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE
} from 'foo';
```

```typescript
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'foo';

// good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE
} from 'foo';
```

* Multiline imports should be indented just like multiline array and object literals.
* The curly braces follow the same indentation rules as every other curly brace block in the style guide, as does the no trailing comma rule.

### TSLint

`"import-spacing": true`


## Webpack imports

> Webpack imports

```javascript
// bad
import 'css!sass!foo.scss';
import 'style!css!bar.css';

// good
import 'foo.scss';
import 'bar.css';
```

```typescript
// bad
import 'css!sass!foo.scss';
import 'style!css!bar.css';

// good
import 'foo.scss';
import 'bar.css';
```

* Disallow Webpack loader syntax in module import statements.
* Since using Webpack syntax in the imports couples the code to a module bundler. Prefer using the loader syntax in webpack.config.js.

### ESLint

`"import/no-webpack-loader-syntax": "error"`
