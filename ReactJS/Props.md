## 🧠 React Props in Functional and Class Components

### 🔹 What are Props?

- `props` (short for **properties**) are used to pass data from a **parent component** to a **child component**.
    
- Props are **read-only** and **immutable** within the receiving component.
    

---

### ✅ Functional Component — Using Props

#### 🧪 Example 1: Accessing props directly


```jsx
function ShipDetail(props) 
{     
return (    
<h1>Ship in {props.detail.color} and width of {props.detail.size}</h1>     );
}
```

#### 🧪 Example 2: Destructuring props

```jsx
function ShipDetail({ detail }) 
{
const { color, size } = detail;   
return (  
<h1>Ship in {color} and width of {size}</h1>  
); 
}
```


---

### ✅ Class Component — Using Props

#### 🧪 Example 1: Accessing props inside `render`

```jsx
import React from "react"; 
class Evergreen extends React.Component {    
render() {  
const { detail } = this.props; 
const { color, speed } = detail;  
return (      
<h1>Hi from Evergreen with speed of {speed} and color {color}</h1>         ); 
}
}
```

#### 🧪 Example 2: Storing props in constructor

```jsx
import React from "react"; 
class Evergreen extends React.Component {  
constructor(props) {    
super(props);     
this.color = props.detail.color;  
this.speed = props.detail.speed;  
} 
render() {     
return (      
<h1>Hi from Evergreen with speed of {this.speed} and color {this.color}</h1>     
);  
} 
}
```

### 🔍 Notes

- Always call `super(props)` in class constructors before accessing `this.props`.
    
- Destructuring makes JSX more readable.
    
- Props are not state; they are passed down from parent to child and cannot be changed inside the child.