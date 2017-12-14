# Actions

```javascript
import {Flux} from 'arkhamjs';
import {AppConstants} from '../constants/AppConstants';

export class AppActions {
  static test(str) {
    // Dispatch our action.
    return Flux.dispatch({type: AppConstants.TEST, demo: str});
  }
}
```

```typescript
import {Flux, FluxAction} from 'arkhamjs';
import {AppConstants} from '../constants/AppConstants';

export class AppActions {
  static test(str: string): FluxAction {
    // Dispatch our action.
    return Flux.dispatch({type: AppConstants.TEST, demo: str});
  }
}
```

Actions are where all the excitement happens. They usually will contain your API calls, file reads/writes, and promises. When your data is pulled from an external source or generated within the app, you'll want to take your results and drop them into an action object and shoot them out with a dispatch call.

### Action objects

An action object is simple an object with at least one required property, the `type`. The `type` is a unique string that identifies the action. It is used within the stores to indicate how the data should be added to the store. It also is used as the event type. All types are case sensitive. And although it is best practice to keep all type strings as constants, you can simply use a string if you wanted.

In addition to the `type` property, you can add as many property key/values as you wish. All will be sent with the action to the store and to all listeners. In our example, we are adding a `demo` property to set the `str` string parameter.

### Dispatching

Once we have an action object, we want to dispatch it to the framework. We do this by calling `Flux.dispatch(action)`. ArkhamJS will check every store to see if the type matches any cases. If so, it will update the data in the stores. After all stores have been updated, an event will be dispatched to the `Flux` object, where any view/component listening in to that event will be triggered.

<aside class="notice">
A store does not have to listen for an action. An action can be dispatched and not update any data. A view/component may or may not be listening for an action to be called. Its all depends on the purpose of the action.
</aside>
