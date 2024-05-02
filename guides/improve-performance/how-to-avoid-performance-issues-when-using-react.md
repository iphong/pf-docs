# How to avoid performance issues when using React

Facebook has done a great job when creating React, a simple and flexible library, for building web-based user interfaces. However, like other technologies, React has problems related to performance. In this article, we will discuss some common React performance issues and how to avoid them.

## Unnecessary re-rendering

Re-rendering components while unnecessary is one of the most common problems that affect performance when using React. This problem happens when a component re-renders while both of its props and states are not changed.

To avoid this problem, you should use `React.memo` or `shouldComponentUpdate`. `React.memo` is a higher-order component that memoizes a React function component and re-renders it only when its props are changed. On the other hand, `shouldComponentUpdate` is a lifecycle method that allows you to determine whether a React class component should update.

(to be continued)
