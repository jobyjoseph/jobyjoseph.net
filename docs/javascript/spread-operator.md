---
id: spread-operator
title: Spread Operator
---

From ES6, there is an operator in JavaScript to spread. Spread what? From ES6, we can spread Arrays. From ES9, we can spread Objects.

## Spreading Arrays

For understanding the concept, let us take an array.

```javascript
const cards = [2, 7, 9];
```

In your brain imagine the array `cards` as an array of playing cards. We now have 3 cards with value 2, 7 and 9.

Spread operator looks like this: `...`. If you see the spread operator with an array, then it means, we are telling JavaScript engine to take the array(set of cards) and distribute it(spread it) one by one. It will be like taking the 3 cards and giving one card each to some one. We will see different scenarios where spread operator makes things easy for us.

### Add New Elements to Array

We need to add 2 more elements `3` and `5` to our `cards` array and return a new array. Using spread operator it is written like this.

```javascript
const newCards = [...cards, 3, 5];
```

### Copy Elements of an Array

We can easily do a shallow copy of one array to another.

```javascript
const cardsCopy = [...cards];
```

## Spreading Objects

Spread operator when used with objects helps to extract the different elements of an object. At the time of writing, this is a new feature. Spread operator with objects was added in ES9. We can do many tasks quickly using spread operator like copying objects and adding new properties.

### Shallow Copy an Object

We can use spread operator to shallow copy an object. Here, we have an object with 3 elements.

```javascript
const car = {
  name: "Mercedes",
  model: "GLS",
  year: 2019
};
```

Our intention is to copy the elements of `car` to a new constant called `newCar`. We can do that with spread operator.

```javascript
const newCar = { ...car };
```

Here `...car` picks all elements of `car` and distributes it to form the different elements of new object. The newly created object is then assigned to `newCar`.

> Since it is a new feature at the time of writing, my Babel is not able to understand the syntax and throwing an error. When webpack compiled, it throwed an error saying "Module build failed: SyntaxError: Unexpected token" and is pointing to the line containing `...car`.

#### Add Babel Support for Object Spread Operator

There is a babel plugin which brings the support for object spread operator. It is called **babel-plugin-transform-object-rest-spread** in Babel v6 and **@babel/plugin-proposal-object-rest-spread** in Babel v7.

In Babel 6, we can install it by running following command in project folder.

```
npm install --save-dev babel-plugin-transform-object-rest-spread
```

or you can install using yarn by

```
yarn add --dev babel-plugin-transform-object-rest-spread
```

Once the plugin is installed, add `"transform-object-rest-spread"` to the `plugins` array inside `.babelrc` file. Thats all to make object spread operator to work. Now you can run the project to see it working.
