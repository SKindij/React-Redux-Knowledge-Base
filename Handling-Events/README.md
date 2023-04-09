# Handling Events

&emsp;In React, you can handle user events using **event handlers** -- functions that are triggered when a user interacts with a component in some way, 
such as clicking a button or typing into an input field.

&emsp;To handle events in a component, you can define an event handler as a **method** on the component class. 
This method should be **bound** to the component's `this` context, so that it can access the component's `state` and `props`.\
&emsp;You can then pass this method as a **callback** to the appropriate **event attribute** of the element you want to handle the event for.

&emsp;Some common event handlers in React include:
+ `onClick`: _triggered when the user clicks an element;_
+ `onChange`: _riggered when the value of an input element changes;_
+ `onSubmit`: _riggered when a form is submitted;_
+ `onKeyDown`: _riggered when a key is pressed down while an element has focus;_

> _Here's an example of how to handle a button click event in a React component:_
> > ```javascript
> >  import React, { Component } from 'react';
> >  
> >  class MyButton extends Component {
> >    // method is bound to component's this context using an arrow function
> >    handleClick = () => {
> >      console.log('Button clicked!');
> >    }
> >    // method is passed as callback to onClick attribute
> >    render() {
> >      return (
> >        <button onClick={this.handleClick}>Click me!</button>
> >      );
> >    }
> >  }
> > ```




