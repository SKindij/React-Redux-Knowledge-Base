# 📚 React Router

## <a name="introduction"></a>📖 Introduction to React Router

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


## <a name="settings"></a>📖 Setting up Routes

&emsp; Once installed, you can import necessary components from react-router-dom and define your routes. 

> _Let's say we have **pages** folder with attached files. It contains **index.js** file, through which we can organize general export of our pages._
> > ```javascript
> >  import MainPage from "./MainPage";
> >  import ResidentialGates from "./ResidentialGates";
> >  import IndustrialGates from "./IndustrialGates";
> >  import GarageRollerShutters from "./GarageRollerShutters";
> >  import WindowRollerShutters from "./WindowRollerShutters";
> >  import Page404 from './404';
> > 
> > export {MainPage, ResidentialGates, IndustrialGates, GarageRollerShutters, WindowRollerShutters, Page404};
> > ```

&emsp; The `<Switch>` component is used to render only the first `<Route>` or `<Redirect>` that matches the current location. This is useful when you want to ensure that only one route is rendered at a time. 

&emsp; The `<Route>` component can be used without the path prop to render content that should always be visible, regardless of the current location. This is useful for creating components such as headers, footers, or sidebars that are displayed on every page. 

> _Here's an example of setting up routes:_
> > ```javascript
> >  import React from 'react';
> >  import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
> >  
> >  import AppHeader from "../appHeader/AppHeader";
> >  import { MainPage, ResidentialGates, IndustrialGates, GarageRollerShutters, WindowRollerShutters, Page404 } from '../pages';
> >    
> >  function App() {
> >    return (
> >      <Router>
> >        <div className="app">
> >          {/* Route can be used without path prop */}  
> >          <Route component={AppHeader} />
> >          <main>
> >            <Switch >
> >            {/* ensures that only one route is rendered at a time */}  
> >              <Route exact path="/" component={MainPage} />
> >              <Route path="/residential" component={ResidentialGates} />
> >              <Route path="/industrial" component={IndustrialGates} />
> >              <Route path="/garageroller" component={GarageRollerShutters} /> 
> >              <Route path="/windowroller" component={WindowRollerShutters} />  
> >              <Route path="*" component={Page404} />
> >            </Switch>
> >              <Route component={AppFooter} />
> >          </main>
> >        </div>
> >      </Router>
> >    );
> >  }
> >  
> >  export default App;
> > ```

&emsp; `<Route>` component has several configuration options. Here are some commonly used ones:
+ **path**: _specifies URL pattern to match for route;_
+ **component**: _specifies component to render for matched route;_
+ **exact**: _matches route exactly (without it, partial matches will also render component);_
+ **render**: _allows rendering inline function as component instead of separate component file;_
+ **children**: _similar to render, but always renders, regardless of URL match._

### `useParams` hook allows you to access the dynamic parameters from the URL. 

> _For example, you have a route for displaying product details_\
> _each product has unique identifier, which is used in URL to identify specific product_
> > ```javascript
> >  // you can use useParams hook to retrieve product ID from URL 
> >  // and fetch corresponding product details from API
> >  import React, { useEffect, useState } from 'react';
> >  import { useParams } from 'react-router-dom';
> >  
> >  function ProductDetails() {
> >    const { productId } = useParams();
> >    // retrieved product details are stored in product state 
> >    const [product, setProduct] = useState(null);
> >
> >    // use to fetch product details when productId changes
> >    useEffect( () => {
> >      // fetch product details based on productId
> >      // this can be API call or data retrieval from database
> >      const fetchProductDetails = async () => {
> >        try {
> >          const response = await fetch(`/api/products/${productId}`);
> >          const data = await response.json();
> >          setProduct(data);
> >        } catch (error) {
> >          console.error('Error fetching product details:', error);
> >        }
> >      };
> >      fetchProductDetails();
> >    }, [productId] );
> >    // while waiting for product details to be fetched, we display loading message
> >    if (!product) {
> >      return <div>Loading...</div>;
> >    }
> >    // once product details are available, we render product information
> >    return (
> >      <div>
> >        <h2>{product.name}</h2>
> >        <p>{product.description}</p>
> >        <p>Price: ${product.price}</p>
> >        {/* Additional product details and components */}
> >      </div>
> >    );
> >  }
> >  
> >  export default ProductDetails;
> > ```
> _To set up the route for products, you can add a new <Route> component in your route configuration:_
> > ```javascript
> >  <Route path="/products/:productId" component={ProductDetail} />
> >  // when you access URL like /products/127, ProductDetail component will be rendered, and 
> >  // productId parameter will be available for use through useParams hook
> > ```

  
## <a name="navlink"></a>📖 Navigation and Linking

&emsp; In React Router, `<Link>` component is used for internal navigation within your application. It provides declarative navigation, allowing you to navigate to different routes without causing a full page reload. On the other hand, `<a>` tag is a standard HTML anchor tag used for external navigation, which can cause a full page reload when clicked.

> _Here's an example of using `<Link>` in MainPage component with Bootstrap styles_
> > ```javascript
> > import React from 'react';
> > import { Link } from 'react-router-dom';
> >   
> > import residentialGateImg from '../../resources/residential-gate-image.png';
> > import industrialGateImg from '../../resources/industrial-gate-image.png';
> > 
> > function MainPage() {
> >   return (
> >     <div className="container">
> >       <h2>Main Page</h2>
> >       <div className="row">
> >         <div className="col-md-6">
> >           <div className="card mb-4">
> >             <img src={residentialGateImg} className="card-img-top" alt="Residential Garage Gate" />
> >             <div className="card-body">
> >               <h5 className="card-title">Residential Gates</h5>
> >               <p className="card-text">Explore our range of residential gates.</p>
> >               <Link to="/residential" className="btn btn-primary">View Residential Garage Gates</Link>
> >             </div>
> >           </div>
> >         </div>
> >         <div className="col-md-6">
> >           <div className="card mb-4">
> >             <img src={industrialGateImg} className="card-img-top" alt="Industrial Garage Gate" />
> >             <div className="card-body">
> >               <h5 className="card-title">Industrial Gates</h5>
> >               <p className="card-text">Discover our selection of industrial gates.</p>
> >               <Link to="/industrial" className="btn btn-primary">View Industrial Garage Gates</Link>
> >             </div>
> >           </div>
> >         </div>
> >         {/* Add more cards for other categories */}
> >       </div>
> >     </div>
> >   );
> > }
> > 
> > export default MainPage;
> > ```

#### **history object** 
+ represents the navigation history of your application; 
+ allows to programmatically navigate between different URLs, manipulate browser history, and control navigation flow;
+ includes methods like:
  * ``push(path, [state])``
    - used to navigate to new URL and add it to navigation history stack;
    - ```javascript
        // path: string representing URL or path you want to navigate to
        history.push('/new-page');
        // state (optional): object that you can pass to carry state data along with URL
        history.push('/products/123', { productId: 123, category: 'electronics' });
      ```
    - allows user to navigate back to previous page using browser's back button;
  * ``replace(path, [state])``
    - replaces the current URL in the navigation history stack with a new URL
    - ```javascript
        // path: string representing URL or path you want to navigate to
        history.replace('/another-page');
        // state (optional): object that carries state data to be accessed in destination component
        history.replace('/products/147', { productId: 147, category: 'accessories' });
      ```
    - useful when you want to replace current URL in history stack, without adding new entry;
    - commonly used for scenarios like form submissions or after completing certain action;    
  * ``goBack()``
    - used to navigate back to previous URL in navigation history stack;
    - it is similar to browser's back button functionality;
    - ```javascript
        // path: string representing URL or path you want to navigate to
        history.goBack();
      ```  
  
> _We can test this functionality, for example, in the ResidentialGate component._
> > ```javascript
> >  import React from 'react';
> >  import { useLocation, useHistory } from 'react-router-dom';
> >  
> >  const ResidentialGates = () => {
> >    const location = useLocation();
> >    const history = useHistory();
> >  
> >    const handleProductClick = (productId) => {
> >      history.push(`/residential/${productId}`);
> >    };
> >    // this will effectively resetting section or returning to beginning of section
> >    const handleReplaceClick = () => {
> >      history.replace('/residential');
> >    };
> >  
> >    return (
> >      <div>
> >        <h2>Residential Gates</h2>
> >  	  <p>Current location: {location.pathname}</p>
> >        <p>Select a product:</p>
> >        <ul>
> >          <li onClick={() => handleProductClick('rd101')}>Product 101</li>
> >          <li onClick={() => handleProductClick('rd102')}>Product 102</li>
> >          <li onClick={() => handleProductClick('rd103')}>Product 103</li>
> >  		<li onClick={() => handleProductClick('rd104')}>Product 104</li>
> >  		<li onClick={() => handleProductClick('rd105')}>Product 105</li>
> >        </ul>
> >     {/* this is standard way to implement "Go Back" functionality in React Router */} 
> >  	  <p>Go back to the previous action:</p>
> >     <button onClick={history.goBack}>Go Back</button>
> >     {/* it provides way for user to go back to initial state of Residential Gates section */}  
> >  	  <p>Return to the beginning of the section:</p>
> >  	  <button onClick={handleReplaceClick}>Replace</button>
> >      </div>
> >    );
> >  };
> >  
> >  export default ResidentialGates;
> > ```  

&emsp; The `<Redirect>` component is used to perform programmatic redirects to a specified URL. It can be used, for example, after a form submission or when certain conditions are met. 
> ```javascript
>  import React, { useState } from 'react';
>  import { Redirect } from 'react-router-dom';
>  
>  function LoginPage() {
>    const [isLoggedIn, setLoggedIn] = useState(false);
>  
>    const handleLogin = () => {
>      // perform login logic
>      setLoggedIn(true);
>    };
>  
>    if (isLoggedIn) {
>      // go to dashboard after login
>      return <Redirect to="/dashboard" />; 
>    }
>  
>    return (
>      <div>
>        <h2>Login Page</h2>
>        {/* Login form */}
>        <button onClick={handleLogin}>Login</button>
>      </div>
>    );
>  }
>  
>  export default LoginPage;
> ```  
  
  
## <a name="guards"></a>📖 Route Guards and Authentication 

### using `<Prompt>` component
&emsp; This component is used to prompt the user for confirmation before navigating away from the current page. It is often used to prevent accidental loss of data when the user has entered information in a form but has not submitted it yet. 
  
> ```javascript
>  import React, { useState } from 'react';
>  import { Prompt } from 'react-router-dom';
>  
>  function ContactForm() {
>    const [formData, setFormData] = useState({ name: '', email: '' });
>    const [isFormDirty, setFormDirty] = useState(false);
>  
>    const handleChange = (e) => {
>      // use destructuring to extract name and value properties from e.target object
>      const { name, value } = e.target;
>      // callback func receives previous state (prevData)
>      // spread operator (...prevData) create new object that copies all properties from prevData
>      // only specific form field being changed is updated in state, while rest of data remains unchanged
>      setFormData((prevData) => ({ ...prevData, [name]: value }));
>      setFormDirty(true);
>    };
>  
>    const handleSubmit = (e) => {
>      e.preventDefault();
>      // perform form submission logic
>      setFormDirty(false);
>    };
>  
>    return (
>      <div>
>        <h2>Contact Form</h2>
>        <Prompt
>          when={isFormDirty}
>          message="Are you sure you want to leave? Your changes may not be saved."
>        />
>        <form onSubmit={handleSubmit}>
>          {/* form fields */}
>          <input type="text" name="name" value={formData.name} onChange={handleChange} />
>          <input type="email" name="email" value={formData.email} onChange={handleChange} />
>          <button type="submit">Submit</button>
>        </form>
>      </div>
>    );
>  }
>  
>  export default ContactForm;
> ```
      
### checking user authentication status
  
&emsp; Route guards and authentication involve checking whether a user is authenticated before allowing them to access certain routes or components. This can be done by creating a higher-order component (HOC) or a custom hook that performs the authentication check and redirects the user if necessary.   
  
> ```javascript
>  import React from 'react';
>  import { Route, Redirect } from 'react-router-dom';
>  
>  // Assume you have a function that checks the user's authentication status
>  const isAuthenticated = () => {
>    // Check authentication status (e.g., from a token, session, or local storage)
>    // Return true if authenticated, false otherwise
>  };
>  
>  // PrivateRoute takes in component prop (which represents component to render) and
>  //  any other props specified using spread operator (...rest)
>  const PrivateRoute = ({ component: Component, ...rest }) => (
>    <Route
>      {...rest}
>      render={(props) =>
>        isAuthenticated() ? (
>          <Component {...props} />
>        ) : (
>          <Redirect to="/login" /> // go to login page if not authenticated
>        )
>      }
>    />
>  );
>  
>  function Dashboard() {
>    return <h2>Dashboard</h2>;
>  }
>  
>  function App() {
>    return (
>      <Router>
>        <div className="app">
>          <Switch>
>            <Route path="/login" component={LoginPage} />
>            <PrivateRoute path="/dashboard" component={Dashboard} />
>            <Redirect to="/login" />
>          </Switch>
>        </div>
>      </Router>
>    );
>  }
>  
>  export default App;
> ```
  
  

## <a name="advanced"></a>📖 Advanced Topics  
  
### Server-side Rendering  
&emsp; SSR is a technique in web development where the server generates the initial HTML content and sends it to the client. In the context of React Router, server-side rendering refers to rendering the React components on the server and sending the fully rendered HTML to the client, rather than relying on the client-side JavaScript to render the components. 
  
&emsp; Server-side rendering is useful for several reasons:
1. **SEO**: Search engine crawlers can more easily parse and index the content of your website if it is rendered on the server. This can improve the visibility of your website in search engine results.
2. **Performance**: SSR can provide faster initial page load times since the server sends the pre-rendered HTML to the client. This can enhance the perceived performance of your application, especially for users with slower network connections.
3. **Accessibility**: SSR ensures that your content is accessible even if the client's browser has JavaScript disabled or encounters issues loading JavaScript.  

&emsp; To implement SSR with React Router, you need to use a server-side rendering framework or tool that supports React, such as Next.js, Razzle, or Express.js with a custom setup. These frameworks allow you to define server-side routes that correspond to your React components. When a request is made to a specific route, the server renders the corresponding component and sends the generated HTML to the client.
  
&emsp; The process typically involves the following steps:
1. Set up a server-side rendering framework or tool that supports React.
2. Define server-side routes that correspond to your React components. These routes determine how the server should handle requests and render the components.
3. Configure the server to handle requests and render the React components using the appropriate server-side rendering framework or tool. This may involve setting up middleware, configuring routes, and defining server-side rendering logic.
4. When a request is made to a specific route, the server renders the corresponding React component and generates the HTML content.
5. Send the generated HTML content as the response to the client.
6. On the client-side, the JavaScript bundle is loaded and takes over the rendering and navigation of the application. The client-side JavaScript rehydrates the React components, attaching event handlers and state.
  
&emsp; However, keep in mind that server-side rendering adds complexity to the development process and may require additional setup and configuration compared to client-side rendering.  
   
### code-splitting & lazy-loading
&emsp; They are techniques used in React Router to optimize the loading and performance of your application. These techniques allow you to split your application's code into smaller, more manageable chunks and load them on-demand when needed.  
 
&emsp; **Code-splitting** involves breaking down your application's JavaScript bundle into smaller chunks, also known as "chunks" or "bundles." Each chunk contains a portion of your application's code, such as a specific route or component. By splitting your code, you can reduce the initial bundle size, which leads to faster loading times.

&emsp; **Lazy-loading** refers to the practice of loading components or routes asynchronously when they are needed, rather than loading them all upfront. This means that components or routes are only loaded when a user navigates to them, resulting in faster initial page load times and improved performance.  
  
> _React's lazy function enables lazy-loading of components._
> _Suspense allows you to show fallback content, such as loading spinner, while lazily loaded component is being fetched._
> > ```javascript  
> >  const MyComponent = React.lazy(() => import('./MyComponent'));
> >  
> >  function App() {
> >    return (
> >      <div>
> >        <Suspense fallback={<div>Loading...</div>}>
> >          <MyComponent />
> >        </Suspense>
> >      </div>
> >    );
> >  }
> > ```  
    
### animations and transitions between routes 
  
  
  
  
  
  
  
  


