# Views

> Root view component example.

```javascript
import {Arkham, Flux, FluxDebugLevel} from 'arkhamjs';
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
      // Enable debugger.
      debugLevel: FluxDebugLevel.DISPATCH,
      
      // Name of your app.
      name: 'MyApp'
    };

    // Register stores
    this.stores = [AppStore];
    
    // Bind methods
    this.onAppTest = this.onAppTest.bind(this);
  }
  
  componentWillMount() {
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
      <Arkham config={this.fluxOptions} stores={this.stores}>
        {this.state.myTest}
      </Arkham>
    );
  }
}
```

```typescript
import {Arkham, Flux, FluxDebugLevel, FluxOptions, Store} from 'arkhamjs';
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
      // Enable debugger.
      debugLevel: FluxDebugLevel.DISPATCH,
      
      // Name of your app.
      name: 'MyApp'
    };

    // Register stores
    this.stores = [AppStore];
    
    // Bind methods
    this.onAppTest = this.onAppTest.bind(this);
  }
  
  componentWillMount(): void {
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

The third and final piece is the view layer. This is where data updates are initiated. All updates are triggered by some time of user interaction (or timer). 

### ReactJS

The view layer is created by React. React has a fast and concise rendering algorithm. Making re-rendering isloated to only those components that need to be updated.

### 