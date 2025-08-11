
---
# 🔄 `useEffect` Hook - Overview

The `useEffect` hook in React lets you perform **side effects** in function components. Side effects include:

- Data fetching
    
- DOM manipulation
    
- Setting up subscriptions or timers
    

---

## 📘 Basic Syntax

```jsx
useEffect(() => {
    // Side-effect logic
    return () => {
        // Cleanup logic (optional)
    };
}, [dependencies]);
```

- The first argument is the function to run after render.
    
- The second argument (optional) is the **dependency array**.
    

---

## 🧠 Why use `useEffect`?

- To perform operations **after** render
    
- To avoid repetitive code in event handlers
    
- To manage **asynchronous behavior**
    

---

## 🔁 Different Usages of `useEffect`

### 1. 📦 Run Once on Mount (like `componentDidMount`)

```jsx
useEffect(() => {
    console.log("Component mounted");
}, []); // Empty dependency array
```

### 2. 🔄 Run on Every Render

```jsx
useEffect(() => {
    console.log("Rendered or updated");
}); // No dependency array
```

### 3. 🧠 Run When Specific State(s) Change

```jsx
useEffect(() => {
    console.log("count changed");
}, [count]);
```

### 4. 🧹 With Cleanup (like `componentWillUnmount`)

```jsx
useEffect(() => {
    const interval = setInterval(() => {
        console.log("Timer");
    }, 1000);

    return () => {
        clearInterval(interval);
        console.log("Cleaned up");
    };
}, []);
```

### 5. 🌐 Fetching Data

```jsx
useEffect(() => {
    async function fetchData() {
        const res = await fetch("https://api.example.com");
        const data = await res.json();
        console.log(data);
    }
    fetchData();
}, []);
```

---

## 🔗 Multiple Dependencies Example

```jsx
useEffect(() => {
    console.log("count or name changed");
}, [count, name]);
```

The effect runs when either `count` or `name` changes.

---

## ⚠️ Common Mistakes

- Forgetting to add dependencies → causes stale data
    
- Updating state inside effect without dependencies → causes infinite loop
    

---

## 📝 Summary

|Pattern|Behavior|
|---|---|
|`useEffect(() => {}, [])`|Runs once on mount|
|`useEffect(() => {})`|Runs after every render|
|`useEffect(() => {}, [a, b])`|Runs when `a` or `b` changes|
|`return () => {}`|Cleanup on unmount or re-run|

---