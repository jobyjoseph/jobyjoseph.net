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
