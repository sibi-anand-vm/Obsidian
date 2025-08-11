# React SPA with Authentication and Private Route (Context + Protected Pages)

This guide demonstrates a typical pattern for:
- Managing auth state using Context API.
- Creating a `PrivateRoute` wrapper to protect certain routes.
- Redirecting to login if the user is not authenticated.

---

## 🧱️ 1. `AuthContext.jsx`

```jsx
import { createContext, useContext, useState } from "react";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [auth, setAuth] = useState({
    isAuthenticated: false,
    user: null,
    token: null,
  });

  const login = ({ user, token }) => {
    setAuth({ isAuthenticated: true, user, token });
  };

  const logout = () => {
    setAuth({ isAuthenticated: false, user: null, token: null });
  };

  return (
    <AuthContext.Provider value={{ auth, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  return useContext(AuthContext);
}
```

---

## 🛡️ 2. `PrivateRoute.jsx`

```jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "./AuthContext";

export default function PrivateRoute({ children }) {
  const { auth } = useAuth();

  if (!auth.isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  return children;
}
```

---

## 🔑 3. `Login.jsx`

```jsx
import { useAuth } from "./AuthContext";
import { useNavigate } from "react-router-dom";

export default function Login() {
  const { login } = useAuth();
  const navigate = useNavigate();

  const handleLogin = () => {
    const user = { name: "Captain" };
    const token = "demo-token-123";
    login({ user, token });
    navigate("/profile", { replace: true });
  };

  return (
    <div>
      <h2>Login Page</h2>
      <button onClick={handleLogin}>Login</button>
    </div>
  );
}
```

### `navigate("/profile", { replace: true })` in React Router:

> **Purpose:** After successful login, it redirects the user to the `/profile` page, and replaces the current history entry instead of adding a new one.

---

### 🔄 With vs Without `replace: true`

| `replace: false` (default)                                  | `replace: true`                       |
| ----------------------------------------------------------- | ------------------------------------- |
| Pushes `/profile` **on top of** `/login` in browser history | Replaces `/login` **with** `/profile` |

---

## 👤 4. `UserProfile.jsx`

```jsx
import { useAuth } from "./AuthContext";

export default function UserProfile() {
  const { auth, logout } = useAuth();

  return (
    <div>
      <h2>Welcome, {auth.user.name}</h2>
      <p>Your token: {auth.token}</p>
      <button onClick={logout}>Logout</button>
    </div>
  );
}
```

---

## 🧱️ 5. `App.jsx`

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { AuthProvider } from "./AuthContext";
import Login from "./Login";
import UserProfile from "./UserProfile";
import PrivateRoute from "./PrivateRoute";

export default function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Routes>
          <Route path="/login" element={<Login />} />
          <Route
            path="/profile"
            element={
              <PrivateRoute>
                <UserProfile />
              </PrivateRoute>
            }
          />
          <Route path="*" element={<h2>404 Page</h2>} />
        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}
```

---

## 🛠️ Setup

```bash
npm install react-router-dom
```

---

## ✅ Behavior

- Accessing `/profile` without login redirects to `/login`.
- After login, redirected to `/profile`.
- Logout clears session and navigates back to `/login`.

You can use this `PrivateRoute` pattern for any page that requires authentication.
