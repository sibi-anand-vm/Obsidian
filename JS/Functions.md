## 🔢 **1. Function Declaration (Named Function)**

- Declared with the `function` keyword.
    
- Can be called before its declaration due to **hoisting**.

```
function sayHello() {   console.log("Hello!"); }
```

✅ **Hoisted**  
✅ **Named**

---

## 💼 **2. Function Expression**

- Function assigned to a variable.
    
- Not hoisted — must be defined before use.

```
const greet = function() {   console.log("Hi!"); };
```

❌ **Not hoisted**  
🆗 **Can be anonymous or named**

---

## ⚡ **3. Arrow Function** (ES6+)

- A compact syntax introduced in ES6.
    
- Doesn’t bind its own `this`, `arguments`, `super`, or `new.target`.

```
const add = (a, b) => a + b;
```

✅ **Shorter**  
❌ **No `this` binding**

---

## 🕵️ **4. Anonymous Function**

- A function **without a name**.
    
- Often used as **callback functions**.

```
setTimeout(function() {   console.log("Executed after delay"); }, 1000);
```

---

## 🔙 **5. Immediately Invoked Function Expression (IIFE)**

- Runs as soon as it's defined.
    
- Good for **isolating scope**.

```
(function() {   console.log("IIFE runs instantly!"); })();
```
---

## 🔁 **6. Callback Function**

- A function **passed as an argument** to another function.
```
function process(callback) {   callback(); }  process(() => console.log("Callback called!"));
```

---

## 🧱 **7. Constructor Function**

- Used to create objects.
    
- Called using the `new` keyword.

```
function Person(name) {   this.name = name; }  const p1 = new Person("Captain");
```

---

## 🧠 **8. Generator Function** (Advanced)

- Declared with `function*`.
    
- Can pause and resume execution using `yield`.
```
function* generatorFunc() {   yield 1;   yield 2; }
```

---

## 📋 Summary Table

|Function Type|Description|Syntax Style|Hoisted|
|---|---|---|---|
|Function Declaration|Traditional named function|`function name() {}`|✅ Yes|
|Function Expression|Function stored in a variable|`const fn = function(){}`|❌ No|
|Arrow Function|Short ES6 function, no `this` binding|`const fn = () => {}`|❌ No|
|Anonymous Function|Function without a name|`function() {}`|❌ No|
|IIFE|Self-invoking function|`(function(){})()`|❌ No|
|Callback Function|Passed as argument to another function|`func(() => {})`|✅/❌|
|Constructor Function|Used with `new` to create instances|`function Name(){}`|✅ Yes|
|Generator Function|Pauses execution using `yield`|`function* name() {}`|✅ Yes|
