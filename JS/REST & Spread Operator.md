### **Refined Explanation: REST vs SPREAD Operators in JavaScript**

The `...` syntax in JavaScript can be used in two distinct ways:

---
### **1. REST Operator**

- **Used on the LEFT side of assignment**, typically in function parameters or destructuring.
    
- **Collects** multiple elements into a **single array or object**.
    
- It “gathers” values.
    
#### **Function Parameters Example:**
```
function sum(...numbers) {   return numbers.reduce((acc, val) => acc + val, 0); }  sum(1, 2, 3); // 6
```

Here, `...numbers` gathers all arguments into an array.
#### **Destructuring Example:**

```
const [first, ...rest] = [10, 20, 30, 40]; 
console.log(first); // 10 
console.log(rest);  // [20, 30, 40]
```

---

### **2. SPREAD Operator**

- **Used on the RIGHT side of assignment or function call**.
    
- **Expands** elements from an array or object.
    
- It “spreads” values out.
    
#### **Example:**

```
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; 
console.log(arr2); // [1, 2, 3, 4]
```

#### **Function Call Example:**
```
function greet(name1, name2) {   
console.log(`Hello ${name1} and ${name2}`); }  
const names = ["Captain", "Sibi"]; 
greet(...names); // Hello Captain and Sibi
```

---
### **Key Difference:**

|Operator Type|Position|Action|Common Use|
|---|---|---|---|
|**REST**|Left side|Gathers elements|Function parameters, destructuring|
|**SPREAD**|Right side|Spreads elements|Arrays, objects, function calls|

---

### **Your Example (Corrected):**

> When you use `...` on the left (like in a function parameter), it's called the **rest operator**—because it collects the remaining values.  
> When you use `...` on the right (like in an array or function call), it's the **spread operator**—because it spreads elements out.