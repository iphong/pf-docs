# Refactor PageFly applying OOP

Currently, PageFly uses functional programming. In detail, PageFly uses React function components and global state hooks.

Functional programming emphasizes creating pure functions that do not have side effects, making it easier to reason about the code's behavior. However, global state hooks allow the use of hooks almost everywhere, even inside other hooks. This characteristic causes functions to become not pure and need more time traversing through hooks to understand the code.

While using React function components and global state hooks allows rapid development time, the code structure is loose and hard to follow. So, the code needs reviewing and maintaining thoroughly. Otherwise, it would become a mess.

The current code of PageFly is a result of not being reviewed and maintained carefully. There is a clean folder structure, but the code structure is unclear. Hooks are imported and used everywhere without rules, making the source code too complex. Many repeated code and hard coding make updates time-consuming and prone to bugs. Components and modules are not independent enough, and their reusable is not good yet.

All these things make PageFly hard to maintain and not easy to keep track of performance and stability.

It is the reason I propose a new structure for refactoring PageFly that applies the object-oriented programming (OOP) concept. The proposal also has adapters to allow refactoring PageFly piece by piece without affecting the app functionalities.
