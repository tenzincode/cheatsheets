# React

## Functional Component with State

Functional components and hooks for managing state:

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

## Controlled Form Component

A controlled component where form input values are managed via state:

```jsx
import React, { useState } from 'react';

function Form() {
  const [name, setName] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
      />
      <button type="submit">Submit</button>
    </form>
  );
}

export default Form;
```

## List Rendering with `map`

Rendering a list of items using the `map` function:

```jsx
import React from 'react';

function ItemList({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

export default ItemList;
```

## Conditional Rendering

Rendering content based on a condition:

```jsx
import React from 'react';

function UserGreeting({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <h1>Welcome Back!</h1> : <h1>Please Sign In</h1>}
    </div>
  );
}

export default UserGreeting;
```

## `useEffect` for Side Effects

Using `useEffect` hook for handling side effects like fetching data:

```jsx
import React, { useEffect, useState } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);

  return (
    <div>
      {data ? <p>{data}</p> : <p>Loading...</p>}
    </div>
  );
}

export default DataFetcher;
```

## `useContext` for Context API

`useContext` hook to consume a context value without needing to pass props manually through components:

```jsx
import React, { createContext, useContext } from 'react';

// Create a Context
const ThemeContext = createContext('light');

function ThemedButton() {
  const theme = useContext(ThemeContext);  // Consuming the context value

  return (
    <button style={{ backgroundColor: theme === 'dark' ? '#333' : '#ccc' }}>
      Themed Button
    </button>
  );
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedButton />
    </ThemeContext.Provider>
  );
}

export default App;
```

## `useReducer` for State Management

`useReducer` hook as alternative to `useState`, useful for managing more complex state logic:

```jsx
import React, { useReducer } from 'react';

// Reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}

export default Counter;
```

## `useMemo` for Performance Optimization

`useMemo` hook to memoize expensive calculations and prevent unnecessary recalculations:

```jsx
import React, { useMemo, useState } from 'react';

function ExpensiveComponent({ number }) {
  const computeFactorial = (n) => {
    console.log('Computing factorial...');
    return n <= 1 ? 1 : n * computeFactorial(n - 1);
  };

  // Memoize the result to avoid re-computing
  const factorial = useMemo(() => computeFactorial(number), [number]);

  return <div>Factorial of {number} is {factorial}</div>;
}

function App() {
  const [number, setNumber] = useState(5);

  return (
    <div>
      <input
        type="number"
        value={number}
        onChange={(e) => setNumber(Number(e.target.value))}
      />
      <ExpensiveComponent number={number} />
    </div>
  );
}

export default App;
```

## `useRef` for Referencing DOM Elements

`useRef` hook to store a mutable reference to a DOM element or any value that persists across renders

```jsx
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();  // Access the DOM element directly
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Click button to focus" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}

export default FocusInput;
```

## Styled Components

Use template literals to define CSS styles for components:

```jsx
import React from 'react';
import styled from 'styled-components';

// Define a styled button component
const StyledButton = styled.button`
  background-color: ${(props) => (props.primary ? '#007bff' : '#ccc')};
  color: white;
  font-size: 1rem;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;

  &:hover {
    background-color: ${(props) => (props.primary ? '#0056b3' : '#999')};
  }
`;

const App = () => {
  return (
    <div>
      <StyledButton primary>Primary Button</StyledButton>
      <StyledButton>Secondary Button</StyledButton>
    </div>
  );
};

export default App;

```
