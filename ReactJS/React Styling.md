# React Styling Examples

## 1. Inline Styling

You can apply styles directly using the `style` prop in JSX.

```jsx
let myStyle = {
    color: "black",
    padding: "20px",
    backgroundColor: "blue"
};

<h1 style={myStyle}>Hi and hello</h1>
<h3 style={{color: "yellow", background: "grey"}}>Thank you</h3>
```

> Note: Property names are camelCase (e.g., `backgroundColor`, not `background-color`).

---

## 2. CSS Modules (Scoped Styling)

Create a `.module.css` file (e.g., `Header.module.css`) and import it:

```jsx
import styles from './Header.module.css';

<h2 className={styles.greenTheme}>Hi from header</h2>
```

**Header.module.css:**

```css
.greenTheme {
  color: green;
  margin: 10px;
}
```

> Tip: Avoid quotes around property values in CSS files.

---

## 3. Mapping and Rendering Components

When rendering a list:

```jsx
{details.map((d) => (
  <ShipDetail key={d.speed} detail={d} />
))}
```

> Mistake to avoid:
> 
> - Returning inside a block without parentheses
>     

---
