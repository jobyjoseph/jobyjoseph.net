---
id: prototypes
title: Prototypes
---

JavaScript is known to be as prototype-based language. That itself shows how important is **prototypes** in JavaScript. We will see what it is and what role it plays in JavaScript.

## What is `prototype`?

When asked this question, I have heard several answers like `prototypes` are link from one object to another object or it brings inheritance and so on. But in order to visualize something, we need to give a shape to it. So the right answer is `prototype` is an **object**.

Oh! are you saying that `prototype` is just an object? Yes it is. It is an object which JavaScript engine has given a special meaning. Assume, God has given you two buckets. Whatever you put in one bucket needs to be consumed before you die. Whatever you put in second bucket will be inherited by your children. Now in JavaScript world, the two buckets are just two objects. The second bucket's name is `prototype`. So if you see a bucket kept in a house with label `prototype`, it means the contents are kept for getting inherited. God in story is the JavaScript engine and it decides the meaning and purpose of `prototype` object.

## `Function.prototype` and `__proto__`

We have seen both and most of us are confused. We dont know if both are same or something different. The correct answer is `Function.prototype` and `__proto__` are different. Some people try to argue that both of them point to same object, so they are same and so on. I do not agree with that. It is like saying donkey and horse are same because both of them have many common properties.

#### `prototype`

Every function in JavaScript is an object. `prototype` is a property in every functions. Below we have a simple function that does nothing.

```javascript
function f() {}
```

After executing above line, go to console and type `f.`. We can see a set of properties and methods for `f`. One property will be `prototype`.

![prototype as a function property](assets/images/prototype-property.png)

For a normal function, this property does not have an importance. But when a function is used as a **constructor function**, then this `prototype` property has the main role.
