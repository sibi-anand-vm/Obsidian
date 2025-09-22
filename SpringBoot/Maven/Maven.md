# 📒 Maven Notes

## 🔹 What is Maven?
- **Maven** = Project Management + Build Automation Tool (mainly for Java).  
- Helps standardize project structure and builds.  

---

## 🔹 Core Features
- **Compile** Java source code  
- **Run** applications  
- **Test** (JUnit, TestNG)  
- **Package** into JAR/WAR/EAR  
- **Deploy** to servers or repositories  

---

## 🔹 Dependency Management
- No need to manually download JARs ✅  
- Declare dependencies inside `pom.xml`.  
- Maven will:  
  - Download libraries automatically from **Maven Central Repository**  
  - Handle **transitive dependencies** (dependencies of dependencies)  
  - Keep builds reproducible & clean  

---

## 🔹 Project Structure (Convention over Configuration)
my-maven-app/  
│── pom.xml # Project Object Model file  
└── src/  
├── main/java/ # Application source  
└── test/java/ # Unit tests
