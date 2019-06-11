---
id: objects
title: Objects Basics
---

An **object** is a collection of related data and/or functionality. In the following code, `car` is an example of _object_ in JavaScript.

```javascript
const car = {
  model: "GLS",
  company: "Mercedes"
};
```

As you can see an object is a collection of key value pairs.

## Empty Object

An object with no properties or methods inside it is an empty object.

```javascript
const car = {};
```

#### Usage Scenario

Say, we are going to create a `student` object. But all the properties of `student` object is not available initially. In that case we start with an empty object at the start of program.

```javascript
const student = {};
```

Then as the program progresses, we start assigning properties to `student` object.

```javascript
//...
student.name = `${firstName} ${lastName}`;
//...
student.marks = totalMarks;
```

Finally, we will get a `student` object with two properties, `name` and `marks`.

## Object Literal

As seen above, in JavaScript we can literally write an object by wrapping a set of key value pairs inside curly brackets `{}`.

```javascript
const car = {
  model: "GLE",
  company: "Mercedes"
};
```

In case of strings, we have string literals like `"hello"`, `"apple"` and so on. Object literals are something in similar lines for Objects.

#### Usage Scenario

In our application, we might need to store the configuration of something as an object literal. The key-value pair will be later used in our application.

```javascript
const config = {
  dbName: "library",
  host: "localhost",
  username: "johndoe",
  password: "pass123"
};
```

## Reading an Object properties

As we already discussed, object is a collection of related information. We have an object here `student` with some properties and method.

```javascript
const student = {
  name: "Joby",
  course: "Computer Science",
  subject1Mark: 92,
  subject2Mark: 89,
  subject3Mark: 91,
  getAverageMark: function() {
    return (this.subject1Mark + this.subject2Mark + this.subject3Mark) / 3;
  }
};
```

### Using Dot `.` operator

As you already know, we can use dot(`.`) operator to read the value of an object key. We can read the value of `name` property using `.` operator.

```javascript
console.log(student.name); // "Joby"
```

### Using Bracket Notation `[]`

We can also access object properties using `[]` notation.

```javascript
console.log(student["name"]); // "Joby"
```

The syntax looks very similar to how we access elements of an array. That is the reason why objects can also be called as **associative arrays**.

#### Usage Scenario:

Sometimes objects have illegal identifier characters in the key.

```javascript
const person = {
  "full-name": "Joby Joseph"
};
```

`person` is a perfectly legal object. Now if we are trying to get the value of `full-name` using `.` operator, it will not work as expected.

```javascript
console.log(person.full - name);
```

In this situation we need to use the bracket syntax.

```javascript
console.log(person["full-name"]); // "Joby Joseph"
```

#### Usage Scenario:

Sometimes the key to extract might reside inside a variable. In that case, we use bracket notation `[]`, to get the value. From the above `student` object, if we are printing the marks in a loop, we can do like this.

```javascript
for (let i = 1; i <= 3; i++) {
  console.log(student[`subject${i}Mark`]);
}
```

Above code will output `92`, `89`, `91` in different lines. Here we used template literal string inside bracket notation.

### Reading non-existent property

Say we have an object `car` with two properties `model` and `year`.

```javascript
const car = {
  model: "Mercedes GLS",
  year: 2019
};
```

Now we are trying to get the value of a property `color` which is not in `car` object. Will it throw an error? No. Instead it will return `undefined`.

```javascript
console.log(car.color); // undefined
```

## Setting Object Properties

We saw that we can read properties of an object either using dot(`.`) operator or using bracket notation`[]`. We can use the same operators to add / edit properties of an object. Here, we have an object `car`.

```javascript
const car = {
  model: "Mercedes GLS",
  year: 2019
};
```

### Adding new property

In JavaScript, we can dynamically create new properties or methods for an object. It can be done by just setting it. In `car` object, there is no `color` property. We can create it by just setting `color` property.

```javascript
car.color = "Black";
```

Now the `car` object looks like:

```javascript
{
  model : "Mercedes GLS",
  year : 2019,
  color : "Black"
}
```

In the above code, we created a new property `color` using dot(`.`) notation. Instead, we can also create a new property using bracket notation`[]`. Here is how it is done.

```javascript
car["color"] = "Black";
```

### Updating existing property

When we set a property of an object that does not exist, that property is created. If that property exists, then the value of that property is updated. In our `car` object, the `model` and `year` property exists. The value of `year` property is `2019`. Now we are going to set the value of `year` property with a different year.

```javascript
car.year = 2020;
```

Now the `year` property is updated. Now the `car` object looks like:

```javascript
{
  model : "Mercedes GLS",
  year : 2020
}
```

As in the case of creating a new property, we can also update a property using bracket notation`[]`.

```javascript
car["year"] = 2020;
```

> Note that when we used bracket notation, `year` is wrapped in quotes to form a string literal. If we use it without quotes, JavaScript engine will consider it as a variable `year` and will try to resolve it.

### Using bracket notation`[]` to handle dynamic keys

We can use variables inside bracket notation. This can come handy. We have a `student` object here.

```javascript
const student = {
  name: "Joby",
  age: 33
};
```

What if the student `"Joby"` have a unique property `dreamingAbout`? How can we add that?

```javascript
let dynamicProperty = "dreamingAbout";
let dynamicValue = "Riding Mercedes GLS AMG";
student[dynamicProperty] = dynamicValue;
```

See how we used variables to add a key value pair for an object. This can be achieved only using bracket notation`[]`. Now the new property is ready to use.

```javascript
console.log(student.dreamingAbout); // "Riding Mercedes GLS AMG"
```
