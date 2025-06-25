## **JavaScript Promises**

### **What is a Promise?**

A **Promise** is an object representing the eventual **completion** or **failure** of an asynchronous operation.

### **Three States of a Promise:**

1. **Pending** – Initial state, operation not completed yet.
    
2. **Fulfilled** – Operation completed successfully (`resolve()` is called).
    
3. **Rejected** – Operation failed (`reject()` is called).
    

### **Creating a Promise:**

```
const promise = new Promise((resolve, reject) => {   
let success = true;   
if (success) {     
resolve("Task completed successfully!");  
} 
else {   
reject("Task failed.");  
}
});
```

### **Handling Promises:**

- `.then()` – Executes when the promise is **fulfilled**.
    
- `.catch()` – Executes when the promise is **rejected**.
    
- `.finally()` – Executes **regardless** of the outcome.

```
promise.then(result => console.log(result))     // "Task completed successfully!"   

.catch(error => console.log(error))      // If failed: "Task failed." 

.finally(() => console.log("Done"));     // Always runs
```

---

## **Async/Await**

### **Why use async/await?**

`async/await` makes asynchronous code look and behave more like synchronous code, improving readability.

### **Syntax:**

```
async function fetchData() { 
try {    
const response = await fetch("https://api.example.com/data");   
const data = await response.json();   
console.log(data);  
}
catch (error) {    
console.error("Error fetching data:", error);  
}
}
```

> **await** pauses the function until the Promise resolves.  
> **try...catch** handles errors just like synchronous code.

---

### **Key Differences:**

|Feature|Promises (then/catch)|Async/Await|
|---|---|---|
|Syntax|Chain-based|Linear, clean|
|Error handling|`.catch()`|`try...catch`|
|Readability|Okay for short chains|Better for logic|

---

## **Callbacks in JavaScript**

### **What is a Callback?**

A **callback** is a **function passed as an argument to another function**, which is then **invoked inside the outer function** to complete some kind of routine or action.

It allows you to execute code **after** something else has finished executing — **especially useful in asynchronous programming**.

---

### **Basic Example of a Callback:**

```
function greet(name, callback) { 
console.log("Hello " + name);  
callback();
}  
function sayBye() {   
console.log("Goodbye!"); 
}  
greet("Sibi", sayBye);
```

**Output:**
`Hello Sibi Goodbye!`

### **Callbacks in Asynchronous Operations:**

Callbacks are heavily used in asynchronous JavaScript — such as reading a file, fetching data, or setting timeouts.

```
setTimeout(function () {   console.log("Executed after 2 seconds"); }, 2000);
```

Here, the **anonymous function** is a **callback** that runs after 2 seconds.

---

### **Why Use Callbacks?**

- To ensure **asynchronous operations** complete **before** moving forward.
    
- Helps to **avoid blocking code execution** (non-blocking behavior).
    

---

### **Callback Hell**

If callbacks are nested too deeply (e.g., callback inside callback inside callback), it becomes hard to read and maintain — known as **"Callback Hell"** or **"Pyramid of Doom"**.

```
doTask1(() => {  
doTask2(() => {     
doTask3(() => {       
console.log("All tasks done!");     
});   
});
});
```

To avoid this, developers prefer **Promises** or **async/await**.

---

### **Conclusion:**

Callbacks are one of the fundamental concepts in JavaScript, especially for asynchronous operations. However, modern JavaScript often prefers **Promises** and **async/await** for better readability and control flow.