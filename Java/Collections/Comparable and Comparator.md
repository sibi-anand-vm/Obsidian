In Java, both [Comparable](https://www.geeksforgeeks.org/comparable-interface-in-java-with-examples/) and [Comparator](https://www.geeksforgeeks.org/comparator-interface-java/) are used for sorting objects. The main difference between Comparable and Comparator is:

- ****Comparable:**** It is used to define the ****natural ordering of the objects**** within the class.
- ****Comparator****: It is used to define ****custom sorting logic**** externally.
![[Pasted image 20241230224409.png]]
**Sample Code:**
```
import java.util.*;

class Student implements Comparable<Student> {
    private String name;
    private int age;
    private int marks;

    // Constructor
    public Student(String name, int age, int marks) {
        this.name = name;
        this.age = age;
        this.marks = marks;
    }

    // Getters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public int getMarks() {
        return marks;
    }

    // Comparable: Default sorting by marks
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.marks, other.marks);
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + ", marks=" + marks + "}";
    }
}

public class ComparableComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 20, 85));
        students.add(new Student("Bob", 22, 75));
        students.add(new Student("Charlie", 19, 95));

        // Using Comparable: Sort by marks (default)
        Collections.sort(students);
        System.out.println("Sorted by marks (Comparable):");
        for (Student s : students) {
            System.out.println(s);
        }

        // Using Comparator: Sort by name
        Comparator<Student> com= (o1, o2) -> {  
           if (o1.getAge()> o2.getAge())  
return 1;  
           else return -1;  
       };  
        Collections.sort(students,com);  
        System.out.println("\nSorted by age (Comparator):");  
        for (Student s : students) {  
            System.out.println(s);  
        }
    }
}

```