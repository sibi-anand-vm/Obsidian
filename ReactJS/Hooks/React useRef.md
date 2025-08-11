
`useRef` is a React hook that lets you create a **mutable reference object** that persists across the re-renders of a component. Unlike state, updating a ref's value does not cause the component to re-render. 
## React useRef Practical Examples

## 1. Managing Focus


```jsx
import { useRef } from "react";

export default function FocusExample() {
  const inputRef = useRef();

  const handleFocus = () => inputRef.current.focus();

  return (
    <div>
      <input ref={inputRef} placeholder="Focus me..." />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

---

## 2. Scrolling to Elements

```jsx
import { useRef } from "react";

export default function ScrollExample() {
  const sectionRef = useRef();

  const scrollToSection = () => {
    sectionRef.current.scrollIntoView({ behavior: "smooth" });
  };

  return (
    <div style={{ height: "150vh", padding: "20px" }}>
      <button onClick={scrollToSection}>Scroll to Section</button>
      <div style={{ marginTop: "120vh", height: "100px", background: "lightcoral" }} ref={sectionRef}>
        <h2>Target Section</h2>
      </div>
    </div>
  );
}
```

---

## 3. Measuring Dimensions

```jsx
import { useEffect, useRef, useState } from "react";

export default function MeasureExample() {
  const boxRef = useRef();
  const [size, setSize] = useState({ width: 0, height: 0 });

  useEffect(() => {
    const { offsetWidth, offsetHeight } = boxRef.current;
    setSize({ width: offsetWidth, height: offsetHeight });
  }, []);

  return (
    <div>
      <div
        ref={boxRef}
        style={{ width: "300px", height: "150px", background: "lightgreen" }}
      >
        Box
      </div>
      <p>Width: {size.width}px, Height: {size.height}px</p>
    </div>
  );
}
```

---

## 4. Using a Third-Party Canvas Library

```jsx
import { useEffect, useRef } from "react";

export default function ThirdPartyExample() {
  const canvasRef = useRef();

  useEffect(() => {
    const ctx = canvasRef.current.getContext("2d");
    ctx.fillStyle = "orange";
    ctx.fillRect(10, 10, 150, 100);
  }, []);

  return (
    <div>
      <canvas ref={canvasRef} width="200" height="150" style={{ border: "1px solid black" }} />
      <p>Canvas drawn with 2D context via useRef.</p>
    </div>
  );
}
```
