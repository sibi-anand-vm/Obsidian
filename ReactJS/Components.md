## ⚛️ React Functional Components

### 🔹 What is a Functional Component?

- A **functional component** is a plain JavaScript function that **returns JSX**.
    
- It is used to define a **UI building block** in React.
    
- It is the most common way to write components in **modern React** (especially with Hooks).
```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
// import './index.css';
// import App from './App.jsx';

function Titanic() {
  return (
    <>
      <h1>I am bigger than all ships</h1>
      <Yacht />
    </>
  );
}

function Yacht() {
  return (
    <>
      <h1>I am smaller than all ships</h1>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Titanic />
  </StrictMode>
);

```

### 🧠 What’s Happening Here?

#### ✅ Functional Components

- `Titanic` and `Yacht` are **React functional components**.
    
- Functional components are just **JavaScript functions** that return JSX.
    
- They **must start with a capital letter** (React convention).
    

#### 🧩 Component Composition

- `Titanic` is the **parent component**.
    
- It renders an `<h1>` and the **child component** `<Yacht />`.

### 📘 What is a Class Component?

- A **class component** is a React component defined using **ES6 class syntax**.
    
- It must:
    
    - Extend `React.Component`
        
    - Have a `render()` method that returns JSX
```
import React from "react";

class Evergreen extends React.Component {
  render() {
    return <h1>Hi from Evergreen</h1>;
  }
}

export default Evergreen;

```

### ✅ In React Class Components

You can also define **custom methods** inside a React class component, just like in Java:

```
import React from "react";

class Evergreen extends React.Component {
  sayHi() {
    console.log("Hi from a method!");
  }

  render() {
    this.sayHi();  // call the method during render
    return <h1>Hi from Evergreen</h1>;
  }
}

export default Evergreen;

```

In a React **class component**, **only the `render()` method** must return JSX.

But you can define **other methods** for:

- Handling logic
    
- Fetching data
    
- Updating state
    
- Utility/helper functions
    
- Event handlers
    

These methods **do not** need to return JSX — they behave just like regular JavaScript methods.

```
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  // Not returning JSX — just logic
  incrementCount() {
    this.setState({ count: this.state.count + 1 });
  }

  // Also a non-JSX function
  logMessage() {
    console.log("Button was clicked!");
  }

  render() {
    return (
      <>
        <h1>Count: {this.state.count}</h1>
        <button
          onClick={() => {
            this.incrementCount();
            this.logMessage();
          }}
        >
          Increment
        </button>
      </>
    );
  }
}

```

## Summary

| Method             | Returns JSX? | Purpose                   |
| ------------------ | ------------ | ------------------------- |
| `render()`         | ✅ Yes        | Renders the UI            |
| `incrementCount()` | ❌ No         | Handles logic             |
| `logMessage()`     | ❌ No         | Logs a message to console |
| `fetchData()`      | ❌ No         | Handles API calls, etc.   |