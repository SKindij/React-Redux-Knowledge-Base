## In React a component goes through various phases during its lifecycle.

1. **Mounting Phase**
    * `constructor()`:
        - is called when a component is first initialized;
        - is used to set up the initial state and to bind event handlers;
    * `render()`:
        - is responsible for returning the JSX to be rendered on the screen;
    * `componentDidMount()`:
        - is called after the component has been rendered on the screen;
        - is commonly used for initializing data that requires DOM node to be present, such as making an API request;
2. **Updating Phase**
    * `shouldComponentUpdate()`:
        - is called before the component is re-rendered;
        - can be used to optimize performance by determining whether or not a re-render is necessary;
    * `render()`:
        - is responsible for returning the updated JSX to be rendered on the screen;
    * `componentDidUpdate()`:
        - is called after the component has been updated;
        - is commonly used for performing side-effects, such as updating the DOM or making an API request;
3. **Unmounting Phase**
    * `componentWillUnmount()`:
        - is called just before the component is removed from the screen;
        - is commonly used for cleaning up resources, such as removing event listeners or cancelling pending API requests.

<p align="center">
  <img src="https://github.com/SKindij/SKindij/blob/main/recources/react-lifecycle-methods.jpg" 
    title="react-lifecycle-method" alt="react-lifecycle-method" width="640" height="270"/>  
</p> 

_ _ _

#### An example of using these methods to fetch data from an external API and update the component's state with that data.

> Let's assume that we have a WorkerComponent that displays the number of hours worked by a factory worker:

```javascript
import React, { Component } from 'react';

class WorkerComponent extends Component {
  constructor(props) {
    super(props);

    this.state = {
      hoursWorked: null,
      error: null,
    };
  }

  // to encapsulate the logic for fetching worker hours
  fetchWorkerHours() {
    fetch('https://example.com/api/worker-hours')
      .then((response) => {
        if (!response.ok) { throw new Error('Failed to fetch worker hours'); }
        return response.json();
      })
      .then((data) => {
          this.setState({
            hoursWorked: data.hours,
          });
      })
      .catch((error) => {
        this.setState({ error: error.message });
      });
  }
  // worker hours are fetched when the component is mounted
  componentDidMount() {
    this.fetchWorkerHours();
  }
  // to prevent unnecessary re-renders when the hoursWorked state hasn't changed
  shouldComponentUpdate(nextProps, nextState) {
    if (nextState.hoursWorked === this.state.hoursWorked) {
      return false; // Prevent unnecessary re-render
    }
    return true;
  }
  // method is called after the component is updated
  componentDidUpdate(prevProps, prevState) {
    if (prevState.hoursWorked !== this.state.hoursWorked) {
      console.log(`Worker hours updated from ${prevState.hoursWorked} to ${this.state.hoursWorked}`);
    }
  }

  render() {
    const { hoursWorked, error } = this.state;

    if (error) { return <div>Error: {error}</div>; }
    if (hoursWorked === null) { return <div>Loading...</div>; }

    return (
      <div>
        Hours worked: {hoursWorked}
      </div>
    );
  }
}

export default WorkerComponent;
```






