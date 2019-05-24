---
id: object-oriented-js
title: Object Oriented JavaScript
---

Object Oriented Programming is a programming paradigm that is centered around objects. So it is just a way of writing code. If there is a language that supports such a style of writing, then that language is called Object Oriented Programming(OOP) Language. Examples of OOP language are C#, Java and JavaScript.

Any OOP language supports 4 concepts.

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

## Procedural Programming

In Procedural Programming, all the functions and data needed in our program is lying straight in the global space.

```javascript
let name = "Mercedes";
function printName() {
  console.log(name);
}
function sum(a, b) {
  return a + b;
}
console.log(sum(2, 3));
```

Here as you can see all functions and variables are just lying around. It is not possible to group them to address a particular functionality.

In Object Oriented Programming, we can group related functions and data in an object.
