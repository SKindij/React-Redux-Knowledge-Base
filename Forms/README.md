# Forms in React

&emsp;Here are some important things to know:
* In React, there are two types of form components: 
  + **controlled** - are those that are fully controlled by React, meaning that React manages the state of the form input elements; 
  + **uncontrolled**, on the other hand, - are managed by the browser and React only reads their values when needed.
* When form is submitted, use `onSubmit` event handler to capture form data and perform any necessary actions; 
  + to prevent the default behavior of the form (i.e., page reload), you'll need to call the `event.preventDefault()` method.

> _Here's example of handling form submission without using the useState hook_
```javascript
import React from 'react';

class MyForm extends React.Component {
  constructor(props) {
    super(props);
    // we initialize component's state with empty values
    this.state = {
      name: '',
      age: '',
      email: '',
      errorMessage: '',
    };
  }
  // function is called when the user submits the form
  handleSubmit = (event) => {
    event.preventDefault();
    const { name, age, email } = this.state;
    // checking that all fields are filled in
    if (!name || !age || !email) {
      this.setState({
        errorMessage: 'Please fill in all fields',
      });
      return;
    }
    // checking that age field is a number
    if (isNaN(age)) {
      this.setState({
        errorMessage: 'Age must be a number',
      });
      return;
    }
    // Submit the form data to the server or update the app state here
    console.log('Form data:', this.state);
  };
  // function updates corresponding state variable with new value
  handleInputChange = (event) => {
    const { name, value } = event.target;
    this.setState({
      [name]: value,
      errorMessage: '',
    });
  };

  render() {
    const { name, age, email, errorMessage } = this.state;
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" name="name" value={name} onChange={this.handleInputChange} />
        </label>
        <label>
          Age:
          <input type="number" name="age" value={age} onChange={this.handleInputChange} />
        </label>
        <label>
          Email:
          <input type="email" name="email" value={email} onChange={this.handleInputChange} />
        </label>
        {errorMessage && <p>{errorMessage}</p>}
        <button type="submit">Submit</button>
      </form>
    );
  }
}

```
> _If the input data is valid, the function submits the form data to the server or updates the app state as needed._




