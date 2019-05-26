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

## Encapsulation

In Object Oriented Programming, we group related variables and methods that operate on them into an object. This is called **encapsulation**.

Say we are working on a banking application. We are adopting a procedural way of writing code.

```javascript
let firstName = "Joby";
let lastName = "Joseph";
let age = 33;
let fixedInterestRate = 9.7;

// Functions
function getName(fName, lName) {
  return `${fName} ${lName}`;
}
function isSenior(age) {
  if (age >= 60) {
    return true;
  } else {
    return false;
  }
}
function getFixedInterestAmount(amount, rate) {
  return (amount * rate) / 100;
}

// Function Invocation
console.log(getName(firstName, lastName));
console.log(isSenior(age));
console.log(getFixedInterestAmount(1000, fixedInterestRate));
```

There are two main modules where we are working, _Employee_ module and _Banking_ module. But there is no segregation in our coding style. Any function can access any variable. Let us follow encapsulation principle to group these functionalities. We are going to create two objects for the two modules.

```javascript
const employeeModule = {
  firstName: "Joby",
  lastName: "Joseph",
  age: 33,
  getName: function() {
    return `${this.firstName} ${this.lastName}`;
  },
  isSenior: function() {
    if (this.age >= 60) {
      return true;
    } else {
      return false;
    }
  }
};

const bankingModule = {
  fixedInterestRate: 9.7,
  getFixedInterestAmount: function(amount) {
    return (amount * this.fixedInterestRate) / 100;
  }
};

console.log(employeeModule.getName());
console.log(employeeModule.isSenior());
console.log(bankingModule.getFixedInterestAmount(1000));
```

## Abstraction

When the complexities of a module is hidden from the user, it is called **Abstraction**.

In the above section, we are using a `fixedInterestRate` property inside `bankingModule`. It is now wrapped inside `bankingModule` object. Therefore `fixedInterestRate` variable is now not available in global scope, there by reducing polluting global scope.
