In JavaScript, **literals** are fixed values that appear directly in the code. Examples include:

- **Number literals**: `100`, `3.14`
    
- **String literals**: `'Hello'`, `"World"`
    
- **Boolean literals**: `true`, `false`
    
- **Array literals**: `[1, 2, 3]`
    
- **Object literals**: `{ name: "Sibi", age: 22 }`
    

But what you’re really referring to is **template literals**, so let’s focus on that.

---

### **Template Literals (ES6 Feature)**

Template literals allow **string interpolation**—inserting variables or expressions inside a string. This is what you were trying to describe with the "balance" example.

#### **Syntax:**

```
Balance: ${amount}
```

- **Backticks ( )** instead of single/double quotes.
    
- `${expression}` is used to insert variables or expressions into the string.
    

#### **Example:**
```
let name = "Captain"; 
let balance = 150; 
console.log(`Hello ${name}, your balance is ₹${balance}.`); // Output: Hello Captain, your balance is ₹150.
```

This is powerful because:

- You don’t need to use `+` to concatenate strings and variables.
    
- You can even use expressions inside `${}`: ```
```
Total: ${price * quantity}
```
    

---

### **Clarifying Your Bank Balance Example:**

You were trying to say:

- The phrase `"Balance: "` is constant (a literal).
    
- The number part is dynamic (from a variable).    

---

### **Recap**

- **Literals**: Direct, fixed values in your code.
    
- **Template literals**: Modern way to build dynamic strings with embedded variables or expressions using backticks and `${}`.