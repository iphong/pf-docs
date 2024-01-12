# Refactor UI components

According to the new structure, we will need to refactor the current components of PageFly, from React function components using hooks and global state subscriptions to component classes updating internal states based on events.

I've created the `Component` class that extends the native `PureComponent` class of React as the base for real-life UI components to build upon. Below is the interface of the base class.

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
Every UI component should _**extend**_ the `Component` class and _**override**_ the `render` method of the base class to display the appropriate content.
{% endhint %}

Below is the refactored version of the UI component that renders the dashboard screen for new users.

{% tabs %}
{% tab title="Legacy" %}
```javascript
export default function NewUserDashboardContent() {
  return (
    <VerticalStack gap={'4'}>
      <OnBoardingTasksCard />
      <LazyComponent component={'LazyNewUserDashboardContent'} />
    </VerticalStack>
  )
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export default class ScreenDashboardNewUser extends Component<void, void> {
  render(): ReactNode {
    return (
      <VerticalStack gap={'4'}>
        <Render componentName="ScreenDashboardOnboardingTasks" />
        <LazyComponent component={'LazyNewUserDashboardContent'} />
      </VerticalStack>
    )
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
A subclass can _**override**_ the following static properties to direct the `Component` class to initialize its behavior.

* `defaultProps` is for defining the default values for the component properties. The properties passed to the component when rendering will override the default values.
* `propsToState` directs the base class to auto-populate the component state from the properties passed to the component when rendering based on the defined mapping object assigned.
* `storageToState` directs the base class to auto-populate the component state from the specified storage. When a subclass uses this directive, it should always define a list of storage classes to populate the component state from for the `storages` key of the `defaultProps` property.
{% endhint %}

{% hint style="success" %}
When a subclass overrides the `propsToState` property to customize its initial behavior, it _**should declare**_ the static method `getDerivedStateFromProps`. React will call this method to update the internal state of a component class according to changes in the properties passed to that component when rendering.

However, when executing the `getDerivedStateFromProps` method, React does not keep the original context of the method. Because of this behavior, the base class does not implement the static method `getDerivedStateFromProps` in its interface but requires declaring it in subclasses.
{% endhint %}

Below is an example of using the `propsToState` property and declaring the `getDerivedStateFromProps` method to auto-populate the component state from the passed properties when rendering.

```javascript
class ComponentCookieConsentBarClass extends Component<ComponentCookieConsentBarProps, ComponentCookieConsentBarState> {
  // Map component props to state.
  static propsToState: StringMapping = {
    'hooks.cookieConsent.cookiesState': 'cookiesState',
    'hooks.cookieConsent.gaTrackingState': 'gaTrackingState',
  }

  static getDerivedStateFromProps(props, state) {
    return ExtObject.createByPathMapping(props, ComponentCookieConsentBarClass.propsToState, state)
  }
}
```

{% hint style="success" %}
If a subclass overrides methods other than the `render` method of the `Component` class, it should manually call the original methods using the `super` keyword for proper initialization, reactivation, and destruction.
{% endhint %}

Below is an interface of the refactored version of the UI component for rendering the cookie consent bar that demonstrates the use of the `super` keyword.

{% tabs %}
{% tab title="Legacy" %}
```javascript
const CookieBar = () => {
  const { setState, acceptCookies, acceptCrisp, acceptGATracking, gaTrackingState, cookiesState } = useCookiesConsent()

  const { t } = useTranslation()
  const [isExpand, setIsExpand] = useState(false)
  const [activeToast, setActiveToast] = useState(false)
  const toggleActiveToast = useCallback(() => setActiveToast(activeToast => !activeToast), [])
  const toastMarkup = activeToast ? <Toast content={t('SETTINGS_SAVED')} onDismiss={toggleActiveToast} /> : null
  const { mdUp, mdDown } = useBreakpoints()
  const { openModal } = useModal()

  useEffect(() => {
    setState({
      gaTrackingState: acceptGATracking,
      cookiesState: acceptCookies,
      crispTrackingState: acceptCrisp,
    })
  }, [])

  const acceptGA = () => {}

  useEffect(() => {
    const cookiesBar = document.querySelector('.Consent-Banner') || null
    if (cookiesBar) {
      const observer = new ResizeObserver(() => {
        const cookiesBarHeight = cookiesBar?.getBoundingClientRect().height || 0
        updateStyleAttribute(document.body, '--cookie-bar', `${cookiesBarHeight}px`)
      })
      observer.observe(cookiesBar)
      const cookiesBarHeight = cookiesBar?.getBoundingClientRect().height || 0
      updateStyleAttribute(document.body, '--cookie-bar', `${cookiesBarHeight}px`)

      return () => {
        observer.unobserve(cookiesBar)
      }
    }
    updateStyleAttribute(document.body, '--cookie-bar', `0px`)
  }, [cookiesState, gaTrackingState])

  if (cookiesState === null || gaTrackingState === null) return null

  return '...'
}

```
{% endtab %}

{% tab title="Refactored" %}
```javascript
class ComponentCookieConsentBarClass extends Component<ComponentCookieConsentBarProps, ComponentCookieConsentBarState> {
  // Map component props to state.
  static propsToState: StringMapping = {
    'hooks.cookieConsent.cookiesState': 'cookiesState',
    'hooks.cookieConsent.gaTrackingState': 'gaTrackingState',
  }

  // Define initial state.
  state = {
    isExpand: false,
    activeToast: false,
    cookiesState: null,
    gaTrackingState: null,
  }

  // Cookies bar HTML element.
  private cookiesBar

  // Observer that handles resize action on viewport.
  private observer

  static getDerivedStateFromProps(props, state) {
    return ExtObject.createByPathMapping(props, ComponentCookieConsentBarClass.propsToState, state)
  }

  toggleActiveToast = () => this.setState({ activeToast: !this.state.activeToast })

  updateBodyHeight = () => {
    const reservedHeight = this.cookiesBar?.getBoundingClientRect().height || 0
    updateStyleAttribute(document.body, '--cookie-bar', `${reservedHeight}px`)
  }

  addObserver = () => {
    if (!this.observer && this.cookiesBar) {
      this.observer = new ResizeObserver(this.updateBodyHeight)
      this.observer.observe(this.cookiesBar)
    }
  }

  removeObserver = () => {
    if (this.observer && this.cookiesBar) {
      this.observer.unobserve(this.cookiesBar)
      this.observer = null
    }
  }

  componentDidMount(): void {
    this.addObserver()
    super.componentDidMount()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<ComponentCookieConsentBarState>): void {
    // Get current state.
    const { cookiesState, gaTrackingState } = this.state

    if (cookiesState !== prevState.cookiesState || gaTrackingState !== prevState.gaTrackingState) {
      this.cookiesBar = document.querySelector('.Consent-Banner')

      if (this.cookiesBar) {
        this.addObserver()
      } else {
        this.removeObserver()
      }

      this.updateBodyHeight()
    }
  }

  componentWillUnmount(): void {
    this.removeObserver()
    super.componentWillUnmount()
  }

  render(): ReactNode {
    // Get current state.
    const { isExpand, activeToast } = this.state

    // Extract necessary props.
    const {
      hooks: {
        translation: { t },
        modal: { openModal },
        breakpoints: { mdUp, mdDown },
        cookieConsent: { gaTrackingState, cookiesState },
      },
    } = this.props

    return '...'
  }
}

const ComponentCookieConsentBar = adaptHooks(ComponentCookieConsentBarClass, {
  modal: useModal,
  breakpoints: useBreakpoints,
  translation: useTranslation,
  cookieConsent: useCookiesConsent,
})

export default ComponentCookieConsentBar
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Currently, PageFly strongly relies on hooks and contexts to work as intended. So, I've created `adaptHooks` and `adaptContexts` functions as adapters to pass hooks and contexts to a React component class.
{% endhint %}

In the refactored code above, the `ComponentCookieConsentBar` is created by calling the `adaptHooks` function to pass the results of the `useModal`, `useBreakpoints`, `useTranslation`, and `useCookieConsent` hooks to the component class.

Below is a sample use of the `adaptContexts` function.

```javascript
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
