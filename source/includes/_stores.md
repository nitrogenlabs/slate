# Stores

> Example store

```javascript
import {Store} from 'arkhamjs';

// Extend the ArkhamJS Store class.
export class AppStore extends Store {
  constructor() {
    // Set the store name.
    super('app');
  }

  initialState() {
    // Define default values.
    return {
      content: 'default'
    };
  }

  onAction(type, data, state) {
    // Define how each action type will affect the state.
    switch(type) {
      case 'APP_CONTENT_UPDATE':
        return {...state, content: data.content};
      case 'APP_CONTENT_RESET':
        return this.initialState();
      default:
        return state;
    }
  }
}
```

```typescript
import {Store} from 'arkhamjs';

// Extend the ArkhamJS Store class.
export class AppStore extends Store {
  constructor() {
    // Set the store name.
    super('app');
  }

  initialState(): object {
    // Define default values.
    return {
      content: 'default'
    };
  }

  onAction(type: string, data, state): object {
    // Define how each action type will affect the state.
    switch(type) {
      case 'APP_CONTENT_UPDATE':
        return {...state, content: data.content};
      case 'APP_CONTENT_RESET':
        return this.initialState();
      default:
        return state;
    }
  }
}
```

ArkhamJS runs off of a single store object. That root store is then branched off to help organize your data. Each branch is a property in the root store object.

![ArkhamJS store](./images/store-arkhamjs.png "ArkhamJS store")

### Constructing a store

All stores should extend the `Store` class. There are three methods to focus on: `constructor`, `initialState`, and `onAction`.

#### constructor

Let's start with giving your store a name. This name will be referenced when accessing you store's data. In the example, `Flux.getStore('app.test')`, we would be traversing the `app` store and obtaining the test property. We define the name of the store in the constructor, setting the parameter of `super` to the name.

#### initialState

It is best practice to give all your properties a default value but not required. When ArkhamJS is initialized, it will grab the defaults to be used as initial values before any action is dispatched. Values can be any value, including numbers, strings, arrays, objects, and functions.

#### onAction

When an action is dispatched, it first calls triggers the stores before an event is dispatched to the view layer. As it hits each store, you can use the `switch` conditional to alter the data. Each case must return the full object of that partial store. So in the scenario of the example, we would return the `app` object, the `app` state.

<aside class="notice">
All data manimulation should occur in the action, not the store. Stores should only store data in its respective properties.
</aside>