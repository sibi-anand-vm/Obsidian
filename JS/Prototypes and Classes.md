## **Prototypes in JavaScript**

**Definition**: Every JavaScript object has a hidden internal property called `[[Prototype]]` (or `__proto__` in older syntax), which points to another object. This is the foundation of **prototypal inheritance**.

### **Why Use Prototypes?**

They allow objects to share properties and methods, saving memory and supporting inheritance.

### **Example:**

```
const person = {   
greet() {    
console.log("Hello!");   
	} 
};  
const student = {   
name: "Captain" 
};  
// Link `student` to `person` via prototype

student.__proto__ = person;  
student.greet(); // "Hello!" - inherited from person
```

> **Note:** Modern JavaScript prefers `Object.setPrototypeOf()` or `Object.create()` instead of directly using `__proto__`.

---

## **Classes in JavaScript**

**Definition**: Classes are syntactic sugar over JavaScript's prototypal inheritance. They make object creation and inheritance more readable and structured, similar to other OOP languages.

### **Structure:**

- `class` keyword defines a class.
    
- `constructor()` is used to initialize object properties.
    
- Methods are added inside the class body.
    

### **Example:**
```
class Person {   
constructor(name, age) {     
this.name = name;     
this.age = age;   
}    
greet() {     
console.log(`Hi, I'm ${this.name}`);   
} 
}  
// Creating an object (instance) from the class 
const captain = new Person("Captain", 22); 
captain.greet(); // "Hi, I'm Captain"
```

### Key Points:

- `constructor()` runs when you create an instance.
    
- No `return` needed in the constructor.
    
- Methods inside the class are placed on the prototype (not duplicated per instance).
    

---