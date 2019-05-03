---
id: react-with-redux
title: React With Redux
---

Redux is a state management library. In React, we know that we can maintain state inside a class component. Now when we are working with a complex app with many pages, there will be different components rendered by React-Router. These components do not share a common state to exchange data. Redux can help us here to act as a common place to get or set state.

Redux and its features can be learned and tried independently. You can read the [Redux article](../redux/index.md) to get an understanding. We need to have a store setup to follow below content.

In order to use Redux with React, first we need to add `react-redux` package to our project.

```
yarn add react-redux
```

`react-redux` is comparitively a small package. It contains one component named `<Provider />` and one function named `connect()`. `Provider` component is used to wrap our root component and mention the store which our app can use. Then, which ever components require data from the store, they are wrapped using `connect()`.

Let us import `Provider` component from `react-redux`.

```javascript
import { Provider } from "react-redux";

//...

const app = (
  <Provider store={store}>
    <App />
  </Provider>
);

ReactDOM.render(app, document.getElementById("app"));
```

Then our earlier root component `<App />` is wrapped inside `<Provider />`. We also need to pass the redux store as a property to `<Provider />`. Now all the child components of `<App />` can access `store` data directly. We will see how.

## Connecting a Component with Redux Store

When a component is wrapped inside `<Provider />`, we know that the component can access the store. Let us create a component that requires data from store.

Let us create a new component `TodoList`.

```jsx
import React from "react";

const TodoList = () => {
  return <h1>TodoList</h1>;
};

export default TodoList;
```

Next, there is a method `connect()` inside `react-redux` package. Let us import it.

```jsx
import { connect } from "react-redux";
```

`connect()` is a function that returns another function. The returned function then returns a Higher Order Component which injects more data to the child component.
