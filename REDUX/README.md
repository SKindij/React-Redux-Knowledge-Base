# REDUX











## Redux Toolkit - opinionated, batteries-included toolset for efficient development

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






