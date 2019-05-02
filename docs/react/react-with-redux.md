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

Then our earlier root component `<App />` is wrapped inside `<Provider />`. We also need to pass the redux store as a property to `<Provider />`.
