## 📘 ReactJS Overview

### 🔹 What is ReactJS?

- ReactJS is a **JavaScript library** used for building **user interfaces (UIs)**.
    
- It is **written in JavaScript**, not over it.
    
- React enables **dynamic, component-based UIs** without reloading the full page.
    

---

### 🔸 ReactJS vs Traditional HTML

#### 🧱 Traditional HTML Workflow:

- The browser sends a request to the server.
    
- The server responds with a **complete HTML page**.
    
- For every new page or interaction, the **entire page reloads**.
    

#### ⚛️ ReactJS Workflow:

- On the **initial load**, the server sends:
    
    - A **minimal HTML file**
        
    - A **JavaScript bundle** that includes React and app logic
        
- After that, React handles UI changes **on the client side**.
    
- If any data is needed, it sends **AJAX/fetch requests** to the server, not full page reloads.
    

---

### ⚡ How React Updates the UI

- React uses a **Virtual DOM** to track changes in the UI.
    
- When state or props change:
    
    - React calculates the **difference (diffing)** between the old and new virtual DOM.
        
    - It then updates **only the necessary parts** of the actual DOM.
        
- This makes UI updates **fast, efficient**, and **smoother** than traditional methods.

## ⚛️ JSX (JavaScript XML)

### 🔹 What is JSX?

- **JSX** stands for **JavaScript XML**.
    
- It is a **syntax extension** for JavaScript, used in React to **write HTML-like code** inside JavaScript.
    
- It makes code **more readable** and allows UI structure to be defined **declaratively**.
    

---

### 🔸 Why Use JSX?

- JSX allows you to write components in a way that looks like HTML but behaves like JavaScript.
    
- Helps **visualize the component structure** clearly.
    
- Easier to manage the logic (JavaScript) and UI (HTML-like JSX) in one place.
    

---

### 🧠 How JSX Works Behind the Scenes

- JSX is **not valid JavaScript** — the browser **cannot understand JSX directly**.
    
- Tools like **Babel** compile JSX into `React.createElement()` calls.