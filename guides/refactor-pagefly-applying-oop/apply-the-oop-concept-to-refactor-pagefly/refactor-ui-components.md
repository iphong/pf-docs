# Refactor UI components

Using the dynamic render mechanism, it will be better if we refactor the current UI components of PageFly from React functional components to component classes. This work aims to make UI components more encapsulated and independent. This behavior can optimize the loading trunk and help prevent failure from spreading from one UI component to another.

However, because the React functional component mechanism is simple and easy to create, it promotes the composition design pattern. So, stand-alone UI components that can composite with others to build a complete UI can be kept as is to save time and effort.

On the other hand, UI components that can be used as a base to build advanced UI components should be refactored from React functional components to component classes. The inheritance ability of the React component class mechanism can save us a lot of code duplication to process similar logic, render similar content, and handle similar behavior.

I've created the `Component` class that extends the native `PureComponent` class of React as the base for real-life UI components to build upon. Below is the interface of the base class.

```typescript
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

{% hint style="success" %}
UI components should _**extend**_ the `Component` class and _**override**_ the `render` method of the base class to display the appropriate content.
{% endhint %}

{% hint style="info" %}
A subclass can _**override**_ the following static properties to direct the `Component` class to initialize its behavior.

* `defaultProps` is for defining the default values for the component properties. The properties passed to the component when rendering will override the default values.
* `propsToState` directs the base class to auto-populate the component state from the properties passed to the component when rendering based on the defined mapping object assigned.
* `storageToState` directs the base class to auto-populate the component state from the specified storage. When a subclass uses this directive, it should always define a list of storage classes to populate the component state from for the `storages` key of the `defaultProps` property.
{% endhint %}

{% hint style="warning" %}
When a subclass overrides the `propsToState` property to customize its initial behavior, it _**should declare**_ the static method `getDerivedStateFromProps`. React will call this method to update the internal state of a component class according to changes in the properties passed to that component when rendering.

When executing the `getDerivedStateFromProps` method, React does not keep the original context of the method. Because of this behavior, the base class does not implement the static method `getDerivedStateFromProps` in its interface but requires declaring it in subclasses.
{% endhint %}

Below is an example of using the `propsToState` property and declaring the `getDerivedStateFromProps` method to auto-populate the component state from the passed properties when rendering.

```typescript
class InspectorControllerClass extends Component<InspectorControllerProps, InspectorControllerState> {
  static propsToState = {
    'contexts.InspectorContext': 'store',
    'contexts.ParameterDetail': 'parameterDetail',
  }

  state: InspectorControllerState = {
    store: null,
    parameterDetail: null,
  }

  static getDerivedStateFromProps(props, state) {
    return ExtObject.createByPathMapping(props, InspectorControllerClass.propsToState, state)
  }
}
```

{% hint style="success" %}
If a subclass overrides methods other than the `render` method of the `Component` class, it _**should manually call**_ the original methods using the `super` keyword for proper initialization, reactivation, and destruction.
{% endhint %}

Below is an interface of the refactored version of the UI component for rendering the cookie consent bar that demonstrates the use of the `super` keyword.

```typescript
export default class InspectorControl<P, S> extends Component<P & InspectorControlProps, S & InspectorControlState> {
  static contextType: Context<any> = PushParameterEvent

  // Define the default props.
  static defaultProps = {
    contexts: {},
    keyPath: 'data.value',
    storages: [StorageInspector],
  }

  // Define initial state.
  state: InspectorControlState = {}

  componentDidMount(): void {
    super.componentDidMount()

    // Populate the initial input value.
    const {
      value,
      keyPath,
      storage,
      contexts: { InspectorContext },
    } = this.props

    if (value !== undefined) {
      this.setState({ value })
    } else {
      this.setState({
        value: InspectorContext ? ExtObject.pathValue(InspectorContext, keyPath) : storage?.get(keyPath),
      })
    }
  }
}
```

{% hint style="info" %}
Currently, PageFly strongly relies on hooks and contexts to work as intended. So, I've created `adaptHooks` and `adaptContexts` functions as adapters to pass hooks and contexts to a React component class.
{% endhint %}

Below is a sample use of the `adaptHooks` function.

```typescript
class EditorWorkspaceClass extends Component<void, EditorState> {
  render(): ReactNode {
    return '...'
  }
}

const EditorWorkspace = adaptHooks(EditorWorkspaceClass, {
  // eslint-disable-next-line react-hooks/rules-of-hooks
  hotKeyWindow: () => useHotKey(window),
  // eslint-disable-next-line react-hooks/rules-of-hooks
  hotKeyEditor: () => useHotKey(editorWindow.current, true),
})
```

Below is a sample use of the `adaptContexts` function.

```typescript
      // Pass some legacy contexts when rendering inspector element.
      // @TODO: Should replace the use of context with storage?
      const RenderWithContexts = adaptContexts(Render, {
        ParameterDetail,
        InspectorContext,
        PushParameterEvent,
      })

      const control = createElement(RenderWithContexts, {
        ...this.props,
        preRenderPlaceholder: createElement(SkeletonDisplayText),
      })
```

{% hint style="success" %}
After creating a new UI component or refactoring an existing one, you need to define a mapping from the component name to its declaration file in the object `components` declared in the file `includes/loaders/components.ts`.
{% endhint %}
