# REDUX
> _React-Redux is a popular library for managing the state of a React application._\
> _It's often used in conjunction with React to simplify state management, especially for large and complex applications._

Redux is a predictable state container for JavaScript applications. It helps manage the state of your application in a predictable way by maintaining a single global store and dispatching actions to modify that store. This is particularly useful for managing application-wide data and ensuring that changes to the state are controlled and predictable.

First, you need to set up Redux in your React application.
```bash
  npm install redux react-redux
```

### Here's an overview of React-Redux concepts and how they work:
> I'd be happy to explain the theory of using Redux with code examples in the context of a relationship between a manufacturer (supplier of spare parts) and a service center (recipient of these spare parts). In this scenario, we'll create a simple Redux application to manage the spare parts inventory and requests from the service center.

#### Store

The store is the central data repository for your application's state. It holds the entire state tree of your application. In Redux, you create a store using the createStore function.

```javascript


```


#### Actions

Actions are plain JavaScript objects that describe changes to the state. They must have a type property to specify the type of action being performed. Additional data can be included as well.

Actions represent events or user interactions that trigger changes to the state. In our case, actions might include requesting spare parts or receiving them.

```javascript
// actions.js
export const REQUEST_SPARE_PART = 'REQUEST_SPARE_PART';
export const RECEIVE_SPARE_PART = 'RECEIVE_SPARE_PART';

export const requestSparePart = (partName, quantity) => ({
  type: REQUEST_SPARE_PART,
  partName,
  quantity,
});

export const receiveSparePart = (partName, quantity) => ({
  type: RECEIVE_SPARE_PART,
  partName,
  quantity,
});
```


#### Reducers

Reducers are functions that specify how the state changes in response to actions. They take the current state and an action as arguments and return the new state.

You'll have separate reducers for different parts of your state. In this case, we'll have one for the manufacturer and one for the service center.

```javascript
// manufacturerReducer.js
import { REQUEST_SPARE_PART } from './actions';

const initialState = {
  sparePartsRequests: [],
};

const manufacturerReducer = (state = initialState, action) => {
  switch (action.type) {
    case REQUEST_SPARE_PART:
      return {
        ...state,
        sparePartsRequests: [
          ...state.sparePartsRequests,
          {
            partName: action.partName,
            quantity: action.quantity,
          },
        ],
      };
    default:
      return state;
  }
};

export default manufacturerReducer;
```

```javascript
// serviceCenterReducer.js
import { RECEIVE_SPARE_PART } from './actions';

const initialState = {
  sparePartsInventory: [],
};

const serviceCenterReducer = (state = initialState, action) => {
  switch (action.type) {
    case RECEIVE_SPARE_PART:
      return {
        ...state,
        sparePartsInventory: [
          ...state.sparePartsInventory,
          {
            partName: action.partName,
            quantity: action.quantity,
          },
        ],
      };
    default:
      return state;
  }
};

export default serviceCenterReducer;
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




