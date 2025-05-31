## 1. **Type Coercion (Not “Cohesion”)**

**Type coercion** is the automatic or implicit conversion of values from one data type to another.

### Example 1: Implicit Coercion (String + Number)

```
console.log("5" + 5); // Output: "55"
```

- Here, `5` (number) is coerced into a string.
    
- `"5" + "5"` becomes `"55"`
    

### Example 2: Implicit Coercion with Subtraction

```
console.log("5" - 2); // Output: 3
```

- Here, `"5"` is coerced into a number.
    
- `5 - 2` results in `3`
    

> **Note:** JavaScript coerces based on the operator:

- `+` favors string conversion
    
- `-`, `*`, `/` favor number conversion
    

---

## 2. **Nullish Coalescing Operator (`??`)**

This operator returns the **right-hand value** if the **left-hand value is `null` or `undefined`**.

### Syntax:

```
let name = userInput ?? "Guest";`
```

- If `userInput` is `null` or `undefined`, it returns `"Guest"`.
    
- Otherwise, it returns `userInput`.
    

### Difference from `||` (OR operator):

- `||` returns right-hand value for **falsey values** like `0`, `""`, `false`, `null`, `undefined`.
    
- `??` only returns right-hand value if left is **null or undefined**.
```
console.log(0 || 100);   // 100 (0 is falsey)
console.log(0 ?? 100);   // 0 (0 is not null/undefined)
```

---

## 3. **Closures**

A **closure** is created when a function is defined **inside another function** and retains access to the **outer function's scope** even after the outer function has returned.

### Example:
```
function outer() {  
let counter = 0;   
return function inner() {     
counter++;     
console.log(counter);   
};
}  const count = outer(); 
count(); // 1 
count(); // 2
```

- The `inner()` function keeps access to `counter`, even after `outer()` has finished.
    
- This is what makes it a **closure**.

### Use Cases:

- Private variables
    
- Data encapsulation
    
- Memoization
    
- Function factories