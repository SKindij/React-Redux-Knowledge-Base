# Forms in React

&emsp;Here are some important things to know:
* In React, there are two types of form components: 
  + **controlled** - are those that are fully controlled by React, meaning that React manages the state of the form input elements; 
  + **uncontrolled**, on the other hand, - are managed by the browser and React only reads their values when needed.
* When form is submitted, use `onSubmit` event handler to capture form data and perform any necessary actions; 
  + to prevent the default behavior of the form (i.e., page reload), you'll need to call the `event.preventDefault()` method.





