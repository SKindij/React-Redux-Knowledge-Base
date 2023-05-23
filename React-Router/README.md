## 📚 React Router

### <a name="introduction"></a>📖 Introduction to React Router

&emsp;In a single-page application (SPA), all the necessary HTML, CSS, and JavaScript are loaded initially, and subsequent interactions with the application are handled dynamically without requiring full page reloads.\
&emsp;Routing is essential in SPAs to handle different views or pages within the application without actually navigating to a new HTML page.

&emsp;React Router is a library that allows you to add routing functionality to your React applications. 
It helps to create URLs for different pages or components in your application, allowing the user to navigate between them using the browser's address bar or links.

React Router offers several features and benefits, including:
+ Component-based routing: 
  - _you can associate specific components with different routes, making it easy to render appropriate component based on current URL._
+ Nested routing: 
  - _it allows you to nest routes within each other, creating hierarchical structure for your application's views._
+ Programmatic navigation: 
  - _you can programmatically navigate between routes, either in response to user actions or as result of certain conditions being met._
+ URL parameter handling: 
  - _it provides built-in support for extracting and utilizing URL parameters in your components._
+ Query parameter handling: 
  - _it allows you to parse and retrieve query parameters from the URL, enabling more dynamic behavior in your application._
+ Route guards and authentication: 
  - _features for implementing route guards, allowing you to control access to certain routes based on authentication or other conditions._
 
&emsp;React Router v6, the latest major version, introduces a more intuitive and simplified API compared to previous versions. It provides improved nesting, route matching, and streamlined navigation methods.

> To install the React Router:\
> ```bash
>  npm install react-router-dom \
>    localforage \
>    match-sorter \
>    sort-by
> ```
> >  - _package, which provides the necessary components and functionality for routing_
> >  - _JavaScript library that simplifies usage of web browser's IndexedDB API for storing data;_
> >  - _It provides simple API for storing and retrieving data in a key-value format._
> >  - _utility for sorting and filtering arrays or collections based on given search query_
> >  - _package for sorting array of objects based on given property or properties;_


### <a name="setting-routes"></a>📖 Setting up Routes

&emsp; Once installed, you can import necessary components from react-router-dom and define your routes. 

> _Here's an example of setting up routes:_
> ```javascript
>  import React from 'react';
>  import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
>  import Home from './components/Home';
>  import ResidentialGates from './components/ResidentialGates';
>  import IndustrialGates from './components/IndustrialGates';
>  import NotFound from './components/NotFound';
>  
>  function App() {
>    return (
>      <Router>
>        <Switch >
>        {/* ensures that only one route is rendered at a time */}  
>          <Route exact path="/" component={Home} />
>          <Route path="/about" component={ResidentialGates} />
>          <Route path="/about" component={IndustrialGates} />
>          <Route component={NotFound} />
>        </Switch>
>      </Router>
>    );
>  }
>  
>  export default App;
> ```


The <Route> component has several configuration options. Here are some commonly used ones:
+ **path**: Specifies the URL pattern to match for the route.
+ **component**: Specifies the component to render for the matched route.
+ **exact**: Matches the route exactly (without it, partial matches will also render the component).
+ **render**: Allows rendering an inline function as the component instead of a separate component file.
+ **children**: Similar to render, but always renders, regardless of the URL match.






















