# Refactor editor elements

To simplify the creation of page elements, I've created the `EditorElement` class as the ground to build page elements. It will automatically do necessary initialization when rendering a page element, such as subscribing to storage, applying style, etc. Below is the interface of the base component.

```javascript
export default class EditorElement<P, S> extends Component<P & EditorElementProps, S & EditorElementState> {
  // Define the default props.
  static defaultProps = {
    contexts: {},
    storages: [StorageEditor],
  }

  // Define initial state.
  state = { count: 0 }

  // Editor storage instance.
  editorStorage: StorageEditorInstance = null

  // Data store reference.
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
