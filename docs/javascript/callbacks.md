---
id: callbacks
title: Callbacks
---

**Callbacks** are functions that are passed as arguments to another functions. A function that receives a callback function as its argument is called **Higher Order Function**.

```javascript
function callback(name) {
  console.log(`Hi, ${name}`);
}

function higherOrderFunction(nameArg, callbackArg) {
  callbackArg(nameArg);
}

higherOrderFunction("Joby", callback); // "Hi, Joby"
```

In the above code snippet, `higherOrderFunction` is a Higher Order Function because it is expecting a function as its second argument. We then supplied a function `callback` to `higherOrderFunction`, which is later invoked.

We were using callbacks in lot of places without even knowing they were callbacks. Let us go through different code snippets where a callback function is involved.

**Array.map()**

The ES6 `map()` method of `Array` object requires a function as its argument. Here is an example.

```javascript
[2, 4, 5, 7].map(item => console.log(item));
```

**setTimeout()**

We all are very fluent with this `setTimeout()` method. It is a function that takes a function as its first argument.

```javascript
setTimeout(() => {
  console.log("I am ready");
}, 5000);
```

Above code prints `"I am ready"` in console after 5 seconds.

**jQuery button click handler**

We use `.on()` method to attach event handlers in jQuery. In order to attach a click event handler to a button with id `myButton`, here is the code in jQuery.

```javascript
$("#myButton").on("click", function() {
  console.log("Button clicked");
});
```

Here also we are passing a function as second argument to `.on()` method. The second argument which is an anonymous function is also a callback function.

**AJAX request**
In jQuery, we can use `$.getJSON()` to do an AJAX call for JSON request. An example code will be:

```javascript
$.getJSON("ajax/test.json", function(data) {
  console.log(data);
});
```

Here the passed callback function receives response data in `data` variable.

> If you observe the case of `setTimeout()`, button click handler or AJAX request, the passed callback functions are not immediately executed. In case of of `setTimeout()` it is executed only after 5 seconds. In case of click handler, the callback function is executed only when a user clicks on the button. Therefore we can say that callbacks help us to delay the execution of a function to a later point in time.

## Callback Hell

How can callbacks create a hell like situation? Let us try to understand that. In the following code, we are waiting for the response of a login API.

```javascript
function codeAfterAJAX() {
  console.log("Here I continue rest of the functionality");
}

$.ajax({
  method: "POST",
  url: "api/login",
  data: { username: "John", password: "John123!" }
}).done(codeAfterAJAX);
```

Here we make an AJAX call. If the AJAX response come successfully, we execute `codeAfterAJAX` to continue our logic. What if the jQuery AJAX function had some bug and calls the callback function twice? Things might not end well.

So in case of callbacks, we are blindly trusting some code and ask that code to execute a callback when ready. There happens an **inversion of control** in this place. There can be some times when things wont work as expected and create a hell like situation.
