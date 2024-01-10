# Refactor editor elements

To simplify the creation of page elements, I've created the `EditorElement` class as the ground for building page elements. It will automatically do necessary initialization when rendering a page element, such as subscribing to storage, applying style, etc. Below is the interface of the base component.

```javascript
export default class EditorElement<P, S> extends Component<P & EditorElementProps, S & EditorElementState> {
  // Define the default props.
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
```

When creating a new page element or refactoring existing page elements, you need to create a React component class that _**extends**_ the base `EditorElement` class and _**overrides**_ either the `renderElement` method or the `renderEdit` and `renderView` methods to display appropriate content.

If a subclass overrides either the `componentDidMount` or `componentWillUnmount` method of the base class, remember to use the `super` keyword to manually call the respective original method to ensure proper initialization, reactivation, and destruction.

Below is the code of the `Section` element after refactoring.

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

  static inspector = sectionInspectors

  state = {
    count: 0,
    backgroundColor: '',
    backgroundImage: '',
    showPlaceholder: true,
  }

  componentDidMount(): void {
    super.componentDidMount()
    this.shouldShowPlaceholder()
  }

  componentDidUpdate(prevProps: Readonly<{}>, prevState: Readonly<{}>, snapshot?: any): void {
    this.shouldShowPlaceholder()
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

An element class that extends the `EditorElement` class no longer needs to manually call the `useElementState` hook to update the component according to changes in the element state subscription. The base class will automatically do that work when rendering an element. This behavior helps reduce code duplication and also helps avoid bugs occurring because of missing initialization or wrong state.

I've created the new `RenderElement` component and renamed the existing `RenderElement` component to `RenderLegacyElement`. Similar to the `Render` component, `RenderElement` takes a page element name from the property `componentName` and will look for its declaration file in the mapping object `elements` declared in the file `modules/editor/includes/loaders/elements.ts` to import dynamically and will render the element after importing completes. If the value passed to the property `componentName` is a legacy page element that is a React function component, `RenderElement` will automatically use the `RenderLegacyElement` to render the page element.

In the current code base of PageFly, input controls that display on the inspector panel of page elements are defined in the inspector module and are always loaded regardless of whether the editor workspace has a related page element. This behavior causes the editor and the inspector module to depend on each other to work as intended. This behavior also causes the main code trunk of the editor screen to contain unnecessary code.

In the new structure, if a page element is customizable via the inspector panel, its component class must assign a list of input controls to the static property `inspector`. The base class `EditorElement` will automatically register the declared input controls of a page element at initialization after importing the component class. This new behavior helps reduce the size of the main code trunk and also helps separate the editor module from the inspector module to make them more _**independent**_.

Let's take the `Section` element above as an example of this new behavior. After refactoring the UI component of the `Section` element from a function component to a component class, I moved the file that defines inspector controls for the element from the inspector module to the editor module. Then, I removed the inspector controls definition of the `Section` element from the current list containing inspector controls of all page elements. Finally, I import the list of inspector controls belonging to the `Section` element and assign it to the static property `inspector` in the body of the component class.

By doing that, the inspector controls of the `Section` element will be loaded with the component class only when the editor workspace has the `Section` element. The base component `EditorElement` will automatically assign the declared inspector controls in the component class of the `Section` element to the list of inspector controls of all page elements.
