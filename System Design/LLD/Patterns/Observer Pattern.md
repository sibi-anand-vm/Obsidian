# 👀 Observer Pattern — Overview

## 🎯 Goal
Define a **one-to-many dependency** between objects so that when one object changes state, **all its dependents are notified automatically**.

---

## 🔹 Why Use Observer
- When one object’s change must **update many other objects**.  
- Loose coupling: Subject doesn’t need to know details of observers.

---

## 🧱 Example
```java
// Observer interface
interface Observer {
    void update(String message);
}

// Concrete observers
class User implements Observer {
    private String name;
    public User(String name) { this.name = name; }
    public void update(String message) {
        System.out.println(name + " received: " + message);
    }
}

// Subject
class NewsPublisher {
    private List<Observer> users = new ArrayList<>();

    public void addObserver(Observer o) { users.add(o); }
    public void removeObserver(Observer o) { users.remove(o); }

    public void notifyObservers(String news) {
        for(Observer o : users) o.update(news);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        NewsPublisher publisher = new NewsPublisher();

        User alice = new User("Alice");
        User bob = new User("Bob");

        publisher.addObserver(alice);
        publisher.addObserver(bob);

        publisher.notifyObservers("New article published!");
    }
}
```

✅ Output:  
```
Alice received: New article published!
Bob received: New article published!
```

---

## ⚙️ Summary
| Feature   | Observer Pattern                           |
| --------- | ------------------------------------------ |
| Purpose   | Notify many dependents automatically       |
| Coupling  | Loose between subject and observers        |
| Use cases | Event systems, GUI updates, messaging apps |
