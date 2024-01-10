# Refactor the inspector module

The current inspector module in the code base of PageFly contains code to process logic related to the editor module and uses assets belonging to the editor module. This situation ensures the inspector module works as intended with the editor module in the page editor context. However, this behavior also makes using the inspector module outside the page editor context becomes difficult because the module is not independent.

I've created two new React components that help make the inspector module more independent after refactoring. The `RenderControl` component supports flexibly rendering input controls, and the `InspectorControl` component is the base class for building independent and fully reusable input controls.

The `RenderControl` component can take a custom React component from the `InspectorController` property and use it to render an input control. This characteristic supports rendering advanced input controls in specific use cases, such as inside the page editor context.

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

  const title =
    compareWithGlobalStyles && classGlobalStyling ? (
      <ControllerLabel label={displayLabel} showIcon={showIcon} showTooltip={showIcon && stylesModified} />
    ) : (
      displayLabel
    )

  const deviceSensitivitySelector = (device || showReset) && (
    <HorizontalStack gap={'1'} blockAlign="center">
      {showReset && <ResetValue disabled={disableReset || !stylesModified} onResetValue={handleResetValue} />}
      {device && <DeviceSensitivity />}
    </HorizontalStack>
  )

  return (
    <RenderControl
      {...props}
      title={title}
      inline={inline}
      tooltip={tooltip}
      helpText={helpText}
      storage={store.elementStore}
      helpTextOptions={helpTextOptions}
      pushGAEventParams={pushParameterEvent}
      titleAddon={deviceSensitivitySelector}
      componentName={props.componentName || 'InspectorControl'}
    >
      {children}
    </RenderControl>
  )
}
```
{% endtab %}
{% endtabs %}

As you can see, the refactored component no longer renders the inspector control itself. It instead uses the new `RenderControl` component to render the HTML code. The `RenderControl` supports rendering both the refactored and non-refactored input controls.

I've also refactored the `InspectorGroup` component, which renders a group of input controls, to use the `RenderControl` component to render an input control as follows.

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
