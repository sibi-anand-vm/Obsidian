## ✅ 1. **Event Handlers**

Event handlers are functions that run when an event (like a click or key press) occurs on an element.

### 🔹 Common ways to add event handlers:


```
Inline (not recommended) 
<button onclick="sayHello()">Click</button> 

// Using JavaScript (preferred) 
document.getElementById("btn").onclick = sayHello;  

// Better: addEventListener document.getElementById("btn").addEventListener("click", sayHello);
```

---

## ✅ 2. **Mouse Events**

### 🖱️ Common Mouse Events:

|Event Type|Description|
|---|---|
|`click`|When an element is clicked|
|`dblclick`|Double-click|
|`mousedown`|Mouse button is pressed|
|`mouseup`|Mouse button is released|
|`mouseover`|Mouse enters element|
|`mouseout`|Mouse leaves element|
|`mousemove`|Mouse is moved over the element|
|`contextmenu`|Right-click|

### 🔹 Example:

```
<button id="btn">Click Me</button> 
<script>  
document.getElementById("btn").addEventListener("click", function() {     alert("Button clicked!");   });
</script>
```

---

## ✅ 3. **Keyboard Events**

### ⌨️ Common Keyboard Events:

|Event Type|Description|
|---|---|
|`keydown`|Key is pressed down|
|`keyup`|Key is released|
|`keypress`|(Deprecated) Key that produces a character is pressed|

### 🔹 Example:
```
<input type="text" id="inputBox" placeholder="Type something..." />  

<script>  
document.getElementById("inputBox").addEventListener("keydown", function(event) {    
console.log("Key pressed:", event.key);  
});
</script>
```

---

## ✅ Bonus: `event` object

When an event happens, the handler receives an `event` object containing details:

```
element.addEventListener("click", function(event) {   console.log(event.target); // the element clicked   console.log(event.type);   // "click" });
```