### ✅ Hibernate Tutorial (Step by Step)

#### **S1: Create Maven Project**

- Create a new Maven project in your IDE (IntelliJ, Eclipse, etc.).

#### **S2: Add Dependencies in `pom.xml`**

Add PostgreSQL JDBC and Hibernate Core

#### S3: Create `Student` Class
```java
package org.example;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Student {
    @Id
    private int aid;
    private String aname;
    private String tech;

    // Getters and Setters
    public int getAid() {
        return aid;
    }
    public void setAid(int aid) {
        this.aid = aid;
    }
    public String getAname() {
        return aname;
    }
    public void setAname(String aname) {
        this.aname = aname;
    }
    public String getTech() {
        return tech;
    }
    public void setTech(String tech) {
        this.tech = tech;
    }
}

```

#### S4.Setting Hibernate config
```xml
<hibernate-configuration xmlns="http://www.hibernate.org/xsd/orm/cfg">  
    <session-factory>        <property name="hibernate.connection.driver_class">org.postgresql.Driver</property>  
        <property name="hibernate.connection.url">jdbc:postgresql://localhost:5432/demo</property>  
        <property name="hibernate.connection.username">jack</property>  
        <property name="hibernate.connection.password">ACCESS_LOCk42</property>  
  
        <property name="hibernate.hbm2ddl.auto">create</property>  
        <property name="hibernate.show_sql">true</property>
    </session-factory></hibernate-configuration>
```

### 🔎 What this config does

- **`hibernate.connection.driver_class`** → Loads PostgreSQL JDBC driver.
- **`hibernate.connection.url`** → Connects to your `demo` database.
- **`hibernate.connection.username/password`** → Credentials (`jack / ACCESS_LOCk42`).
- **`hibernate.hbm2ddl.auto = create`** → Drops and recreates the schema every time you run (⚠️ data will be lost each run).
- `hibernate.show_sql` → Prints executed SQL in console (good for debugging).

#### **S5 → Write main application to save a record
```java
package org.example;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.setAid(1);
        s1.setAname("User1");
        s1.setTech("Java");

        // Load config & annotated class
        Configuration config = new Configuration()
                .configure("hibernate.cfg.xml")
                .addAnnotatedClass(Student.class);

        SessionFactory sf = config.buildSessionFactory();
        Session ss = sf.openSession();

        Transaction trans = ss.beginTransaction();
        ss.persist(s1);   // Insert student into DB
        trans.commit();

        ss.close();
        sf.close();

        System.out.println("✅ Student saved successfully!");
    }
}

```
Always make sure to close the session and factory.