# Spring XML Dependency Injection – Age Example

---
## 1️⃣ Setter Injection

### Person.java

```java
package org.example;

public class Person {

    private int age;

    // Setter for XML injection
    public void setAge(int age) {
        this.age = age;
    }

    public void showAge() {
        System.out.println("Person age: " + age);
    }
}
```

### spring.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Person bean with setter injection -->
    <bean id="person" class="org.example.Person">
        <property name="age" value="25"/>
    </bean>
</beans>
```

### Main.java

```java
package org.example;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
        Person person = context.getBean(Person.class);
        person.showAge();
    }
}
```

**Output:**

```
Person age: 25
```

---

## 2️⃣ Constructor Injection

### Person.java

```java
package org.example;

public class Person {

    private int age;

    // Constructor for XML injection
    public Person(int age) {
        this.age = age;
    }

    public void showAge() {
        System.out.println("Person age: " + age);
    }
}
```

### spring.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Person bean with constructor injection -->
    <bean id="person" class="org.example.Person">
        <constructor-arg value="30"/>
    </bean>
</beans>
```

**Output:**

```
Person age: 30
```

---

### 🔑 Key Points

- Setter Injection: Requires a setter method, value injected after object creation.
    
- Constructor Injection: Injected at object creation, no setter required.
    
- Works for primitive types like `int age`.

# Spring XML Dependency Injection Notes

---
## 1️⃣ Setter Injection (XML)

### Developer.java

```java
package org.example;

public class Developer {

    private Laptop lap; // dependency

    // Setter required for XML injection
    public void setLap(Laptop lap) {
        this.lap = lap;
    }

    public void work() {
        lap.compile();
    }
}
```

### Laptop.java

```java
package org.example;

public class Laptop {
    public void compile() {
        System.out.println("Compiling from laptop");
    }
}
```

### spring.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Define Laptop bean -->
    <bean id="lap" class="org.example.Laptop"/>

    <!-- Developer bean with setter injection -->
    <bean id="dev" class="org.example.Developer">
        <property name="lap" ref="lap"/>
    </bean>
</beans>
```

### Main.java

```java
package org.example;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
        Developer dev = context.getBean(Developer.class);
        dev.work();
    }
}
```

**Output:**

```
Compiling from laptop
```

✅ Key Points:

- Requires **setter method** for XML `<property>` injection.
    
- Spring calls the setter to inject the dependency.
    

---

## 2️⃣ Constructor Injection (XML)

### Developer.java

```java
package org.example;

public class Developer {

    private Laptop lap; // dependency

    // Constructor for XML injection
    public Developer(Laptop lap) {
        this.lap = lap;
    }

    public void work() {
        lap.compile();
    }
}
```

### spring.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Laptop bean -->
    <bean id="lap" class="org.example.Laptop"/>

    <!-- Developer bean with constructor injection -->
    <bean id="dev" class="org.example.Developer">
        <constructor-arg ref="lap"/>
    </bean>
</beans>
```

**Output remains the same:**

```
Compiling from laptop
```

✅ Key Points:

- Uses **constructor** instead of setter.
    
- Ensures **dependency is injected at creation time**.
    
- No setter method is required.
    

---

## 🔑 Summary Table

|Injection Type|XML Tag Used|Key Feature|
|---|---|---|
|Setter Injection|`<property name="..."/>`|Requires setter, optional deps|
|Constructor Injection|`<constructor-arg ref="..."/>`|Injects during object creation, mandatory deps|