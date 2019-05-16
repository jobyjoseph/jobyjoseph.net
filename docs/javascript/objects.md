---
id: objects
title: Objects
---

An **object** is a collection of related data and/or functionality. In the following code, `car` is an example of _object_ in JavaScript.

```javascript
const car = {
  model: "GLS",
  company: "Mercedes"
};
```

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
