# Add-ons

Components used alongside the framework. Containers, UI components, services, etc. 

## arkhamjs-views-react

React view containers to simplify routing\. Uses [React Router](https://reacttraining.com/react-router/) to route the views. Updates title in the browser on successful route. `ArkhamRouteActions` wraps actions around the history. Easily notify your components on a route action. 


### Installation

> Install Logger

```javascript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-views-react

// Install using yarn:
$ yarn add @nlabs/arkhamjs-views-react
```

```typescript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-views-react

// Install using yarn:
$ yarn add @nlabs/arkhamjs-views-react
```

The logger middleware can be found as a node module at [arkhamjs-views-react](https://www.npmjs.com/package/@nlabs/arkhamjs-views-react).


### ArkhamRouteActions

> Import ArkhamRouteActions

```javascript
import {ArkhamRouteActions} from '@nlabs/arkhamjs-views-react';
```

```typescript
import {ArkhamRouteActions} from '@nlabs/arkhamjs-views-react';
```

Import ArkhamRouteActions to gain access to the route history methods.


### ArkhamRouteActions.goBack()

> Go back

```javascript
ArkhamRouteActions.goBack();
```

```typescript
ArkhamRouteActions.goBack();
```

Go to the previous view.

#### Returns
A promise resolving an action. Actions props include:

 * [`history`]\(*object*) - Router history object.


### ArkhamRouteActions.goForward()

> Go forward

```javascript
ArkhamRouteActions.goForward();
```

```typescript
ArkhamRouteActions.goForward();
```

Go to the next view.

#### Returns
A promise resolving an action. Actions props include:

 * [`history`]\(*object*) - Router history object.


### ArkhamRouteActions.goReplace(path [, params])

> Replace view

```javascript
ArkhamRouteActions.goReplace('/login', {token});
```

```typescript
ArkhamRouteActions.goReplace('/login', {token});
```

Replace the current view with a new view. This method will also replace the view in the history.

#### Arguments
 * [`path`] \(*string*): New route path.
 * [`params`] \(*string*): New route params.

#### Returns
A promise resolving an action. Actions props include:

 * [`history`]\(*object*) - Router history object.
 * [`path`]\(*string*) - Route path.
 * [`params`]\(*object*) - Route params.


### ArkhamRouteActions.goto(path [, params])

> Go to a new view

```javascript
ArkhamRouteActions.goto('/details', {user});
```

```typescript
ArkhamRouteActions.goto('/details', {user});
```

Push another view into the history.

#### Arguments
 * [`path`] \(*string*): New route path.
 * [`params`] \(*string*): New route params.

#### Returns
A promise resolving an action. Actions props include:

 * [`history`]\(*object*) - Router history object.
 * [`path`]\(*string*) - Route path.
 * [`params`]\(*object*) - Route params.


### ArkhamRouteActions.updateTitle(title)

> Update title

```javascript
ArkhamRouteActions.updateTitle('New page title');
```

```typescript
ArkhamRouteActions.updateTitle('New page title');
```

Manually update page title in the browser.

#### Arguments
 * [`title`] \(*string*): New page title.

#### Returns
A promise resolving an action. Actions props include:

 * [`history`]\(*object*) - Router history object.
 * [`title`] \(*string*) - Page title.


> Root view component example.

```javascript
import {Logger, LoggerDebugLevel} from '@nlabs/arkhamjs-middleware-logger';
import {Arkham} from '@nlabs/arkhamjs-views-react';
import {Flux} from 'arkhamjs';
import * as React from 'react';
import {AppActions} from '../actions/AppActions';
import {AppConstants} from '../constants/AppConstants';
import {AppStore} from '../stores/AppStore';

export class AppView extends React.Component {
  fluxOptions;
  stores;
  
  constructor(props) {
    super(props);
    
    // Set the initial state.
    this.state = {
      myTest: ''
    };
    
    // Initialize Flux with custom configuration (optional)
    this.fluxOptions = {
      // Name of your app.
      name: 'MyApp'
    };

    // Register stores
    this.stores = [AppStore];

    // Middleware
    const logger: Logger = new Logger({
      debugLevel: LoggerDebugLevel.DISPATCH
    });
    this.middleware = [logger];
    
    // Bind methods
    this.onAppTest = this.onAppTest.bind(this);
  }
  
  componentDidMount() {
    // Add event listener for our action. Here we are
    // listening for the TEST action to be dispatched.
    // When triggered, will call method, onAppTest.
    Flux.on(AppConstants.TEST, this.onAppTest);
    
    // When the component loads and is mounted, it 
    // will call the AppActions.test method. This
    // dispatches our TEST action with the string
    // provided ('Hello World').
    AppActions.test('Hello World');
  }

  componentWillUnmount() {
    // Stop listening for the action when we unmount.
    Flux.off(AppConstants.TEST, this.onAppTest);
  }
  
  onAppTest() {
    // Get the string from the store. If the string
    // happened to be null, we provided a default.
    const myTest = Flux.getStore('app.test', ' default text');
    
    // Show the output in the console.
    console.log('onAppTest::myTest', myTest);
    
    // Set state to re-render component.
    this.setState({myTest});
  }
  
  render() {
    return (
      <Arkham config={this.fluxOptions} stores={this.stores} middleware={this.middleware}>
        {this.state.myTest}
      </Arkham>
    );
  }
}
```

```typescript
import {Logger, LoggerDebugLevel} from '@nlabs/arkhamjs-middleware-logger';
import {Arkham} from '@nlabs/arkhamjs-views-react';
import {Flux, FluxOptions, Store} from 'arkhamjs';
import * as React from 'react';
import {AppActions} from '../actions/AppActions';
import {AppConstants} from '../constants/AppConstants';
import {AppStore} from '../stores/AppStore';

export class AppView extends React.Component {
  private fluxOptions: FluxOptions;
  private stores: Store[];
  
  constructor(props) {
    super(props);
    
    // Set the initial state.
    this.state = {
      myTest: ''
    };
    
    // Initialize Flux with custom configuration (optional)
    this.fluxOptions = {
      // Name of your app.
      name: 'MyApp'
    };

    // Register stores
    this.stores = [AppStore];

    // Middleware
    const logger: Logger = new Logger({
      debugLevel: LoggerDebugLevel.DISPATCH
    });
    this.middleware = [logger];
    
    // Bind methods
    this.onAppTest = this.onAppTest.bind(this);
  }
  
  componentDidMount(): void {
    // Add event listener for our action. Here we are
    // listening for the TEST action to be dispatched.
    // When triggered, will call method, onAppTest.
    Flux.on(AppConstants.TEST, this.onAppTest);
    
    // When the component loads and is mounted, it 
    // will call the AppActions.test method. This
    // dispatches our TEST action with the string
    // provided ('Hello World').
    AppActions.test('Hello World');
  }

  componentWillUnmount(): void {
    // Stop listening for the action when we unmount.
    Flux.off(AppConstants.TEST, this.onAppTest);
  }
  
  onAppTest(): void {
    // Get the string from the store. If the string
    // happened to be null, we provided a default.
    const myTest = Flux.getStore('app.test', ' default text');
    
    // Show the output in the console.
    console.log('onAppTest::myTest', myTest);
    
    // Set state to re-render component.
    this.setState({myTest});
  }
  
  render(): JSX.Element {
    return (
      <Arkham config={this.fluxOptions} stores={this.stores}>
        {this.state.myTest}
      </Arkham>
    );
  }
}
```
