---
author: Joby Joseph
title: JavaScript Interview Questions
---

Here is a collection of JavaScript questions that can help you prepare for an interview.

**Write a polyfill for JavaScript `Array.map()` method**

**What are the differences between normal functions and ES6 arrow functions**

**How does JavaScript `bind()` works?**

**What is `this` keyword and how the value of `this` is determined?**

**Given a string, remove all duplicates without using `if` or loops.**

**Make a generic method for adding numbers. It can be `sum(1, 2, 3)` or `sum(1)(2, 3)` or `sum(1)(2)(3)`**

**What is a `prototype` in JavaScript? Is it an object, function or something else?**

`prototype` is a property in JavaScript constructor function. The `property` object contains properties and methods which are inherited by instance objects.

## `this`

**Question:**

We have an object `obj` with two methods.

```javascript
var obj = {
  a: function() {
    console.log(this);
  },
  b: () => {
    console.log(this);
  }
};
```

What will be the value printed in the following 3 statements?

```javascript
obj.a();
obj.b();
obj.b.call(obj);
```

**Answer:**

`obj.a()` logs `obj`. Whenever you see a dot(`.`) operator, the method is called in the context of the object. `this` returns the invocation context in JavaScript.

`obj.b()` logs `window` object if executed in a browser in non-strict mode. This because the method `b()` is defined using ES6 arrow functions. Arrow functions do not have binding to `this`. It takes the value of `this` where the function is invoced. In this `obj.b()` is in global scope.

`obj.b.call(obj)` also logs `window` object. Arrow functions do not have any impact on `this`, even if it is used with `call` or `apply`. So here also, `this` simply took the invocation context, which is global.
