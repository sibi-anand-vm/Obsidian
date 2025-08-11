# React State Management - Obsidian Note

---

## 🧠 What is State?

In React, **state** is a built-in object that stores property values that belong to a component. When the state object changes, the component re-renders automatically.

---

## ❓ Why State is Needed

- To store and manage dynamic data in components
    
- Trigger UI updates based on user actions
    
- Preserve data across re-renders
    

> Without state, React components would always render the same output.

---

## 🧩 State in Functional Components (Using `useState`)

### 📦 Example: Car Component (Object State)

```jsx
import { useState } from "react";

function Car(){
    const [car, setCar] = useState({
        color: "Red",
        Rate: 20000
    });

    const changeColor = () => {
        setCar((prevState) => {
            return { ...prevState, color: "Green" };
        });
    };

    return (
        <>
        <h1>The car is {car.color} color and rate: {car.Rate}</h1>
        <button onClick={changeColor}>Change color</button>
        </>
    );
}
```

---

## 🔁 State in Class Components

### 🏍️ Example: Bike Component (Object State)

```jsx
import React from "react";

class Bike extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            color: "Red",
            Rate: 10000
        };
    }

    changeColor = () => {
        this.setState((prevState) => {
            return { ...prevState, color: "Green" };
        });
    }

    render(){
        return (
            <>
            <h1>The Bike is {this.state.color} color and rate: {this.state.Rate}</h1>
            <button onClick={this.changeColor}>Change color</button>
            </>
        );
    }
}
```

---

## 📋 State with Arrays (CRUD Example)

### 🧾 List Component - Functional Style

```jsx
import { useState } from "react";

function List(){
    const [items, setItems] = useState([]);
    const [count, setCount] = useState(1);

    const addItem = () => {
        let newItem = "Item: " + count;
        setItems((prev) => [...prev, newItem]);
        setCount((prev) => prev + 1);
    };

    const removeItem = (index) => {
        setItems((prev) => prev.filter((_, i) => i !== index));
    };

    const updateItem = (index) => {
        setItems((prev) =>
            prev.map((item, i) => (i === index ? item + " (Updated)" : item))
        );
    };

    return (
        <>
        <ul>
            {items.map((item, index) => (
                <li key={index}>
                    {item} &nbsp;
                    <button onClick={() => updateItem(index)}>Update</button> &nbsp;
                    <button onClick={() => removeItem(index)}>Remove</button>
                </li>
            ))}
        </ul>
        <button onClick={addItem}>Add Item</button>
        </>
    );
}
```

---

## 📝 Summary

|Concept|Functional Component|Class Component|
|---|---|---|
|Initial State|`useState(initialValue)`|`this.state = {}`|
|Update State|`setState(value)`|`this.setState()`|
|Re-render|Automatic after state change|Automatic after state change|

---