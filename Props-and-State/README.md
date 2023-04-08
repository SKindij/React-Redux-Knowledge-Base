# Props and State

### ``Props`` (_short for properties_) are a way to pass data from a parent component to a child component.
* props are read-only: 
  + once you pass props from a parent component to a child component, the child component cannot modify those props;
  + if you need to change the value of a prop, you should do it in the parent component;
* props can be any type of data: 
  + strings, numbers, booleans, arrays, objects, or even functions;
* props can have default values: 
  + you can specify default values for props in the child component in case they are not passed down from the parent component;
* props can be validated: 
  + you can also validate the props that are passed down to a child component;
  + this helps ensure that the correct data types are being passed down from the parent component.

> _Child component with default props and prop type validation:_
> > ```javascript
> >  import React from 'react';
> >  import PropTypes from 'prop-types';
> >  
> >  function ChildComponent(props) {
> >    return (
> >      <div>
> >        <p>TM: {props.carMake}</p>
> >        <p>Model: {props.carModel}</p>
> >        <p>Year: {props.carYear}</p>
> >      </div>
> >    );
> >  }
> >  ChildComponent.defaultProps = {
> >    carModel: 'Mondeo'
> >  };
> >  ChildComponent.propTypes = {
> >    carMake: PropTypes.string.isRequired,
> >    carModel: PropTypes.string.isRequired,
> >    carYear: PropTypes.number
> >  };
> >  
> >  export default ChildComponent;
> > ```

> _Parent component:_
> > ```javascript
> >  import React from 'react';
> >  import ChildComponent from './ChildComponent';
> >  
> >  function ParentComponent() {
> >    const carMake = 'Ford';
> >    const carYear = 2011;
> >    return (
> >      <div>
> >        <ChildComponent carMake={carMake} carYear={carYear} />
> >      </div>
> >    );
> >  }
> >  
> >  export default ParentComponent;
> > ```

### ``State`` is an internal data store of a component.

&emsp; It's used to manage data that can change over time, and is typically used for things like user input, component interactions, or network responses.

&emsp; A component's state is private and can only be accessed and modified within the component itself. When state changes, React automatically re-renders the component and its children to reflect the new state.

> _Here's an example of managing state within a component:_
> > ```javascript
> >  import React, { Component } from 'react';
> >  
> >  class CarProduction extends Component {
> >    constructor(props) {
> >      super(props);
> >      // initializing mondeoCount state in constructor method
> >      this.state = {
> >        mondeoCount: 0
> >      };  
> >      this.handleIncrement = this.handleIncrement.bind(this);
> >      this.handleReset = this.handleReset.bind(this);
> >    }
> >    // defining event handler methods that update state using this.setState
> >    handleIncrement() {
> >      this.setState({ mondeoCount: this.state.mondeoCount + 1 });
> >    }
> >    handleReset() {
> >      this.setState({ mondeoCount: 0 });
> >    }
> >    // we're accessing mondeoCount using this.state.mondeoCount and binding event handlers to appropriate buttons
> >    render() {
> >      return (
> >        <div>
> >          <p>Mondeo cars produced this week: {this.state.mondeoCount}</p>
> >          <button onClick={this.handleIncrement}>Increment</button>
> >          <button onClick={this.handleReset}>Reset</button>
> >        </div>
> >      );
> >    }
> >  }
> >  
> >  export default CarProduction;
> > ```
> > > &emsp;_In the CarProduction class component, ``this.handleIncrement`` and ``this.handleReset`` are event handler methods that are called when the "Increment" and "Reset" buttons are clicked._\
> > > &emsp;_In JavaScript, the value of `this` is determined by how a function is called. When an event handler is triggered by an event like a `button click`, the value of `this` can be different than what we expect._\
> > > &emsp;_To ensure that `this` refers to the component instance within these event handlers, we need to `bind` them to the component instance using the bind method. This creates a new `function` with a fixed `this value` that can be called later._




