# Refactor the inspector module

The current inspector module in the code base of PageFly contains code to process logic related to the editor module and uses assets belonging to the editor module. This situation ensures the inspector module works as intended with the editor module in the page editor context. However, this behavior also makes using the inspector module outside the page editor context becomes difficult because the module is not independent.

I've created two new React components that help make the inspector module more independent after refactoring. The `RenderControl` component supports flexibly rendering input controls, and the `InspectorControl` component is the base class for building independent and fully reusable input controls.

{% hint style="info" %}
The `RenderControl` component can take a custom React component from the `InspectorController` property and use it to render an input control. This characteristic supports rendering advanced input controls in specific use cases, such as inside the page editor context.
{% endhint %}

I've refactored and moved the file that declares the current `InspectorController` component from the inspector module to the editor module because it contains code to process logic related to the editor module. Below is the code of the `InspectorController` component after refactoring.

{% tabs %}
{% tab title="Legacy" %}
```javascript
export default function InspectorController(props: InspectorControllerProps) {
  const { t } = useTranslation()
  const {
    label,
    children,
    device = true,
    tooltip,
    showReset,
    disableReset,
    onResetValue,
    elementStore,
    styleKey,
    compareWithGlobalStyles,
    inline = false,
    helpText = '',
    helpTextOptions = {},
  } = props
  const styleKeys = Array.isArray(styleKey) ? styleKey : [styleKey].filter(key => !!key)
  const store = useContext(InspectorContext)

  const classGlobalStyling = elementStore?.data?.classGlobalStyling
  let globalStyles: any = {},
    currentStyles: any = {}

  if (elementStore && styleKeys.length && classGlobalStyling) {
    globalStyles = elementStore?.styleStore?.getGlobalStyle(`.__pf .${classGlobalStyling}`)
    currentStyles = elementStore?.styleStore?.getCurrentStyle()
  }

  const diff = globalStyles.length ? compareGlobalStylesWithCurrentStyles(globalStyles, currentStyles) : []
  const showIcon = styleKeys.some(k => globalStyles && !!globalStyles[k])
  const stylesModified =
    styleKeys.some(k => diff.includes(k) && globalStyles && !!globalStyles[k]) ||
    styleKeys.some(k => elementStore?.styleStore?.getCurrentStyle()[k])
  const displayLabel = typeof label === 'string' && t(label)

  const handleResetValue = () => {
    onResetValue && onResetValue()
    // If styleKeys include general keys such as padding, margin,...,
    // We need to reset all of the other keys except the general keys
    const properties = Object.keys(BOX_MODEL_PROPERTIES)
    const generalKey = styleKeys.find(key => properties.includes(key))
    if (generalKey) {
      elementStore?.styleStore?.updateStyle({
        ...BOX_MODEL_PROPERTIES[generalKey].styleKeys.reduce(
          (acc, cur) => (properties.includes(cur) ? null : (acc[cur] = ''), acc),
          {}
        ),
      })
    } else {
      elementStore?.styleStore?.updateStyle({
        ...styleKeys.reduce((acc, cur) => (properties.includes(cur) ? null : (acc[cur] = ''), acc), {}),
      })
    }
    // Push event GA
    const eValue1 = t(label.toString())
    const eValue2 = showIcon ? 'enable' : 'disable'
    eventGA('reset_parameter', [eValue1, eValue2])
  }
  const parameterDetail = useContext(ParameterDetail)

  const pushParameterEvent = (value = '', unit = '') => {
    // Send GA Event
    if (store && parameterDetail) {
      eventGA('edit_element', [
        parameterDetail['category'],
        parameterDetail['group'],
        label,
        combineType(store.elementStore?.state),
        value,
        unit,
      ])
    }
  }

  return (
    <PushParameterEvent.Provider value={pushParameterEvent}>
      <VerticalStack gap={'2'}>
        <HorizontalStack align="space-between" blockAlign="center" gap={helpText ? '2' : '4'}>
          <HorizontalStack>
            {compareWithGlobalStyles && classGlobalStyling ? (
              <ControllerLabel label={displayLabel} showIcon={showIcon} showTooltip={showIcon && stylesModified} />
            ) : (
              displayLabel
            )}
            {tooltip && (
              <Tooltip content={tooltip} dismissOnMouseOut>
                <Icon source={QuestionMarkMajor} />
              </Tooltip>
            )}
          </HorizontalStack>
          {(device || showReset) && (
            <HorizontalStack gap={'1'} blockAlign="center">
              {showReset && <ResetValue disabled={disableReset || !stylesModified} onResetValue={handleResetValue} />}
              {device && <DeviceSensitivity />}
            </HorizontalStack>
          )}
          {inline ? children : null}
        </HorizontalStack>
        {!inline ? <Box>{children}</Box> : null}
        {helpText && (
          <HelpTextStatic content={typeof helpText === 'string' ? t(helpText, { ...helpTextOptions }) : helpText} />
        )}
      </VerticalStack>
    </PushParameterEvent.Provider>
  )
}
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
class InspectorControllerClass extends Component<InspectorControllerProps, InspectorControllerState> {
  static propsToState = {
    'contexts.InspectorContext': 'store',
    'contexts.ParameterDetail': 'parameterDetail',
  }

  state: InspectorControllerState = {}

  static getDerivedStateFromProps(props, state) {
    return ExtObject.createByPathMapping(props, InspectorControllerClass.propsToState, state)
  }

  handleResetValue = () => {
    const { onResetValue, styleKeys, elementStore, label, showIcon } = this.props

    if (typeof onResetValue === 'function') {
      onResetValue()
    }

    // If styleKeys include general keys such as padding, margin,...,
    // We need to reset all of the other keys except the general keys
    const properties = Object.keys(BOX_MODEL_PROPERTIES)
    const generalKey = styleKeys.find(key => properties.includes(key))

    if (generalKey) {
      elementStore?.styleStore?.updateStyle({
        ...BOX_MODEL_PROPERTIES[generalKey].styleKeys.reduce(
          (acc, cur) => (properties.includes(cur) ? null : (acc[cur] = ''), acc),
          {}
        ),
      })
    } else {
      elementStore?.styleStore?.updateStyle({
        ...styleKeys.reduce((acc, cur) => (properties.includes(cur) ? null : (acc[cur] = ''), acc), {}),
      })
    }

    // Push event to GA.
    const eValue1 = t(label.toString())
    const eValue2 = showIcon ? 'enable' : 'disable'

    eventGA('reset_parameter', [eValue1, eValue2])
  }

  pushParameterEvent = (value = '', unit = '') => {
    const { label } = this.props
    const { store, parameterDetail } = this.state

    // Send event to GA.
    if (store && parameterDetail) {
      eventGA('edit_element', [
        parameterDetail['category'],
        parameterDetail['group'],
        label,
        combineType(store.elementStore?.state),
        value,
        unit,
      ])
    }
  }

  render(): React.ReactNode {
    const { store } = this.state

    const {
      label,
      tooltip,
      children,
      styleKey,
      showReset,
      disableReset,
      elementStore,
      componentName,
      compareWithGlobalStyles,
      device = true,
      helpText = '',
      inline = false,
      helpTextOptions = {},
    } = this.props

    // Prepare style data.
    let globalStyles: any = {}
    let currentStyles: any = {}

    const classGlobalStyling = elementStore?.data?.classGlobalStyling
    const styleKeys = Array.isArray(styleKey) ? styleKey : [styleKey].filter(key => !!key)

    if (elementStore && classGlobalStyling && styleKeys.length) {
      globalStyles = elementStore?.styleStore?.getGlobalStyle(`.__pf .${classGlobalStyling}`)
      currentStyles = elementStore?.styleStore?.getCurrentStyle()
    }

    const showIcon = styleKeys.some(k => globalStyles && !!globalStyles[k])
    const diff = globalStyles.length ? compareGlobalStylesWithCurrentStyles(globalStyles, currentStyles) : []

    let stylesModified = styleKeys.some(k => diff.includes(k) && globalStyles && !!globalStyles[k])

    if (!stylesModified) {
      stylesModified = styleKeys.some(k => elementStore?.styleStore?.getCurrentStyle()[k])
    }

    // Prepare control label.
    const displayLabel = typeof label === 'string' && t(label)

    // Prepare title element.
    const title = classGlobalStyling && compareWithGlobalStyles
      ? <ControllerLabel label={displayLabel} showIcon={showIcon} showTooltip={showIcon && stylesModified} />
      : displayLabel

    // Prepare device selector.
    const deviceSensitivitySelector = (device || showReset) && (
      <HorizontalStack gap={'1'} blockAlign="center">
        {showReset && <ResetValue disabled={disableReset || !stylesModified} onResetValue={this.handleResetValue} />}
        {device && <DeviceSensitivity />}
      </HorizontalStack>
    )

    return (
      <RenderControl
        {...this.props}
        title={title}
        inline={inline}
        tooltip={tooltip}
        helpText={helpText}
        storage={store?.elementStore}
        helpTextOptions={helpTextOptions}
        titleAddon={deviceSensitivitySelector}
        pushGAEventParams={this.pushParameterEvent}
        componentName={componentName || 'InspectorControl'}
      >
        {children}
      </RenderControl>
    )
  }
}

const InspectorController = adaptContexts(InspectorControllerClass, {
  ParameterDetail,
  InspectorContext,
})

export default InspectorController
```
{% endtab %}
{% endtabs %}

As you can see, the refactored component no longer renders the inspector control itself. It instead uses the new `RenderControl` component to render the appropriate input control. The `RenderControl` supports rendering both the refactored and non-refactored input controls.

I've also refactored the `InspectorGroup` component, which renders a group of input controls, to use the `RenderControl` component to render input controls as follows.

```javascript
export default class InspectorGroup extends Component<InspectorGroupProps, InspectorGroupState> {
  static defaultProps = {
    inputs: [],
    header: null,
    category: null,
  }

  state = {
    open: true,
  }

  render(): ReactNode {
    const { open } = this.state
    const { header, group, category, inputs } = this.props

    return (
      <StyledGroup>
        <Box borderBlockEndWidth="1" borderColor="border-subdued">
          <div className="is-link" onClick={() => this.setState({ open: !open })}>
            <Box padding="4" paddingBlockStart="3" paddingBlockEnd="3">
              <HorizontalStack align="space-between">
                <Text variant="headingMd" as="h6">
                  {t(header)}
                </Text>
                <Box as="span">
                  <Icon source={open ? CaretUpMinor : CaretDownMinor} />
                </Box>
              </HorizontalStack>
            </Box>
          </div>
          <Collapsible expandOnPrint id={header} open={open} transition={{ duration: '150ms', timingFunction: 'ease' }}>
            <Box padding="4" paddingBlockStart="0">
              <VerticalStack gap="4">
                {inputs.map((input, k) => {
                  const { Component, ...rest } = input

                  if (!Component) {
                    return
                  }

                  return (
                    <ParameterDetail.Provider key={`${header}-${k}`} value={{ category, group: group || header }}>
                      <RenderControl key={k} componentName={Component} {...rest} />
                    </ParameterDetail.Provider>
                  )
                })}
              </VerticalStack>
            </Box>
          </Collapsible>
        </Box>
      </StyledGroup>
    )
  }
}
```

If the value passed to the `componentName` property is an input control name, `RenderControl` will look for the declaration file from the mapping object `controls` declared in the file `modules/inspector/includes/loaders/controls.ts` to import dynamically and render the input control after importing completes. Otherwise, if the value is a legacy input control that is a React function component, `RenderControl` will render the input control normally. This behavior ensures the use of both refactored and non-refactored input controls seamlessly.

{% hint style="success" %}
The new mechanism _**requires**_ changing the definition of inspector controls.
{% endhint %}

Below is the refactored definition for the text editor for inputting content for the `Heading` element.

{% tabs %}
{% tab title="Legacy" %}
```javascript
export function ControlledHeadingContent() {
  const { t } = useTranslation()
  const store = useContext(InspectorContext)
  const elementStore = getElementStore(store.id)
  const {
    data: { value },
    setData,
  } = store

  const onChange = value => {
    setData({ value })
  }

  return (
    <TextEditingInspector
      title={'HEADING_TEXT'}
      value={value}
      placeholder={t('PLACEHOLDER_ELEMENT_TEXT')}
      onChange={onChange}
      elementStore={elementStore}
    />
  )
}

const heading2Configs = {
  tab: 'general',
  group: 'heading2Content',
  groupHeader: 'CONTENT',
  keyword: [t('CONTENT')],
}

const _heading2Inspectors = [
  {
    Component: ControlledHeadingContent,
    ...heading2Configs,
    gaKey: 'HEADING_TEXT',
    keyword: [t('HEADING_TEXT')],
  },
]
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
const heading2Configs = {
  tab: 'general',
  group: 'heading2Content',
  groupHeader: 'CONTENT',
  keyword: [t('CONTENT')],
}

const _heading2Inspectors = [
  {
    InspectorController,
    Component: 'InspectorControlTextEditor',
    ...heading2Configs,
    device: false,
    label: 'HEADING_TEXT',
    gaKey: 'HEADING_TEXT',
    keyword: [t('HEADING_TEXT')],
  },
]
```
{% endtab %}
{% endtabs %}

Below is the refactored code of the component `TextEditingInspector`, which renders a text editor.

{% tabs %}
{% tab title="Legacy" %}
```javascript
function TextEditingInspector(props: Props) {
  const {
    value,
    onChange,
    title,
    variables,
    placeholder,
    link,
    sizeEditor,
    successMessage,
    errorMessage,
    id,
    helpText,
  } = props
  const editorRef = useRef(null)

  const handleChange = (val: string) => {
    typeof onChange === 'function' && onChange(val)
  }

  return (
    <InspectorController label={title} device={false} helpText={helpText}>
      <VerticalStack gap={'2'}>
        <TextEditor
          value={value}
          onChange={handleChange}
          size={sizeEditor}
          placeholder={placeholder}
          link={link}
          successMessage={successMessage}
          id={id}
          errorMessage={errorMessage}
          editorRef={editorRef}
        />
        {variables && <TagsGroup variables={variables} onChange={onChange} editorRef={editorRef} />}
      </VerticalStack>
    </InspectorController>
  )
}
export default TextEditingInspector
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export default class InspectorControlTextEditor extends InspectorControl<InspectorControlTextEditorProps, void> {
  editorRef: RefObject<any> = null

  constructor(props) {
    super(props)

    // Create a reference to the editor HTML element.
    this.editorRef = createRef()
  }

  renderInput(): ReactNode {
    const { value } = this.state
    const { id, link, variables, sizeEditor, placeholder, errorMessage, successMessage } = this.props

    return (
      <VerticalStack gap={'2'}>
        <TextEditor
          id={id}
          link={link}
          value={value}
          size={sizeEditor}
          onChange={this.onChange}
          placeholder={placeholder}
          editorRef={this.editorRef}
          errorMessage={errorMessage}
          successMessage={successMessage}
        />
        {variables && <TagsGroup variables={variables} onChange={this.onChange} editorRef={this.editorRef} />}
      </VerticalStack>
    )
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
In the new structure, input control components no longer need to manually set the value inputted by end-users to the appropriate store and also don't need to wrap the HTML output inside the `InspectorController` component. The base class `InspectorControl` will set the value automatically based on the `keyPath` and `storage` properties passed by the `RenderControl` component when rendering.&#x20;
{% endhint %}

Below is the interface of the `InspectorControl` component.

```javascript
export default class InspectorControl<P, S> extends Component<P & InspectorControlProps, S & InspectorControlState> {
  // Define the default props.
  static defaultProps = {
    contexts: {},
    keyPath: 'data.value',
    storages: [StorageInspector],
  }

  // Define initial state.
  state: InspectorControlState = {}

  // Populate the initial input value.
  componentDidMount() => void

  // Getter method to get enhanced component props.
  get enhancedProps() => any

  // Handle changes in input fields.
  onChange(value: any) => void

  // Render the inspector control.
  render() => ReactNode

  // Render the input field.
  renderInput() => ReactNode
}
```

{% hint style="success" %}
When creating a new input control or refactoring an existing one, you should create a class that _**extends**_ the `InspectorControl` class and _**overrides**_ the `renderInput` method to display the appropriate input field.
{% endhint %}

{% hint style="danger" %}
The `render` and `onChange` methods of the base class _**should not be overridden**_ to ensure proper initialization, reactivation, and destruction.
{% endhint %}

{% hint style="info" %}
`InspectorControl` can take a function via the `onChange` property passed to the component when rendering to handle change instead of using the built-in `onChange` method.
{% endhint %}

{% hint style="info" %}
You can use the `keyPath` property to direct the `InspectorControl` class to set the value inputted by end-users to a key-path other than the default `data.value` key-path.
{% endhint %}

Below are the definitions of input controls for custom ID and class attributes that use a custom key-path to update data to the specified storage.

{% tabs %}
{% tab title="Legacy" %}
```javascript
export const ControlledId = () => {
  const {
    data: { id },
    setData,
  } = useInspectorContext('id')

  return (
    <TextInput value={id} onChange={v => setData({ id: stripHtmlTags(v) })} capitalizeTitle={false} title={t('ID')} />
  )
}

export const ControlledClass = () => {
  const {
    data: { className },
    setData,
  } = useInspectorContext('className')

  return <TextInput value={className} onChange={v => setData({ className: stripHtmlTags(v) })} title={t('CLASS')} />
}

const attributeConfigs = {
  tab: 'general',
  group: 'attributes',
  groupHeader: 'Attributes',
  keyword: [t('ATTRIBUTES')],
}

const _attributeInspectors = [
  {
    Component: ControlledId,
    ...attributeConfigs,
    keyword: [t('ID')],
  },
  {
    Component: ControlledClass,
    ...attributeConfigs,
    keyword: [t('CLASS')],
  },
]
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
const attributeConfigs = {
  tab: 'general',
  group: 'attributes',
  groupHeader: 'Attributes',
  keyword: [t('ATTRIBUTES')],
}

const _attributeInspectors = [
  {
    InspectorController,
    Component: 'InspectorControlTextInput',
    ...attributeConfigs,
    label: 'ID',
    device: false,
    keyPath: 'data.id',
    keyword: [t('ID')],
    capitalizeTitle: false,
    onPrepareValue: value => stripHtmlTags(value),
  },
  {
    InspectorController,
    Component: 'InspectorControlTextInput',
    ...attributeConfigs,
    device: false,
    label: 'CLASS',
    keyword: [t('CLASS')],
    capitalizeTitle: false,
    keyPath: 'data.className',
    onPrepareValue: value => stripHtmlTags(value),
  },
]
```
{% endtab %}
{% endtabs %}

Below is the refactored code of the component `TextInput`, which renders a single-line text field.

{% tabs %}
{% tab title="Legacy" %}
```javascript
function TextInput(props: ITextInput) {
  const { title, tooltip, helpText, spacing, ...rest } = props

  return (
    <InspectorController label={title} device={false} tooltip={tooltip} helpText={helpText} spacing={spacing}>
      <TextInputComponent {...rest} />
    </InspectorController>
  )
}

function TextInputComponent(props: TextInputComp) {
  const pushParameterEvent = useContext(PushParameterEvent)
  const { onChange, value, onFocus, type, placeholder, allowNull = true, onBlur } = props
  const [temp, setTemp] = useState(value)
  const [isFocusing, setIsFocusing] = useState(false)
  const val = useDebounce(temp, DEBOUNCE_SYNC_TEXT_ELEMENTS_TO_TEXT_EDITOR)

  useEffect(() => {
    if (temp !== value) {
      onChange(val)
    }
  }, [val])

  useEffect(() => {
    setTemp(value)
  }, [value])

  const handleOnBlur = e => {
    onBlur && onBlur(e.target.value)

    if (!allowNull && !e.target.value) {
      setTemp(value)
    }
    // Send GA Event
    pushParameterEvent && pushParameterEvent()
  }

  return (
    <>
      <Popover
        active={isFocusing && temp === '' && !allowNull}
        activator={
          <div
            onMouseLeave={() => {
              setIsFocusing(false)
            }}
          >
            <TextField
              label=""
              value={temp}
              type={type}
              onChange={setTemp}
              placeholder={placeholder || t('ENTER_TEXT_HERE')}
              onBlur={handleOnBlur}
              onFocus={e => {
                setIsFocusing(true)
                onFocus && onFocus(e.target)
              }}
              autoComplete="off"
            />
          </div>
        }
        onClose={() => {}}
      >
        <Box padding={'4'}>
          <HorizontalStack gap={'2'} align="space-between" blockAlign="center">
            <Icon source={AlertMinor} />
            <span>{t('EMPTY_INPUT_WARNING_MESSAGE')}</span>
          </HorizontalStack>
        </Box>
      </Popover>
    </>
  )
}

export default TextInput
```
{% endtab %}

{% tab title="Refactored" %}
```javascript
export default class InspectorControlTextInput extends InspectorControl<InspectorControlTextInputProps, InspectorControlTextInputState> {
  static contextType: Context<any> = PushParameterEvent

  static defaultProps: InspectorControlTextInputProps = {
    allowNull: true,
    ...InspectorControl.defaultProps,
  }

  state: InspectorControlTextInputState = {
    isFocusing: false,
  }

  changeTimer: any

  handleFocus = e => {
    const { onFocus } = this.props

    this.setState({ isFocusing: true })

    if (typeof onFocus === 'function') {
      onFocus(e.target)
    }
  }

  handleChange = (value: string) => {
    this.setState({ value })

    if (this.changeTimer) {
      clearTimeout(this.changeTimer)
    }

    this.changeTimer = setTimeout(() => this.onChange(value), DEBOUNCE_SYNC_TEXT_ELEMENTS_TO_TEXT_EDITOR)
  }

  handleBlur = e => {
    const { value } = this.state
    const {
      onBlur,
      allowNull,
      value: lastValue,
      contexts: { PushParameterEvent },
    } = this.props

    if (typeof onBlur === 'function') {
      onBlur(e.target.value)
    }

    if (!allowNull && !value) {
      this.setState({ value: lastValue })
    }

    // Send GA Event.
    const pushParameterEvent = PushParameterEvent || this.context

    if (typeof pushParameterEvent === 'function') {
      pushParameterEvent()
    }
  }

  renderInput(): ReactNode {
    const { value, isFocusing } = this.state
    const { placeholder, allowNull, type } = this.props

    return (
      <Popover
        active={isFocusing && !value && !allowNull}
        activator={
          <div onMouseLeave={() => this.setState({ isFocusing: false })}>
            <TextField
              label=""
              type={type}
              value={value}
              autoComplete="off"
              onBlur={this.handleBlur}
              onFocus={this.handleFocus}
              onChange={this.handleChange}
              placeholder={placeholder || t('ENTER_TEXT_HERE')}
            />
          </div>
        }
        onClose={() => {}}
      >
        <Box padding={'4'}>
          <HorizontalStack gap={'2'} align="space-between" blockAlign="center">
            <Icon source={AlertMinor} />
            <span>{t('EMPTY_INPUT_WARNING_MESSAGE')}</span>
          </HorizontalStack>
        </Box>
      </Popover>
    )
  }
}
```
{% endtab %}
{% endtabs %}

As you can see, the `TextInput` and the `TextEditingInspector` input controls, after refactoring, no longer contain any code that processes logic or renders specific things for the editor module. This new behavior makes them independent and reusable outside the page editor. This characteristic helps the structure of the inspector module and the entire app be more straightforward.

{% hint style="success" %}
After creating a new inspect control or refactoring an existing one, you need to define a mapping from the inspect control name to its declaration file in the mapping object `controls` declared in the file `modules/inspector/includes/loaders/controls.ts` and remove the old inspector control declaration from the list of inspector controls defined in the file `modules/inspector/group.ts`.
{% endhint %}
