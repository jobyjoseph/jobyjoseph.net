---
id: react-router
title: React Router
---

A website consist of multiple web pages. Each web pages can have different UI states like _Tab 1 selected_, _Form submitted_ and so on. It is good to have a unique path to identify different web pages and UI states. These unique paths are called **Routes**.

## Server Side Routing vs Client Side Routing

Server-side routing is more traditional approach. We are seeing it from beginning of web. We have seen web servers like Apache, serving html files like:

```
http://example.com/index.html
http://example.com/about.html
http://example.com/contact.html
```

When websites started heavily dependant on search engines like Google, Bing and so on. Search engines provided most of the traffic to websites. As part of optimizing websites for search engines, developers started rendering pretty urls without unwanted file extensions. After making above urls pretty, it might look like this:

```
http://example.com/
http://example.com/about
http://example.com/contact
```

Again, this prettying job is done from the server side. We can configure web servers like Apache and tell Apache to serve `about.html` if somebody is requesting for `/about` path.

Client-side routing is more modern approach. Here, creating unique paths to different pages is done by the browser.

Client-side routing in most of the cases provide better performance compared to server-side routing. Let us take a simple scenario to understand this. In most of the websites, the header and footer of the site is same in all pages. In server-side rendering, for each page requests like `/`, `/about` or `/contact`, the full header and footer is transferred from server on every page load. That results in more bytes transferred from server to client. That makes the site slow. In client-side rendering, we can keep header and footer intact when visiting a new page. Only the page specific content is loaded from server in the background and shown to user. This provides a better user experience.
