---
id: higher-order-component
title: Higher Order Component
---

A Higher Order Component(HOC) renders another component. It might seem strange or you might be thinking about the use of such a component. We will take it step by step.

## Avoid Repetition

Imagine we are going to create many reusable react components which other developers can use. Assume that the components below are a _Slider_ component and _Carousel_ component created by us.

```javascript
const Slider = () => <h1>This is a Slider</h1>;

const Carousel = () => <h1>This is a Carousel</h1>;
```

Now, say our product name is _ReactPack_. So we would like to add the branding message in every component we provide.

```javascript
const Slider = () => (
  <div>
    <h1>This is a Slider</h1>
    <p>Powered by ReactPack</p>
  </div>
);

const Carousel = () => (
  <div>
    <h1>This is a Carousel</h1>
    <p>Powered by ReactPack</p>
  </div>
);
```

Are you getting a feeling that the repeated usage of branding message could be prevented? Yes. It can be done with the help of a Higher Order Component.

First let us write a normal function that returns our HOC.

```javascript
const reactPack = Component => {};
```

This function accepts a Component as input. Later we will be passing `Slider` and `Carousel` as the arguments to `reactPack`. As discussed earlier, `reactPack` is intended to return a Higher Order Component. So we are going to return a component from `reactPack`.

```javascript
const reactPack = Component => {
  return () => {};
};
```

Now the returned component is going to wrap the input component. It will also add the branding text while wrapping.

```javascript
const reactPack = Component => {
  return () => (
    <div>
      <Component />
      <p>Powered by ReactPack</p>
    </div>
  );
};
```

We can then use the `Slider` component by calling `reactPack(Slider)`. Here is the complete code.

```javascript
import React from "react";
import ReactDOM from "react-dom";

// Component 1
const Slider = () => <h1>This is a Slider</h1>;
// Component 2
const Carousel = () => <h1>This is a Carousel</h1>;

const reactPack = Component => {
  // Returning Higher Order Component
  return () => (
    <div>
      <Component />
      <p>Powered by ReactPack</p>
    </div>
  );
};

const MySlider = reactPack(Slider);

ReactDOM.render(<MySlider />, document.getElementById("app"));
```

We can also use the `Carousel` component by `reactPack(Carousel)`. Now we successfully implemented Higher Order Component to reuse code.
