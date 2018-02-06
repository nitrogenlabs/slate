# Add Storage

By default ArkhamJS does not use a persistent storage. All state data is stored in memory. ArkhamJS can persist data depending on the environment.

Persist storage is the continuance of data after its cause is removed. This means that the data survives after the process with which it was created has ended. For a data store to be considered persistent, it must write to non-volatile storage so when the app reloads, the previously saved data is still available.

![ArkhamJS cache](./img/cache-arkhamjs.png "ArkhamJS cache")

There are three official persistent stores available:

 * [@nlabs/arkhamjs-storage-browser](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-browser) - Browser, local and session storage.
 * [@nlabs/arkhamjs-storage-native](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-native) - React Native, AsyncStorage.
 * [@nlabs/arkhamjs-storage-node](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-node) - NodeJS, file storage.


## Create custom

> Custom storage structure

```javascript
export class CustomStorage {
  constructor() {
    this.getStorageData = this.getStorageData.bind(this);
    this.setStorageData = this.setStorageData.bind(this);
  }

  getStorageData(key) {
    // ...
  }

  setStorageData(key, value) {
    // ...
  }
}
```

```typescript
export class CustomStorage {
  constructor() {
    this.getStorageData = this.getStorageData.bind(this);
    this.setStorageData = this.setStorageData.bind(this);
  }

  getStorageData(key: string) {
    // ...
  }

  setStorageData(key: string, value: any) {
    // ...
  }
}
```

With so many ways of storing data, a custom storage plugin can be created to fit your needs. A storage class simply requires two methods:

 * **getStorageData** - Retrieves a key/value pair from storage.
 * **setStorageData** - Sets a key/value pair into storage.

As long as these two methods are included, you can add as many helper functions as needed. For an in-depth example with options and static helper methods, you may take a look at the [arkhamjs-storage-browser](https://github.com/nitrogenlabs/arkhamjs/blob/master/packages/arkhamjs-storage-browser/src/BrowserStorage/BrowserStorage.ts) source code.


### #getStorageData(key)

> Get app data

```javascript
const storage = new CustomStorage();
storage.getStorageData('dataKey');
```

```typescript
const storage = new CustomStorage();
storage.getStorageData('dataKey');
```

Get app data from storage. This method is used internally to access cached data.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from app storage.


### #setStorageData(key)

> Set app data

```javascript
const storage = new CustomStorage();
storage.setSessionData('dataKey', 'dataValue');
```

```typescript
const storage = new CustomStorage();
storage.setSessionData('dataKey', 'dataValue');
```

Save app data to storage. This method is used internally to save data to cache.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to SessionStorage. All objects will converted to a string before saving.

#### Returns
A boolean indicating if data was successfully saved to storage.


## arkhamjs-storage-browser

> Configure and initialize

```javascript
import {BrowserStorage} from '@nlabs/arkhamjs-storage-browser';

// Browser storage configuration
const storage = new BrowserStorage({type: 'session'});

// ArkhamJS configuration
Flux.init({
  storage
});
```

```typescript
import {BrowserStorage} from '@nlabs/arkhamjs-storage-browser';

// Browser storage configuration
const storage: BrowserStorage = new BrowserStorage({type: 'session'});

// ArkhamJS configuration
Flux.init({
  storage
});
```

HTML5 web storage provides two objects for storing data on the client: `window.localStorage` and `window.sessionStorage`. With web storage, applications can store data locally within the browser.

### Options
 * **type** - Use either `session` or `local` storage. Default _session_.


### Installing

> Install browser storage

```javascript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-browser

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-browser
```

```typescript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-browser

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-browser
```

The browser storage plugin can be found as a node module at [arkhamjs-storage-browser](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-browser).


### .delLocalData(key)

> Remove data in local storage

```javascript
BrowserStorage.delLocalData('dataKey');
```

```typescript
BrowserStorage.delLocalData('dataKey');
```

Remove an object from localStorage.

#### Arguments
* [`key`] \(*string*): Key of the object to remove.

#### Returns
A boolean indicating if data was successfully removed from LocalStorage.


### .delSessionData(key)

> Set data in session storage

```javascript
BrowserStorage.delSessionData('dataKey');
```

```typescript
BrowserStorage.delSessionData('dataKey');
```

Remove an object from sessionStorage.

#### Arguments
* [`key`] \(*string*): Key of object to delete.

#### Returns
A boolean indicating if data was successfully removed from sessionStorage.


### .getLocalData(key)

> Get data from local storage

```javascript
BrowserStorage.getLocalData('dataKey');
```

```typescript
BrowserStorage.getLocalData('dataKey');
```

Get an object from localStorage.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from local storage.


### .getSessionData(key)

> Get data from session storage

```javascript
BrowserStorage.getSessionData('dataKey');
```

```typescript
BrowserStorage.getSessionData('dataKey');
```

Get an object from sessionStorage.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from session storage.


### .setLocalData(key, value)

> Set data in local storage

```javascript
BrowserStorage.setLocalData('dataKey', 'Hello World');
```

```typescript
BrowserStorage.setLocalData('dataKey', 'Hello World');
```

Save an object to localStorage.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to LocalStorage. All objects will converted to a string before saving.

#### Returns
A boolean indicating if data was successfully saved in localStorage.


### .setSessionData(key, value)

> Set data in session storage

```javascript
BrowserStorage.setSessionData('dataKey', 'Hello World');
```

```typescript
BrowserStorage.setSessionData('dataKey', 'Hello World');
```

Save an object to sessionStorage.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to SessionStorage. All objects will converted to a string before saving.

#### Returns
A boolean indicating if data was successfully saved to sessionStorage.


## arkhamjs-storage-native

> Configure and initialize

```javascript
import {NativeStorage} from '@nlabs/arkhamjs-storage-native';

// React Native storage configuration
const storage = new NativeStorage();

// ArkhamJS configuration
Flux.init({
  storage
});
```

```typescript
import {NativeStorage} from '@nlabs/arkhamjs-storage-native';

// Storage configuration
const storage: NativeStorage = new NativeStorage();

// ArkhamJS configuration
Flux.init({
  storage
});
```

React native uses a native storage used between both, Android and iOS, platforms, called `AsyncStorage`. AsyncStorage is a simple, unencrypted, asynchronous, persistent, key-value storage system that is global to the app.

On iOS, AsyncStorage is backed by native code that stores small values in a serialized dictionary and larger values in separate files. On Android, AsyncStorage will use either RocksDB or SQLite based on what is available.

More details on AsyncStorage can be found on the [React Native](https://facebook.github.io/react-native/docs/asyncstorage.html) web site.


### Installing

> Install React Native storage

```javascript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-native

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-native
```

```typescript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-native

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-native
```

The React Native storage plugin can be found as a node module at [arkhamjs-storage-native](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-native).


### .delAsyncData(key)

> Remove data in AsyncStorage

```javascript
NativeStorage.delAsyncData('dataKey');
```

```typescript
NativeStorage.delAsyncData('dataKey');
```

Remove an object from AsyncStorage.

#### Arguments
* [`key`] \(*string*): Key of the object to remove.

#### Returns
A boolean indicating if data was successfully removed from AsyncStorage.


### .getAsyncData(key)

> Get data from AsyncStorage

```javascript
NativeStorage.getAsyncData('dataKey');
```

```typescript
NativeStorage.getAsyncData('dataKey');
```

Get an object from AsyncStorage.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from AsyncStorage.


### .setAsyncData(key, value)

> Set data in AsyncStorage

```javascript
NativeStorage.setAsyncData('dataKey', 'Hello World');
```

```typescript
NativeStorage.setAsyncData('dataKey', 'Hello World');
```

Save an object to AsyncStorage.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to AsyncStorage.

#### Returns
A boolean indicating if data was successfully saved in AsyncStorage.


## arkhamjs-storage-node

> Install and initialize

```javascript
import {NodeStorage} from '@nlabs/arkhamjs-storage-node';

// Node storage configuration
const storage = new NodeStorage({
    continuous: true,
    dir: '/tmp',
    encoding: 'utf8',
    expiredInterval: 3 * 60 * 1000,
    forgiveParseErrors: false,
    interval: false,
    logging: false,
    parse: JSON.parse,
    stringify: JSON.stringify,
    ttl: false
  });

// ArkhamJS configuration
Flux.init({
  storage
});
```

```typescript
import {NodeStorage} from '@nlabs/arkhamjs-storage-node';

// Node storage configuration
const storage: NodeStorage = new NodeStorage({
    continuous: true,
    dir: '/tmp',
    encoding: 'utf8',
    expiredInterval: 3 * 60 * 1000,
    forgiveParseErrors: false,
    interval: false,
    logging: false,
    parse: JSON.parse,
    stringify: JSON.stringify,
    ttl: false
  });

// ArkhamJS configuration
Flux.init({
  storage
});
```

Data is stored as JSON documents in the file system for persistence. App data is just in-memory, which will result in lightning fast retrivals and stores.


### Options
 * **continuous** -  Continously persist to disk. Default _true_.
 * **dir** - Directory to save cache files. Default _'/tmp'_.
 * **encoding** - Content encoding. Default _'utf8'_.
 * **expiredInterval** - Interval process will clean-up the expired cache. Default _3 * 60 * 1000_.
 * **forgiveParseErrors** - In some cases, you (or some other service) might add non-valid storage files to your storage dir, i.e. Google Drive, make this true if you'd like to ignore these files and not throw an error. Default _false_.
 * **interval** - Persist to disk on an interval. Default _false_.
 * **logging** - Custom logging function. Default _false_.
 * **parse** - Custom JSON parse function. Default _JSON.parse_.
 * **stringify** - Custom JSON stringify function. Default _JSON.stringify_.
 * **ttl** - Time to live. Default _false_.


### Installing

> Install NodeJS persistent storage

```javascript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-node

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-node
```

```typescript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-storage-node

// Install using yarn:
$ yarn add @nlabs/arkhamjs-storage-node
```

The NodeJS persistent storage plugin can be found as a node module at [arkhamjs-storage-node](https://www.npmjs.com/package/@nlabs/arkhamjs-storage-node).


### .clearPersistData()

> Clear all data

```javascript
NodeStorage.clearPersistData();
```

```typescript
NodeStorage.clearPersistData();
```

Removes all keys from persistant data.

#### Returns
A promise resolving a boolean indicating if data was successfully removed.


### .delPersistData(key)

> Remove data

```javascript
NodeStorage.delPersistData('dataKey');
```

```typescript
NodeStorage.delPersistData('dataKey');
```

Removes a key from persistant data.

#### Arguments
* [`key`] \(*string*): Key of the object to remove.

#### Returns
A promise resolving a boolean indicating if data was successfully removed.


### .getPersistData(key)

> Get data

```javascript
NodeStorage.getPersistData('dataKey');
```

```typescript
NodeStorage.getPersistData('dataKey');
```

Get a key value from persistant data.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A promise resolving a value from storage.


### .setAsyncData(key, value)

> Set data

```javascript
NodeStorage.setPersistData('dataKey', 'Hello World');
```

```typescript
NodeStorage.setPersistData('dataKey', 'Hello World');
```

Saves data to persistant data.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to storage.

#### Returns
A promise resolving a boolean indicating if data was successfully saved in storage.
