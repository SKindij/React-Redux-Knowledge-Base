# REDUX
> _React-Redux is a popular library for managing the state of a React application._\
> _It's often used in conjunction with React to simplify state management, especially for large and complex applications._

### Here's an overview of React-Redux concepts and how they work:

#### Store

The store is the central data repository for your application's state. It holds the entire state tree of your application. In Redux, you create a store using the createStore function.

```javascript


```


#### Actions

Actions are plain JavaScript objects that describe changes to the state. They must have a type property to specify the type of action being performed. Additional data can be included as well.

```javascript


```


#### Reducers

Reducers are functions that specify how the state changes in response to actions. They take the current state and an action as arguments and return the new state.

```javascript


```


#### Provider

To make the Redux store accessible to your React components, you wrap your app with the Provider component provided by React-Redux.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

#### Connect

To connect your React components to the Redux store, you use the connect function provided by React-Redux. This function allows components to access state and dispatch actions.

```javascript


```


#### Usage in Components

You can now use the connected component in your application, and it will have access to the Redux state and actions.


```javascript


```




- - -

### Redux Toolkit - opinionated, batteries-included toolset for efficient development

[Redux Toolkit](https://redux-toolkit.js.org/introduction/getting-started#whats-included) includes these APIs:
* ``configureStore()``
  + _wraps createStore to provide simplified configuration options and good defaults_
  + _it can automatically combine your slice reducers, adds whatever Redux middleware you supply_
* ``createReducer()``
  + _lets you supply a lookup table of action types to case reducer functions, rather than writing switch statements_
  + _it automatically uses the immer library to let you write simpler immutable updates with normal mutative code_
* ``createAction()``
  + _generates an action creator function for the given action type string_
* ``createSlice()``
  + _automatically generates a slice reducer with corresponding action creators and action types_
* ``createAsyncThunk``
  + _accepts an action type string and a function that returns a promise, and generates a thunk_
* ``createEntityAdapter``
  + _generates a set of reusable reducers and selectors to manage normalized data in the store_
* ``createSelector``
  + _utility from the Reselect library, re-exported for ease of use_

- - -




