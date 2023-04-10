## Introduction to React Hooks

### Understanding what React Hooks are and their benefits:
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

## State Hook
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









