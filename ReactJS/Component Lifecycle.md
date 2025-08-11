# 🔁 React Component Lifecycle

React components go through a lifecycle from creation to destruction. Lifecycle methods (in class components) or hooks (in functional components) allow us to run code at specific points in that lifecycle.

---

## 🧱 Lifecycle Phases

1. **Mounting** – when the component is created and inserted into the DOM.
2. **Updating** – when the component is re-rendered due to changes in props or state.
3. **Unmounting** – when the component is removed from the DOM.

---

## 🏛 Class Component Lifecycle Methods

| Phase       | Method                  | Purpose                                      |
|------------|-------------------------|----------------------------------------------|
| Mounting   | `constructor()`         | Initialize state, bind methods               |
| Mounting   | `static getDerivedStateFromProps()` | Sync state with props                      |
| Mounting   | `render()`              | Render JSX                                   |
| Mounting   | `componentDidMount()`   | Run after component is added to DOM          |
| Updating   | `shouldComponentUpdate()`| Return true/false to control re-render       |
| Updating   | `getSnapshotBeforeUpdate()`| Capture some info before update (e.g., scroll pos) |
| Updating   | `componentDidUpdate()`  | Run after re-render                          |
| Unmounting | `componentWillUnmount()`| Cleanup (timers, listeners, etc.)            |

---

## 🪝 Functional Component Equivalent with Hooks

```jsx
import { useEffect, useState } from 'react';

function Example() {
    const [count, setCount] = useState(0);

    // Mimics componentDidMount (runs once)
    useEffect(() => {
        console.log('Component mounted');
    }, []);

    // Mimics componentDidUpdate (runs when count changes)
    useEffect(() => {
        console.log('Count updated:', count);
    }, [count]);

    // Mimics componentWillUnmount (cleanup function)
    useEffect(() => {
        const interval = setInterval(() => {
            setCount(prev => prev + 1);
        }, 1000);

        return () => {
            clearInterval(interval);
            console.log('Component unmounted');
        };
    }, []);

    return <h1>{count}</h1>;
}