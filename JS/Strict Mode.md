**Strict Mode** enables a restricted version of JavaScript, helping developers avoid silent bugs and write cleaner, more secure code.

#### **How to Enable Strict Mode**

You enable it using the string:
```
"use strict";
```

- Placing it **at the top of a script** enables strict mode for the **entire file**.
    
- Placing it **inside a function** enables strict mode only for that **function scope**. 
### **What Strict Mode Does**

It prevents or throws errors for:

1. **Undeclared variables**
```
"use strict"; x = 10; // ReferenceError
```
2. **Re-declaring variables with `var`**
```
"use strict"; var a = 5; var a = 10; // SyntaxError
```
3. **Deleting variables or functions**
```
"use strict"; var a = 1; delete a; // SyntaxError
```
4. **Duplicate parameter names in a function**
```
"use strict"; function test(a, a) {} // SyntaxError
```
#### **Other Benefits**

- Helps in avoiding use of reserved keywords.
    
- Prevents accidental creation of global variables.
    
- Makes assignments to read-only properties throw errors instead of silen