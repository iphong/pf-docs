# Refactor PageFly applying OOP

Currently, PageFly uses functional programming. In detail, PageFly uses React function components, hooks, and global state subscriptions.

Functional programming emphasizes creating pure functions that do not have side effects, making it easier to reason about the code's behavior. However, the hook mechanism of React allows the use of hooks almost everywhere, even inside other hooks. This characteristic causes functions to become not pure and need more time traversing through hooks to understand the code.

Global state subscriptions also allow changing the global state from almost everywhere in the codebase. When a global state changes, all subscribed components will be updated automatically. This behavior causes a component subscribing to a global state to depend on untrackable numbers of other components outside.

While using React function components, hooks, and global state subscriptions allows rapid development time, the code structure is loose and hard to follow. Therefore, the code needs reviewing and maintaining thoroughly. Otherwise, it would become a mess.

The current code of PageFly is a result of not being reviewed and maintained carefully. Hooks are imported and used everywhere without rules, making the source code too complex. Almost all components depend on global state subscriptions to render content and update behavior. So, when a component changes a global state, it can affect many other components subscribing to that state. Hence, components and modules are not independent and reusable.

All these things make PageFly hard to maintain and not easy to keep track of performance and stability.

Because of that, I propose a new structure for refactoring PageFly that applies the object-oriented programming (OOP) concept. The proposal also has adapters to allow refactoring PageFly piece by piece without affecting the app functionalities.
