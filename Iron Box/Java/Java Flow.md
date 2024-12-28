# <mark style="background: #FF5582A6;">JVM</mark>
<span style="color:rgb(255, 0, 0)"></span>1.**Write Code**: Create a file named `hello.java` with your Java code. Ensure it includes `public static void main(String[] args)` as the entry point.

2.**Compile**: Use `javac hello.java` to compile the source code. This generates `hello.class`, a bytecode file.

3.**Run**: Use `java hello` to execute the bytecode. The JVM processes the bytecode and produces the output.

4.**JVM Role**: The JVM ensures platform independence, interpreting the bytecode and running it on any OS.

5.**Entry Point**: The JVM identifies the class with the `main` method as the starting point for execution.
![[Pasted image 20241225113407.png]]
# <mark style="background: #FF5582A6;">JRE</mark>
1. **JRE (Java Runtime Environment)**:
    - Includes the **JVM (Java Virtual Machine)** and **external libraries**.
    - Provides the runtime environment needed to execute Java applications.

2. **JVM's Role**:
    - Handles bytecode execution and retrieves required libraries from the JRE when the application needs them.
    - Ensures platform independence by interpreting bytecode for the underlying OS.

3. **JDK (Java Development Kit)**:
    - Contains the JRE and development tools like `javac` for compiling Java programs.

4. **Distribution**:
    - To run a Java application on another system (like a friend's laptop), only the **JRE and JVM** are required, not the full JDK.
 
5. **WORA (Write Once, Run Anywhere)**:
    - Java’s OS-independent nature stems from its use of the JVM, enabling applications to run seamlessly across platforms.
    ![[Screenshot from 2024-12-25 11-48-00.png]]

