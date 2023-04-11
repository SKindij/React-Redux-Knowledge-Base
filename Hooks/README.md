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
&emsp; It allows you to add state to a functional component. It enables you to manage and update the state of your component without having to write a class.

> _Let's say we're building a dashboard for a repair center that services microcircuits and electric motors. We want to track the number of items that come in for diagnostics and repair, and whether the repairs are covered by warranty or not._
> > ```javascript
> >  import React, { useState } from 'react';
> >  
> >  function RepairDashboard() {
> >    const [diagnostics, setDiagnostics] = useState(0);
> >    const [warrantyRepairs, setWarrantyRepairs] = useState(0);
> >    const [nonWarrantyRepairs, setNonWarrantyRepairs] = useState(0);
> >  
> >    function handleDiagnosticsIncrement() {
> >      setDiagnostics(diagnostics + 1);
> >    }
> >  
> >    function handleWarrantyRepairsIncrement() {
> >      setWarrantyRepairs(warrantyRepairs + 1);
> >    }
> >  
> >    function handleNonWarrantyRepairsIncrement() {
> >      setNonWarrantyRepairs(nonWarrantyRepairs + 1);
> >    }
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
> >      </div>
> >    );
> >  }
> > ```

## <a name="effect-hook"></a>Effect Hook allows you
+ to handle side effects - any actions that your component performs outside of its scope, such as fetching data, updating the document title and DOM, subscribing to events, or setting a timer;
+ to run code after every render, and specify which state variables or props it should depend on. This ensures that the effect is only re-run when its dependencies have changed, and avoids unnecessary computations.

&emsp; The Effect Hook in React can be used to replace the functionality of componentDidMount, componentDidUpdate, and componentWillUnmount lifecycle methods.

> Here's the basic syntax for using the `useEffect` hook:
```javascript
import React, { useEffect } from 'react';

function MyComponent() {
  // hook takes two arguments:
  useEffect( () => { // arg1 - function containing side effect code    
       // this code will run after component has rendered

     // Cleanup function (optional)
     return () => {
        // Cleanup code here
        // This code will run when the component unmounts or when the effect dependencies change
      };
  }, [] ); // arg2 - array of dependencies that effect depends on
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
> >    useEffect(() => {
> >      fetch('https://jsonplaceholder.typicode.com/users')
> >        .then(response => response.json())
> >        .then(data => setUsers(data));
> >    }, []);
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




### <a name="use-context"></a>useContext Hook



### <a name="use-reducer"></a>useReducer Hook
