# 🏛️ Facade Pattern — Overview

## 🎯 Goal
Provide a **simplified interface** to a **complex subsystem**.  
Hides the complexity of multiple classes and makes the system easier to use.

---

## 🔹 Why Use Facade
- When a system has **many classes** that clients must interact with.  
- You want to **reduce dependencies** and simplify the interface.  
- Makes client code cleaner and easier to maintain.

---

## 🧱 Example
```java

class CPU {
    void start() { System.out.println("CPU started"); }
}
class Memory {
    void load() { System.out.println("Memory loaded"); }
}
class HardDrive {
    void read() { System.out.println("Hard drive read"); }
}

class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    private HardDrive hd;

    public ComputerFacade() {
        cpu = new CPU();
        memory = new Memory();
        hd = new HardDrive();
    }

    public void startComputer() {
        cpu.start();
        memory.load();
        hd.read();
        System.out.println("Computer started successfully!");
    }
}

public class Main {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.startComputer();
    }
}
```

---

## ⚙️ Summary
| Feature | Facade Pattern |
|---------|----------------|
| Purpose | Simplify complex subsystem interface |
| Client code | Only interacts with Facade |
| Use cases | APIs, library wrappers, system startup |

---
