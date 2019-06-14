---
id: promises
title: Promises
---

Promise in a real life as we all know is an assurance given by someone to deliver something. If we visit a Pizza corner and order a pizza, they will not immediately handover us a pizza. Instead they will handover a piece of paper with a token number. That piece of paper is a promise given to us assuring pizza delivery.

## Creating Promise

Assume we are creating a function to order pizza. As mentioned earlier, it or the person who takes the order should return a promise.

```javascript
function orderPizza() {
  return new Promise(() => {
    // set of instructions to process order
  });
}
```

A new promise(pizza order token) is created using `new Promise()` and then returned by `orderPizza()` function. As a user, we have to just call `orderPizza()`, get the token and wait for the pizza. But inside `orderPizza()` function body, there should be set of instructions to process the order. And that set of instructions is passed as a callback function to `Promise` constructor function.

While processing the pizza order, there can be two outcomes. One, the pizza is prepared successfully or in other words the task is resolved. Two, due to some reasons the order has to be cancelled or rejected. To visualize, we can imagine there is a red and green button in the pizza counter. If the order is ready, the counter staff will press green button(resolve), otherwise red button(reject). In our code, we can inject these buttons to handle resolve and reject case. Here is the updated `orderPizza()` function.

```javascript
function orderPizza() {
  return new Promise((resolve, reject) => {
    let pizzaStatus;
    if (pizzaStatus === "prepared") {
      resolve(); // pressed green button
    } else {
      reject(); // pressed red button
    }
  });
}
```

We just put an `if...else` to understand how `resolve` and `reject` are used. We will change it later.

## Getting a Promise

In the previous section, we created a function to create a promise. Now, let us call the function to order a pizza.

```javascript
var pizzaPromise = orderPizza();
```

`pizzaPromise` is the token number we have received. Let us go in depth on `pizzaPromise`.

Firstly, since `orderPizza()` function returns a `new Promise()`, `pizzaPromise` is an instance of `Promise` constructor function. So `pizzaPromise` have a set of properties and methods defined by `Promise` constructor function. If we type `pizzaPromise.` in browser console, we can see the list of keys present in it.

![Contents of promise instance](assets/images/promises-1.png)

As we can see `pizzaPromise` is an object with several methods. The methods which we are interested are `.then()` and `.catch()`. These are event listeners of a promise, just like a button object have `onclick()`, `onblur()` and so on. We will cover more in the coming sections.

For now, we have received a promise object which has some event listeners.

## Fulfilling a promise

Now the customer has received the token. There is no use in simply sitting with the token. We need to listen to get the update about our order.

### `.then()`

As we saw earlier, `.then()` is a method of `pizzaPromise`. It is an event listener for both success and failure case of promise. Let us first define two functions to handle resolve and reject cases.

```javascript
function pizzaIsReady() {
  console.log("I am very happy");
}

function pizzaFinished() {
  console.log("I am sad");
}
```

We can now set to call `pizzaIsReady()` if the promise is resolved or call `pizzaFinished()` if the promise is rejected.

```javascript
pizzaPromise.then(pizzaIsReady, pizzaFinished);
```

Let us now see if the success scenario works. We can modify our `orderPizza()` function to resolve the promise after 5 seconds, just to mimick that the pizza is ready after 5 seconds. Here is the complete code so far.

```javascript
// Function that returns a new promise
function orderPizza() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve();
    }, 5000);
  });
}

// Success handler
function pizzaIsReady() {
  console.log("I am very happy");
}

// Error handler
function pizzaFinished() {
  console.log("I am sad");
}

// Getting and listening to promise
var pizzaPromise = orderPizza();
pizzaPromise.then(pizzaIsReady, pizzaFinished);
```

This code will print `"I am very happy"` in console after 5 seconds of page load. If we change `resolve()` in `orderPizza()` to `reject()`, then `pizzaFinished()` is called.

We just learned that `.then()` is an event listener. It accepts 2 arguments. First one is success handler for promise and second one is error handler.

### `.catch()`

In the previous section, we used only `then()` to handle resolve and reject. Instead, for better code readability, we can use `.then()` to handle `resolve()` and `.catch()` to handle `reject()`.

```javascript
pizzaPromise.then(pizzaIsReady).catch(pizzaFinished);
```

The difference is only in the syntax. Internally `.catch()` calls `.then()` and pass the callback as `.then()`'s second argument.

## Passing Data in `resolve()` or `reject()`

We saw earlier how Promises are resolved. W

## Multiple `resolve()` Invocation

## Invoking Order for `.then()` and `.catch()`

## Chaining Promises

We saw that if a Promise is resolved, `.then()` is triggered. `.then()` also returns a Promise object on which we can access the `.then()` again. So the pseudocode looks like:

```
wait of something to finish
  then do some task until finish
  then do some other task until finish
  ...
catch error at any steps
```

This is called chaining of promises. It allows a sequential flow control.
