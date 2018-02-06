# Add Middleware

Middleware is a class that contains plugins to the framework for customization. You can add in existing middleware modules or create a custom class to include.

## Custom middleware

> Custom class

```javascript
export class CustomMiddleware {
  constructor() {
    this.name = 'customName';

    // Methods
    this.postDispatch = this.postDispatch.bind(this);
    this.preDispatch = this.preDispatch.bind(this);
  }

  preDispatch(action, previousStore) {
    // ... Alter action if needed
    return Promise.resolve(action);
  }

  postDispatch(action, nextStore) {
    // ... Alter action if needed
    return Promise.resolve(action);
  }
}
```

```typescript
import {FluxAction} from 'arkhamjs';

export class CustomMiddleware {
  name: string = 'customName';

  constructor() {
    // Methods
    this.postDispatch = this.postDispatch.bind(this);
    this.preDispatch = this.preDispatch.bind(this);
  }

  preDispatch(action: FluxAction, previousStore): Promise<FluxAction> {
    // ... Alter action if needed
    return Promise.resolve(action);
  }

  postDispatch(action: FluxAction, nextStore: object): Promise<FluxAction> {
    // ... Alter action if needed
    return Promise.resolve(action);
  }
}
```

There are two requirements for a custom middleware module, it must have a name and there must be at least one plugin. You can provide multiple plugins within a middleware module. There are currently two types of plugins available:

 * **preDispatch** - Called before parsing through the stores.
 * **postDispatch** - Called after parsing through the stores but before an event is emitted.

![ArkhamJS middleware](./img/middleware-arkhamjs.png "ArkhamJS middleware")

## Logger

> Add the logger middleware

```javascript
import {Flux} from 'arkhamjs';

// Configure
const logger = new Logger({
  debugLevel: LoggerDebugLevel.DISPATCH
});

// Add to ArkhamJS
Flux.addMiddleware([logger]);
```

```typescript
import {Flux} from 'arkhamjs';

// Configure
const logger: Logger = new Logger({
  debugLevel: LoggerDebugLevel.DISPATCH
});

// Add to ArkhamJS
Flux.addMiddleware([logger]);
```

Logs actions to the console log after each dispatch. Tracking changes in the state. View state actions and changes in detail.

The logger also provides a way to wrap your console methods (log, warning, and error) to better facilitate enabling and disabling logging in console. Instead of forgotten logs or unnecessary error logging. You may also wrap your logs with a custom wrapper to send to analytics, add color, etc.

![Loggert screenshot](./img/logger.png "Logger screenshot")


### Options

  * **debugLevel** (*number*): Enable the debugger. You can specify to show console.logs and/or Flux dispatches. You can use a numeric value or one of the pre-defined constants: LoggerDebugLevel.DISABLED (0, disable debugger), LoggerDebugLevel.LOGS (1, only allow console logs), LoggerDebugLevel.DISPATCH (2, display both, console logs and dispatcher action details).
  * **debugLogFnc** (*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `debugLog()` is run.
  * **debugInfoFnc** (*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `debugError()` is run.
  * **debugErrorFnc** \(*function*) - (optional) Passes the debug data to the specified function with the debugLevel as the first parameter and the data as the 1-n parameters. Executed when `debugInfo()` is run.


### Installation

> Install Logger

```javascript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-middleware-logger

// Install using yarn:
$ yarn add @nlabs/arkhamjs-middleware-logger
```

```typescript
// Install using npm:
$ npm install --save @nlabs/arkhamjs-middleware-logger

// Install using yarn:
$ yarn add @nlabs/arkhamjs-middleware-logger
```

The logger middleware can be found as a node module at [arkhamjs-middleware-logger](https://www.npmjs.com/package/@nlabs/arkhamjs-middleware-logger).


### #enableDebugger(toggle)

> Toggle debugger

```javascript
const logger = new Logger();
logger.enableDebugger(LoggerDebugLevel.DISPATCH);
```

```typescript
const logger: Logger = new Logger();
logger.enableDebugger(LoggerDebugLevel.DISPATCH);
```

Turn on the console debugger to display each action call and store changes. By default the framework has the debugger disabled.

#### Arguments
* [`level`] \(*number*): Enable or disable the debugger. Uses the constants:
   *   LoggerDebugLevel.DISABLED (0) - Disable.
   *   LoggerDebugLevel.LOGS (1) - Enable console logs.
   *   LoggerDebugLevel.DISPATCH (2) - Enable console logs and dispatch action data (default).



### #debugLog(obj1 [, obj2, ..., objN])

> Safely add debug logging

```javascript
const logger = new Logger();
logger.debugLog('console log');
```

```typescript
const logger: Logger = new Logger();
logger.debugLog('console log');
```

Logs data in the console. Only logs when in debug mode.  Will also call the debugLogFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are appended together in the order listed and output.


### #debugInfo(obj1 [, obj2, ..., objN])

> Safely add info logging

```javascript
const logger = new Logger();
logger.debugInfo('console info');
```

```typescript
const logger: Logger = new Logger();
logger.debugInfo('console info');
```

Logs informational messages to the console. Will also call the debugInfoFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are appended together in the order listed and output.


### #debugError(obj1 [, obj2, ..., objN])

> Safely add error logging

```javascript
const logger = new Logger();
logger.debugError('console error');
```

```typescript
const logger: Logger = new Logger();
logger.debugError('console error');
```

Logs errors in the console. Will also call the debugErrorFnc method set in the config.

#### Arguments
* [`obj`] \(*any*): A list of JavaScript objects to output. The string representations of each of these objects are appended together in the order listed and output.

