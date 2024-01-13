# Refactor the editor module

To simplify the creation of page elements, I've created the `EditorElement` class as the ground for building page elements. It will automatically do necessary initialization when rendering a page element, such as subscribing to storage, applying style, etc. Below is the interface of the base component.

<pre class="language-javascript"><code class="lang-javascript"><strong>export default class EditorElement&#x3C;P, S> extends Component&#x3C;P &#x26; EditorElementProps, S &#x26; EditorElementState> {
</strong>  // Define the default props.
  static defaultProps = {
    storages: [StorageEditor],
  }

  // Define inspector controls to customize the page element for real life use.
  static inspector = []

  // Define initial state.
  state = { count: 0 }

  // Editor storage instance.
  editorStorage: StorageEditorInstance = null

  // Reference to data store created by the `useElementStore` hook.
  store: any = null

  // Element store reference.
  elementStore: StorageEditorElementInstance = null

  // Element state subscription reference.
  elementState: StorageEditorElementStateInstance = null

  // Getter method to get the current editor mode.
  get mode() => 'edit' | 'view'

  // Getter method to get the type of editor element.
  get type() => string

  // Getter method to get enhanced component props.
  get enhancedProps() => any

  componentDidMount() => void

  componentWillUnmount() => void

  // Render the editor element wrapped inside a QueryClientProvider component.
  render() => ReactNode

  // Render the editor element depending on the current mode.
  renderElement() => ReactNode

  // Render the element in edit mode.
  renderEdit() => ReactNode

  // Render the element in view mode.
  renderView() => ReactNode

  // Method to apply initial style for rendered element.
  applyElementStyle() => void

  handleStorageChange(storageName: string, data: any) => void
}
</code></pre>

{% hint style="success" %}
When creating a new page element or refactoring existing page elements, you need to create a new class that _**extends**_ the `EditorElement` class and _**overrides**_ either the `renderElement` method or both the `renderEdit` and `renderView` methods to display the appropriate content.
{% endhint %}

Below is the refactored version of the `Body` element.

{% tabs %}
{% tab title="Legacy" %}
```javascript
const Div = styled.div``

export default function Body({ children, ...rest }: IPFElementProps) {
  return <Div>{children}</Div>
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
const StyledDiv = styled.div``

export default class EditorElementBody extends EditorElement<void, void> {
  renderElement(): ReactNode {
    return <StyledDiv {...this.enhancedProps}>{this.props.children}</StyledDiv>
  }
}
```
{% endtab %}
{% endtabs %}

Let's refactor the `Section` element, which is more advanced than the `Body` element. Below is the current code of the `Section` element.

```javascript
interface SectionProps extends IPFElementProps {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
  const {
    container,
    containerWidth,
    bgType,
    videoBg,
    parallaxBg,
    parallaxSpeed,
    filterColor,
    store,
    children,
    store: { type, mode },
  } = props
  const containerStyle = container
    ? { [`--cw` as any]: isNaN(containerWidth) ? containerWidth : `${containerWidth}px` }
    : undefined
  const overlayStyle =
    filterColor && filterColor !== 'rgba(0,0,0,0)' ? { [`--overlay` as any]: filterColor } : undefined
  const styleStickyPage: any = mode === 'edit' ? { position: 'relative', top: 'initial', zIndex: 'initial' } : {}
  const [showPlaceholder, setShowPlaceholder] = useState(true)
  useEffect(() => {
    setTimeout(() => {
      const shouldNotRenderPlaceholder =
        store.mode === 'view' ||
        children.length !== 0 ||
        store.styleStore.currentStyle.backgroundColor !== '' ||
        store.styleStore.currentStyle.backgroundImage !== ''

      setShowPlaceholder(!shouldNotRenderPlaceholder)
    }, 300)
  })

  useElementState(store.elementStore, ['backgroundColor', 'backgroundImage'])

  function renderPlaceholder() {
    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${store.id.split('-')[1]}`}
        style={store.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        className={store.mode === 'edit' ? 'pf-editor-section' : ''}
      >
        <Background bgType={bgType} videoBg={videoBg} parallaxBg={parallaxBg} filterColor={filterColor} mode={mode} />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && mode === 'edit' ? (
          showPlaceholder && <LayoutPlaceholder {...props} />
        ) : (
          <PlaceholderLayout type={type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }

  return children.length ? (
    <StyledSection
      data-parallax={bgType === 'parallax' || undefined}
      data-parallax-speed={bgType === 'parallax' && mode === 'view' && parallaxSpeed ? parallaxSpeed : undefined}
      style={{ ...overlayStyle, ...styleStickyPage }}
      data-section-id={`pf-${store.id.split('-')[1]}`}
    >
      <Background bgType={bgType} videoBg={videoBg} parallaxBg={parallaxBg} filterColor={filterColor} mode={mode} />
      {overlayStyle && <StyledOverlay />}
      <Container style={containerStyle}>{children}</Container>
    </StyledSection>
  ) : (
    renderPlaceholder()
  )
}
```

First, create a new file named `index.tsx` under the folder `modules/editor/elements/section` to recreate the `Section` element according to the new structure.

There is no need to change element properties, so copy and paste them into the new file. Below is the initial declaration in the new file.

{% tabs %}
{% tab title="Legacy" %}
```javascript
interface SectionProps extends IPFElementProps {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export type EditorElementSectionProps = EditorElementProps & {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

export default class EditorElementSection extends EditorElement<EditorElementSectionProps> {
  static defaultProps = {
    container: true,
    containerWidth: 1170,
    parallax: false,
    parallaxBg: '',
    parallaxSpeed: 4,
    parallaxRev: false,
    src: '',
    videoBg: '',
    bgType: 'standard',
    sectionName: '',
    filterColor: 'rgba(0,0,0,0)',
    name: t('SECTION'),
    // Subclass must include default props from the base class.
    ...EditorElement.defaultProps,
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Class declaration of every page element _**must include**_ default props from the `EditorElement` class when defining the default props of that element. This action ensures a proper initialization and reactivation when rendering the page element.
{% endhint %}

In the current function component of the `Section` element, three states control the behavior of the page element, which are `showPlaceholder`, `backgroundColor`, and `backgroundImage`. The function component creates the `showPlaceholder` state using the `useState` function. Then, it calls the `useElementState` function to refresh itself when either the `backgroundColor` or `backgroundImage` state changes in the element state subscription. Let's declare these states in the new component class.

{% tabs %}
{% tab title="Legacy" %}
```javascript
interface SectionProps extends IPFElementProps {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
  const {
    container,
    containerWidth,
    bgType,
    videoBg,
    parallaxBg,
    parallaxSpeed,
    filterColor,
    store,
    children,
    store: { type, mode },
  } = props

  const [showPlaceholder, setShowPlaceholder] = useState(true)

  useElementState(store.elementStore, ['backgroundColor', 'backgroundImage'])
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export type EditorElementSectionProps = EditorElementProps & {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

export type EditorElementSectionState = EditorElementState & {
  backgroundColor: string
  backgroundImage: string
  showPlaceholder: boolean
}

export default class EditorElementSection extends EditorElement<EditorElementSectionProps, EditorElementSectionState> {
  static defaultProps = {
    container: true,
    containerWidth: 1170,
    parallax: false,
    parallaxBg: '',
    parallaxSpeed: 4,
    parallaxRev: false,
    src: '',
    videoBg: '',
    bgType: 'standard',
    sectionName: '',
    filterColor: 'rgba(0,0,0,0)',
    name: t('SECTION'),
    // Subclass must include default props from the base class.
    ...EditorElement.defaultProps,
  }

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }
}
```
{% endtab %}
{% endtabs %}

As you can see, component classes of page elements no longer need to manually call the `useElementState` hook to update the component according to changes in the element state subscription. The base class will automatically compare the component's internal state with the data from the element state subscription to decide whether the component should update itself. This behavior helps reduce code duplication and also helps avoid bugs occurring because of missing initialization or wrong state.

Now, we will convert the use of the `useEffect` hooks to the equivalent class methods.

{% tabs %}
{% tab title="Legacy" %}
```javascript
interface SectionProps extends IPFElementProps {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
  const {
    container,
    containerWidth,
    bgType,
    videoBg,
    parallaxBg,
    parallaxSpeed,
    filterColor,
    store,
    children,
    store: { type, mode },
  } = props

  const [showPlaceholder, setShowPlaceholder] = useState(true)

  useEffect(() => {
    setTimeout(() => {
      const shouldNotRenderPlaceholder =
        store.mode === 'view' ||
        children.length !== 0 ||
        store.styleStore.currentStyle.backgroundColor !== '' ||
        store.styleStore.currentStyle.backgroundImage !== ''

      setShowPlaceholder(!shouldNotRenderPlaceholder)
    }, 300)
  })

  useElementState(store.elementStore, ['backgroundColor', 'backgroundImage'])
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export type EditorElementSectionProps = EditorElementProps & {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

export type EditorElementSectionState = EditorElementState & {
  backgroundColor: string
  backgroundImage: string
  showPlaceholder: boolean
}

export default class EditorElementSection extends EditorElement<EditorElementSectionProps, EditorElementSectionState> {
  static defaultProps = {
    container: true,
    containerWidth: 1170,
    parallax: false,
    parallaxBg: '',
    parallaxSpeed: 4,
    parallaxRev: false,
    src: '',
    videoBg: '',
    bgType: 'standard',
    sectionName: '',
    filterColor: 'rgba(0,0,0,0)',
    name: t('SECTION'),
    // Subclass must include default props from the base class.
    ...EditorElement.defaultProps,
  }

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }

  shouldShowPlaceholder() {
    const dontShowPlaceholder =
      this.mode === 'view' ||
      this.enhancedProps.children.length !== 0 ||
      this.store.styleStore.currentStyle.backgroundColor !== '' ||
      this.store.styleStore.currentStyle.backgroundImage !== ''

    if (this.state.showPlaceholder !== !dontShowPlaceholder) {
      this.setState({ showPlaceholder: !dontShowPlaceholder })
    }
  }

  componentDidMount(): void {
    super.componentDidMount()
    this.shouldShowPlaceholder()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<{}>, snapshot?: any): void {
    this.shouldShowPlaceholder()
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
If a subclass overrides either the `componentDidMount` or `componentWillUnmount` method of the base class, remember to use the `super` keyword to _**manually call**_ the respective original method to ensure proper initialization, reactivation, and destruction.
{% endhint %}

If the legacy function component declares nested functions, we need to move these nested functions to class methods. The current code of the `Section` element has a nested function named `renderPlaceholder`. Let's move it to a method of the new component class.

{% tabs %}
{% tab title="Legacy" %}
```javascript
interface SectionProps extends IPFElementProps {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
  const {
    container,
    containerWidth,
    bgType,
    videoBg,
    parallaxBg,
    parallaxSpeed,
    filterColor,
    store,
    children,
    store: { type, mode },
  } = props

  const [showPlaceholder, setShowPlaceholder] = useState(true)

  useEffect(() => {
    setTimeout(() => {
      const shouldNotRenderPlaceholder =
        store.mode === 'view' ||
        children.length !== 0 ||
        store.styleStore.currentStyle.backgroundColor !== '' ||
        store.styleStore.currentStyle.backgroundImage !== ''

      setShowPlaceholder(!shouldNotRenderPlaceholder)
    }, 300)
  })

  useElementState(store.elementStore, ['backgroundColor', 'backgroundImage'])

  function renderPlaceholder() {
    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${store.id.split('-')[1]}`}
        style={store.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        className={store.mode === 'edit' ? 'pf-editor-section' : ''}
      >
        <Background bgType={bgType} videoBg={videoBg} parallaxBg={parallaxBg} filterColor={filterColor} mode={mode} />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && mode === 'edit' ? (
          showPlaceholder && <LayoutPlaceholder {...props} />
        ) : (
          <PlaceholderLayout type={type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export type EditorElementSectionProps = EditorElementProps & {
  container: boolean
  containerWidth: number
  parallax: boolean
  parallaxBg: string
  parallaxSpeed: number
  parallaxRev: boolean
  src: string
  sectionName: string
  bgType: string
  videoBg: string
  filterColor: string
  mode?: string
}

export type EditorElementSectionState = EditorElementState & {
  backgroundColor: string
  backgroundImage: string
  showPlaceholder: boolean
}

export default class EditorElementSection extends EditorElement<EditorElementSectionProps, EditorElementSectionState> {
  static defaultProps = {
    container: true,
    containerWidth: 1170,
    parallax: false,
    parallaxBg: '',
    parallaxSpeed: 4,
    parallaxRev: false,
    src: '',
    videoBg: '',
    bgType: 'standard',
    sectionName: '',
    filterColor: 'rgba(0,0,0,0)',
    name: t('SECTION'),
    // Subclass must include default props from the base class.
    ...EditorElement.defaultProps,
  }

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }

  shouldShowPlaceholder() {
    const dontShowPlaceholder =
      this.mode === 'view' ||
      this.enhancedProps.children.length !== 0 ||
      this.store.styleStore.currentStyle.backgroundColor !== '' ||
      this.store.styleStore.currentStyle.backgroundImage !== ''

    if (this.state.showPlaceholder !== !dontShowPlaceholder) {
      this.setState({ showPlaceholder: !dontShowPlaceholder })
    }
  }

  componentDidMount(): void {
    super.componentDidMount()
    this.shouldShowPlaceholder()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<{}>, snapshot?: any): void {
    this.shouldShowPlaceholder()
  }

  renderPlaceholder() {
    const { bgType, videoBg, parallaxBg, filterColor } = this.enhancedProps

    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${this.store.id.split('-')[1]}`}
        className={this.mode === 'edit' ? 'pf-editor-section' : ''}
        style={this.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        {...this.enhancedProps}
      >
        <Background
          bgType={bgType}
          mode={this.mode}
          videoBg={videoBg}
          parallaxBg={parallaxBg}
          filterColor={filterColor}
        />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && this.mode === 'edit' ? (
          this.state.showPlaceholder && <LayoutPlaceholder {...this.enhancedProps} />
        ) : (
          <PlaceholderLayout type={this.type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }
}
```
{% endtab %}
{% endtabs %}

It's time to finalize the refactor work by moving the remaining code in the function component to the `renderElement` method of the class component.

{% tabs %}
{% tab title="Legacy" %}
```javascript
Section.defaultProps = {
  container: true,
  containerWidth: 1170,
  parallax: false,
  parallaxBg: '',
  parallaxSpeed: 4,
  parallaxRev: false,
  src: '',
  videoBg: '',
  bgType: 'standard',
  sectionName: '',
  filterColor: 'rgba(0,0,0,0)',
  name: t('SECTION'),
}

export default function Section(props: SectionProps) {
  const {
    container,
    containerWidth,
    bgType,
    videoBg,
    parallaxBg,
    parallaxSpeed,
    filterColor,
    store,
    children,
    store: { type, mode },
  } = props
  const containerStyle = container
    ? { [`--cw` as any]: isNaN(containerWidth) ? containerWidth : `${containerWidth}px` }
    : undefined
  const overlayStyle =
    filterColor && filterColor !== 'rgba(0,0,0,0)' ? { [`--overlay` as any]: filterColor } : undefined
  const styleStickyPage: any = mode === 'edit' ? { position: 'relative', top: 'initial', zIndex: 'initial' } : {}
  const [showPlaceholder, setShowPlaceholder] = useState(true)
  useEffect(() => {
    setTimeout(() => {
      const shouldNotRenderPlaceholder =
        store.mode === 'view' ||
        children.length !== 0 ||
        store.styleStore.currentStyle.backgroundColor !== '' ||
        store.styleStore.currentStyle.backgroundImage !== ''

      setShowPlaceholder(!shouldNotRenderPlaceholder)
    }, 300)
  })

  useElementState(store.elementStore, ['backgroundColor', 'backgroundImage'])

  function renderPlaceholder() {
    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${store.id.split('-')[1]}`}
        style={store.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        className={store.mode === 'edit' ? 'pf-editor-section' : ''}
      >
        <Background bgType={bgType} videoBg={videoBg} parallaxBg={parallaxBg} filterColor={filterColor} mode={mode} />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && mode === 'edit' ? (
          showPlaceholder && <LayoutPlaceholder {...props} />
        ) : (
          <PlaceholderLayout type={type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }

  return children.length ? (
    <StyledSection
      data-parallax={bgType === 'parallax' || undefined}
      data-parallax-speed={bgType === 'parallax' && mode === 'view' && parallaxSpeed ? parallaxSpeed : undefined}
      style={{ ...overlayStyle, ...styleStickyPage }}
      data-section-id={`pf-${store.id.split('-')[1]}`}
    >
      <Background bgType={bgType} videoBg={videoBg} parallaxBg={parallaxBg} filterColor={filterColor} mode={mode} />
      {overlayStyle && <StyledOverlay />}
      <Container style={containerStyle}>{children}</Container>
    </StyledSection>
  ) : (
    renderPlaceholder()
  )
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export default class EditorElementSection extends EditorElement<EditorElementSectionProps, EditorElementSectionState> {
  static defaultProps = {
    src: '',
    videoBg: '',
    parallaxBg: '',
    container: true,
    parallax: false,
    sectionName: '',
    parallaxSpeed: 4,
    name: t('SECTION'),
    bgType: 'standard',
    parallaxRev: false,
    containerWidth: 1170,
    filterColor: 'rgba(0,0,0,0)',
    // Subclasses must include the `defaultProps` from the base class.
    ...EditorElement.defaultProps,
  }

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }

  shouldShowPlaceholder() {
    const dontShowPlaceholder =
      this.mode === 'view' ||
      this.enhancedProps.children.length !== 0 ||
      this.store.styleStore.currentStyle.backgroundColor !== '' ||
      this.store.styleStore.currentStyle.backgroundImage !== ''

    if (this.state.showPlaceholder !== !dontShowPlaceholder) {
      this.setState({ showPlaceholder: !dontShowPlaceholder })
    }
  }

  componentDidMount(): void {
    super.componentDidMount()
    this.shouldShowPlaceholder()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<{}>, snapshot?: any): void {
    this.shouldShowPlaceholder()
  }

  renderPlaceholder() {
    const { bgType, videoBg, parallaxBg, filterColor } = this.enhancedProps

    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${this.store.id.split('-')[1]}`}
        className={this.mode === 'edit' ? 'pf-editor-section' : ''}
        style={this.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        {...this.enhancedProps}
      >
        <Background
          bgType={bgType}
          mode={this.mode}
          videoBg={videoBg}
          parallaxBg={parallaxBg}
          filterColor={filterColor}
        />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && this.mode === 'edit' ? (
          this.state.showPlaceholder && <LayoutPlaceholder {...this.enhancedProps} />
        ) : (
          <PlaceholderLayout type={this.type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }

  renderElement(): React.ReactNode {
    const { store, bgType, videoBg, children, container, parallaxBg, filterColor, parallaxSpeed, containerWidth } = this.enhancedProps

    if (!children.length) {
      return this.renderPlaceholder()
    }

    const containerStyle = container
      ? { [`--cw` as any]: isNaN(containerWidth) ? containerWidth : `${containerWidth}px` }
      : undefined

    const overlayStyle =
      filterColor && filterColor !== 'rgba(0,0,0,0)' ? { [`--overlay` as any]: filterColor } : undefined

    const styleStickyPage: any = this.mode === 'edit' ? { position: 'relative', top: 'initial', zIndex: 'initial' } : {}

    const parallaxSpeedProp = bgType === 'parallax' && this.mode === 'view' && parallaxSpeed ? parallaxSpeed : undefined

    return (
      <StyledSection
        data-parallax-speed={parallaxSpeedProp}
        style={{ ...overlayStyle, ...styleStickyPage }}
        data-section-id={`pf-${store.id.split('-')[1]}`}
        data-parallax={bgType === 'parallax' || undefined}
        {...this.enhancedProps}
      >
        <Background
          bgType={bgType}
          mode={this.mode}
          videoBg={videoBg}
          parallaxBg={parallaxBg}
          filterColor={filterColor}
        />
        {overlayStyle && <StyledOverlay />}
        <Container style={containerStyle}>{children}</Container>
      </StyledSection>
    )
  }
}
```
{% endtab %}
{% endtabs %}

In the current code base of PageFly, input controls that display on the inspector panel of page elements are defined in the inspector module. They are always loaded regardless of whether the editor workspace has a related page element. This behavior causes the editor and the inspector module to depend on each other to work as intended. This behavior also causes the main code trunk of the editor screen to contain unnecessary code.

{% hint style="success" %}
In the new structure, if a page element is customizable via the inspector panel, its component class _**must assign**_ a list of input controls to the static property `inspector`. The base class `EditorElement` will automatically register the declared input controls of a page element at initialization after importing the component class. This new behavior helps reduce the size of the main code trunk and also helps separate the editor module from the inspector module to make them more _**independent**_.
{% endhint %}

Let's take the `Section` element above as an example of this new behavior. After refactoring the UI component of the `Section` element from a function component to a component class, I moved the file that defines inspector controls for the element from the inspector module to the editor module. Then, I removed the inspector control definition of the `Section` element from the current list containing inspector controls of all page elements defined in the file `modules/inspector/group.ts`. Finally, I import the list of inspector controls belonging to the `Section` element and assign it to the static property `inspector` in the body of the component class.

Below is the final version of the component class of the page element `Section`.

```javascript
export default class EditorElementSection extends EditorElement<EditorElementSectionProps, EditorElementSectionState> {
  static inspector = sectionInspectors

  static defaultProps = {
    src: '',
    videoBg: '',
    parallaxBg: '',
    container: true,
    parallax: false,
    sectionName: '',
    parallaxSpeed: 4,
    name: t('SECTION'),
    bgType: 'standard',
    parallaxRev: false,
    containerWidth: 1170,
    filterColor: 'rgba(0,0,0,0)',
    // Subclasses must include the `defaultProps` from the base class.
    ...EditorElement.defaultProps,
  }

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }

  shouldShowPlaceholder() {
    const dontShowPlaceholder =
      this.mode === 'view' ||
      this.enhancedProps.children.length !== 0 ||
      this.store.styleStore.currentStyle.backgroundColor !== '' ||
      this.store.styleStore.currentStyle.backgroundImage !== ''

    if (this.state.showPlaceholder !== !dontShowPlaceholder) {
      this.setState({ showPlaceholder: !dontShowPlaceholder })
    }
  }

  componentDidMount(): void {
    super.componentDidMount()
    this.shouldShowPlaceholder()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<{}>, snapshot?: any): void {
    this.shouldShowPlaceholder()
  }

  renderPlaceholder() {
    const { bgType, videoBg, parallaxBg, filterColor } = this.enhancedProps

    return (
      <StyledSection
        data-element-placeholder
        data-parallax={bgType === 'parallax'}
        data-section-id={`pf-${this.store.id.split('-')[1]}`}
        className={this.mode === 'edit' ? 'pf-editor-section' : ''}
        style={this.mode === 'edit' ? { position: 'relative', minHeight: 50 } : {}}
        {...this.enhancedProps}
      >
        <Background
          bgType={bgType}
          mode={this.mode}
          videoBg={videoBg}
          parallaxBg={parallaxBg}
          filterColor={filterColor}
        />
        {isSectionEditor() && !templateSelectedSubscription.state.preview && this.mode === 'edit' ? (
          this.state.showPlaceholder && <LayoutPlaceholder {...this.enhancedProps} />
        ) : (
          <PlaceholderLayout type={this.type} outline={true} name={t('SECTION')} />
        )}
      </StyledSection>
    )
  }

  renderElement(): React.ReactNode {
    const { store, bgType, videoBg, children, container, parallaxBg, filterColor, parallaxSpeed, containerWidth } =
      this.enhancedProps

    if (!children.length) {
      return this.renderPlaceholder()
    }

    const containerStyle = container
      ? { [`--cw` as any]: isNaN(containerWidth) ? containerWidth : `${containerWidth}px` }
      : undefined

    const overlayStyle =
      filterColor && filterColor !== 'rgba(0,0,0,0)' ? { [`--overlay` as any]: filterColor } : undefined

    const styleStickyPage: any = this.mode === 'edit' ? { position: 'relative', top: 'initial', zIndex: 'initial' } : {}

    const parallaxSpeedProp = bgType === 'parallax' && this.mode === 'view' && parallaxSpeed ? parallaxSpeed : undefined

    return (
      <StyledSection
        data-parallax-speed={parallaxSpeedProp}
        style={{ ...overlayStyle, ...styleStickyPage }}
        data-section-id={`pf-${store.id.split('-')[1]}`}
        data-parallax={bgType === 'parallax' || undefined}
        {...this.enhancedProps}
      >
        <Background
          bgType={bgType}
          mode={this.mode}
          videoBg={videoBg}
          parallaxBg={parallaxBg}
          filterColor={filterColor}
        />
        {overlayStyle && <StyledOverlay />}
        <Container style={containerStyle}>{children}</Container>
      </StyledSection>
    )
  }
}
```

By doing that, the inspector controls of the `Section` element will be loaded with the component class only when the editor workspace has the `Section` element. The base component `EditorElement` will automatically assign the declared inspector controls in the component class of the `Section` element to the list of inspector controls of all page elements.

To support dynamically rendering page elements, I've created a new `RenderElement` component and renamed the existing `RenderElement` component to `RenderLegacyElement`. The new `RenderElement` component takes a page element name from the property `componentName` and will look for its declaration file in the object `elements` declared in the file `modules/editor/includes/loaders/elements.ts` to import dynamically and render the element after importing completes. If the value passed to the property `componentName` is a legacy page element that is a React function component, `RenderElement` will automatically use the `RenderLegacyElement` to render the page element.

{% hint style="success" %}
After creating a new element or refactoring an existing one, you need to define a mapping from the page element name to its declaration file in the object `elements` declared in the file `modules/editor/includes/loaders/elements.ts` and remove the old component declaration from the list of element components defined in the file `elements/index.tsx`.
{% endhint %}
