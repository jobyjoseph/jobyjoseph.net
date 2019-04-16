---
id: react-router
title: React Router
---

A website might have multiple web pages. Each web pages can have different UI states like _Tab 1 selected_, _Form submitted_ and so on. It is good to have a unique path to identify different web pages and UI states. These unique paths are called **Routes**.

## Server Side Routing vs Client Side Routing

Server-side routing is more traditional approach. We are seeing it from beginning of web. We have seen web servers like Apache, serving html files like:

```
http://example.com/index.html
http://example.com/about.html
http://example.com/contact.html
```

Most of the websites heavily depend on search engines like Google, Bing and so on to bring more traffic. As part of optimizing websites for search engines, developers started rendering pretty URLs without file extensions. After making above urls pretty, it might look like this:

```
http://example.com/
http://example.com/about
http://example.com/contact
```

Again, this prettying job is done from the server side. We can configure web servers like Apache and tell Apache to serve `about.html` if somebody is requesting for `/about` path.

Client-side routing is more modern approach. Here, creating unique paths to different pages is done by the browser.

Client-side routing in most of the cases provide better performance compared to server-side routing. Let us take a simple scenario to understand this. In most of the websites, the header and footer of the site is same in all pages. In server-side rendering, for each page requests like `/`, `/about` or `/contact`, the full header and footer is transferred from server on every page load. That results in more bytes transferred from server to client. That makes the site slow. In client-side rendering, we can keep header and footer intact when visiting a new page. Only the page specific content is loaded from server in the background and shown to user. This provides a better user experience.

Client side routing is there in all popular frameworks like Angular, Vue and Backbone. But they all, including React Router uses HTML5 History API to implement client side routing. HTML5 History API detects url change and a set of actions can be implemented based on the url path.

## React Router

[React Router](https://reacttraining.com/react-router/web/guides/quick-start) helps to implement routing in React apps. In order to use React Router in our application, first we need to install it using `npm` or `yarn`

```
yarn add react-router-dom
```

There are 3 different packages with name `react-router`, `react-router-dom` and `react-router-native`. `react-router` contains code to handle routing in both web and mobile native apps. If we want to use react-router only on web, we need to install `react-router-dom`.

> At the time of writing, I faced issues while installing `react-router-dom` in node v11. I had to downgrade to node v8 to successfully install the package.

### Configuring Routes

Let us assume we have an `app.js` which contains the root component. We are going to define our routes in `app.js`. First step is to import required modules from `react-router-dom` along with other imports for `react`, `react-dom` and so on.

```
import { BrowserRouter, Route } from "react-router-dom";
```

`BrowserRouter` is used once to create a new router. `Route` is used for defining routes for each pages. For that we will provide `Route` with path to match for, like _/about_ and which component to be rendered when user visits that path.

In our `app.js` file, let us define a constant `routes` which contains the `<BrowserRouter>` component.

```javascript
const routes = <BrowserRouter>{/* Routes to be defined*/}</BrowserRouter>;

ReactDOM.render(routes, document.getElementById("app"));
```

As we can see, we are just rendering `<BrowserRouter>` component inside app container. Let us now see how to define different routes inside `<BrowserRouter>`. Before defining routes, let us keep different page components ready. Just for understanding purpose, we have 3 functional components one for home page, about page and contact page.

```javascript
const Home = () => <div>This is home page</div>;
const About = () => <div>This is about page</div>;
const Contact = () => <div>This is contact page</div>;
```

We have imported a `Route` module along with `BrowserRouter` module from `react-router-dom`. We are going to set routes using that. We update our `routes` constant as below.

```javascript
const routes = (
  <BrowserRouter>
    <Route path="/" component={Home} />
  </BrowserRouter>
);
```

As we can see, the line is pretty readable. If `path` is `/`, `Home` component is rendered. Now we need to add more `Route` elements to show other paths. But `<BrowserRouter>` accepts only one immediate node. For the same reason, we are going to wrap all `Route`s in a `div`.

```javascript
const routes = (
  <BrowserRouter>
    <div>
      <Route path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
    </div>
  </BrowserRouter>
);
```

Now as expected, when we visit `/` path, it will render `Home` component. But when we try to access `/about`, it says

```
Cannot GET /about
```

What happens here is, I am depending on `webpack-dev-server` to serve web pages. As soon the browser receives a new url request, ie `/about`, it will try to fetch that content from server. But in server, there is no path defined for `/about`. So we need to tell `webpack-dev-server` that we are planning to use HTML5 history API. For that, update the `devServer` configuration section in `webpack.config.js` as follows.

```javascript
devServer: {
  contentBase: path.join(__dirname, "public"),
  historyApiFallback: true
}
```

`historyApiFallback` tells `webpack-dev-server` that we are going to manage routing from client side. Now if `webpack-dev-server` does not find any url, it will serve `index.html` instead of 404 error. `index.html`, with the help of React Router can correctly show the component defined.

> Above webpack-dev-server issue is applicable only during development. Also, after making any change in the `webpack.config.js` file, we need to restart the server.

With the above modifications done, let us visit `/about` path. Now it will show following in the browser.

```
This is home page
This is about page
```

That is not something which we expected. We expected only second line.

This happened because when React matches a path, it will start from first character. So in our case our path is `/about`. React will then check if there is any paths defined for `/`. Yes there is. Thats why it showed `Home` component. Then it will check if there is any path starting with `/a`, then `/ab`. Like that when it reached `/about`, it got a match. Based on that match, React Router rendered `About` component also. How can we solve this?

There is an attribute for `Route` which is `exact`. Setting `exact` to `true` will render a component only if it finds an exact match.

```javascript
const routes = (
  <BrowserRouter>
    <div>
      <Route path="/" component={Home} exact={true} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
    </div>
  </BrowserRouter>
);
```

Now `Home` component is rendered if the path is exactly `/`. Now the output will render only `About` component.

```
This is about page
```

## Setting 404 Page

404 stands for the error code if a requested page is not found. In case of React Router client side routing, we so far saw how to render different components based on the router paths. But we have not handled the case when user types an invalid path in browser.

In the previous code, what will happen if user requested for `/gallery` path? It will be a blank page since no components are mapped to `/gallery` path.

Instead of showing a blank page, let us try to render a custom page for all _404 page not found_ cases.

First, let us create a component to be shown for 404 pages.

```javascript
const NotFound = () => <div>This is 404 page</div>;
```

Next, we need to add `Route` for 404 page. Here is the updated code with 404 route.

```javascript
const routes = (
  <BrowserRouter>
    <div>
      <Route path="/" component={Home} exact={true} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
      <Route component={NotFound} />
    </div>
  </BrowserRouter>
);
```

`path` attribute of `Route` is optional. Since we added _NotFound_ route as the last line out of all routes, it acts as a catch all bucket. So if we request for a path like `/gallery`, it did not make a match in the first 3 Routes. The 4th Route without `path` attribute will take all paths. For the same reason `NotFound` component will be rendered in browser as follows.

```
This is 404 page
```

Even though it seems to work, there is a problem. Let us try visiting our `/about` page. It now shows following content in browser.

```
This is about page
This is 404 page
```

What happened is React Router got a match in second Route(`<Route path="/about" component={About} />`) and also in 4th Route(`<Route component={NotFound} />`). Is there a way to tell React Router to stop at first match? Yes. It is by using `<Switch>`.

`<Switch>` is also another component defined in `react-router-dom`. To use it, we need to modify our import statement.

```javascript
import { BrowserRouter, Route, Switch } from "react-router-dom";
```

Next, we need to wrap all our `Route` components inside `<Switch>`.

```javascript
const routes = (
  <BrowserRouter>
    <Switch>
      <Route path="/" component={Home} exact={true} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
      <Route component={NotFound} />
    </Switch>
  </BrowserRouter>
);
```

Now if you remember in the previous section of this article, We learned that the `<div>` tag was used inside `BrowserRouter` for the sake of having just one node inside `BrowserRouter`. Since now we have `<Switch>` tag to wrap, let us replace `<div>` with `<Switch>`.

When `Route`s are wrapped inside `Switch`, if a match is found then further routes are discarded. So, in our case when a match is found for `/about`, React Router will show the `About` component and will not go to `NotFound` route.

We have successfully implemented _Page Not Found_ page. Just in case if you are wondering how my `app.js` file looks like now, here it is.

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter, Route, Switch } from "react-router-dom";

const Home = () => <div>This is home page</div>;
const About = () => <div>This is about page</div>;
const Contact = () => <div>This is contact page</div>;
const NotFound = () => <div>This is 404 page</div>;

const routes = (
  <BrowserRouter>
    <Switch>
      <Route path="/" component={Home} exact={true} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
      <Route component={NotFound} />
    </Switch>
  </BrowserRouter>
);

ReactDOM.render(routes, document.getElementById("app"));
```
