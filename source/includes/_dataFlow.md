# Data Flow

> Various ways to access store data.

```javascript

```

```typescript
import {Arkham, Flux, FluxDebugLevel, FluxOptions, Store} from 'arkhamjs';
import * as React from 'react';
import {AppActions} from '../actions/AppActions';
import {AppConstants} from '../constants/AppConstants';
import {AppStore} from '../stores/AppStore';

export class AppView extends React.Component {
  constructor(props) {
    ...

    // Bind methods
    this.onAppTest = this.onAppTest.bind(this);
  }
  
  componentWillMount(): void {
    Flux.on(AppConstants.TEST, this.onAppTest);
    ...
  }
  
  onAppTest(data): void {
    // Solution 1
    const myTest = Flux.getStore('app.test', ' default text');

    // Solution 2
    const myTest = data.test; // data.type = AppConstants.TEST
    
    ...
  }

  someMethod(): void {
    // Solution 3
    // Where someAction returns the Flux.dispatch for a 
    // AppConstants.TEST action.
    AppActions.someAction()
      .then((data) => {
        const myTest = data.test;
      });
  }
  ...
}
```

The most important part of an app is the dynamic data.

### Accessing Data

ArkhamJS is made to be flexible for your project. Thus, we have made it easy for you to access the most important part of your app, the data.

There are three ways to access the data after an action has been dispatched.

  1. It is best practice to get a value from the `Flux.getStore()` method. This will let you traverse down the store to the nested property value. If a value does not exist, a default value can be provided. You can call `Flux.getStore()` anywhere in your view and/or action.
  2. Through the data parameter in your event listener callback. 
  3. Sometimes you may not want an event listener for a dispatched action. In this case, you can chain a `then` method off your dispatch. Yes, each dispatch method returns a promise. 