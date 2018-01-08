# Methods

## Configuration

### #config(options)

> Set configuration within root view component

```javascript
import {BrowserStorage} from '@nlabs/arkhamjs-storage-browser';
import {Flux} from 'arkhamjs';

const env = 'development';
const storage = new BrowserStorage({type: 'session'});

Flux.config({
  name: 'MyApp',
  storage
});
```

```typescript
import {BrowserStorage} from '@nlabs/arkhamjs-storage-browser';
import {Flux} from 'arkhamjs';

const env: string = 'development';
const storage: BrowserStorage = new BrowserStorage({type: 'session'});

Flux.config({
  name: 'MyApp',
  storage
});
```

Set configuration options.

#### Arguments
* [`options`] \(*object*): Configuration options.
  * **name** \(*string*) - Name of your app. Should not contain spaces. Is used as the session storage property for your cache. *Default: arkhamjs*
  * **storage** \(*object*) - Add a persistent storage for the app state.

#### Returns
A promise with a null object.


## Events

### #on(eventType, data)

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


### #off(eventType, data).
Removes an event listener.

#### Arguments
* [`eventType`] \(*string*): Event to unsubscribe.
* [`listener`] \(*function*): The callback associated with the subscribed event.


### #dispatch(action, silent)
Dispatches an Action to all stores.

#### Arguments
* [`action`] \(*object*): An action object. The only required property is *type* which will indicate what is called in
the stores, all other properties will be sent to the store within the *data* object.
* [`silent`] \(*boolean*): Silence event emitter for this dispatch. Default: false.

#### Returns
A promise with an action object.

## Stores

### #getStore(name, default)

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
* [`name`] \(*string*|*string[]*): (optional) A store name. May also use an array to get a nested property value.
* [`default`] \(*any*): (optional) The default value, if undefined. This may be a string, number, array or object.

#### Returns
The app store object.


### #setStore(name, value)

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

Used for unit testing. Set a store value. If only a particular store or property needs to be set, it can be specified. It is best practice to set update the state via actions, not directly using `setStore`.

#### Arguments
* [`name`] \(*string*|*string[]*): A store name. May also use an array to get a nested property value.
* [`value`] \(*any*): The value to set. This may be a string, number, boolean, array, or object.

#### Returns
The updated store and returns the stored object.


### #getClass(name)

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


### #registerStores(stores)

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
* [`Class`] \(*Store[]*): The store class(s) to add to Flux.

#### Returns
An array of store class objects.


### #deregisterStores(names)

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
* [`names`] \(*string[]*): Name of store(s) to remove from Flux.


### #clearAppData()

> Clear all app data stored in state.

```javascript
Flux.clearAppData();
```

```typescript
Flux.clearAppData();
```

Removes all app data from state.

#### Returns
A boolean indicating if app data was successfully removed.


## State

### #getInitialState()

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


## Middleware

### #addMiddleware(middleware)

> Add middleware

```javascript
const loggerMiddleware: Logger = new Logger();
Flux.addMiddleware([loggerMiddleware]);
```

```typescript
const loggerMiddleware: Logger = new Logger();
Flux.addMiddleware([loggerMiddleware]);
```

Adds middleware from the framework. Middleware modules will be processed in the order they are added.

#### Arguments
* [`middleware`] \(*object[]*): An array of middleware objects to add.


### #clearMiddleware()

> Remove all middleware

```javascript
Flux.clearMiddleware();
```

```typescript
Flux.clearMiddleware();
```

Removes all middleware from the framework.

#### Returns
A boolean. True if the middleware has been successfully removed.


### #removeMiddleware(middleware)

> Remove middleware

```javascript
Flux.removeMiddleware(['logger']);
```

```typescript
Flux.removeMiddleware(['logger']);
```

Removes middleware from the framework.

#### Arguments
* [`middleware`] \(*string[]*): An array of middleware names to add.

