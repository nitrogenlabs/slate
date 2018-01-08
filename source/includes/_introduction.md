# Introduction

ArkhamJS is a lightweight framework that can accommodate a project of any size. From small start-up ideas to large enterprise projects. ReactJS is an amazing library but unfortunately, it is not a framework. Although the creators of ReactJS recommend using React in a Flux architecture, there is no official framework. The result is a wide variety of great third-party frameworks. Our goal is to create a simple framework with flexibility. And thus came ArkhamJS.

## Features

### Lightweight

The framework is small. The bulk of your app should lay within your code, not the framework. While larger frameworks come with lots of "magic", they become very limited when new features arise within your project. ReactJS is very powerful in itself. ArkhamJS simply complements it.

### Typescript

Compatible with typescript. Definitions are included to support your Typescript project.

### Single Store

All data is stored within a single store. The data can be accessed through all your views and components. Data is organized into multiple stores within the single store.

### Immutability

To prevent object referencing, we use immutable objects. When a state changes in a ReactJS component, the state's property is not the only item that is changed, the item it references is also updated. To prevent passing around an object between different scopes, immutable objects give your data a one way update path.

### Cache

Your single store can be persisted in a cache. Caches available are browser (local or session), React Native's AsyncStorage, and Node. While caching is optional, it can be very useful when saving state.

### Debugger

The most important factor in choosing a framework is how easy it is to build with it. And with building comes debugging. A detailed debugger is optional with the framework. When included, it will display any actions that come through the framework. Making the previous and new state visible to the developer. Great way to make your data transparent! Supported browsers: Chrome, Firefox, and Safari.