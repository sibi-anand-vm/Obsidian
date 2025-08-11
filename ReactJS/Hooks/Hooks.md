# 📘 React Hooks - Essential 7 Hooks with Use Cases & Examples


### 🪝 What Are Hooks in React?

**Hooks** are special functions introduced in **React 16.8** that allow **functional components** to use **state** and other **React features** that were previously only available in **class components**.

---

### ✅ Why Hooks?

Before hooks, features like state and lifecycle methods could only be used in class components. Hooks make it possible to:

- Manage state in functional components (`useState`)
    
- Use lifecycle-like behavior (`useEffect`)
    
- Access context (`useContext`)
    
- Optimize performance (`useMemo`, `useCallback`)
    
- Reuse logic via custom hooks
    

---

### 🔍 Key Benefits

- **Cleaner Code**: No need for boilerplate class syntax
    
- **Logic Reuse**: Create **custom hooks** to reuse code across components
    
- **Better Organization**: Group related logic together
    
- **Functional-first Approach**: Encourages writing more functional and testable code
    
---
---

## 1. `useState`

- **Use case:** To store and manage state in functional components.
    

```jsx
const [count, setCount] = useState(0);
```

```jsx
<button onClick={() => setCount(count + 1)}>Increment</button>
```

---

## 2. `useEffect`

- **Use case:** Side effects like fetching data, subscriptions, or manual DOM updates.
    

```jsx
useEffect(() => {
  console.log("Component mounted or updated");
}, [dependency]);
```

---

## 3. `useContext`

- **Use case:** Consume context without prop drilling.
    

```jsx
const value = useContext(MyContext);
```

```jsx
return <h1>{value}</h1>;
```

---

## 4. `useRef`

- **Use case:** Referencing DOM elements or persisting mutable values across renders.
    

```jsx
const inputRef = useRef(null);
```

```jsx
<input ref={inputRef} />
<button onClick={() => inputRef.current.focus()}>Focus</button>
```

---

## 5. `useMemo`

- **Use case:** Memoize expensive calculations.
    

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

---

## 6. `useCallback`

- **Use case:** Memoize function instances to prevent re-renders.
    

```jsx
const handleClick = useCallback(() => {
  doSomething();
}, [dependency]);
```

---

## 7. `useReducer`

- **Use case:** Manage complex state logic with actions.
    

```jsx
import React, { useReducer, useState } from "react";

const initialState = { result: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return { result: state.result + action.payload };
    case "subtract":
      return { result: state.result - action.payload };
    case "multiply":
      return { result: state.result * action.payload };
    case "divide":
      if (action.payload === 0) {
        alert("Cannot divide by zero");
        return state;
      }
      return { result: state.result / action.payload };
    case "reset":
      return initialState;
    default:
      return state;
  }
}

function Calculator() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const [input, setInput] = useState(0);

  return (
    <div style={{ padding: "20px", fontFamily: "Arial" }}>
      <h2>useReducer Calculator</h2>
      <input
        type="number"
        value={input}
        onChange={(e) => setInput(Number(e.target.value))}
        placeholder="Enter number"
      />
      <div style={{ marginTop: "10px" }}>
        <button onClick={() => dispatch({ type: "add", payload: input })}>
          Add
        </button>
        <button onClick={() => dispatch({ type: "subtract", payload: input })}>
          Subtract
        </button>
        <button onClick={() => dispatch({ type: "multiply", payload: input })}>
          Multiply
        </button>
        <button onClick={() => dispatch({ type: "divide", payload: input })}>
          Divide
        </button>
        <button onClick={() => dispatch({ type: "reset" })}>
          Reset
        </button>
      </div>
      <h3>Result: {state.result}</h3>
    </div>
  );
}

export default Calculator;
```

# 8.useActionState
### 🧠 What is `useActionState`?

`useActionState` is a React hook that:

- Manages state transitions like `useReducer`
    
- Uses an **async action handler**
    
- Good for server actions or complex state updates
    

> Think of it as:  
> 🔁 `useState` + 🧠 `useReducer` + 🔄 Async logic = `useActionState`

```jsx
import React, { useState, useActionState } from "react";

const initialState = { result: 0 };

async function calculatorAction(prevState, action) {
  const { type, value } = action;

  // Simulate network delay
  await new Promise((resolve) => setTimeout(resolve, 1000));

  switch (type) {
    case "add":
      return { result: prevState.result + value };
    case "subtract":
      return { result: prevState.result - value };
    case "multiply":
      return { result: prevState.result * value };
    case "divide":
      if (value === 0) {
        alert("Cannot divide by zero");
        return prevState;
      }
      return { result: prevState.result / value };
    case "reset":
      return initialState;
    default:
      return prevState;
  }
}

export default function CalculatorWithPendingState() {
  const [input, setInput] = useState(0);
  const [state, dispatch, isPending] = useActionState(calculatorAction, initialState);

  return (
    <div style={{ padding: "20px", fontFamily: "Arial" }}>
      <h2>Calculator with isPending</h2>
      <input
        type="number"
        value={input}
        onChange={(e) => setInput(Number(e.target.value))}
        disabled={isPending}
      />
      <div style={{ marginTop: "10px" }}>
        <button onClick={() => dispatch({ type: "add", value: input })} disabled={isPending}>
          Add
        </button>
        <button onClick={() => dispatch({ type: "subtract", value: input })} disabled={isPending}>
          Subtract
        </button>
        <button onClick={() => dispatch({ type: "multiply", value: input })} disabled={isPending}>
          Multiply
        </button>
        <button onClick={() => dispatch({ type: "divide", value: input })} disabled={isPending}>
          Divide
        </button>
        <button onClick={() => dispatch({ type: "reset" })} disabled={isPending}>
          Reset
        </button>
      </div>
      <h3>Result: {state.result}</h3>
      {isPending && <p style={{ color: "orange" }}>Calculating...</p>}
    </div>
  );
}

```

# 9.useFormStatus

### ⚛️ `useFormStatus` – Quick Summary

| Property  | Description                                           |
| --------- | ----------------------------------------------------- |
| `pending` | `true` while the form is submitting                   |
| `data`    | The FormData that was submitted (if using formAction) |
| `method`  | The HTTP method of the form (`GET`, `POST`, etc.)     |
| `action`  | The action URL or function                            |
| `origin`  | Origin of the submission (used in server contexts)    |
```
'use client'; // Required for useFormStatus

import { useFormStatus } from 'react-dom';

function SubmitButton() {
  const { pending } = useFormStatus();

  return (
    <button type="submit" disabled={pending}>
      {pending ? 'Submitting...' : 'Submit'}
    </button>
  );
}

export default function MyForm() {
  async function handleSubmit(formData) {
    'use server';
    const name = formData.get('name');
    console.log(`Server received: ${name}`);
    // Save to DB or do something else
  }

  return (
    <form action={handleSubmit}>
      <input type="text" name="name" placeholder="Your name" />
      <SubmitButton />
    </form>
  );
}

```
---
# 10.`useLayoutEffect`
#### Why `useLayoutEffect` works better than `useEffect` here:

If you used `useEffect` instead:

- The DOM would update (`button clicked`, state changes)
    
- The browser might briefly repaint with the **old background**
    
- Then your effect runs and updates the `body` style
    

Which may result in a **flicker** or short lag.

With `useLayoutEffect`:

- The background is changed **before paint**, so no flicker occurs.
```jsx
import { useLayoutEffect, useState } from "react";

export default function UseLayoutEffectExample() {
  const [color, setColor] = useState("red");

  useLayoutEffect(() => {
    document.body.style.backgroundColor = color;
  }, [color]);

  return (
    <div>
      <h1>UseLayoutEffect Example</h1>
      <button onClick={() => setColor("lightblue")}>Change BG</button>
    </div>
  );
}
```
- This runs **immediately after React has made DOM changes** but **before the browser paints**.
    
- That means when you click the button, the background changes **without any visual delay or flicker**.
## ✅ Summary Table

| Hook             | Use Case                                                                                  |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `useState`       | State management in functional components                                                 |
| `useEffect`      | Handle side effects                                                                       |
| `useContext`     | Access context data without props                                                         |
| `useRef`         | Mutable reference to DOM or variables                                                     |
| `useMemo`        | Optimize performance for expensive calcs                                                  |
| `useCallback`    | Optimize function reference stability                                                     |
| `useReducer`     | Advanced state management                                                                 |
| `useActionState` | handling **async operations**, **loading indicators**, or **disabling UI** while waiting. |
