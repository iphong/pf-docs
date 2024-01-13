# Storage mechanism

I've created the `Storage` class as a base for manipulating data. Below are the public properties and methods of this base class.

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

An instance of the `Storage` class is similar to a data store created by executing the current `createSubscription` function but more encapsulated.

{% hint style="success" %}
Every individual storage needs to _**extend**_ the `Storage` class to _**inherit**_ construction, initialization, and methods for working with data.
{% endhint %}

I've created the following storages for working with global config, dashboard state, and cookie consent settings.

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

{% hint style="info" %}
A subclass that _**extends**_ the class `Storage` can _**override**_ static properties defined in the base class to customize its behavior. Below is the list of static properties that can be used to customize the behavior of a subclass.

* `syncWithLegacyStores` directs the base class to synchronize storage data with one or more legacy stores created by calling the legacy function `createSubscription`.
* `syncWithServerURL` directs the base class to fetch initial data when constructing a storage instance from the specified URL if initial data is not provided when getting a storage instance.
* `syncChangesToServerURL` directs the base class whether to automatically synchronize changes in storage data with the URL specified for the property `syncWithServerURL`.
* `syncWithWebStorage` directs the base class to synchronize storage data with the web storage under the key specified for the static property `webStorageKey`.
* `syncWithRedisStorage` directs the base class to synchronize storage data with the Redis storage under the key specified for the static property `redisStorageKey`.
{% endhint %}

When declaring the `StorageConfig` class, I override two static properties as follows.

* The `syncWithLegacyStores` property directs the base class to synchronize the storage data with the current `globalConfigSubscription` store to ensure that refactored code that works with an instance of the `StorageConfig` class and non-refactored code that works with the `globalConfigSubscription` store can work seamlessly together.
* The `syncWithServerURL` property directs the base class to fetch initial data from the server endpoint `/api/get/config` when constructing an instance of the class. You also can provide initial data dynamically as an optional argument when creating a storage instance at runtime. The base class will ensure assigning the initial data to storage instances only once at instantiation.

The `Storage` class also supports synchronizing data of a storage instance with more than one legacy store created by the current `createSubscription` function. A sample use of this behavior is the `ConfigDashboard` class.

When declaring the `ConfigDashboard` class, I override the `syncWithLegacyStores` property to direct the base class to sync the `dismiss` key in the storage data with the `dismissSubscription` store and the `onboarding` key in the storage data with the `onboardingSubscription` store.

{% hint style="info" %}
The `Storage` class provides the following public methods to work with data:

* The `get()` method returns the current value of a key-path.
* The `set()` method assigns a new value for a key-path.
* The `update()` method merges an object on top of the current data.
* The `reset()` method overrides the current data with the initial data.
* The `clear()` method overrides the current data with an empty object.
* The `subscribe()` method saves a callback function to execute it when data changes.
* The `unsubscribe()` method removes a callback function previously saved by the `subscribe()` method.
{% endhint %}

{% hint style="danger" %}
Subclasses extending the `Storage` class _**should not override**_ public methods of the base class to ensure the storage mechanism works as expected.
{% endhint %}

Below are some examples of using these public methods in reality.

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
