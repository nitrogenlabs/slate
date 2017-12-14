# Getting Started

## Source files

### Github
The ArkhamJS project is regularly maintained on GitHub. All contributions, and suggested features are welcome. 

### Download the Zip
Although we recommend installing the node module, you may access the source files by downloading the latest [.zip](https://github.com/nitrogenlabs/arkhamjs/archive/master.zip) (~25kb).


## Installation

### ArkhamJS

> Install using [npm](http://npmjs.com):

```javascript
// Install ArkhamJS
$ npm install --save arkhamjs
```

```typescript
// Install ArkhamJS
$ npm install --save arkhamjs
```

> Install using [yarn](https://yarnpkg.com):

```javascript
$ yarn add arkhamjs
```

```typescript
$ yarn add arkhamjs
```

ArkhamJS can be used in all modern browsers.

### ArkhamJS Native

> Install using [npm](http://npmjs.com):

```javascript
// Install ArkhamJS Native
$ npm install --save arkhamjs-native
```

```typescript
// Install ArkhamJS Native
$ npm install --save arkhamjs-native
```

> Install using [yarn](https://yarnpkg.com):

```javascript
$ yarn add arkhamjs-native
```

```typescript
$ yarn add arkhamjs-native
```

If planning on using ArkhamJS with React Native, then please use the ArkhamJS Native version. It is modified slightly to work within the mobile environment. Some of those differences include saving state in AsyncStorage instead of SessionStorage.

## Importing

```javascript
// Import for ArkhamJS
import {Flux} from 'arkhamjs';
```

```typescript
// Import for ArkhamJS
import {Flux} from 'arkhamjs';
```

Then with a module bundler like webpack that supports either CommonJS or ES2015 modules, use as you would anything else:

## Starter Skeleton

For the quickest way to get started, we setup a skeleton to get started. You can [download](https://github.com/nitrogenlabs/arkhamjs-skeleton/archive/master.zip) the latest version and have a sample site up within minutes!

The project is complete with a pre-existing file structure, sample layout views, components, and even server setup with Webpack.
