### **Refined Explanation of Hoisting in JavaScript**

**Hoisting** is JavaScript’s default behavior of _moving declarations_ to the top of their scope during the **compile phase**, before code execution.

#### What Gets Hoisted?

- **Function declarations** (fully hoisted—both name and body).
    
- **Variable declarations** (`var`, `let`, `const`)—_only the declarations, not initializations_.
    
- **Class declarations**—hoisted but placed in the **Temporal Dead Zone (TDZ)** (like `let` and `const`).
    

---

### **How `var`, `let`, and `const` Differ with Hoisting**

#### **`var`**:

- **Hoisted** and **initialized as `undefined`**.
    
- You can access the variable _before_ its line of declaration—but it’ll return `undefined`.
```
console.log(a); // undefined var a = 10;
```    
#### **`let` and `const`**:

- Also **hoisted**, but **not initialized**.
    
- They exist in a **Temporal Dead Zone (TDZ)** from the start of the block until the declaration line.
    
- Accessing them in the TDZ will throw a **ReferenceError**.
```
console.log(b); // ReferenceError let b = 20;
```

> **Note**: You mentioned “cast” instead of `const` a couple of times—just a small typo.

---
### **Important Note on Hoisting and Functions**

Function **declarations** are hoisted entirely:
```
greet(); // Hello function greet() {   console.log("Hello"); }
```

But **function expressions** (like `const greet = function() {}`) follow variable hoisting rules—they're not accessible before declaration.