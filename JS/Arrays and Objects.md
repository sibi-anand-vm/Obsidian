## **Arrays in JavaScript**

**Definition**: Arrays are ordered collections of values.  
They store multiple items under a single variable name, and the values are accessed using **index numbers** (starting at 0).

### **Example:**

```
let fruits = ["apple", "banana", "cherry"]; 
console.log(fruits[0]); // "apple"
```

### **Common Array Methods:**

1. **`forEach()`** – Executes a function for each item.
    
```
fruits.forEach(fruit => console.log(fruit));
```
    
2. **`map()`** – Creates a new array by transforming each item.

```
const upperFruits = fruits.map(f => f.toUpperCase());
```
    
3. **`filter()`** – Returns a new array with items that match a condition.
    
```
const longFruits = fruits.filter(f => f.length > 5);
```
    
4. **`find()`** – Returns the first item that satisfies a condition.
```
const cherry = fruits.find(f => f === "cherry");
```
    
5. **`reduce()`** – Reduces the array to a single value (used for sum, etc.).
    
```
const numbers = [1, 2, 3]; const sum = numbers.reduce((a, b) => a + b, 0); // 6
```
    

---

## **Objects in JavaScript**

**Definition**: Objects store data in **key-value** pairs.  
They're used to group related data and functions.

### **Example:**

```
const person = {   name: "Captain",   age: 22,   city: "Coimbatore" }; console.log(person.name); // "Captain"
```

### **Common Object Methods:**

1. **`Object.keys(obj)`** – Returns an array of the object’s keys.

```
Object.keys(person); // ["name", "age", "city"]
```

2. **`Object.values(obj)`** – Returns an array of the object’s values.

```
Object.values(person); // ["Captain", 22, "Coimbatore"]
```
    
3. **`Object.entries(obj)`** – Returns an array of `[key, value]` pairs.

```
Object.entries(person); // [["name", "Captain"], ["age", 22], ["city", "Coimbatore"]]
```
    

---

### **Object.freeze(obj)**

- Prevents **adding**, **removing**, or **changing** properties.
    
- Object becomes **completely immutable**.

```
Object.freeze(person); person.name = "Someone"; // No effect
```

### **Object.seal(obj)**

- Prevents **adding or removing** properties.
    
- Allows **changing existing values**.

```
Object.seal(person); 
person.city = "Chennai"; // Works 
delete person.name;      // Doesn't work
```