# Props and State

&emsp; Props (short for properties) are a way to pass data from a parent component to a child component.
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








