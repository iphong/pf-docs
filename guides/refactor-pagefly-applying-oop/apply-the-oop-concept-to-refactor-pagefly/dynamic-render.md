# Dynamic render

Besides the need to refactor components and modules to be more modular, I've created a React component for dynamically rendering UI components. The new `Render` component loads the declaration of a React component only when needed. Dynamic rendering coupled with encapsulated UI components and modules can reduce the main trunk volume and boost the loading speed.

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

{% hint style="success" %}
To dynamically render a React component using the `Render` component, you need to define a mapping from the component name to its declaration file path in an object named`components` declared in the `includes/loaders/components.ts` file.
{% endhint %}

The content of the file `includes/loaders/components.ts` is similar to the following.

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
