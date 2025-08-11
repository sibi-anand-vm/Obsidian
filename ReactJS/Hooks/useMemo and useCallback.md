// Difference Between useMemo and useCallback
```jsx
import { useState, useMemo, useCallback } from "react";

export default function MemoVsCallback() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // useMemo memoizes the return value of a function
  // It will only re-run the function if one of the dependencies has changed.
  // In this case, it performs an expensive computation.
  const expensiveComputation = useMemo(() => {
    console.log("🧮 useMemo: computing...");
    let total = 0;
    for (let i = 0; i < 100000000; i++) {
      total += i;
    }
    return total;
  }, [count]);

  // useCallback memoizes the function itself
  // It returns the same function instance unless the dependencies change.
  // Useful when passing callbacks to child components to avoid unnecessary re-renders.
  const handleClick = useCallback(() => {
    console.log("🖱️ useCallback: button clicked");
    alert("Button clicked!");
  }, [text]);

  return (
    <div>
      <h2>useMemo vs useCallback</h2>

      <h3>Expensive Computation Result: {expensiveComputation}</h3>
      <button onClick={() => setCount(c => c + 1)}>Increment Count</button>

      <hr />

      <input
        type="text"
        placeholder="Type something..."
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}
```


✅ useMemo vs useCallback Summary:

useMemo:
- Returns a **memoized value**.
- Good for expensive computations.
- Example: Caching the result of a heavy calculation.

useCallback:
- Returns a **memoized function**.
- Good for event handlers and callbacks.
- Prevents unnecessary re-renders in child components receiving props.

