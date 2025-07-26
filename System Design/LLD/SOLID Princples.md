The **SOLID principles** are a set of five object-oriented design principles that help developers create software that is easy to maintain, extend, and scale. These principles are especially important in **OOP (Object-Oriented Programming)** and are widely used in designing **robust backend systems**.

## 🔹 1. **Single Responsibility Principle (SRP)**

> A class should have **only one reason to change** — one responsibility.

### ❌ Bad Example:

```
class UserManager {    
public void createUser(String name) {         
// logic to create user     
}     
public void saveToDatabase(String user) {        
// logic to save user    
}    
public void sendEmail(String user) {        
// logic to send welcome email   
}
}
```

This class handles **user creation**, **DB storage**, and **emailing** — 3 responsibilities.

---

### ✅ Good Example (Apply SRP):


```
class UserService {  
public void createUser(String name) {      
// logic to create user    
} 
}  
class UserRepository {    
public void saveToDatabase(String user) {      
// only DB logic     }
} 
class EmailService {     
public void sendEmail(String user) {        
// only email logic    
}
}
```

Each class has one reason to change — **SRP followed**.

---

## 🔹 2. **Open/Closed Principle (OCP)**

> Open for extension, closed for modification.

### ❌ Bad Example:

```class AreaCalculator {    
public double calculateArea(Object shape) {         
if (shape instanceof Circle) {          
Circle c = (Circle) shape;
return Math.PI * c.radius * c.radius;       
} else if (shape instanceof Rectangle) {  
Rectangle r = (Rectangle) shape;      
return r.length * r.breadth;      
}         
return 0;    
} 
}
```

To add new shapes, you must **modify** the `AreaCalculator` — violates OCP.

---

### ✅ Good Example (Apply OCP):

```
interface Shape 
{     
double area(); 
}  
class Circle implements Shape {     
double radius;     
Circle(double r)
{ this.radius = r; }     
public double area() {         
return Math.PI * radius * radius;    
} 
}  
class Rectangle implements Shape {     
double length, breadth;     
Rectangle(double l, double b) { 
this.length = l; 
this.breadth = b; 
}      
public double area() {   
return length * breadth;   
} 
}  
class AreaCalculator {   
public double calculateArea(Shape shape) 
{         
return shape.area(); 
// Extension without modification    
} }
```

Now you can add `Triangle`, `Square`, etc., without changing `AreaCalculator`.

---

## 🔹 3. **Liskov Substitution Principle (LSP)**

> Subtypes should be replaceable for their base types.

### ❌ Bad Example:


```
class Bird {   
public void fly() {       
System.out.println("Bird is flying");    
}
}  
class Ostrich extends Bird {   
@Override     
public void fly() 
{         
throw new UnsupportedOperationException("Ostrich can't fly");    
}
}
```

An `Ostrich` is a `Bird`, but it **can’t fly**, breaking substitution.

---

### ✅ Good Example (Apply LSP):

```interface Bird {} 
interface FlyingBird extends Bird {    
void fly(); 
} 
class Parrot implements FlyingBird {     
public void fly()
{        
System.out.println("Parrot is flying");    
}
}  
class Ostrich implements Bird {   
// Ostrich doesn't implement fly
}
```

Now `Ostrich` and `Parrot` can be safely used in their own contexts.

---

## 🔹 4. **Interface Segregation Principle (ISP)**

> Don’t force a class to implement methods it doesn't use.

### ❌ Bad Example:


```
interface MultiFunctionMachine {    
void print();    
void scan();    
void fax();
} 
class OldPrinter implements MultiFunctionMachine {    
public void print() 
{ /* ok */ }   
public void scan()
{ throw new UnsupportedOperationException(); }    
public void fax() 
{ throw new UnsupportedOperationException(); } }
```

`OldPrinter` is forced to implement `scan` and `fax` unnecessarily.

---

### ✅ Good Example (Apply ISP):


```
interface Printer 
{     void print(); } 
interface Scanner {    
void scan(); }  
class OldPrinter implements Printer {   
public void print() {      
System.out.println("Printing...");    
}
}
```

Now each class implements **only what it needs**.

---

## 🔹 5. **Dependency Inversion Principle (DIP)**

> High-level modules should depend on abstractions, not concrete classes.

### ❌ Bad Example:

```
class MySQLDatabase {    
public void connect() {       
System.out.println("Connected to MySQL");    
} 
}  
class App {   
MySQLDatabase db = new MySQLDatabase();  // Tightly coupled      
void start() {      
db.connect();    
}
}
```

Now, changing the DB type requires changing the `App` class.

---

### ✅ Good Example (Apply DIP):

java

CopyEdit

```
interface Database {   
void connect(); 
}  
class MySQLDatabase implements Database {    
public void connect() {       
System.out.println("Connected to MySQL");   
}
}  
class App {    
private Database db;  
App(Database db) {   
this.db = db;    
} 
void start() {     
db.connect(); 
// Works with any DB implementing Database  
}
}
```
Now you can pass a `PostgreSQLDatabase`, `MongoDB`, etc., easily.

---

## 🧠 Final Recap Table:

|Principle|Real-life analogy|
|---|---|
|SRP|One person, one job|
|OCP|Add new plugins without changing the engine|
|LSP|Replace one part with another of the same type|
|ISP|Only teach relevant skills to the role|
|DIP|Use adaptors/interfaces, not hard-wired connections|

---