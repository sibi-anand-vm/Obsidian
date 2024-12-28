Encapsulation is all about hiding the internal state of an object and only allowing controlled access through public methods, typically getters and setters. It ensures data integrity and provides better modularity.
## ==this keyword==
The `this` keyword is indeed crucial for distinguishing between instance variables and local variables with the same name. It ensures clarity and avoids conflicts in your code.

```
class Student {
    // Private variables for encapsulation
    private int rollNumber;
    private int marks;

    // Setter methods using 'this' keyword
    public void setRollNumber(int rollNumber) {
        this.rollNumber = rollNumber; // 'this' refers to the instance variable
    }

    public void setMarks(int marks) {
        this.marks = marks; // 'this' refers to the instance variable
    }

    // Getter methods
    public int getRollNumber() {
        return rollNumber;
    }

    public int getMarks() {
        return marks;
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an object of the Student class
        Student student = new Student();

        // Set values using setter methods
        student.setRollNumber(101);
        student.setMarks(95);

        // Get and display values using getter methods
        System.out.println("Roll Number: " + student.getRollNumber());
        System.out.println("Marks: " + student.getMarks());
    }
}

```
### Explanation:

1. The `rollNumber` and `marks` variables in the `Student` class are private to enforce encapsulation.
2. The `setRollNumber` and `setMarks` methods use the `this` keyword to assign values to instance variables, differentiating them from the local parameters.
3. The `getRollNumber` and `getMarks` methods allow controlled access to the private variables.
4. The `Main` class creates a `Student` object, sets the values using the setter methods, and retrieves the values using the getter methods.