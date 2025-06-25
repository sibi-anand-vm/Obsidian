## ✅ 1. **`getElementById()`**

### 🔹 Purpose: Get **one element** by its unique `id`.


```
<p id="myPara">Hello</p> 
<script>  
const para = document.getElementById("myPara");   
para.innerText = "Updated using ID!"; 
</script>
```

🔸 **Returns**: A single DOM element  
🔸 **Note**: ID must be unique in the entire page.

---

## ✅ 2. **`getElementsByName()`**

### 🔹 Purpose: Get **all elements** with a specific `name` attribute (commonly used in forms).


```
<p name="info">Paragraph 1</p>
<p name="info">Paragraph 2</p> 
<script>   
const elements = document.getElementsByName("info");   
for (let el of elements) {    
el.innerText = "Updated using Name!";  
} 
</script>
```

🔸 **Returns**: A **NodeList** (like an array) of elements  
🔸 **Note**: Mostly used for form inputs (like radio buttons), but works with any tag.

---

## ✅ 3. **`getElementsByClassName()`**

### 🔹 Purpose: Get **all elements** with a specific class.

```
<p class="message">Line 1</p> 
<p class="message">Line 2</p>  
<script>   
const messages = document.getElementsByClassName("message");   
for (let msg of messages) {   
msg.innerText = "Updated using Class!";  
} 
</script>
```

🔸 **Returns**: An **HTMLCollection** (similar to NodeList)  
🔸 **Note**: Use class when many elements need the same style or behavior.

---

## ✅ 4. **`getElementsByTagName()`**

### 🔹 Purpose: Get **all elements** of a given HTML tag name.

```
<p>This is para 1</p>
<p>This is para 2</p> 
<script>   
const paras = document.getElementsByTagName("p");   
for (let p of paras) {  
p.innerText = "Updated using Tag!";   
} </script>
```

🔸 **Returns**: An **HTMLCollection** of all matching elements  
🔸 **Use**: To select all `<p>`, `<div>`, `<img>`, etc.


### **DOM Methods & Properties – Fully Commented Program**

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>DOM Properties & Methods</title>
  <style>
    .highlight {
      background-color: yellow;
      color: red;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>

  <h1 id="header">Original Heading</h1>

  <p id="para"><b>Visible Text</b> with some <i>HTML</i></p>
  <p id="hiddenPara" class="hidden">This is hidden text.</p>

  <input type="text" id="myInput" value="Initial Value">
  <button onclick="runDemo()">Run Demo</button>

  <div id="demoContainer"></div>

  <script>
    function runDemo() {
      const header = document.getElementById("header");
      const para = document.getElementById("para");
      const hiddenPara = document.getElementById("hiddenPara");
      const input = document.getElementById("myInput");
      const container = document.getElementById("demoContainer");

      // 1. innerText: visible text only
      console.log("1. innerText:", para.innerText);
      // Output: "Visible Text with some HTML"

      // 2. innerHTML: includes tags
      console.log("2. innerHTML:", para.innerHTML);
      // Output: "<b>Visible Text</b> with some <i>HTML</i>"

      // 3. textContent: includes hidden text too
      console.log("3. textContent (hiddenPara):", hiddenPara.textContent);
      // Output: "This is hidden text."

      // 4. outerHTML: whole element including self
      console.log("4. outerHTML of para:", para.outerHTML);
      // Output: <p id="para"><b>Visible Text</b> with some <i>HTML</i></p>

      // 5. value: input value
      console.log("5. Input value:", input.value);
      // Output: "Initial Value"
      input.value = "Updated via JS"; // input field text will change

      // 6. setAttribute
      header.setAttribute("title", "This is the heading"); // tooltip on hover
      header.setAttribute("class", "highlight"); // applies CSS class

      // 7. getAttribute
      const titleAttr = header.getAttribute("title");
      console.log("7. Title attribute of header:", titleAttr);
      // Output: "This is the heading"

      // 8. style.property
      para.style.color = "blue"; // text color becomes blue
      para.style.fontSize = "18px"; // font size increases

      // 9. className / classList
      para.className = "highlight"; // sets class
      para.classList.remove("highlight"); // removes it
      para.classList.add("highlight"); // adds it back again

      // 10. appendChild() / removeChild()
      const newPara = document.createElement("p");
      newPara.innerText = "Appended paragraph via appendChild()";
      container.appendChild(newPara); // paragraph appears

      // remove it after 3 seconds
      setTimeout(() => {
        container.removeChild(newPara);
        // The paragraph disappears after 3s
      }, 3000);

      // 11. append() / prepend()
      container.append(" ← Appended text at end");
      container.prepend("Prepended text at start → ");
      // These texts appear before and after the container content

      // 12. createElement()
      const boldElement = document.createElement("b");
      boldElement.innerText = "Bold Text Created!";
      container.appendChild(boldElement); // bold text is added

      // 13. parentNode, childNodes, firstChild, lastChild
      console.log("13. parentNode of input:", input.parentNode.tagName);
      // Output: "BODY"

      console.log("13. childNodes of container:", container.childNodes.length);
      // Output: number of child nodes in #demoContainer

      console.log("13. firstChild:", container.firstChild.textContent.trim());
      // Output: "Prepended text at start →"

      console.log("13. lastChild:", container.lastChild.textContent.trim());
      // Output: may vary depending on timing; likely "Bold Text Created!"
    }
  </script>

</body>
</html>

```