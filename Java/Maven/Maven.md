Maven is a **build automation and project management tool** for Java projects. It simplifies project management by providing a standardized way to build, test, package, and deploy applications. It is widely used in Java development for handling dependencies, compiling code, running tests, and generating documentation.

### **Key Features of Maven**:

1. **Dependency Management** – Automatically downloads and manages libraries (JAR files) from the central repository.
2. **Build Automation** – Compiles, tests, packages, and deploys Java projects with a single command (`mvn clean install`).
3. **Standardized Project Structure** – Follows a convention-over-configuration approach with a predefined directory layout.
4. **Plugins and Extensibility** – Supports various plugins for testing, reporting, and deploying applications.
5. **Multi-Module Project Support** – Helps in managing large projects with multiple sub-projects.
6. **Integration with CI/CD** – Works well with Jenkins, GitHub Actions, and other DevOps tools.

### **Basic Maven Commands**:

- `mvn clean` – Deletes all compiled files and the target directory.
- `mvn compile` – Compiles the source code.
- `mvn test` – Runs unit tests.
- `mvn package` – Creates a JAR or WAR file.
- `mvn install` – Installs the package in the local repository.
- `mvn deploy` – Uploads the artifact to a remote repository.
### **Maven `pom.xml` (Project Object Model)**:

The `pom.xml` file is the heart of a Maven project. It defines dependencies, plugins, and configurations.
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <dependencies>
        <!-- Example: Adding JUnit for testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

```

**Maven** is a build automation and dependency management tool for Java. It uses a configuration file called **`pom.xml`** (**Project Object Model**) to manage dependencies. By adding dependencies to this file, Maven automatically downloads the required **JAR files** from the internet, making project setup easier. However, **Maven does not install Java itself**—you still need to have the **JDK installed**.