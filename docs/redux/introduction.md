---
id: introduction
title: Redux
---

Redux is a state management JavaScript library. It allows us to track changing data.

## Setup Redux

Redux is an independent library. What it means is, in order to try Redux we do not have to add `React` or `Angular`. Let us create a JavaScript file with name, `redux-learning.js` file. Now set `redux-learning.js` as the entry point in `webpack`. Now the bundle created by webpack will be containing the code from `redux-learning.js`. If you are new to Webpack, there are many tutorials available online on how to setup a basic webpack project. Redux can be added to our project using

```
yarn add redux
```

At the time of writing, Redux v4.0.1 was installed in my laptop.

## Create Store

Now in `redux-learning.js`, add reference to `redux`. There is a named import called `createStore` inside `redux` package.

```javascript
import { createStore } from "redux";
```

`createStore` is used to create a redux store. As we learned Redux is a state management library. Redux saves the state in the created store.
In the above line, we only imported `createStore` function. We did not create a store. We are going to do that now.

Before creating a store, let us design a basic project requirement. Our project is a very minimal ecommerce webapp. The webapp needs to store the number of items in user's cart because this number is accessed by many components in our application. Now we can create a new store that stores the number of items in cart.

```javascript
import { createStore } from "redux";

const initialState = {
  numberOfItemsInCart: 0
};

const store = createStore((state = initialState) => {
  return state;
});
```

`createStore()` function accepts a callback function. That function takes the current state as its argument. When the store is created for the first time, state will be empty. At that time, the `initialState` object is assigned to it. Inside `initialState` object, you can see the `numberOfItemsInCart` is set to 0.

Ok. Now, we have written code to create a store. We also set an initial state. Let us verify if the store and initial state is set properly. For that, `store` has a method called `getState()` which returns the current state of store.

```javascript
console.log(store.getState()); // {numberOfItemsInCart: 0}
```

We have successfully created a Redux store with an initial state.
