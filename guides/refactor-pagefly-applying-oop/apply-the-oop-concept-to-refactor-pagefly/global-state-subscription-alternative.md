# Global state subscription alternative

The use of global state subscriptions is the primary reason that makes PageFly hard to keep track of performance and bugs. Global state subscriptions control the content and behavior of multiple UI components and can be changed by any UI component. This behavior causes one UI component to be potentially uncontrollable because it depends on the behavior of an untrackable number of other UI components.

Therefore, we need to find a solution either to replace global state subscriptions or to control global state subscriptions tighter. Next, I will describe a solution that uses storage combined with custom events to replace global state subscriptions.

Currently, we create a global state using the `createSubscription` function and use the `useSubscription` function to make UI components subscribe to changes made in the global state. While the `useSubscription` method allows defining a list of dependencies to decide whether a UI component needs to update itself according to changes in the global state, developers might not proactively know and control it.

My idea is to use storage and custom events to replace the global state subscription. UI components will read data from storage to render content and decide an appropriate behavior but not directly subscribe to changes in the storage. Instead, a UI component should listen to a custom event on a common HTML element, such as the `window` object or the `document.body` element, to proactively know when the storage data changes and decide whether to update itself. When a UI component changes storage data, it needs to trigger a custom event on the chosen HTML element to let other UI components know about it.

To support this idea, I've created a base class named `Event` for working with custom events. Below is the interface of this base class.

```typescript
export default class Event {
  /**
   * Listen to an event on an object.
   *
   * @param sourceObject     This argument can be any object.
   * @param eventName        Name of the event.
   * @param callbackFunction Function that will be executed when the event is triggered.
   *
   * @returns void
   */
  static add(sourceObject: any | any[], eventName: string, callbackFunction: EventHandler) => void

  /**
   * Stop listening to an event on an object.
   *
   * @param sourceObject     This argument can be any object.
   * @param eventName        Name of the event.
   * @param callbackFunction Function that was previously registered.
   *
   * @returns void
   */
  static remove(sourceObject: any | any[], eventName: string, callbackFunction: EventHandler) => void

  /**
   * Trigger an event on an object.
   *
   * @param sourceObject This argument can be any object.
   * @param eventName    Name of the event.
   * @param eventData    Event data.
   *
   * @returns void
   */
  static trigger(sourceObject: any | any[], eventName: string, eventData: any = {}) => void
}
```

I will demonstrate the idea of using storage and custom events to replace global state subscriptions by refactoring the use of the global state `cookieSubscription`. Currently, the global state `cookieSubscription` stores cookie consent settings. Several UI components subscribe to this global state to render appropriate content based on the current cookie consent settings.

Below is the storage `StorageCookieConsent` I've created to replace the global state `cookieSubscription` for saving the cookie consent settings.

```typescript
import Storage from '@/@refactoring/includes/storage'

type StorageCookieConsentDataType = {
  cookiesState?: boolean
  lastActionFrom?: string
  isModalVisible?: boolean
  gaTrackingState?: boolean
  isOpenCrispChat?: boolean
  crispTrackingState?: boolean
  isOpenViaGetFeedback?: boolean
}

export default class StorageCookieConsent<T, K> extends Storage<
  T & StorageCookieConsentDataType,
  K & StorageCookieConsentDataType
> {
}
```

The global state `cookieSubscription` is updated by the hook function `useCookiesConsent`, the component `EditorCookieBar`, the component `CookieBar`, and the component `CookiesRequiredModal`. Changes made in the global state `cookieSubscription` affects the content and behavior of the following UI components: `CatalogItem`, `CatalogMenu`, `EditorCrispChat`, `OldPageAlert`, `PageReviewModal`, `PageOutline`, `Editor`, `CardUndo`, `CookieBar`, `CookiesRequiredModal`, `HelpSupport`, `LiveChat`, `ModalFooter`, `SearchModal`, `CardFreeServices`, `FeedbackModal`, `SupportResourcesCard`, `UndoCard`, `MediaEditorModal`, `FontUploadItem`, `Question`, `CookiesManagerModal`, `BeforeLeaveModal`, and `UserInterface`.

Luckily, when viewing the code, I find that only a few of the components listed above directly subscribe to `cookieSubscription` by calling the function `useSubscription` or directly change data in `cookieSubscription` by calling the `updateState` method. They are the following UI components: `CatalogItem`, `CatalogMenu`, `OldPageAlert`, `Editor`, and `CookiesManagerModal`. Other components indirectly subscribe to or change data in the global state `cookieSubscription` via the hook function `useCookiesConsent`. This situation means we only need to refactor the hook function `useCookiesConsent` and five UI components instead of all the affected components.

However, while viewing the code of these components, I found the following closely related code blocks repeatedly used across multiple source code files.

```typescript
    crispTrackingState ? openChat() : showModal(true)
```

```typescript
    crispTrackingState ? openChat() : openModal('FUNCTIONAL_MODAL')
```

```typescript
    if (crispTrackingState) {
      openChat()
    } else {
      closeModal()
      openModal('FUNCTIONAL_MODAL')
    }
```

```typescript
    if (crispTrackingState) {
      openChat()
    } else {
      openModal('FUNCTIONAL_MODAL')
      handleChange()
    }
```

Code duplication like this is not a good behavior. So, I've converted these lines of code to a function named `openChatOrRequestPermission` and replaced all the code duplications with a calling to that function.

```typescript
export function openChatOrRequestPermission(
  callback: Function = null, closeVisibleModalFirst: boolean = false, showCustomModal: Function = null
) {
  if (StorageCookieConsent.getInstance().get('crispTrackingState')) {
    openChat()
  } else {
    // Close all visible modals first if necessary.
    if (closeVisibleModalFirst) {
      modalSubscription.updateState(mapValues(modalSubscription.state, () => false))
    }

    // Open the cookie consent modal for requesting permission.
    if (typeof showCustomModal === 'function') {
      showCustomModal()
    } else {
      modalSubscription.updateState({ FUNCTIONAL_MODAL: true })
    }

    if (typeof callback === 'function') {
      callback()
    }
  }
}
```

{% tabs %}
{% tab title="Before" %}
```typescript
    crispTrackingState ? openChat() : showModal(true)
```

```typescript
    crispTrackingState ? openChat() : openModal('FUNCTIONAL_MODAL')
```

```typescript
    if (crispTrackingState) {
      openChat()
    } else {
      closeModal()
      openModal('FUNCTIONAL_MODAL')
    }
```

```typescript
    if (crispTrackingState) {
      openChat()
    } else {
      openModal('FUNCTIONAL_MODAL')
      handleChange()
    }
```
{% endtab %}

{% tab title="After" %}
```typescript
    openChatOrRequestPermission(null, false, () => showModal(true))
```

```typescript
    openChatOrRequestPermission()
```

```typescript
    openChatOrRequestPermission(null, true)
```

```typescript
    openChatOrRequestPermission(handleChange)
```
{% endtab %}
{% endtabs %}

The code is much cleaner now. It's time to replace the global state subscription `cookieSubscription` with the storage `StorageCookieConsent` combined with a custom event named `changeStorageCookieConsent`.

First, we will refactor the hook function `useCookiesConsent` as follows.

{% tabs %}
{% tab title="Before" %}
```typescript
const useCookiesConsent = () => {
  // ...

  const {
    state: { isModalVisible, gaTrackingState, cookiesState, crispTrackingState, isOpenViaGetFeedback },
    setState,
  } = useSubscription(cookieSubscription)

  // ...

  return {
    setState,
    acceptAllCookies,
    updateCookiesConsent,
    isModalVisible,
    showModal,
    handleCancel,
    acceptCookies,
    acceptGATracking,
    acceptCrisp,
    gaTrackingState,
    cookiesState,
    crispTrackingState,
    acceptAllCookiesWithoutEnableUIOptimization,
    isOpenViaGetFeedback,
    clickGetFeedback,
    PFReviewCheckerShopDomain,
  }
}
```
{% endtab %}

{% tab title="After" %}
```typescript
const useCookiesConsent = () => {
  // ...

  const storage: StorageInstance = StorageCookieConsent.getInstance()

  const [cookieConsentState, updateCookieConsentState] = useState({
    isModalVisible: storage.get('isModalVisible'),
    gaTrackingState: storage.get('gaTrackingState'),
    cookiesState: storage.get('cookiesState'),
    crispTrackingState: storage.get('crispTrackingState'),
    isOpenViaGetFeedback: storage.get('isOpenViaGetFeedback'),
  })

  const setState = newState => {
    storage.update(newState)
    Event.trigger(document.body, 'changeStorageCookieConsent', newState)
  }

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const newState = {}

      for (const prop in cookieConsentState) {
        const newValue = event.data[prop]

        if (newValue !== undefined && cookieConsentState[prop] !== newValue) {
          newState[prop] = newValue
        }
      }

      if (Object.keys(newState).length) {
        updateCookieConsentState({ ...cookieConsentState, ...newState })
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  }, [])

  // ...

  return {
    setState,
    acceptAllCookies,
    updateCookiesConsent,
    showModal,
    handleCancel,
    acceptCookies,
    acceptGATracking,
    acceptCrisp,
    acceptAllCookiesWithoutEnableUIOptimization,
    clickGetFeedback,
    PFReviewCheckerShopDomain,
    ...cookieConsentState
  }
}
```
{% endtab %}
{% endtabs %}

As you can see, I updated the hook function `useCookiesConsent` to trigger a custom event named `changeStorageCookieConsent` every time it changes the data in the storage `StorageCookieConsent` and also listens to that custom event to update its internal state with changes in the storage. Now, we have two options: update UI components that directly subscribe to `cookieSubscription` to get data from the storage `StorageCookieConsent` and listen to the custom event `changeStorageCookieConsent`, or update these UI components to use the hook function `useCookiesConsent`.

The first option needs self-validation and can reduce affections and limit dependencies. So, I decided to update these UI components that directly subscribe to `cookieSubscription` to get data from the storage `StorageCookieConsent` and listen to the custom event `changeStorageCookieConsent` to decide whether to re-render.

Below are the refactored versions of these components.

{% tabs %}
{% tab title="Before" %}
```typescript
export default function CatalogItem({ onCloseDrawer, elementVariants, groupKey }) {
  // ...

  const {
    state: { gaTrackingState, cookiesState },
  } = useSubscription(cookieSubscription)

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
export default function CatalogItem({ onCloseDrawer, elementVariants, groupKey }) {
  // ...

  const storage = StorageCookieConsent.getInstance()
  const [cookiesState, updateCookiesState] = useState(storage.get('cookiesState'))
  const [gaTrackingState, updateGaTrackingState] = useState(storage.get('gaTrackingState'))

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const { cookiesState: _c, gaTrackingState: _g } = event.data

      if (_c !== undefined && cookiesState !== _c) {
        updateCookiesState(_c)
      } else if (_g !== undefined && gaTrackingState !== _g) {
        updateGaTrackingState(_g)
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  })

  // ...
}
```
{% endtab %}
{% endtabs %}

There are a few more lines of code. However, by doing this way, I take all the responsibility for the changes in the storage and only update the component if the changes affect its behavior.

{% tabs %}
{% tab title="Before" %}
```typescript
export default function CatalogMenu() {
  // ...

  const {
    state: { gaTrackingState },
  } = useSubscription(cookieSubscription)

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
export default function CatalogMenu() {
  // ...

  const storage = StorageCookieConsent.getInstance()
  const [gaTrackingState, updateGaTrackingState] = useState(storage.get('gaTrackingState'))

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const { gaTrackingState: _g } = event.data

      if (_g !== undefined && gaTrackingState !== _g) {
        updateGaTrackingState(_g)
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  })

  // ...
}
```
{% endtab %}
{% endtabs %}

When a component calls the function `useSubscription` to subscribe to a global state without specifying a list of dependencies, every change in the global state will force the component to update its behavior. And because using a global state subscription is too easy, we usually forget to specify dependencies, which might cause the component to update itself when unnecessary. This behavior results in a not-good performance or even causes bugs to occur.

When using storage combined with custom events, we will need to proactively listen to changes that occur in storage and manually verify the changes for individual cases. Hence, mistakes will likely controlled better than using the global state subscription.

{% tabs %}
{% tab title="Before" %}
```typescript
export const OldPageAlert = () => {
  const {
    state: { gaTrackingState, cookiesState },
  } = useSubscription(cookieSubscription)

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
export const OldPageAlert = () => {
  const storage = StorageCookieConsent.getInstance()
  const [cookiesState, updateCookiesState] = useState(storage.get('cookiesState'))
  const [gaTrackingState, updateGaTrackingState] = useState(storage.get('gaTrackingState'))

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const { cookiesState: _c, gaTrackingState: _g } = event.data

      if (_c !== undefined && cookiesState !== _c) {
        updateCookiesState(_c)
      } else if (_g !== undefined && gaTrackingState !== _g) {
        updateGaTrackingState(_g)
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  })

  // ...
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Before" %}
```typescript
function Editor() {
  // ...

  const {
    state: { gaTrackingState, cookiesState },
  } = useSubscription(cookieSubscription)

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
function Editor() {
  // ...

  const storage = StorageCookieConsent.getInstance()
  const [cookiesState, updateCookiesState] = useState(storage.get('cookiesState'))
  const [gaTrackingState, updateGaTrackingState] = useState(storage.get('gaTrackingState'))

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const { cookiesState: _c, gaTrackingState: _g } = event.data

      if (_c !== undefined && cookiesState !== _c) {
        updateCookiesState(_c)
      } else if (_g !== undefined && gaTrackingState !== _g) {
        updateGaTrackingState(_g)
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  })

  // ...
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Before" %}
```typescript
export function CardFreeServices() {
  // ...

  const { crispTrackingState } = useCookiesConsent()

  const handleGetFeedBack = async () => {
    if (crispTrackingState) {
      openChat()
      window.$crisp.push(['set', 'message:text', ['Hi, I want to get feedback on my store ']])
      window.$crisp.push(['set', 'session:segments', [['pagereview']]])
      await updatePageFlyMeta({ popup_feedback: true }).catch(e => console.error(e))
    } else {
      openModal('FUNCTIONAL_MODAL')
    }
  }

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
export function CardFreeServices() {
  // ...

  const handleGetFeedBack = async () => {
    if (StorageCookieConsent.getInstance().get('crispTrackingState')) {
      openChat()
      window.$crisp.push(['set', 'message:text', ['Hi, I want to get feedback on my store ']])
      window.$crisp.push(['set', 'session:segments', [['pagereview']]])
      await updatePageFlyMeta({ popup_feedback: true }).catch(e => console.error(e))
    } else {
      openModal('FUNCTIONAL_MODAL')
    }
  }

  // ...
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Before" %}
```typescript
export function CookiesManagerModal({ action }) {
  // ...

  const {
    state: { gaTrackingState, cookiesState, crispTrackingState },
  } = useSubscription(cookieSubscription)

  const [disabled, setDisabled] = useState(true)
  const [tempCookiesState, setTempCookiesState] = useState({
    gaTrackingState: gaTrackingState,
    cookiesState: cookiesState,
    crispTrackingState: crispTrackingState,
  })

  useEffect(() => {
    setTempCookiesState({
      gaTrackingState: gaTrackingState,
      cookiesState: cookiesState,
      crispTrackingState: crispTrackingState,
    })
  }, [gaTrackingState, cookiesState, crispTrackingState])

  useEffect(() => {
    setDisabled(isEqual(tempCookiesState, { gaTrackingState, cookiesState, crispTrackingState }))
  }, [tempCookiesState])

  // ...
}
```
{% endtab %}

{% tab title="After" %}
```typescript
export function CookiesManagerModal({ action }) {
  // ...

  const [disabled, setDisabled] = useState(true)
  const storage = StorageCookieConsent.getInstance()

  const [tempCookiesState, setTempCookiesState] = useState({
    gaTrackingState: storage.get('gaTrackingState'),
    cookiesState: storage.get('cookiesState'),
    crispTrackingState: storage.get('crispTrackingState'),
  })

  useEffect(() => {
    function shouldUpdate(event: EventObject) {
      const newState = {}

      for (const prop in tempCookiesState) {
        const newValue = event.data[prop]

        if (newValue !== undefined && tempCookiesState[prop] !== newValue) {
          newState[prop] = newValue
        }
      }

      if (Object.keys(newState).length) {
        setTempCookiesState({ ...tempCookiesState, ...newState })
      }
    }

    Event.add(document.body, 'changeStorageCookieConsent', shouldUpdate)

    return () => Event.remove(document.body, 'changeStorageCookieConsent', shouldUpdate)
  }, [])

  useEffect(() => {
    const { gaTrackingState, cookiesState, crispTrackingState } = storage.get()
    setDisabled(isEqual(tempCookiesState, { gaTrackingState, cookiesState, crispTrackingState }))
  }, [tempCookiesState])

  // ...
}
```
{% endtab %}
{% endtabs %}

When changing storage containing a large amount of data, we can trigger multiple custom events to reduce the number of components affected by every change to as few as possible, which can prevent potential errors from spreading.

I recommend you checkout the commit ID `0880f3cb24` in the branch `cuongnm-refactoring-oop` of the repository `pfcore` to review the code changes.
