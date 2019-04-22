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

## Actions

A Redux store can be updated with the help of _Actions_. _Action_ in Redux is an object. Whenever we need to perform any action like increment the number of items in cart, we send this _Action Object_ to Redux store.

An Action object should have a property called `type`. The `type` property is recognized by Redux while executing an action. The value of `type` property is a string that denotes the action. Example, for incrementing the value of cart count, we can give a string value like `INCREMENT_CART_COUNT`. So the _Action_ object looks like:

```javascript
{
  type: "INCREMENT_CART_COUNT";
}
```

The upper case used for `type` value is just for convention.

### Dispatching Action

So far we only learned that _Action_ is an object. Now how can we implment an action? Or how can we tell the store that we need to perform an action? The `store` object earlier recevied has a method called `dispatch()`. We use that method to dispatch an action.

```javascript
store.dispatch({
  type: "INCREMENT_CART_COUNT"
});
```

Now the store understood that, "OK, I need to execute INCREMENT_CART_COUNT action now". But so far we have not written any code to update the store.

Each time `dispatch()` is called, the `createStore()` method is executed and the current state is passed to it. Also the _Action_ object is also passed to `createStore()`. This passed action can be then read by providing a second argument to `createStore()` callback function.

```javascript
const store = createStore((state = initialState, action) => {
  console.log(action);
  return state;
});
```

We have placed a `console.log()` to find the value obtained by `action` when `dispatch()` is called. From that we can understand that `action` variable receives the _Action_ object we passed.

As we just understood, Any _Action Dipatching_ invokes `createStore()` with corresponding action type. Based on the action type, we can then update the store state and return new state. Let us see how we can update the store to increment the cart count.

```javascript
const store = createStore((state = initialState, action) => {
  if (action.type === "INCREMENT_CART_COUNT") {
    return {
      numberOfItemsInCart: state.numberOfItemsInCart + 1
    };
  }
  return state;
});
```

The `createStore()` function now has a `if` condition. If the dispatched action is of type `INCREMENT_CART_COUNT`, then an updated state is returned. We can verify if the store is updated or not by calling `getState()` method.

```javascript
import { createStore } from "redux";

const initialState = {
  numberOfItemsInCart: 0
};

const store = createStore((state = initialState, action) => {
  if (action.type === "INCREMENT_CART_COUNT") {
    return {
      numberOfItemsInCart: state.numberOfItemsInCart + 1
    };
  }
  return state;
});

console.log(store.getState()); // {numberOfItemsInCart: 0}

store.dispatch({
  type: "INCREMENT_CART_COUNT"
});

console.log(store.getState()); // {numberOfItemsInCart: 1}
```

In the above code snippet, the two `getState()` methods output different counts. That verifies that the store is properly updated. To get a better understanding, let us create one more action to decrement the cart count. As you might have assumed, here we are going to reduce the cart count by 1 when `DECREMENT_CART_COUNT` is executed.

We dispatch `DECREMENT_CART_COUNT` using the `store.dispatch()` method.

```javascript
store.dispatch({
  type: "DECREMENT_CART_COUNT"
});
```

We then handle this new action type inside `createStore()` by adding an extra if condition.

```javascript
if (action.type === "DECREMENT_CART_COUNT") {
  return {
    numberOfItemsInCart: state.numberOfItemsInCart - 1
  };
}
```

Now we are going to test if both increment and decrement functionality is working fine. We dispatch `INCREMENT_CART_COUNT` two times and then dispatch `DECREMENT_CART_COUNT` one time, resulting in one item finally in cart. Here is the complete code.

```javascript
import { createStore } from "redux";

const initialState = {
  numberOfItemsInCart: 0
};

const store = createStore((state = initialState, action) => {
  if (action.type === "INCREMENT_CART_COUNT") {
    return {
      numberOfItemsInCart: state.numberOfItemsInCart + 1
    };
  } else if (action.type === "DECREMENT_CART_COUNT") {
    return {
      numberOfItemsInCart: state.numberOfItemsInCart - 1
    };
  } else {
    return state;
  }
});

console.log(store.getState()); // {numberOfItemsInCart: 0}

store.dispatch({
  type: "INCREMENT_CART_COUNT"
});

store.dispatch({
  type: "INCREMENT_CART_COUNT"
});

store.dispatch({
  type: "DECREMENT_CART_COUNT"
});

console.log(store.getState()); // {numberOfItemsInCart: 1}
```
