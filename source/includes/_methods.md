# Methods

## Configuration

### .config(options)

> Set configuration within root view component

```javascript
import {Flux, FluxDebugLevel} from 'arkhamjs';

const env = 'development';

Flux.config({
  debugLevel: env === 'development' 
    ? FluxDebugLevel.DISPATCH 
    : FluxDebugLevel.DISABLED,
  name: 'MyApp',
  useCache: true
});
```

```typescript
import {Flux, FluxDebugLevel} from 'arkhamjs';

const env: string = 'development';

Flux.config({
  debugLevel: env === 'development' 
  ? FluxDebugLevel.DISPATCH 
  : FluxDebugLevel.DISABLED,
  name: 'MyApp',
  useCache: true
});
```

Set configuration options.

#### Arguments
* **options** (*object*): Configuration options.
  * **debugLevel** (*number*): Enable the debugger. You can specify to show console.logs and/or Flux dispatches. You can use a numeric value or one of the pre-defined constants: FluxDebugLevel.DISABLED (0, disable debugger), FluxDebugLevel.LOGS (1, only allow console logs), FluxDebugLevel.DISPATCH (2, display both, console logs and dispatcher action details).
  * **debugLogFnc** (*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `Flux.debugLog()` is run.
  * **debugInfoFnc** (*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `Flux.debugError()` is run.
  * **debugErrorFnc** \(*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `Flux.debugInfo()` is run.
  * **name** \(*string*) - Name of your app. Should not contain spaces. Is used as the session storage property for your cache. *Default: arkhamjs*
  * **useCache** \(*boolean*) - Enable caching to session storage. *Default: true*


## Events

### .on(eventType, data)

> Triggering and listening to events.

```javascript
import {Flux} from 'arkhamjs';
import * as React from 'react';
import {AppConstants} from '../constants/AppConstants';

export class AppView extends React.Component {
  constructor(props) {
    super(props);

    // Bind methods.
    this.onGetItems = this.onGetItems.bind(this);

    // Set initial state.
    this.state = {
      item: {}
    };
  }

  componentWillMount() {
    // Add a listener for GET_ITEM. When the event is 
    // dispatched, the onGetItems method will be 
    // called.
    Flux.on(AppConstants.GET_ITEM, this.onGetItems);
  }

  componentWillMount() {
    // Stop listening when the view is unmounted.
    Flux.off(AppConstants.GET_ITEM, this.onGetItems);
  }

  onGetItems() {
    // Get the item from the updated store.
    const item = Flux.getStore('app.item', {});
    this.setState({item});
  }
  // Get item action would be triggered below with
  // a UI interaction.
  ...
```

```typescript
import {Flux} from 'arkhamjs';
import * as React from 'react';
import {AppConstants} from '../constants/AppConstants';
import {AppItemType} from '../types/AppTypes';

export class AppView extends React.Component {
  constructor(props) {
    super(props);

    // Bind methods.
    this.onGetItems = this.onGetItems.bind(this);

    // Set initial state.
    this.state = {
      item: {}
    };
  }

  componentWillMount(): void {
    // Add a listener for GET_ITEM. When the event is 
    // dispatched, the onGetItems method will be 
    // called.
    Flux.on(AppConstants.GET_ITEM, this.onGetItems);
  }

  componentWillMount(): void {
    // Stop listening when the view is unmounted.
    Flux.off(AppConstants.GET_ITEM, this.onGetItems);
  }

  onGetItems(): void {
    // Get the item from the store.
    const item: AppItemType = Flux.getStore('app.item', {});
    this.setState({item});
  }
  // Get item action would be triggered below with
  // a UI interaction.
  ...
}
```

Adds an event listener. It is called any time an action is dispatched to Flux, and some part of the state tree may potentially have changed. You may then call getStore() to read the current state tree inside the callback.

#### Arguments
* [`eventType`] \(*string*): Event to subscribe for store updates.
* [`listener`] \(*function*): The callback to be invoked any time an action has been dispatched.


### .off(eventType, data).
Removes an event listener.

#### Arguments
* [`eventType`] \(*string*): Event to unsubscribe.
* [`listener`] \(*function*): The callback associated with the subscribed event.


### .dispatch(action, silent)
Dispatches an Action to all stores.

#### Arguments
* [`action`] \(*object*): An action object. The only required property is *type* which will indicate what is called in
the stores, all other properties will be sent to the store within the *data* object.
* [`silent`] \(*boolean*): Silence event emitter for this dispatch. Default: false.

#### Returns
A promise with an action object.

## Stores

### .getStore(name, default)

> Get store data

```javascript
// Get the root store object.
Flux.getStore();

// Using a dot notation.
Flux.getStore('app.test', 'default');

// Using an array to traverse.
Flux.getStore(['app', 'test'], 'default');
```

```typescript
// Get the root store object.
Flux.getStore();

// Using a dot notation.
Flux.getStore('app.test', 'default');

// Using an array to traverse.
Flux.getStore(['app', 'test'], 'default');
```

Get the state tree. If only a particular store is needed, it can be specified.

#### Arguments
* [`name`] \(*string*|*array*): (optional) A store name. May also use an array to get a nested property value.
* [`default`] \(*any*): (optional) The default value, if undefined. This may be a string, number, array or object.

#### Returns
The app store object.


### .setStore(name, value)

> Set store data

```javascript
// Using a dot notation.
Flux.setStore('app.test', 'Hello World');

// Using an array to traverse.
Flux.setStore(['app', 'test'], 'Hello World');
```

```typescript
// Using a dot notation.
Flux.setStore('app.test', 'Hello World');

// Using an array to traverse.
Flux.setStore(['app', 'test'], 'Hello World');
```

Used for unit testing. Set a store value. If only a particular store or property needs to be set, it can be specified.

#### Arguments
* [`name`] \(*string*|*array*): A store name. May also use an array to get a nested property value.
* [`value`] \(*any*): The value to set. This may be a string, number, boolean, array, or object.

#### Returns
The updated store and returns the stored object.


### .getClass(name)

> Get a store class

```javascript
Flux.getClass('app');
// In this example, will return the AppStore class.
```

```typescript
Flux.getClass('app');
// In this example, will return the AppStore class.
```

Get the store class object.

#### Arguments
* [`name`] \(*string*): The name of the store class object to retrieve.

#### Returns
A store class object.


### .registerStores(array)

> Register a store

```javascript
import {AppStore} from '../stores/AppStore';

// Register stores to be used with the app.
Flux.registerStores([AppStore]);
```

```typescript
import {AppStore} from '../stores/AppStore';

// Register stores to be used with the app.
Flux.registerStores([AppStore]);
```

Registers stores with Flux. Use an array of classes to register multiple.

#### Arguments
* [`Class`] \(*array*): The store class(s) to add to Flux.

#### Returns
An array of store class objects.


### .deregisterStore(name)

> Remove a store from the app

```javascript
// Deregister stores from the app.
Flux.deregisterStores(['app']);
```

```typescript
// Deregister stores from the app.
Flux.deregisterStores(['app']);
```

Deregisters stores from Flux. Use an array of names to deregister multiple stores.

#### Arguments
* [`name`] \(*array*): Name of store(s) to remove from Flux.


## SessionStorage

### .getSessionData(key)

> Get data from session storage

```javascript
Flux.getSessionData('myData');
```

```typescript
Flux.getSessionData('myData');
```

Get an object from sessionStorage.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from session storage.


### .setSessionData(key, value)

> Set data in session storage

```javascript
Flux.setSessionData('myData', 'Hello World');
```

```typescript
Flux.setSessionData('myData', 'Hello World');
```

Save an object to sessionStorage.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to SessionStorage. All objects will converted to a string before saving.

#### Returns
A boolean indicating if data was successfully saved to sessionStorage.


### .delSessionData(key)

> Set data in session storage

```javascript
Flux.delSessionData('myData');
```

```typescript
Flux.delSessionData('myData');
```

Remove an object from sessionStorage.

#### Arguments
* [`key`] \(*string*): Key of object to delete.

#### Returns
A boolean indicating if data was successfully removed from sessionStorage.


### .clearAppData()

> Clear all app data saved in session storage

```javascript
Flux.clearAppData();
```

```typescript
Flux.clearAppData();
```

Removes all app related data from sessionStorage.

#### Returns
A boolean indicating if app data was successfully removed from sessionStorage.


## LocalStorage

### .getLocalData(key)

> Get data from local storage

```javascript
Flux.getLocalData('myData');
```

```typescript
Flux.getLocalData('myData');
```

Get an object from localStorage.

#### Arguments
* [`key`] \(*string*): Key of object to retrieve.

#### Returns
A value from local storage.


### .setLocalData(key, value)

> Set data in local storage

```javascript
Flux.setLocalData('myData', 'Hello World');
```

```typescript
Flux.setLocalData('myData', 'Hello World');
```

Save an object to localStorage.

#### Arguments
* [`key`] \(*string*): Key to reference object.
* [`value`] \(*any*): A value to save to LocalStorage. All objects will converted to a string before saving.

#### Returns
A boolean indicating if data was successfully saved in localStorage.


### .delLocalData(key)

> Remove data in local storage

```javascript
Flux.delLocalData('myData');
```

```typescript
Flux.delLocalData('myData');
```

Remove an object from localStorage.

#### Arguments
* [`key`] \(*string*): Key of the object to remove.

#### Returns
A boolean indicating if data was successfully removed from LocalStorage.


## Debug

### .enableDebugger(toggle)

> Toggle debugger

```javascript
Flux.enableDebugger(true);
```

```typescript
Flux.enableDebugger(true);
```

Turn on the console debugger to display each action call and store changes. By default the framework has the debugger disabled.

#### Arguments
* [`toggle`] \(*boolean*): Enable or disable debugger. Default: true.


### .debugLog(obj1 [, obj2, ..., objN])

> Safely add debug logging

```javascript
Flux.debugLog('console log');
```

```typescript
Flux.debugLog('console log');
```

Logs data in the console. Only logs when in debug mode.  Will also call the debugLogFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are 
appended together in the order listed and output.


### .debugInfo(obj1 [, obj2, ..., objN])

> Safely add info logging

```javascript
Flux.debugInfo('console info');
```

```typescript
Flux.debugInfo('console info');
```

Logs informational messages to the console. Will also call the debugInfoFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are appended together in the order listed and output.


### .debugError(obj1 [, obj2, ..., objN])

> Safely add error logging

```javascript
Flux.debugError('console error');
```

```typescript
Flux.debugError('console error');
```

Logs errors in the console. Will also call the debugErrorFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are 
appended together in the order listed and output.


## State

### .getInitialState()

> Returns initial state

```javascript
Flux.getInitialState();
```

```typescript
Flux.getInitialState();
```

Used for unit testing. Gets the initial state of the store.

#### Returns
The initial state of the store as an object.