# REACT knowledge base

## 📚 React Fundamentals
+ 📖 [Сomponents](https://github.com/SKindij/Getting-Started-React.js/tree/main/Components)
    - JSX syntax
    - class component
    - functional component
    - simple component
+ 📖 [Props](https://github.com/SKindij/Getting-Started-React.js/tree/main/Props-and-State)
    - how to pass data from parent to child components
+ 📖 [State](https://github.com/SKindij/Getting-Started-React.js/tree/main/Props-and-State)
    - how to manage state within a component
+ 📖 [Component Lifecycle](https://github.com/SKindij/Getting-Started-React.js/tree/main/Component-Lifecycle)
    - how to use methods to control component behavior
    - common use cases for each method
+ 📖 [Handling Events](https://github.com/SKindij/Getting-Started-React.js/tree/main/Handling-Events)
    - how to handle user events in components
    - examples of common event handlers
+ 📖 [Conditional Rendering](https://github.com/SKindij/Getting-Started-React.js/tree/main/Conditional-Rendering)
    - how to conditionally render components
    - Ternary operator and logical operators
    - Rendering lists and mapping data to components
+ 📖 [Forms in React](https://github.com/SKindij/Getting-Started-React.js/tree/main/Forms)
    - how to handle form submission
    - how to manage form input fields with state
    - validating form input data
+ 📖 [Styling in React](https://github.com/SKindij/Getting-Started-React.js/tree/main/Styling-in-React)
    - different ways to style components
    - CSS-in-JS libraries like Styled Components
    - best practices for styling components


## 📚 React Hooks   
&emsp;React Hooks are a powerful way to manage state and lifecycle methods in React.
+ 📖 [Introduction](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#introduction)

| Hooks                                                                                       | Usage                                           | Features                                                                                                                                                                                                                         |
|---------------------------------------------------------------------------------------------|-------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 📖[useState](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#statehook) | Managing component state                        | - declare and update state variables in functional components;<br>- returns array with current state value and funct to update state;<br>- allows func components to have state similar to class components;                |
| 📖[useEffect](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#effecthook) | Side effects (e.g., data fetching, subscriptions) | - perform side effects in func components;<br>- runs after every render by default;<br>- takes function as its first argument that can perform cleanup operations;<br>- can specify dependencies to control when it should run; |
| 📖[useContext](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#usecontext) | Accessing context within components              | - access and consume data from Context provider in func components;<br>- provides way to avoid prop drilling and pass data between components without intermediaries;                                            |
| 📖[useReducer](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#usereducer) | Managing complex state with actions              | - manage state in more complex and predictable way;<br>- accepts reducer func and initial state, returns current state and dispatch func to update state;<br>- Ideal for state with complex logic.        |
| 📖[useCallback](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#additional) | Optimizing function references                   | - memoize functions to prevent unnecessary re-renders in child components;<br>- returns memoized version of callback function;<br>- Useful when passing callbacks to child components that rely on reference equality.    |
| 📖[useMemo](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#additional) | Memoizing expensive computations                  | - memoize result of expensive computation;<br>- returns memoized value that only recalculates when its dependencies change;<br>- can improve performance by avoiding unnecessary calculations;                          |
| 📖[useRef](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#additional) | Refs and accessing DOM elements                  | - access DOM nodes or store mutable values;<br>- returns mutable ref object that persists across component renders;<br>- allows imperative access to underlying DOM or accessing child component instances;              |

+ 📖 [Custom Hooks](https://github.com/SKindij/Getting-Started-React.js/tree/main/Hooks#customhooks)
    - how to create them
    - extract common logic into Hook
    - best practices


## 📚 React Router
&emsp;If you plan to create multi-page applications, you'll need to learn about React Router.\
This library allows you to manage your application's routes and navigation. 
+ 📖 [Introduction](https://github.com/SKindij/Getting-Started-React.js/tree/main/React-Router#introduction)
    - need for routing in SPA
    - benefits and features
+ 📖 [Route Rendering](https://github.com/SKindij/Getting-Started-React.js/tree/main/React-Router#settings)
    - configuring basic routing in React app
    - `<Switch>` and `<Redirect>` components
    - `<Route>` component with `path` prop
    - setting up entry point for routing
    - route configuration options
    - using `useParams` hook
+ 📖 [Navigation and Linking](https://github.com/SKindij/Getting-Started-React.js/tree/main/React-Router#navlink)
    - difference between `<Link>` and `<a>` tags
    - using `history` object or `useHistory` hook
    - using `useLocation` hook  
+ 📖 [Route Guards and Authentication](https://github.com/SKindij/Getting-Started-React.js/tree/main/React-Router#guards)
    - using `<Prompt>` component
    - checking user authentication status
+ 📖 [Advanced Topics](https://github.com/SKindij/Getting-Started-React.js/tree/main/React-Router#advanced)
    - Server-side Rendering
    - code-splitting & lazy-loading
    - animations and transitions between routes


## 📚 Redux
&emsp;Redux is a popular state management library used in many React applications.\
It can be a bit complex to learn, but it's a powerful tool once you understand it. 
+ 📖 Store
+ 📖 Actions
+ 📖 Reducers
+ 📖 Store Subscriptions
+ 📖 React-Redux
    - Provider component
    - connect function
+ 📖 Middleware
+ 📖 DevTools
+ 📖 Advanced Topics
    - selectors
    - immutability
    - testing

- - -

## 📚 **R&nbsp;E&nbsp;A&nbsp;C&nbsp;T** Libraries for 2023
+ 📖 how to set up React project
  - [Create React App](https://create-react-app.dev/)
  - [Vite](https://vitejs.dev/) _for client-side app_
  - [Next](https://nextjs.org/) _for server-side rendered app_
  - [Remix](https://remix.run/) _for full stack web app_
  - [Astro](https://astro.build/) _for static-side generated app_

+ 📖 deploy and host React application
  - [DigitalOcean](https://www.digitalocean.com/) _if you want to have full control_
  - [Netlify](https://www.netlify.com/) _if you want to have someone taking care of everything_
  - [Vercel](https://vercel.com/) _popular solution for Next.js_
  - [Render](https://render.com/)

- - -

## 📚 Extracurricular reading 

+  📖 user authentication in React app
  - popular tools and libraries
  - custom user auth system
+  📖 








