# 🧱 Builder Pattern — Overview

## 🎯 Goal
Construct **complex objects step by step**, allowing flexible configuration of optional parameters.

---

## 🔹 Why Use Builder
- When object creation has **many optional parameters**.  
- Avoids “telescoping constructors” (constructors with too many parameters).  
- Makes object creation readable and flexible.

---

## 🧱 Example
```java
class Computer {
    private String CPU;  // required
    private String GPU;  // optional
    private int RAM;     // optional

    private Computer(Builder builder) {
        this.CPU = builder.CPU;
        this.GPU = builder.GPU;
        this.RAM = builder.RAM;
    }

    public static class Builder {
        private String CPU;
        private String GPU;
        private int RAM;

        public Builder(String CPU) {
            this.CPU = CPU;
        }

        public Builder setGPU(String GPU) {
            this.GPU = GPU;
            return this;
        }

        public Builder setRAM(int RAM) {
            this.RAM = RAM;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }
    }

    public String toString() {
        return "Computer[CPU=" + CPU + ", GPU=" + GPU + ", RAM=" + RAM + "]";
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Computer pc = new Computer.Builder("Intel i9")
                .setGPU("NVIDIA RTX 4070")
                .setRAM(32)
                .build();

        System.out.println(pc);
    }
}
```

---

## ⚙️ Summary
| Feature | Builder Pattern |
|---------|----------------|
| Purpose | Step-by-step construction of complex objects |
| Flexible | Yes, optional parameters handled elegantly |
| Example | Computer, Car, GUI components |
