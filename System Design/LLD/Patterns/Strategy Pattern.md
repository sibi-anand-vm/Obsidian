# ⚔️ Strategy Pattern — Overview

## 🎯 Goal
Define a family of algorithms, encapsulate each one, and make them interchangeable.  
Strategy lets the algorithm vary independently from clients that use it.

---

## 🔹 Why Use Strategy
- When you have **multiple ways to do something**.  
- You want to **switch algorithms at runtime** without changing client code.  
- Reduces `if-else` or `switch` statements scattered in the code.

---

## 🧱 Example
```java
// Strategy interface
interface PaymentStrategy {
    void pay(int amount);
}

// Concrete strategies
class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

// Context
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        cart.setPaymentStrategy(new CreditCardPayment());
        cart.checkout(500); // Paid 500 using Credit Card

        cart.setPaymentStrategy(new PayPalPayment());
        cart.checkout(300); // Paid 300 using PayPal
    }
}
```

---

## ⚙️ Summary
| Feature | Strategy Pattern |
|---------|----------------|
| Purpose | Make algorithms interchangeable |
| Client code | Can switch strategy at runtime |
| Use cases | Payment methods, sorting algorithms, compression algorithms |

---

# 👀 Observer Pattern — Overview

## 🎯 Goal
Define a **one-to-many dependency** between objects so that when one object changes state, **all its dependents are notified automatically**.

---

## 🔹 Why Use Observer
- When one object’s change must **update many other objects**.  
- Loose coupling: Subject doesn’t need to know details of observers.

---
