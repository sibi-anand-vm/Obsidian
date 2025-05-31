### **Corrections and Enhancements**

1. **`var` (not "where")**  
    The keyword is `var`—it’s the older way of declaring variables.
    
2. **Scoping Differences**
    
    - `var` is **function scoped**, not global scoped by default. It only becomes global scoped if declared outside a function.
```
function test() {   var x = 10; } 
console.log(x); // Error, x is not defined
```
        
3. **`let`**
    
    - `let` is **block scoped**, not function scoped. That means it’s only accessible within the `{}` block where it's declared.
```
if (true) {   let y = 20; } 
console.log(y); // Error: y is not defined
```
            
4. **`const`**
    
    - `const` is also **block scoped**, just like `let`.
        
    - The key difference: once assigned, the variable **cannot be reassigned**.
        
    - However, **objects and arrays declared with `const` can have their contents mutated**:
        
```
const obj = { a: 1 }; obj.a = 2; // This is allowed 
obj = {}; // Error
```