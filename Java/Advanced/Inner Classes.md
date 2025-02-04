### **Inner Class**

An inner class is a class defined within another class. It helps logically group classes that are only used in one place.

```
class Outer {
    class Inner {
        void display() {
            System.out.println("Inside Inner Class");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer.Inner obj = new Outer().new Inner();
        obj.display();
    }
}
```
### ==**Anonymous Inner Class**==

An anonymous inner class is a class without a name, typically used to provide a concrete implementation of an abstract class or interface.

**Example**:
```
abstract class A {
    abstract void display();
}

public class Main {
    public static void main(String[] args) {
        A obj = new A() {
            void display() {
                System.out.println("Anonymous Inner Class Implementation");
            }
        };
        obj.display();
    }
}
```