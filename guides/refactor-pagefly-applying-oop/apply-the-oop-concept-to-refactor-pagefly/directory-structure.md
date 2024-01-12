# Directory structure

Below is the new folder structure I proposed for grouping files by purpose and feature.

```
src/next/@refactoring
|- components
|- constants
|- contexts
|- includes
|  |- loaders
|  |  |- components.ts
|  |  |- storages.ts
|  |- adapters.ts
|  |- component.ts
|  |- event.ts
|  |- ext-object.ts
|  |- helpers.ts
|  |- render.ts
|  |- storage.ts
|  |- use-contexts.ts
|  |- use-hooks.ts
|- modules
|- screens
|- storages
```

The `components` folder is to store UI components that are reusable across different screens of the app, such as cookie consent settings, top bar, etc.

The `constants` and `contexts` folders are to store common constants and contexts.

The `includes` folder contains base functions and classes for building the entire app. The `loaders` directory inside the `includes` folder contains definition files for dynamically loading UI components and storage classes when needed.

The `modules` folder contains packaged source code files for building a single feature or a set of related features, such as editor, inspector, etc. Each directory under the `modules` folder should contain independent code of a single module and should have `components`, `constants`, `contexts`, `includes`, and `storages` directories separated from the common.

The `storages` folder contains declarations of storage classes commonly used across the app, such as global config, onboarding state, etc.
