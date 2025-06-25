## Basics of C Programming

### ✅ 1.1 Structure of a C Program
```
#include <stdio.h>      // Preprocessor Directive  
int main() {            // Main function - Entry point     
printf("Hello, World!\n");   // Output     
return 0;           // Exit code }
```


### 🧩 Parts Breakdown:

- `#include <stdio.h>` → Includes the Standard Input Output library.
    
- `int main()` → The execution starts from here.
    
- `printf()` → Used to display output.
    
- `return 0;` → Ends the program, returning 0 to OS.
    

---

### ✅ 1.2 Compilation & Execution

#### If you're using **Linux**:

```
gcc hello.c -o hello   # Compile 
./hello                # Run
```

#### If you're using **Windows** (with CodeBlocks or Turbo C):

- Write code in `.c` file
    
- Build and Run using the IDE buttons
---

### ✅ 1.3 Data Types and Variables

|Type|Keyword|Size (32-bit)|Example|
|---|---|---|---|
|Integer|`int`|4 bytes|`int age = 21;`|
|Decimal|`float`|4 bytes|`float temp = 98.6;`|
|Large Decimal|`double`|8 bytes|`double pi = 3.14159;`|
|Character|`char`|1 byte|`char grade = 'A';`|

---

### ✅ 1.4 Input/Output

```
#include <stdio.h>  
int main() {     
int age;     
printf("Enter your age: ");     
scanf("%d", &age);         // Input     
printf("You are %d years old.\n", age); // Output     
return 0; 
}
```

---

### ✅ 1.5 Operators in C

|Operator Type|Examples|
|---|---|
|Arithmetic|`+`, `-`, `*`, `/`, `%`|
|Relational|`==`, `!=`, `<`, `>`, `<=`|
|Logical|`&&`, `|
|Assignment|`=`, `+=`, `-=`, `*=`, `/=`|
|Bitwise|`&`, `|