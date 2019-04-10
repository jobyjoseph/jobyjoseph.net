---
id: components
title: Components
---

React is famous for creating components. These components form the building blocks of bigger applications. Here is a screenshot of facebook home page.

## Classes in ES6

Before starting with creating a React component, let us understand a simple ES6 class. Till ES6, `class` was a reserved keyword, which means we could not have an identifier with name _class_ in ES5. Classes in ES6 can be created using `class` keyword.

```javascript
class Person {
  // class body
}
```

`Person` is an empty class with no properties or methods.

### Adding a method

Let us add a new method `showGreeting()` to `Person` class.

```javascript
class Person {
  showGreeting() {
    console.log(`Hello, How are you?`);
  }
}
```

Now, any objects created from `Person` class will have `showGreeting()` as a method. Let us create one object from `Person` class.

```javascript
//...
const person1 = new Person();
person1.showGreeting(); // "Hello, How are you?"
```

`showGreeting()` always display the same message. I want to make it more dynamic. I want `showGreeting()` to greet using the person's name. For that, let us supply the class with a name while creating the object.

```javascript
//...
const person1 = new Person(`Joby`);
//...
```

We supplied a name _Joby_ to `Person` class while instantiating the object. But there is nobody inside `Person` class to receive that name and store it as a property of `person1` object. We need a `constructor()` method inside `Person` class to do this job.

Here is the updated `Person` class.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  showGreeting() {
    console.log(`Hello ${this.name}, How are you?`);
  }
}
```

When new instances of `Person` class is created, each instance objects can be accessed using `this`. Let us create 2 instance objects as shown below:

```javascript
const person1 = new Person(`Joby`);
const person2 = new Person(`Martin`);
person1.showGreeting(); // "Hello Joby, How are you?"
person2.showGreeting(); // "Hello Martin, How are you?"
```

Inside each instances, `person1` and `person2`, `this.name` refers to corresponding name value.

### Inheritance

For a class to inherit from `Person` class, we can use `extends` keyword.

```javascript
class Student extends Person {
  // class body
}
```

`Student` class now inherits all properties and methods from `Person` class. `Student` class can add more properties or methods on its own. Let us add a new method to `Student` class.

```javascript
class Student extends Person {
  showResults() {
    console.log(`Congrats! You passed`);
  }
}
```

Some of the things that we expect from a React Component are:

- React components can be used in our application by just using the component name
- React components should render something on the screen.

Inside React.js file, they have defined a class called `Component`.
