```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>React JSX Example</title>

  <!-- Babel Compiler for JSX -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <!-- React & ReactDOM from CDN -->
  <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
</head>
<body>
  <div id="container"></div>

  <!-- JSX Code Block -->
  <script type="text/babel">
    function SayHello() {
      return <h1>Hi and Hello</h1>;
    }

    const { createRoot } = ReactDOM;
    const root = createRoot(document.getElementById('container'));
    root.render(<SayHello />);
  </script>
</body>
</html>

```

## 🧠 Why React Components Must Be Uppercase

### 1. **JSX Rule: Lowercase = HTML Tag**

In JSX, **lowercase tags like `<div>` or `<span>` are treated as HTML elements**, not custom components.

> So when you write:

`<sayHello />`

React thinks `sayHello` is an **HTML tag**, like `<div>` or `<section>`, and tries to render it as such — but since no such HTML tag exists, **nothing shows up** or an error may occur.

---

### 2. **Uppercase = React Component**

If a tag starts with an **uppercase letter**, React understands that it's a **user-defined component**.

```
<SayHello />
```

React will now **call the `SayHello` function** and render its return value (`<h1>Hi and Hello</h1>`).