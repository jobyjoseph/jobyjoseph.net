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

#### `__proto__`

Any object in JavaScript has a property called `__proto__`. This property holds reference to the object's parent. You can visualize `__proto__` object as the stairway to parent object.

We don't have to manually create `__proto__` property. It is automatically created by JavaScript to have the link to the object parent.

If every object has `__proto__`, let us create a very simple object literal.

```javascript
var obj = {
  name: "Joby",
  age: 33
};
```

Run the above code and go to browser console. There type `obj.` to see the list of properties and methods in `obj`.

![__proto__](assets/images/__proto__.png)

Now print the value of `obj.__proto__` in console.

![Value of __proto__](assets/images/__proto__1.png)

Now you saw the value of `obj.__proto__`. It is an object containing different methods like `constructor()`, `toString()` and so on. If you recollect what we discussed above, this object is the parent object of `obj`. Oh!, in that case, what is this parent object? from where it came? who assigned it?

Even if you are new to JavaScript, I am going to tell few things. Just believe it. When we create a new object literal like `obj`, it is actually an instance of `Object()` constructor function. This `Object()` function is native code or in other terms inbuilt in JavaScript. So we can see `obj` as an object which is a result of an operation something like below.

```javascript
var obj = new Object();
```

So if `obj` is created from `Object()`, `obj`'s parent will be `Object.prototype`. So let us go to browser console and see the value of `Object.prototype`.

![Comparing with Object.prototype](assets/images/__proto__2.png)

As we can see `obj.__proto__` and `Object.prototype` is same. Both point to same object. In other words, we can see this common object as a common drop/pickup point. `Object` puts methods which can be inherited in this common object using `Object.prototype`, something like a giver. On the other hand, every object instances like `obj` is linked to the common object using `__proto__` to consume the inherited methods or properties, something like a taker.
