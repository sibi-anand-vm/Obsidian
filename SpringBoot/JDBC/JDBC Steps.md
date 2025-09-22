The standard steps in JDBC are: **Import packages**, **load/register driver**, create a connection, create a statement, execute SQL, and close resources, with modern JDBC auto-loading drivers from the classpath since JDBC 4.0.[geeksforgeeks+2](https://www.geeksforgeeks.org/java/establishing-jdbc-connection-in-java/)

## Typical steps

- Import JDBC packages such as java.sql to access Connection, Statement, ResultSet, and DriverManager classes.[tutorialspoint](https://www.tutorialspoint.com/jdbc/jdbc-db-connections.htm)
    
- Load or register the JDBC driver (Class.forName or DriverManager.registerDriver), though JDBC 4.0+ drivers auto-load when present on the classpath.[geeksforgeeks+1](https://www.geeksforgeeks.org/java/establishing-jdbc-connection-in-java/)
    
- Create a database Connection using DriverManager.getConnection(url, user, password).[oracle+1](https://docs.oracle.com/cd/A97335_01/apps.102/a83724/basic1.htm)
    
- Create a Statement or, preferably, PreparedStatement/CallableStatement from the connection.[geeksforgeeks](https://www.geeksforgeeks.org/java/establishing-jdbc-connection-in-java/)
    
- Execute SQL: use executeQuery for SELECT returning a ResultSet; use executeUpdate for INSERT/UPDATE/DELETE/DDL.[jyotiprakash](https://blog.jyotiprakash.org/introduction-to-jdbc)
    
- Close ResultSet, Statement, and Connection in finally/try-with-resources to release DB resources.

**Java Code for JDBC**
```java
package org.example;  
import java.sql.*;  
public class Main {  
    public static void main(String[] args) throws Exception {  
	    String url="jdbc:postgresql://localhost:5432/demo";  
	    String username="jack";  
	    String password="ACCESS_LOCk42";  
  
	    String selectQuery="select sname from student where sid=4";  
	    Connection conn=DriverManager.getConnection(url,username,password);  
	    System.out.println("Connection established");  
  
	    System.out.println("Connection closed");  
    }  
}
```