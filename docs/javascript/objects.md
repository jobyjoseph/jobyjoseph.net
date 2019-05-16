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
