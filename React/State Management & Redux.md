# State Management
## Why
As applications grow overtime, data often needs to be shared between components that aren't directly related in the component tree.
Without a dedicated state management solution, developers face 2 major problems:
- **Prop drilling:** Sometimes components are coupled together so they share the same state. The naive method is to pass state as `prop` to child component, but passing to deeply nested components can be hard to maintain and cause redundancy.
- **Inconsistent state:** Multiple components have their own copies of the same data. It is hard to keep them all synchronized. If one of them update the data, this can lead to conflicting UI bugs.
State management libraries like Redux, Zustand, or MobX solve these issues by creating a centralized **store** for the application's shared state. Any component that needs data can subscribe to the store, and any component can dispatch actions to update it.
**=> Single source of truth.**

# Redux
Is a state management library for React. By using Redux, we are enforcing the **uni-directional data flow**, which makes state changes predictable and easier to debug.
The flow can be visualized as: 
**UI Event ➡️ Dispatch Action ➡️ Reducer Updates State ➡️ UI Re-renders**.
## Shopping cart example

Here's a complete example of a shopping cart application using React and Redux with multiple reducers:

**Reducers** are usually in a separate file
```jsx
import React from 'react';
import { createStore, combineReducers } from 'redux';
import { Provider, useSelector, useDispatch } from 'react-redux';

// --- Cart Reducer ---
const cartInitialState = {
  items: [],
};

const cartReducer = (state = cartInitialState, action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        ...state,
        items: [...state.items, action.payload],
      };
    case 'REMOVE_ITEM':
      return {
        ...state,
        items: state.items.filter((item) => item.id !== action.payload),
      };
    default:
      return state;
  }
};

// --- User Reducer ---
const userInitialState = {
  loggedIn: false,
  userInfo: null,
};

const userReducer = (state = userInitialState, action) => {
  switch (action.type) {
    case 'LOGIN':
      return {
        ...state,
        loggedIn: true,
        userInfo: action.payload,
      };
    case 'LOGOUT':
      return {
        ...state,
        loggedIn: false,
        userInfo: null,
      };
    default:
      return state;
  }
};

// --- Root Reducer ---
const rootReducer = combineReducers({
  cart: cartReducer,
  user: userReducer,
});
```

**Consumer** and **dispatch actions**
```jsx
// --- Create Store ---
const store = createStore(rootReducer);

// --- React Components ---
function Cart() {
  const cartItems = useSelector((state) => state.cart.items);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Shopping Cart</h2>
      {cartItems.map((item) => (
        <div key={item.id}>
          <h3>{item.name}</h3>
          <button onClick={() => dispatch({ type: 'REMOVE_ITEM', payload: item.id })}>
            Remove
          </button>
        </div>
      ))}
    </div>
  );
}

function UserInfo() {
  const user = useSelector((state) => state.user.userInfo);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>User Information</h2>
      {user ? (
        <div>
          <p>Welcome, {user.name}!</p>
          <button onClick={() => dispatch({ type: 'LOGOUT' })}>Logout</button>
        </div>
      ) : (
        <button onClick={() => dispatch({ type: 'LOGIN', payload: { name: 'Guest' } })}>
          Login as Guest
        </button>
      )}
    </div>
  );
}

function App() {
  return (
    <Provider store={store}>
      <div>
        <h1>Shopping App</h1>
        <Cart />
        <UserInfo />
      </div>
    </Provider>
  );
}

export default App;
```

**Explanation:**

1. **Multiple Reducers:**
   - `cartReducer` manages the shopping cart items
   - `userReducer` manages user authentication
   - Both are combined into a single store using `combineReducers`

2. **Actions:**
   - `ADD_ITEM`, `REMOVE_ITEM` for cart management
   - `LOGIN`, `LOGOUT` for user authentication

3. **Components:**
   - `Cart` component displays items and allows removal
   - `UserInfo` component handles login/logout
   - Both components access and update the store using `useSelector` and `useDispatch`

4. **Provider:**
   - The `Provider` component makes the Redux store available to all components

## **Reducer Slice**
A **reducer slice** is a collection of the Redux reducer logic and actions for a single feature of your application, typically defined together in a single file.

Benefits of using Reducer slice:
- **Less boiler plate code**
- **Simpler Immutable Logic:** It uses a library called **Immer** internally. This lets you write code that _looks_ like you are mutating the state directly.