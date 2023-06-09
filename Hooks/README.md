### <a name="introduction"></a>Introduction to React Hooks:
&emsp;They are functions that allow developers to use state and other React features in functional components. 
They were introduced in React 16.8 as a new way to write React components and manage state and lifecycle methods without using class components.

&emsp;📖 **The benefits of React Hooks include:**
+ Simplified code: 
  - Hooks allow developers to write more concise and readable code, reducing the amount of boilerplate 
and repetitive code needed to manage state and lifecycle methods.
+ Better code organization: 
  - Hooks enable developers to separate concerns and group related logic together into custom hooks, 
making it easier to reason about and maintain code.
+ Improved performance: 
  - Hooks can improve performance by reducing the amount of re-renders and optimizing the way state is managed.

<p align="center">
  <img src="https://github.com/SKindij/SKindij/blob/main/recources/react-hook-lifecycle.jpg" 
    title="react-hook-lifecycle" alt="react-hook-lifecycle" width="640" />  
</p>

_ _ _

## <a name="statehook"></a>📚 State Hook
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

> _Let's say we're building `repair center app` that services microcircuits and electric motors._\
> _Let's create `dashboard component` to track number of items that come in for diagnostics and repair, and whether the repairs are covered by warranty or not._
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
> >      setDiagnostics(diagnostics => diagnostics + 1);
> >    }
> >  
> >    function handleWarrantyRepairsIncrement() {
> >        if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >          setWarrantyRepairs(warrantyRepairs => warrantyRepairs + 1);
> >        }
> >    }
> >  
> >    function handleNonWarrantyRepairsIncrement() {
> >        if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >      setNonWarrantyRepairs(nonWarrantyRepairs => nonWarrantyRepairs + 1);
> >        }
> >    }
> >  
> >   function handleRejectedRepairsIncrement() {
> >       if (warrantyRepairs + nonWarrantyRepairs + rejectedRepairs < diagnostics) {
> >         setRejectedRepairs(rejectedRepairs => rejectedRepairs + 1);
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
> >        <p>Rejected requests: {rejectedRepairs}</p>
> >        <button onClick={handleRejectedRepairsIncrement}>Reject request</button>
> >      </div>
> >    );
> >  }
> > ```

Here are a few best practices for working with the useState hook:
* _Use a descriptive name for your state variable. This will make your code more readable and easier to understand._
* _Always use the setStateVariable function to update your state variable. Directly modifying the state variable could cause unexpected behavior in your component._
* _If your state variable is an object or an array, make sure to update it immutably. This means creating a new object or array with the updated value, rather than modifying the existing object or array._

- - -

## <a name="effecthook"></a>📚 Effect Hook allows you
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

> _Let's continue working on our application. One idea could be component that displays list of all technicians currently working at repair center, including their names, job titles, and contact information._
> > ```javascript
> >  import React, { useState, useEffect, useCallback } from 'react';
> >  import TechnicianFilter from './TechnicianFilter';
> >  
> >  function TechniciansList() {
> >    const [technicians, setTechnicians] = useState([]);
> >    const [filteredTechnicians, setFilteredTechnicians] = useState([]);
> >    // good practice to display loading state to provide feedback to user
> >    const [isLoading, setIsLoading] = useState(true);
> >    
> >    useEffect( () => {
> >      fetch('https://jsonplaceholder.typicode.com/users')
> >        .then( response => response.json() )
> >        .then( data => {
> >          setTechnicians(data);
> >          setIsLoading(false);
> >        } )
> >        .catch( error => {
> >          // good practice to handle errors when making API requests
> >          console.error('Error fetching user data:', error);
> >          setIsLoading(false);
> >        } );
> >    // [] means that effect should only run once, when component mounts  
> >    }, [] );
> >    
> >    // we define func 'handleFilterChange' using 'useCallback' hook
> >    // this func takes parameter, which represents search term entered by user
> >    const handleFilterChange = useCallback(searchTerm => {
> >     // if searchTerm is empty (after trimming whitespace), it means user cleared search field
> >      if (searchTerm.trim() === '') {
> >        // set original technicians array, displaying all technicians
> >        setFilteredTechnicians(technicians);
> >      } else {
> >        // 'filter' method is used to create new array (filtered) 
> >   	   // containing only technicians whose name matches search term
> >        const filtered = technicians.filter( technician =>
> >          technician.name.toLowerCase().includes(searchTerm.toLowerCase())
> >        );
> >        setFilteredTechnicians(filtered);
> >      }
> >    // ensure that func is memoized and only recreated if technicians array changes
> >    }, [technicians]);
> >    
> >   // In your current code, you don't have any cleanup needed for the effect.
> >   return (
> >     <div>
> >        <h2>Repair Center Technicians</h2>
> >        <TechnicianFilter technicians={technicians} onFilter={handleFilterChange} />  
> >        { isLoading ? (
> >            <p>Loading...</p>
> >          ) : (
> >            <table className="table table-striped">
> >              <thead>
> >                <tr>
> >                  <th>Name</th>
> >                  <th>Job Title</th>
> >                  <th>Email</th>
> >                  <th>Phone</th>
> >                </tr>
> >              </thead>
> >              <tbody>
> >                { filteredTechnicians.map( technician => (
> >                  <tr key={technician.id}>
> >                    <td>{technician.name}</td>
> >                    <td>{technician.company.bs}</td>
> >                    <td>{technician.email}</td>
> >                    <td>{technician.phone}</td>
> >                  </tr>
> >                ))}
> >              </tbody>
> >            </table>
> >          )
> >        }
> >      </div>
> >    );
> >  }
> >  
> >  export default TechniciansList;
> > ```

- - -

## <a name="usecontext"></a>📚 useContext Hook
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
This is useful in cases where multiple components need access to the same data or state, but they are not directly related in the component tree.

> _For example, in a large application, there may be multiple components that need access to the current user's authentication status or user preferences. Rather than passing this data down through each intermediate component, developers can use the useContext Hook to create a shared context object that can be accessed by any component in the tree.\
> &emsp; _You can include multiple arrays or any other data structures in a single `RepairServiceContext` if they are related to the overall state of your application. The RepairServiceContext can hold any data that you want to share and make accessible to other components._
> > ```javascript
> >  import React, { createContext, useContext } from 'react';
> >  // use 'createContext' func from React
> >    // argument is an initial context value
> >  const RepairServiceContext = createContext( {
> >    // both properties are initially set to empty arrays
> >    repairServices: [],
> >    accessoriesOnSale: [],
> >  } );
> >  // custom hook which uses useContext to access value provided by RepairServiceContext
> >  export const useRepairServiceContext = () => useContext( RepairServiceContext );
> >  // define component, which serves as provider for RepairServiceContext
> >  // it receives {children} which represents nested components that will consume context
> >  const RepairServiceContextProvider = ( { children } ) => {
> >    const repairServices = [
> >      { id: 1, type: 'Control unit repair', price: 100, available: true },
> >      { id: 2, type: 'Electric motor repair', price: 150, available: false },
> >      { id: 3, type: 'Garage gate repair', price: 200, available: true },
> >      { id: 4, type: 'Swing gate repair', price: 175, available: true },
> >      { id: 5, type: 'Roll-up gate repair', price: 125, available: false },
> >      { id: 6, type: 'Barrier repair', price: 75, available: true },
> >    ];
> >  
> >    const accessoriesOnSale = [
> >      { id: 101, type: 'radio receiver', price: 16, balanceInStock: 340, available: true },
> >      { id: 102, type: 'remote control', price: 6, balanceInStock: 980, available: true },
> >      { id: 103, type: 'photocells', price: 14, balanceInStock: 420, available: true },
> >      { id: 104, type: 'lamp', price: 10, balanceInStock: 430, available: true },
> >      { id: 105, type: 'antenna', price: 11, balanceInStock: 0, available: false },
> >      { id: 106, type: 'gear rack', price: 3, balanceInStock: 610, available: true },
> >    ];
> >    // wrap {children} inside .Provider component, passing value prop
> >    return (
> >      <RepairServiceContext.Provider value={ { repairServices, accessoriesOnSale } }>
> >        {children}
> >      </RepairServiceContext.Provider>
> >    );
> >  };
> >  
> >  export default RepairServiceContextProvider;
> > ```

> _Now, you can access both arrays in any component that consumes the `RepairServiceContext` by using the `useRepairServiceContext` custom hook:_
> > ```javascript
> >  import React from 'react';
> >  import { useRepairServiceContext } from './RepairServiceContext';
> >  
> >  const RepairServiceList = () => {
> >    const { repairServices, accessoriesOnSale } = useRepairServiceContext();
> >  
> >    return (
> >      <div className="container">
> >        <h2 className="mt-4 mb-3">Repair Services</h2>
> >        <ul className="list-group">
> >          {repairServices.map((repairService) => (
> >            <li className="list-group-item" key={repairService.id}>
> >              <span className="fw-bold">{repairService.type}</span>
> >              <span className="badge bg-primary ms-2">${repairService.price}</span>
> >            </li>
> >          ))}
> >        </ul>
> >  
> >        <h2 className="mt-4 mb-3">Accessories on Sale</h2>
> >        <ul className="list-group">
> >          {accessoriesOnSale.map((accessory) => (
> >            <li className="list-group-item" key={accessory.id}>
> >              <span className="fw-bold">{accessory.type}</span>
> >              <span className="badge bg-success ms-2">${accessory.price}</span>
> >            <span className="badge bg-info ms-2">In Stock: {accessory.balanceInStock}</span>
> >            </li>
> >          ))}
> >        </ul>
> >      </div>
> >    );
> >  };
> >  
> >  export default RepairServiceList;
> > ```

The useContext Hook is also commonly used in combination with the useReducer Hook, which allows for more complex state management and can further reduce the need for prop drilling.

- - -

## <a name="usereducer"></a>📚 useReducer Hook

&emsp;This Hook is a way to manage complex state in your application. It's similar to the useState Hook, but it provides a more powerful way to update and manage state in your application. 
The useReducer Hook takes two arguments: 
  * **reducer function**
    + it responsible for handling state changes in your application;
    + takes two arguments: the current state and an action object;
    + returns new state based on the current state and the action;
  * **initial state value**.

&emsp; It is often used when you have state that transitions through different possible values or when the next state depends on the previous state.

To create a component using the useReducer hook, you generally follow these steps:
1. **Import the necessary dependencies:**
```javascript
  import React, { useReducer } from 'react';
```
2. **Define your reducer function:**
    - it is responsible for updating state based on dispatched actions;
    - it takes current state and action as input and returns new state;
```javascript
  // reducer function follows specific pattern:
  const reducer = (state, action) => {
    switch (action.type) {
      case 'ACTION_TYPE_1':
        // update state based on action type 1
        return newState1;
      case 'ACTION_TYPE_2':
        // update state based on action type 2
        return newState2;
      // add more cases for different action types
      default:
        return state; // return current state if no action type matches
    }
  };
```
3. **Define the initial state:**
    - it represents initial value of your state;
    - it can be object, array, or any other type of data;
```javascript
  const initialState = {
    // define initial state properties
};

```
4. **Use the useReducer hook in your component:**
    - state: represents current state managed by reducer;
    - dispatch: function used to dispatch actions to update state;
```javascript
  const [state, dispatch] = useReducer(reducer, initialState);
```
5. **Dispatch actions to update the state:**
    - type: represents type of action to be performed;
    - payload: optional data associated with action;
```javascript
  // dispatching action triggers reducer function, which updates state based on action type
  dispatch({ type: 'ACTION_TYPE', payload: 'additionalData' });
```
6. **Use the state values in your component:**
> _You can access the state values returned by the reducer and use them in your component to render UI or perform any other logic._


&emsp;📖State Hook and useReducer Hook have some key differences in terms of usage and intended use cases:

<table>
  <thead>
    <tr>
      <th></th>
      <th>useState</th>
      <th>useReducer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Simplicity vs. Complexity</td>
      <td>simpler and more straightforward for managing local component state;<br>
        suitable for managing simple state values or independent state variables;</td>
      <td>powerful for managing complex state logic;<br>
        handle state transitions that depend on previous state, involve multiple properties, or require complex updates;</td>
    </tr>
    <tr>
      <td>API Differences</td>
      <td>returns: current state value and function to update that value;</td>
      <td>returns: current state value and dispatch function to trigger state updates through actions;</td>
    </tr>
    <tr>
      <td>Handling Updates</td>
      <td>primarily used to handle simple state updates where the new state value is directly set or computed based on the previous state;</td>
      <td>more flexible and allows to define reducer function that determines how state transitions from one value to another;</td>
    </tr>
    <tr>
      <td>State Shape</td>
      <td>state is typically a single value, such as a boolean, number, string, or object;</td>
      <td>more complex state structures, as objects, arrays, or any other data structure that suits your needs;</td>
    </tr>
    <tr>
      <td>Use Cases</td>
      <td>suitable for managing independent state variables, such as toggles, form inputs, or any simple state that doesn't require complex transitions;</td>
      <td>manage state with complex transitions, state dependencies, or when state logic becomes too cumbersome with useState alone;<br>
        It is commonly used for state management patterns like Flux or Redux.</td>     
    </tr>
    <tr>
      <td>Predictability and Testing</td>
      <td>more implicit, especially if there are multiple state variables, which may make it slightly harder to track state changes during testing;</td>
      <td>state transitions are explicit and predictable because they are determined by reducer function.<br>
        This can make testing and debugging easier.</td>  
    </tr>
  </tbody>
</table>

> _Let's create component 'RepairOrderForm' that allows users to submit repair orders for devices._
> > ```javascript
> >  import React, { useReducer } from 'react';
> >  
> >  const initialState = {
> >    customerName: '',
> >    deviceName: '',
> >    issue: '',
> >    isSubmitted: false,
> >  };
> >  
> >  function reducer(state, action) {
> >    switch (action.type) {
> >      case 'UPDATE_CUSTOMER_NAME':
> >        return { ...state, customerName: action.payload };
> >      case 'UPDATE_DEVICE_NAME':
> >        return { ...state, deviceName: action.payload };
> >      case 'UPDATE_ISSUE':
> >        return { ...state, issue: action.payload };
> >      case 'SUBMIT_FORM':
> >        return { ...state, isSubmitted: true };
> >      case 'RESET_FORM':
> >        return initialState;
> >      default:
> >        return state;
> >    }
> >  }
> >  
> >  function RepairOrderForm() {
> >    const [state, dispatch] = useReducer(reducer, initialState);
> >  
> >    const handleSubmit = (e) => {
> >      e.preventDefault();
> >      dispatch({ type: 'SUBMIT_FORM' });
> >      // send form data to server or perform other actions
> >      // you can access form data using `state.customerName`, `state.deviceName`, and `state.issue`
> >    };
> >  
> >    const handleReset = () => {
> >      dispatch({ type: 'RESET_FORM' });
> >    };
> >  
> >    return (
> >      <div className="container">
> >        <h2 className="mt-4 mb-3">Submit Repair Order</h2>
> >        {state.isSubmitted ? (
> >          <div className="alert alert-success" role="alert">
> >            Repair order submitted successfully!
> >            <button className="btn btn-primary mt-3" onClick={handleReset}>
> >              Submit Another Order
> >            </button>
> >          </div>
> >      ) : (
> >        <form onSubmit={handleSubmit}>
> >          <div className="mb-3">
> >            <label htmlFor="customerName" className="form-label">Customer Name</label>
> >            <input type="text" className="form-control" id="customerName"
> >              value={state.customerName}
> >              onChange={(e) => dispatch({
> >                  type: 'UPDATE_CUSTOMER_NAME',
> >                  payload: e.target.value,
> >                })
> >              }
> >            required />
> >          </div>
> >          <div className="mb-3">
> >            <label htmlFor="deviceName" className="form-label">Device Name</label>
> >              <input type="text" className="form-control" id="deviceName"
> >                value={state.deviceName}
> >                onChange={(e) => dispatch({
> >                    type: 'UPDATE_DEVICE_NAME',
> >                    payload: e.target.value,
> >                  })
> >                }
> >            required />
> >          </div>
> >          <div className="mb-3">
> >              <label htmlFor="issue" className="form-label">Issue</label>
> >              <textarea className="form-control"mid="issue"
> >                value={state.issue}
> >                onChange={(e) =>
> >                  dispatch({ type: 'UPDATE_ISSUE', payload: e.target.value })
> >                }
> >              required></textarea>
> >          </div>
> >          <button type="submit" className="btn btn-primary me-3">Submit</button>
> >          <button type="button" className="btn btn-secondary" onClick={handleReset}>Reset</button>
> >        </form>
> >      )}
> >    </div>
> >    );
> >  }
> >
> >export default RepairOrderForm;
> > ```

- - -

## <a name="additional"></a>📚 Additional Hooks 

### 📖 useCallback
&emsp;It is used to memoize a function so that it is not recreated on each render unless its dependencies change. It's particularly useful when passing callbacks to child components that rely on reference equality to prevent unnecessary re-renders.
> ```javascript
>   const memoizedCallback = useCallback(callback, dependencies);
> ```
> > * first argument, callback, is the function that you want to memoize.
> > * second argument, dependencies, is an array of values that the memoized callback depends on. 
> >   + if any of these values change, the callback will be recreated; otherwise, the memoized version will be returned;
> >   + tt's important to include all dependencies that are used within the callback to ensure the correct behavior;

_The memoized callback can be passed down as prop to child components, ensuring that child components only re-render when necessary._

> _Render input field for searching technicians and list of technicians based on current search term._
> > ```javascript
> >  import React, { useState, useCallback } from 'react';
> >  
> >  // component receives array of technicians as prop and callback onFilter to handle filtering logic
> >  const TechnicianFilter = ( { technicians, onFilter } ) => {
> >    const [searchTerm, setSearchTerm] = useState('');
> >    // This func is memoized to prevent unnecessary re-rendering when onFilter func dependency changes. 
> >    // It updates searchTerm state and calls onFilter callback func with updated search term.
> >    const handleSearchChange = useCallback(
> >      (event) => {
> >        setSearchTerm(event.target.value);
> >        onFilter(event.target.value);
> >      }, [onFilter] );
> >  
> >    return (
> >      <div>
> >        <h2>Technician Filter</h2>
> >        <input type="text" placeholder="Search technicians..."
> >          value={searchTerm}
> >          onChange={handleSearchChange}
> >        />
> >      </div>
> >    );
> >  };
> >  
> >  export default TechnicianFilter;
> > ```

### 📖 useMemo
&emsp;It is used to memoize the result of a function call, similar to useCallback, but for values instead of functions. 
It allows you to optimize expensive calculations or complex operations within your components. 
> ```javascript
>   const memoizedValue = useMemo(() => calculateValue(a, b), dependencies);
> ```
> > * first argument is a function that returns the value you want to memoize.
> > * second argument, dependencies, is an array of values that the memoized value depends on. 
> >   + if any of these values change, memoized value will be recalculated; otherwise, memoized version will be returned;
> >   + it's crucial to include all dependencies that are used within the function to ensure the correct behavior.

_The memoized value can be used within your component, avoiding unnecessary recalculation if the dependencies haven't changed._




### 📖 useRef
&emsp;This hook is used to create a mutable reference that persists across component renders. 
It provides a way to access and modify DOM elements or values that persist outside of the normal component lifecycle.
> ```javascript
>   const refContainer = useRef(initialValue);
> ```
> > * initialValue will be the initial value of the reference;
> > * refContainer is object with .current property that holds current value of reference;
> > * unlike useState, updating refContainer.current value does not cause re-render of component;
> > * you can access current value using refContainer.current;

_useRef is commonly used to reference DOM elements, store mutable values, or preserve values between renders without triggering a re-render._

&emsp; Here are a few common use cases for useRef:
1. **Referencing DOM elements:**
    - _You can use useRef to get reference to DOM element and interact with it imperatively._
    - _For example, you can focus an input field or scroll to a specific element._
    - ```javascript
        import React, { useRef, useEffect } from 'react';

        function MyComponent() {
          const inputRef = useRef(null);
            useEffect(() => {
              inputRef.current.focus();
            }, []);
          return <input ref={inputRef} />;
        }
      ```
2. **Storing previous values:**
    - _You can use useRef to store previous values of props or state, and compare them during subsequent renders._
    - ```javascript
        import React, { useRef, useEffect } from 'react';

        function MyComponent({ value }) {
          const prevValueRef = useRef();
            useEffect(() => {
              if (prevValueRef.current !== value) {
                // value changed, do something
              }
              prevValueRef.current = value;
            }, [value]);
                  return <div>{value}</div>;
        }
      ```
3. **Storing mutable values:**
    - useRef allows you to store values that persist across renders;
    - similar to instance variables in class components;
    - ```javascript
        import React, { useRef, useEffect } from 'react';

        function MyComponent() {
          const counterRef = useRef(0);
            useEffect(() => {
              counterRef.current += 1;
              console.log(`Counter: ${counterRef.current}`);
            });
          return <div>Counter: {counterRef.current}</div>;
        }
      ```



- - -

## <a name="customhooks"></a>📚 Custom Hooks 

Here are the steps to create a custom hook:
+ Identify the common logic that needs to be shared across multiple components.
+ Create function that implements this logic and accepts any necessary parameters.
+ Return any values or state that need to be used by the component.

> 
> > ```javascript
> >  
> > ```
> 





> 
> > ```
> >  
> > ```




As for best practices for creating custom hooks, here are a few tips:
+ Name your hook with `use` prefix, as this is convention in React that makes it clear that it is hook.
+ Make sure your hook has a clear and specific purpose.
+ Keep your hook simple and focused on a single responsibility.
+ Document your hook with JSDoc comments to make it clear what it does and how to use it.
+ Test your hook thoroughly to ensure that it works as expected.
