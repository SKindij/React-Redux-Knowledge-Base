# Handling Events

&emsp;In React, you can handle user events using **event handlers** -- functions that are triggered when a user interacts with a component in some way, 
such as clicking a button or typing into an input field.

&emsp;To handle events in a component, you can define an event handler as a **method** on the component class. 
This method should be **bound** to the component's `this` context, so that it can access the component's `state` and `props`.\
&emsp;You can then pass this method as a **callback** to the appropriate **event attribute** of the element you want to handle the event for.

&emsp;Some common event handlers in React include:
+ `onClick`: _triggered when the user clicks an element;_
+ `onChange`: _triggered when the value of an input element changes;_
+ `onSubmit`: _triggered when a form is submitted;_
+ `onKeyDown`: _triggered when a key is pressed down while an element has focus;_

> _Example of how to handle a button click event in a React component:_
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

> _Example of action when user changes value of the inputs and ubmits form
> > ```javascript
> >  import React, { Component } from 'react';
> >  
> >  class MyForm extends Component {
> >    state = {
> >      firstName: '',
> >      lastName: ''
> >    }
> >    // method that logs submitted values to console
> >    handleSubmit = event => {
> >      event.preventDefault();
> >      console.log(`Submitted: ${this.state.firstName} ${this.state.lastName}`);
> >    }
> >    // methods that updates state whenever input value changes
> >    handleFirstNameChange = event => {
> >      this.setState({ firstName: event.target.value });
> >    } 
> >    handleLastNameChange = event => {
> >      this.setState({ lastName: event.target.value });
> >    }
> >    // we define a form that has two input fields for the user
> >    render() {
> >      return (
> >        <form onSubmit={this.handleSubmit}>
> >          <label>
> >            First Name:
> >            <input type="text" value={this.state.firstName} onChange={this.handleFirstNameChange} />
> >          </label>
> >          <label>
> >            Last Name:
> >            <input type="text" value={this.state.lastName} onChange={this.handleLastNameChange} />
> >          </label>
> >          <button type="submit">Submit</button>
> >        </form>
> >      );
> >    }
> >  }
> > ```

> _Example of trigger an action when user presses key while input has focus_
> > ```javascript
> >  import React, { Component } from 'react';
> >  
> >  class MyInput extends Component {
> >    state = {
> >      value: ''
> >    }
> >    // method receives event object as argument, which contains info about key code
> >    handleKeyDown = event => {
> >      console.log(`Pressed key with code: ${event.keyCode}`);
> >    }
> >  
> >    handleChange = event => {
> >      this.setState({ value: event.target.value });
> >    }
> >    // you can use this information to implement custom behavior based on specific key that was pressed
> >    render() {
> >      return (
> >        <input type="text" value={this.state.value} onChange={this.handleChange} onKeyDown={this.handleKeyDown} />
> >      );
> >    }
> >  }
> > ```



