# Maven POM & Dependencies (Short Version)

- **POM (Project Object Model)**: `pom.xml` file that defines your project, dependencies, plugins, and build info.
    
- **Dependencies**: External libraries your project needs. Maven downloads them automatically.
    

**Basic POM Structure:**

```xml
<project>     
<modelVersion>4.0.0</modelVersion>     
<groupId>com.example</groupId>     
<artifactId>my-app</artifactId>     
<version>1.0.0</version>      
<dependencies>         
	<dependency>             
	<groupId>junit</groupId>             
	<artifactId>junit</artifactId>             
	<version>4.13.2</version>             
	<scope>test</scope>        
	</dependency>     
</dependencies> 
</project>
```

# How to Get Dependencies from Maven Repository

1. **Go to Maven Central:**  
    https://search.maven.org/
    
2. **Search for the library** you need (e.g., `jackson-databind`).
    
3. **Select the version** you want to use.
    
4. **Copy the dependency snippet**.
5. Example:
```xml
<dependency>     
<groupId>com.fasterxml.jackson.core</groupId>     
<artifactId>jackson-databind</artifactId>     
<version>2.15.0</version> 
</dependency>
```

6. **Paste it inside `<dependencies>`** in your `pom.xml`.
    
```xml
<dependencies>    
 <!-- Your copied dependency here --> 
 </dependencies>
 ```

7. **Reload and Maven will auto-download the JARs** and include any **transitive dependencies**.