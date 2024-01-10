# Dynamic render

The current code of PageFly is not modular enough because of the loose structure. This thing causes, even when using lazy loading for rendering React elements, the very first loading is still not fast because of the large size of the initial trunks.

To solve this problem, besides the need to refactor components and modules to be more modular, I've also created the new `Render` component. This component supports loading the declaration of another React component dynamically.

Using the `Render` component, declaration files will not load in the main trunk. This behavior helps avoid loading unnecessary files and also helps reduce the size of the initial trunk.

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

To dynamically render a React component using the `Render` component, you will need to define a mapping from the component name to its declaration file path in the `components` object declared in the `includes/loaders/components.ts` file. The content of that file is similar to the following.

```javascript
const components: StringToReactComponentMapping = {
  DashboardOnboarding: async () => (await import('/path/to/file')).default,
}
```

The behavior of the `Render` component is similar to the native `lazy` function of React but doesn't need to use the `Suspense` component for rendering a placeholder. Below is a rewriting of the example above using the native `lazy` function of React.

```javascript
const DashboardOnboarding = lazy(() => import('/path/to/file')

function Dashboard() {
  return <Suspense fallback={<img src="./lcp-image" alt="onboarding" />}>
    <DashboardOnboarding />
  </Suspense>
}
```
