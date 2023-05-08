### <a name="introduction"></a>Introduction to React Hooks:
&emsp;They are functions that allow developers to use state and other React features in functional components. 
They were introduced in React 16.8 as a new way to write React components and manage state and lifecycle methods without using class components.

&emsp;**The benefits of React Hooks include:**
+ Simplified code: 
  - Hooks allow developers to write more concise and readable code, reducing the amount of boilerplate 
and repetitive code needed to manage state and lifecycle methods.
+ Better code organization: 
  - Hooks enable developers to separate concerns and group related logic together into custom hooks, 
making it easier to reason about and maintain code.
+ Improved performance: 
  - Hooks can improve performance by reducing the amount of re-renders and optimizing the way state is managed.

_ _ _


## <a name="state-hook"></a>State Hook
&emsp; It allows to add state to functional component. It enables you to manage and update state of your component without having to write class.
With this hook, you can declare state variable and update its value over time, triggering re-render of your component.
* to use the useState hook, you first need to import it from the react library:
  + ```javascript
      import React, { useState } from 'react';
    ```
* next, you can declare your state variable and its initial value:
  + ```javascript
      const [stateVariable, setStateVariable] = useState(initialValue);
      // 'stateVariable' is the name of your state variable
      // 'setStateVariable' is function that update value of 'stateVariable'
      // (initialValue) is initial value of 'stateVariable'
    ```
* once you have declared state variable, you can use it in your component like any other variable
  + ```javascript
      setStateVariable(newValue);
      // React will re-render component with updated value of 'stateVariable'
    ```

> _Let's say we're building a dashboard for a repair center that services microcircuits and electric motors. We want to track the number of items that come in for diagnostics and repair, and whether the repairs are covered by warranty or not._
> > ```javascript
> >  import React, { useState } from 'react';
> >  
> >  function RepairDashboard() {
> >    const [diagnostics, setDiagnostics] = useState(0);
> >    const [warrantyRepairs, setWarrantyRepairs] = useState(0);
> >    const [nonWarrantyRepairs, setNonWarrantyRepairs] = useState(0);
> >    const [rejectedRepairs, setRejectedRepairs] = useState(0);
> >  
> >    function handleDiagnosticsIncrement() {
> >      setDiagnostics(diagnostics + 1);
> >    }
> >  
> >    function handleWarrantyRepairsIncrement() {
> >        if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >          setWarrantyRepairs(warrantyRepairs + 1);
> >        }
> >    }
> >  
> >    function handleNonWarrantyRepairsIncrement() {
> >        if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >      setNonWarrantyRepairs(nonWarrantyRepairs + 1);
> >        }
> >    }
> >  
> >   function handleRejectedRepairsIncrement() {
> >       if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >         setRejectedRepairs(rejectedRepairs + 1);
> >       }
> >     }
> >   
> >    return (
> >      <div>
> >        <h2>Repair Dashboard</h2>
> >        <p>Number of items accepted for diagnostics: {diagnostics}</p>
> >        <button onClick={handleDiagnosticsIncrement}>Accept for diagnostics</button>
> >        <p>Number of warranty repairs: {warrantyRepairs}</p>
> >        <button onClick={handleWarrantyRepairsIncrement}>Accept for warranty repair</button>
> >        <p>Number of non-warranty repairs: {nonWarrantyRepairs}</p>
> >        <button onClick={handleNonWarrantyRepairsIncrement}>Accept for non-warranty repair</button>
> >        <p>Number of rejected repairs: {rejectedRepairs}</p>
> >        <button onClick={handleRejectedRepairsIncrement}>Reject repair</button>
> >      </div>
> >    );
> >  }
> > ```

Here are a few best practices for working with the useState hook:
* _Use a descriptive name for your state variable. This will make your code more readable and easier to understand._
* _Always use the setStateVariable function to update your state variable. Directly modifying the state variable could cause unexpected behavior in your component._
* _If your state variable is an object or an array, make sure to update it immutably. This means creating a new object or array with the updated value, rather than modifying the existing object or array._


## <a name="effect-hook"></a>Effect Hook allows you
+ to handle side effects 
  - any actions that your component performs outside of its scope, 
  - such as fetching data, updating document title and DOM, subscribing to events, or setting timer;
+ to run code after every render
  - specify which state variables or props it should depend on;
  - this ensures that effect is only re-run when its dependencies have changed;
  - this avoids unnecessary computations.

&emsp; The Effect Hook in React can be used to replace the functionality of componentDidMount, componentDidUpdate, and componentWillUnmount lifecycle methods.

> Here's the basic syntax for using the `useEffect` hook:
```javascript
import React, { useEffect } from 'react';

function MyComponent() {
  // hook takes two arguments:
  useEffect( () => { 
      // arg1 - callback function containing side effect code    
       // this code will run after component has rendered

     // cleanup function (such as removing event listeners or canceling timers)
     return () => {
        // cleanup code here
        // this code will run when component unmounts or when effect dependencies change
      };
    // arg2 - array of dependencies (state or props) that effect depends on  
  }, [dependency1, dependency2] ); 
// if empty ([]) -- effect only runs once, similar to componentDidMount
// if array of dependencies -- effect will run similar to componentDidUpdate 

  return (
    // JSX for the component's UI here
  );
}

export default MyComponent;
```

> _Here's an example of how you can use the Effect Hook to fetch data from an API:_
> > ```javascript
> >  import React, { useState, useEffect } from 'react';
> >  
> >  function UserList() {
> >    const [users, setUsers] = useState([]);
> >    // empty array as 2nd argument means that effect should only run once, when component mounts
> >    useEffect( () => {
> >      fetch('https://jsonplaceholder.typicode.com/users')
> >        .then( response => response.json() )
> >        .then( data => setUsers(data) );
> >    }, [] );
> >  
> >    return (
> >      <div>
> >        <h2>User List</h2>
> >        <ul>
> >          {users.map(user => (
> >            <li key={user.id}>{user.name}</li>
> >          ))}
> >        </ul>
> >      </div>
> >    );
> >  }
> > ```


## <a name="use-context"></a>useContext Hook

&emsp;Context in React allows you to share data between components without passing it down through props explicitly. It's a way to manage global state in your application that can be accessed by multiple components at different levels of the component tree.

&emsp;**Context API** consists of two main parts: 
* the **Context object**
  + it is created using the `React.createContext()` function
  + it returns an object with 
    - `Provider` component (_used to wrap parent component(s) that want to share data_), 
    - `Consumer` component (_used to access the shared data in child component(s)_);
* the **useContext Hook**
  + it is built-in hook provided by React,
  + allows to access value from nearest Provider of specific context in your component without using Consumer component;

> &emsp;**Prop drilling** is pattern where you pass down props through multiple levels of components, even if some intermediate components don't actually use those props, just to pass them down to deeply nested component that needs them.\
&emsp;It can lead to complex and hard-to-maintain code.

&emsp;**Context in React** can help you avoid prop drilling by allowing you to share data directly between components that need it, without passing it down through intermediate components. 


## <a name="use-reducer"></a>useReducer Hook

&emsp;This Hook is a way to manage complex state in your application. It's similar to the useState Hook, but it provides a more powerful way to update and manage state in your application. The useReducer Hook takes two arguments: 
  * **reducer function**
    + it responsible for handling state changes in your application;
    + takes two arguments: the current state and an action object;
    + returns new state based on the current state and the action;
  * **initial state value**.

> &emsp;Let's say we have a warehouse that stores products from different suppliers and we need to manage the inventory of those products. Each product has a unique id, a name, a description, and a quantity in stock. We need to keep track of the current inventory and update it as products are received or sold.
> > ```javascript
> >  // importing React & useReducer hook for managing state in our component
> >  import React, { useReducer } from 'react';
> >  // func that determines how state should be updated based on action type
> >  function inventoryReducer(state, action) {
> >    // to handle different action types
> >    switch (action.type) {
> >      // concatenate action.payload (array of products) to existing state.products array (...state)
> >      case 'RECEIVE_PRODUCTS':
> >        return {
> >          ...state,
> >          products: state.products.concat(action.payload),
> >        };
> >      // returns new state object with updated products array
> >      case 'SELL_PRODUCT':
> >        // extracts id property from payload of action object
> >        const productId = action.payload.id;
> >   // finds index of product in products array of current state that matches productId obtained from action 
> >        const productIndex = state.products.findIndex(p => p.id === productId);     
> >        if (productIndex !== -1 && state.products[productIndex].quantity > 0) {
> >          return {
> >    // new state object with same props as current state (...state), but with updated products array
> >            ...state,
> >            products: state.products.map(product => {
> >              if (product.id === productId) {
> >                return {
> >                  ...product,
> >                  quantity: product.quantity - 1
> >                };
> >              }
> >              return product;
> >            })
> >          };
> >        }
> >        return state;
> >      default:
> >        return state;
> >    }
> >  }
> >  // functional component that uses useReducer hook to manage its state
> >  function InventoryManager() {
> >    // initialize the state
> >    const [state, dispatch] = useReducer(inventoryReducer, {
> >      // initial state object, which contains an array of products
> >      products: [
> >        { id: 1, name: 'Product A', description: 'Description A', quantity: 10 },
> >        { id: 2, name: 'Product B', description: 'Description B', quantity: 5 },
> >        { id: 3, name: 'Product C', description: 'Description C', quantity: 3 }
> >      ]
> >    });
> >    // helper functions - dispatch actions to inventoryReducer to update state
> >    function receiveProducts(products) {
> >      dispatch({
> >        type: 'RECEIVE_PRODUCTS',
> >        payload: products
> >      });
> >    }
> >    function sellProduct(productId) {
> >      dispatch({
> >        type: 'SELL_PRODUCT',
> >        payload: { id: productId }
> >      });
> >    }
> >  
> >    return (
> >      <div>
> >        <h2>Inventory Manager</h2>
> >        <ul>
> >          {state.products.map(product => (
> >            <li key={product.id}>
> >              {product.name} ({product.quantity} in stock)
> >              <button disabled={product.quantity === 0} onClick={() => sellProduct(product.id)}>Sell</button>
> >            </li>
> >          ))}
> >        </ul>
> >        <button onClick={ () => receiveProducts([
> >          { id: 4, name: 'Product D', description: 'Description D', quantity: 2 },
> >          { id: 5, name: 'Product E', description: 'Description E', quantity: 7 }
> >        ]) }>Receive Products</button>
> >      </div>
> >    );
> >  }
> >  
> >  export default InventoryManager;
> > ```

- - -

## <a name="custom-hooks"></a>Custom Hooks 

Here are the steps to create a custom hook:
+ Identify the common logic that needs to be shared across multiple components.
+ Create a function that implements this logic and accepts any necessary parameters.
+ Return any values or state that need to be used by the component.

> Here's an example of a custom hook that fetches data from an API:
> > ```javascript
> >  import { useState, useEffect } from 'react';
> >  
> >  function useFetch(url) {
> >    const [data, setData] = useState(null);
> >    const [isLoading, setIsLoading] = useState(true);
> >    const [error, setError] = useState(null);
> >  
> >    useEffect(() => {
> >      async function fetchData() {
> >        try {
> >          const response = await fetch(url);
> >          const json = await response.json();
> >          setData(json);
> >          setIsLoading(false);
> >        } catch (error) {
> >          setError(error);
> >          setIsLoading(false);
> >        }
> >      }
> >  
> >      fetchData();
> >    }, [url]);
> >  
> >    return { data, isLoading, error };
> >  }
> > ```
> It returns an object with data, isLoading, and error properties that can be used by the component.

> To use this hook in a component, simply call it:
> > ```
> >  function MyComponent() {
> >    const { data, isLoading, error } = useFetch('https://api.example.com/data');
> >  
> >    if (isLoading) {
> >      return <div>Loading...</div>;
> >    }
> >  
> >    if (error) {
> >      return <div>Error: {error.message}</div>;
> >    }
> >  
> >    return (
> >      <div>
> >        {data.map((item) => (
> >          <div key={item.id}>{item.name}</div>
> >        ))}
> >      </div>
> >    );
> >  }
> > ```

As for best practices for creating custom hooks, here are a few tips:
+ Name your hook with the use prefix, as this is a convention in React that makes it clear that it is a hook.
+ Make sure your hook has a clear and specific purpose.
+ Keep your hook simple and focused on a single responsibility.
+ Document your hook with JSDoc comments to make it clear what it does and how to use it.
+ Test your hook thoroughly to ensure that it works as expected.
