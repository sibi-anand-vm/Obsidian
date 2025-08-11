### 🔁 `useCallback(() => func(), [deps])`:

- It **returns a memoized function** — `func` is **not executed immediately**.
    
- The **function definition itself** remains the **same across renders** unless deps change.
    
- Useful when passing functions to child components (to avoid unnecessary re-renders).

```jsx
const memoizedFn = useCallback(() => {
  console.log("Callback called");
  return 10;
}, [count]);

```

### 🔄 Key Difference in Behavior:

| Aspect                          | `useMemo`                          | `useCallback`                           |
| ------------------------------- | ---------------------------------- | --------------------------------------- |
| When does code run?             | Immediately when component renders | Only when you **invoke the function**   |
| What's cached?                  | The **result** of the function     | The **function itself**                 |
| Internal logs/side-effects run? | Yes, when dependencies change      | Only when you manually run the function |