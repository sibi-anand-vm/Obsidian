#### 1.Fetch a record
```java
package org.example;  
  
import org.hibernate.Session;  
import org.hibernate.SessionFactory;  
import org.hibernate.cfg.Configuration;  
  
public class Main {  
    public static void main(String[] args) {  
        // Build SessionFactory  
        SessionFactory sf = new Configuration()  
                .configure("hibernate.cfg.xml")  
                .addAnnotatedClass(Student.class)  
                .buildSessionFactory();  
  
        // Open session  
        Session ss = sf.openSession();  
  
        // Fetch student with primary key = 1  
        Student s1 = ss.find(Student.class, 1);  
  
        if (s1 != null) {  
            System.out.println("✅ Student Found: " +  
                    "ID=" + s1.getAid() +  
                    ", Name=" + s1.getAname() +  
                    ", Tech=" + s1.getTech());  
        } else {  
            System.out.println("⚠️ No student found with ID=1");  
        }  
  
        // Close resources  
        ss.close();  
        sf.close();  
    }  
}
```

#### 2.Create or Insert a record

## 🔎 How `merge()` Works in Hibernate

- **`persist()`** → Always treats the object as **new** and inserts it.
- **`update()`** → Assumes the object already exists in DB. If not, it may fail.
- **`merge()`** → Smart one:
    - If a row with the same **primary key** exists → it **updates** that row.
    - If not → it **inserts** a new row.
```java
Student s1 = new Student();
s1.setAid(4);              // PK = 4
s1.setAname("User4");
s1.setTech("ML");

SessionFactory sf = new Configuration()
        .configure("hibernate.cfg.xml")
        .addAnnotatedClass(Student.class)
        .buildSessionFactory();

Session ss = sf.openSession();
Transaction transaction = ss.beginTransaction();

ss.merge(s1);   // Will INSERT if id=4 does not exist, UPDATE if it exists
transaction.commit();

ss.close();
sf.close();

```

## 🔧 Behind the Scenes

1. Hibernate checks if a row with `aid=4` exists in DB.
    - If **not found** → runs an `INSERT INTO student ...`.
    - If **found** → runs an `UPDATE student SET ... WHERE aid=4`.

So in your case (new id=4), it will **insert a new record**.

#### 3.Remove a record

```java
Session ss = sf.openSession();
Transaction tx = ss.beginTransaction();

Student s1 = ss.get(Student.class, 4);  // fetch managed entity
if (s1 != null) {
    ss.remove(s1);                      // delete record from DB
}

tx.commit();
ss.close();

```

This will run:
```sql
DELETE FROM student WHERE aid = 4;
```