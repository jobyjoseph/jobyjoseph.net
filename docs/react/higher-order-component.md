---
id: higher-order-component
title: Higher Order Component
---

A Higher Order Component(HOC) renders another component. It might seem strange or you might be thinking about the use of such a component. We will take it step by step.

## Wrapping Components

Imagine we are going to create many reusable react components which other developers can use. Assume that the components below are a _Slider_ component and _Carousel_ component created by us.

```jsx
const Slider = () => <h1>This is a Slider</h1>;

const Carousel = () => <h1>This is a Carousel</h1>;
```

Now, say our product name is _ReactPack_. So we would like to add the branding message in every component we provide.

```jsx
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

```jsx
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

```jsx
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

We can also use the `Carousel` component by `reactPack(Carousel)`. Now we successfully implemented Higher Order Component to wrap a component with some HTML.

## Passing `props`

In the previous section, we learned how a Higher Order Component renders another component. Now we have a situation where the HOC needs to render a component that depends on props. We are going to learn how a Higher Order Component renders another component that requires `props`.

We have a simple component that prints `name` and `age` from props.

```jsx
const Profile = props => (
  <div>
    {props.name} is {props.age} years old.
  </div>
);
```

Let us create a function that returns a Higher Order Component.

```jsx
const generateHOC = WrappedComponent => {
  return props => (
    <div>
      <WrappedComponent {...props} />
      <p>From HOC</p>
    </div>
  );
};

const ProfileWrapper = generateHOC(Profile);
```

`generateHOC` is a simple function. It accepts a component as its argument. The function returns another component. The returned component gets the `props` and pass it on to the child component. When using `...props`, whatever props coming is passed as attributes to the component.

Later we call `generateHOC` function to obtain the HOC. So, `ProfileWrapper` is an HOC which is used in rendering.

```jsx
ReactDOM.render(
  <ProfileWrapper name="John" age="4" />,
  document.getElementById("app")
);
```

We just learned how to handle props when dealing with Higher Order Components.
