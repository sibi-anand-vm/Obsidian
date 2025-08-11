
# 📘 React Router 

## What is React Router?

React Router is a standard library for routing in React. It enables navigation among views of various components in a React Application, allows changing the browser URL, and keeps UI in sync with the URL.

---

## Installation

```bash
npm install react-router-dom
```

---

## Basic Setup with `BrowserRouter`

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

---

## Navigation with `NavLink`

```jsx
import { NavLink } from 'react-router-dom';

<NavLink to="/" className={({ isActive }) => isActive ? 'active' : ''}>Home</NavLink>
<NavLink to="/about" className={({ isActive }) => isActive ? 'active' : ''}>About</NavLink>
```

### ✅ Advantages over `Link`

- `NavLink` can apply styles based on active route.
    
- Helpful in navigation menus.
    

---

## Dynamic Routing with Parameters

```jsx
<Route path="/user/:id" element={<User />} />
```

In `User.js`:

```jsx
import { useParams } from 'react-router-dom';
const { id } = useParams();
```

---

## Nested Routes

```jsx
<Route path="/books">
  <Route path="old-books" element={<OldBooks />} />
  <Route path="new-books" element={<NewBooks />} />
</Route>
```

---
# Full Code
```jsx
import { BrowserRouter, Routes, Route, NavLink } from "react-router-dom";
import Home from "./components/Home";
import Contact from "./components/Contact";
import Login from "./components/Login";
import User from "./components/User";
import OldBooks from "./components/OldBooks";
import NewBooks from "./components/NewBooks";
import DashBoard from "./components/DashBoard";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <ul>
          <li><NavLink to="/" end className={({ isActive }) => isActive ? "active-link" : ""}>Home</NavLink></li>
          <li><NavLink to="/contact" className={({ isActive }) => isActive ? "active-link" : ""}>Contact</NavLink></li>
          <li><NavLink to="/login" className={({ isActive }) => isActive ? "active-link" : ""}>Login</NavLink></li>
          <li><NavLink to="/user/1" className={({ isActive }) => isActive ? "active-link" : ""}>User 1</NavLink></li>
          <li><NavLink to="/user/2" className={({ isActive }) => isActive ? "active-link" : ""}>User 2</NavLink></li>
          <li><NavLink to="/books/old-books" className={({ isActive }) => isActive ? "active-link" : ""}>Old Books</NavLink></li>
          <li><NavLink to="/books/new-books" className={({ isActive }) => isActive ? "active-link" : ""}>New Books</NavLink></li>
        </ul>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/contact" element={<Contact />} />
        <Route path="/login" element={<Login />} />
        <Route path="/user/:id" element={<User />} />
        <Route path="/books/old-books" element={<OldBooks />} />
        <Route path="/books/new-books" element={<NewBooks />} />
        <Route path="/dashboard" element={<DashBoard />} />
        <Route path="*" element={<h2>404 - Page Not Found</h2>} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;

```
## Summary

- `BrowserRouter` is the router provider.
    
- `Routes` contains all defined `Route` components.
    
- `NavLink` is used for navigation with active styling.
    
- Dynamic and nested routing supported with `useParams` and nested `Route` structure.
    

---

Happy Routing 🚀