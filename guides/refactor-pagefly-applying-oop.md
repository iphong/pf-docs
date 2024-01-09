# Refactor PageFly applying OOP

## The current situation of PageFly

Currently, PageFly uses functional programming. In detail, PageFly uses React function components and global state hooks.

Functional programming emphasizes creating pure functions that do not have side effects, making it easier to reason about the code's behavior. However, global state hooks allow the use of hooks almost everywhere, even inside other hooks. This characteristic causes functions to become not pure and need more time traversing through hooks to understand the code.

While using React function components and global state hooks allows rapid development time, the code structure is loose and hard to follow. So, the code needs reviewing and maintaining thoroughly. Otherwise, it would become a mess.

The current code of PageFly is a result of not being reviewed and maintained carefully. There is a clean folder structure, but the code structure is unclear. Hooks are imported and used everywhere without rules, making the source code too complex. Many repeated code and hard coding make updates time-consuming and prone to bugs. Components and modules are not independent enough, and their reusable is not good yet.

All these things make PageFly hard to maintain and not easy to keep track of performance and stability.

It is the reason I propose a new structure for refactoring PageFly that applies the object-oriented programming (OOP) concept. The proposal also has adapters to allow refactoring PageFly piece by piece without affecting the app functionalities.

## The concept of object-oriented programming (OOP)

The object-oriented approach is more like a set of guiding concepts than a technical method. Specifically, there are four overarching OOP principles: _**encapsulation**_, _**inheritance**_, _**polymorphism**_, and _**reusability**_.

_**Encapsulation**_ represents the mechanism for code to bind with the data it manipulates. Only declared methods within a class can access the class data. This characteristic will prevent failures from spreading to other application components because every class is independent. Developers don't need details about the object's internals to use it effectively. Instead, they only need to know the results produced by class methods.

_**Inheritance**_ makes all properties and methods available to a child class. This characteristic allows developers to reuse common logic and model real-world relationships. Developers can use inheritance to avoid code duplication and simplify object design complexity. Inheritance supports the reusability of code to eliminate boilerplate rewriting and also helps decrease the overall code volume.

_**Polymorphism**_ means objects can adopt multiple forms depending on their context. Polymorphism helps in the dynamic calling of correct functions. This characteristic allows developers to switch implementations when needed. For example, databases can be in many ways, such as talking to a file system or an RDBMS server like MySQL or a NoSQL server like MongoDB. Using polymorphism, developers can define an interface to work with databases, and classes that implement the interface will execute the correct database calls.

_**Reusability**_ is the result of encapsulation, inheritance, and polymorphism. When developers want to create a new class, but an existing class already contains the desired code, they can derive a new class by extending the old one. In OOP, these modular classes enable developers to reuse those classes when needed, even in other applications and projects. This characteristic allows developers to perform fixed operations on particular objects and add functionality as the application and codebase evolve.

## Apply the OOP concept to refactor PageFly

Functional programming and object-oriented programming are two different techniques. So, to refactor PageFly applying OOP, I've created a new structure. Besides the new structure, I've also created some adapters for a seamless combination of refactored and non-refactored code. The adapters will ensure PageFly functions like normal while being refactored.

### New structure and adapters

#### Folders

Below is the new folder structure I proposed for grouping files by purpose and feature.

```
src/next/@refactoring
|- components
|  |- cookie-consent
|  |- top-bar
|  |- ...
|- constants
|  |- dashboard.ts
|  |- ...
|- contexts
|  |- dashboard.ts
|  |- ...
|- includes
|  |- loaders
|  |  |- components.ts
|  |  |- storages.ts
|  |- adapters.ts
|  |- component.ts
|  |- event.ts
|  |- ext-object.ts
|  |- helpers.ts
|  |- render.ts
|  |- storage.ts
|  |- use-contexts.ts
|  |- use-hooks.ts
|- modules
|  |- editor
|  |  |- components
|  |  |  |- workspace.tsx
|  |  |  |- ...
|  |  |- constants
|  |  |  |- editor.ts
|  |  |- contexts
|  |  |  |- editor.ts
|  |  |- elements
|  |  |  |- body.tsx
|  |  |  |- section.tsx
|  |  |  |- ...
|  |  |- includes
|  |  |  |- loaders
|  |  |  |  |- elements.ts
|  |  |  |- element.ts
|  |  |  |- render.ts
|  |  |- storages
|  |  |  |- editor.ts
|  |- inspector
|  |  |- components
|  |  |  |- group.tsx
|  |  |  |- ...
|  |  |- constants
|  |  |  |- inspector.ts
|  |  |- contexts
|  |  |  |- inspector.ts
|  |  |- controls
|  |  |  |- text-editor.tsx
|  |  |  |- ...
|  |  |- includes
|  |  |  |- loaders
|  |  |  |  |- controls.ts
|  |  |  |- control.ts
|  |  |  |- render.ts
|  |  |- storages
|  |  |  |- inspector.ts
|  |- ...
|- screens
|  |- dashboard
|  |  | - index.tsx
|  |  | - ...
|  |- editor
|  |  | - index.tsx
|  |  | - ...
|- storages
|  |- config.ts
|  |- cookie-consent.ts
|  |- dashboard.ts
|  |- ...
```

#### Storage

Data management and manipulation is the center of almost all applications. I've created the `Storage` class to store and manipulate data. Below are the public properties and methods of this base class.

```javascript
export default class Storage {
  // Define synchronization with legacy stores.
  static syncWithLegacyStores: StorageSynchronization

  // The URL that provides initial data.
  static syncWithServerURL: string

  // Whether the storage should automatically sync data
  // to the server URL above?
  static syncChangesToServerURL: boolean

  // Whether the storage should automatically sync data
  // with web storage?
  static syncWithWebStorage: boolean

  // If `webStorageKey` is not defined, the name of the
  // storage class will be used.
  static webStorageKey: string

  // Whether the storage should automatically sync data
  // with Redis storage?
  static syncWithRedisStorage: boolean

  // If `redisStorageKey` is not defined, the name of the
  // storage class will be used.
  static redisStorageKey: string

  // Static method to import a storage class declaration and
  // then return an instance of it.
  static async importThenGetInstance(params: { id?: string; initialData?: any; storageName?: string}) => Promise<StorageInstance>

  // Static method to get an instance of a storage.
  static getInstance(params: { id?: string; initialData?: any }) => StorageInstance

  // Get data from the storage for the given key path.
  get(keyPath?: string) => any

  // Set data to the storage for the given key path.
  set(keyPath: string, value: any, silent?: boolean) => ThisType<any>

  // Update the storage with the given data.
  update(newData: any, silent?: boolean) => ThisType<any>

  // Reset the storage to initial data.
  reset(silent?: boolean) => ThisType<any>

  // Clear the storage data.
  clear(silent?: boolean) => ThisType<any>

  // Subscribe to change in the storage.
  subscribe(callbackFunction: (event: EventObject) => void) => ThisType<any>

  // Unsubscribe from change in the storage.
  unsubscribe(callbackFunction: (event: EventObject) => void) => ThisType<any>

  // Sync data to a server URL using the HTTP PUT request method.
  syncToServerURL() => ThisType<any>

  // Backward compatibility with legacy stores created by the
  // `createSubscription` function.
  get state() => any

  // Backward compatibility with legacy stores created by the
  // `createSubscription` function.
  set state(newState: any) => void

  // Backward compatibility with legacy stores created by the
  // `createSubscription` function.
  resetState() => void

  // Backward compatibility with legacy stores created by the
  // `createSubscription` function.
  updateState(newState: any, forceUpdate: boolean = true) => void
}
```

An instance of the `Storage` class is similar to a data store created by executing the current `createSubscription` function. Any individual storage needs to _**extend**_ the `Storage` class to _**inherit**_ methods for storing and manipulating data. For example, I've created the below storages for working with global config, dashboard state, and cookie consent settings.

{% tabs %}
{% tab title="StorageConfig" %}
```javascript
export default class StorageConfig extends Storage {
  // Define synchronization with legacy stores.
  static syncWithLegacyStores: StorageSynchronization = () => globalConfigSubscription

  // Define API endpoints for requesting config.
  static syncWithServerURL = '/api/get/config'
}
```
{% endtab %}

{% tab title="StorageCookieConsent" %}
```javascript
export default class StorageCookieConsent extends Storage {
  // Define synchronization with legacy stores.
  static syncWithLegacyStores: StorageSynchronization = () => cookieSubscription
}
```
{% endtab %}

{% tab title="StorageDashboard" %}
```javascript
export default class StorageDashboard extends Storage {
  // Define synchronization with legacy stores.
  static syncWithLegacyStores: StorageSynchronization = {
    dismiss: () => dismissSubscription,
    onboarding: () => onboardingSubscription,
  }

  // Sync data with web storage. The data key in web storage
  // will be `StorageDashboard`.
  static syncWithWebStorage = true

  // Sync data with Redis storage. The data key in Redis storage
  // will be `StorageDashboard`.
  static syncWithRedisStorage = true
}
```
{% endtab %}
{% endtabs %}

A subclass that extends the `Storage` class can _**override**_ public properties defined in the base class to customize its behavior.

When declaring the `StorageConfig` class, I override two static properties as follows.

* The `syncWithLegacyStores` property directs the base class to sync the storage data with the current `globalConfigSubscription` store. Of course, after refactoring the entire code of PageFly, we will remove both the `globalConfigSubscription` legacy store and the `syncWithLegacyStores` directive declared in the `StorageConfig` class.
* The `syncWithServerURL` property directs the base class to fetch initial data from the server endpoint `/api/get/config` when creating an instance of the class. You also can provide initial data dynamically as an optional argument when creating a storage instance at runtime. The base class will ensure assigning the initial data to storage instances only once at instantiation.

The `Storage` class also supports sync data of a storage instance with more than one legacy store created by the current `createSubscription` function.

As you can see in the source code above, when declaring the `ConfigDashboard` class, I override the `syncWithLegacyStores` property to direct the base class to sync the `dismiss` key in the storage data with the `dismissSubscription` store and the `onboarding` key in the storage data with the `onboardingSubscription` store.

The `Storage` class provides the following public methods to work with data:

* The `get()` method returns the current value of a key-path.
* The `set()` method assigns a new value for a key-path.
* The `update()` method merges an object on top of the current data.
* The `reset()` method overrides the current data with the initial data.
* The `clear()` method overrides the current data with an empty object.
* The `subscribe()` method saves a callback function to execute it when data changes.
* The `unsubscribe()` method removes a callback function previously saved by the `subscribe()` method.

Below are some examples of using these methods in reality.

```javascript
class StorageTest extends Storage {
  // No custom behavior is needed, leave the subclass declaration empty.
}

// `getInstance` is a static method of the `Storage` class and is
// automatically available in subclasses that extend the `Storage`
// class. This method is to get a storage instance for storing and
// manipulating data. When calling this method, it will create only
// one instance to use during the life circle of the app.
let test = StorageTest.getInstance({ initialData: { foo: 'bar' }})

// Define a function to handle storage changes.
function changeHandler(event) {
  // Get object where changes occur.
  const { target, type, data } = event

  console.log({ target, type }, JSON.stringify(data))
}

// Listen to changes in the `test` storage instance.
test.subscribe(changeHandler)

test.set('my.name.is', 'cuong')

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{"my":{"name":{"is":"cuong"}}}'

console.log(test.get('my.name.is'))

// ===> The following will be logged to the console:
// cuong

test.update({ my: { name: 'cuong' } })

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{"my":{"name":"cuong"}}'

console.log(test.get('my.name.is'))

// ===> The following will be logged to the console:
// undefined

console.log(test.get('my.name'))

// ===> The following will be logged to the console:
// cuong

// Get a new instance of the StorageTest class by passing an ID to the
// static method `getInstance`.
test = StorageTest.getInstance({ id: 'new-instance' })

test.set('my.name.is', 'instance-2')

// ===> Nothing will be logged to the console because the `changeHandler`
// function is not subscribed to the new instance.

console.log(test.get('my.name.is'))

// ===> The following will be logged to the console:
// instance-2

// Get the first instance again.
test = StorageTest.getInstance()

test.set('my.name.is', 'instance-1')

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{"my":{"name":{"is":"instance-1"}}}'

test.reset()

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{"foo":"bar"}'

// Get the second instance again.
test = StorageTest.getInstance({ id: 'new-instance' })

// Listen to changes in the second instance.
test.subscribe(changeHandler)

test.set('my.name.is', 'instance-2')

// ===> Nothing will be logged to the console because the value of the
// `my.name.is` path is not changed.

test.set('my.name.is', 'cuong-2')

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{"my":{"name":{"is":"cuong-2"}}}'

test.clear()

// ===> The following will be logged to the console:
// {target: StorageTest, type: 'change'} '{}'
```

#### Render

The current code of PageFly is not _**modular**_ enough because of the loose structure. This thing causes, even when using lazy loading for rendering React elements, the initial delay is still not fast because of the large size of loading trunks.

To solve this problem, I've created the `Render` React component. This component supports loading the declaration of another React component dynamically. Using the `Render` component, declaration files will not load in the main trunk. This behavior helps avoid loading unnecessary files and also helps reduce the size of the main trunk.

Below is a sample use of the `Render` component.

```javascript
function Dashboard() {
  return <Render
    componentName="DashboardOnboarding"
    preRenderPlaceholder={<img src="./lcp-image" alt="onboarding" />}
  />
}
```

In the example above, when rendering the `Dashboard` component, the `Render` component will look for the declaration file of the `DashboardOnboarding` component and dynamically load it if not loaded before. While loading the declaration file, the `Render` component will render the content provided for the `preRenderPlaceholder` property. If the declaration file is loaded before, the `Render` component will render the `DashboardOnboarding` component immediately.

To dynamically render a React component using `Render`, you will need to define a mapping from the component name to its declaration file path in the `components` object declared in the `src/next/@refactoring/includes/loaders/components.ts` file. The content of that file is similar to the following.

```javascript
const components: StringToReactComponentMapping = {
  ScreenEditor: async () => (await import('@/@refactoring/screens/editor')).default,
  EditorWorkspace: async () => (await import('@/@refactoring/modules/editor/components/workspace')).default,
  InspectorGroup: async () => (await import('@/@refactoring/modules/inspector/components/group')).default,
}
```

The behavior of the `Render` component is similar to the native `lazy` function of React but doesn't need to use the `Suspense` component for rendering a placeholder. Below is a rewriting of the example above using the native `lazy` function of React.

```javascript
const LazyDashboardOnboarding = lazy(() => import('/path/to/file')

function Dashboard() {
  return <Suspense fallback={<img src="./lcp-image" alt="onboarding" />}>
    <LazyDashboardOnboarding />
  </Suspense>
}
```

### Refactor React components

According to the new structure, we will need to refactor all current components of PageFly, from React function components using global state hooks to component classes updating internal state based on changes in storage. I've created the `Component` class that extends the native `PureComponent` class of React as the base for real-life UI components to build upon. Below is the interface of the base class.

```javascript
export default class Component<P, S> extends PureComponent<P & ComponentProps, S & ComponentState> {
  static defaultProps = {
    // Define a list of storage to subscribe to.
    // E.g. [StorageConfig, StorageCookieConsent, StorageDashboard]
    storages: (string | typeof Storage)[]
  }

  // Define a mapping from component props to state.
  // E.g. { 'data-id': 'element.id', 'data-type': 'element.type', 'contexts.parentId': 'element.parentId' }
  static propsToState: StringMapping

  // Define a mapping from storage data to state.
  // E.g. { 'StorageConfig.shopDomain': 'shop', 'StorageDashboard.onboarding.isCompleted': 'hide.onboarding' }
  static storageToState: StringMapping

  // Populate component state from props.
  static getDerivedStateFromProps(props, state) => any

  // Do some initialization tasks after the component is mounted.
  componentDidMount() => void

  // Clean up timers, event handlers, etc. before the component is umounted.
  componentWillUnmount() => void

  // Render HTML elements.
  render() => ReactNode

  // Receive changes in storage and act accordingly.
  onStorageChange(event: EventObject) => void

  // Handle changes in storage and update the component if needed.
  handleStorageChange(storageName: string, data: any) => void
}
```

### Refactor editor elements



### Refactor inspector controls



## References

* [Breaking down the cornerstone components of OOP](https://www.techtarget.com/searchapparchitecture/tip/A-breakdown-of-object-oriented-programming-concepts)
* [Is JavaScript a (true) OOP language?](https://medium.com/@andrea.chiarelli/is-javascript-a-true-oop-language-c87c5b48bdf0)
* [Introduction to Object-Oriented Programming in JavaScript](https://www.geeksforgeeks.org/introduction-object-oriented-programming-javascript/)

