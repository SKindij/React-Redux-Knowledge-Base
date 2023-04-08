## In React a component goes through various phases during its lifecycle.

* **Mounting Phase**
  1. constructor():
    - is called when a component is first initialized;
    - is used to set up the initial state and to bind event handlers;
  2. render():
    - is responsible for returning the JSX to be rendered on the screen;
  3. componentDidMount():
    - is called after the component has been rendered on the screen;
    - is commonly used for initializing data that requires DOM node to be present, such as making an API request;
* **Updating Phase**
  1. shouldComponentUpdate():
    - is called before the component is re-rendered;
    - can be used to optimize performance by determining whether or not a re-render is necessary;
  2. render():
    - is responsible for returning the updated JSX to be rendered on the screen;
  3. componentDidUpdate():
    - is called after the component has been updated;
    - is commonly used for performing side-effects, such as updating the DOM or making an API request;
* **Unmounting Phase**
  1. componentWillUnmount():
    - is called just before the component is removed from the screen;
    - is commonly used for cleaning up resources, such as removing event listeners or cancelling pending API requests.




