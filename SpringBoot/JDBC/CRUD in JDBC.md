```java
package org.example;

import java.sql.*;

public class Main {
    public static void main(String[] args) {
        // Database credentials
        String url = "jdbc:postgresql://localhost:5432/demo";
        String username = "jack";
        String password = "ACCESS_LOCk42";

        // Queries (for different operations)
        String selectQuery = "SELECT sname FROM student WHERE sid=4";
        String insertQuery = "INSERT INTO student VALUES(4,'InsertedUser4',8.0)";
        String updateQuery = "UPDATE student SET sname='UpdatedUser' WHERE sid=3";
        String deleteQuery = "DELETE FROM student WHERE sid=2";

        try {
            // Step 1: Establish connection
            Connection conn = DriverManager.getConnection(url, username, password);
            System.out.println("✅ Connection established");

            // Step 2: Create statement
            Statement st = conn.createStatement();

            // ------------------------------
            // Example 1: INSERT
            // ------------------------------
            int insertCount = st.executeUpdate(insertQuery);
            System.out.println("Rows inserted: " + insertCount);

            // ------------------------------
            // Example 2: UPDATE
            // ------------------------------
            int updateCount = st.executeUpdate(updateQuery);
            System.out.println("Rows updated: " + updateCount);

            // ------------------------------
            // Example 3: DELETE
            // ------------------------------
            int deleteCount = st.executeUpdate(deleteQuery);
            System.out.println("Rows deleted: " + deleteCount);

            // ------------------------------
            // Example 4: SELECT
            // ------------------------------
            ResultSet rs = st.executeQuery(selectQuery);
            while (rs.next()) {
                String sname = rs.getString("sname");
                System.out.println("Student name: " + sname);
            }

            // Step 3: Close connection
            conn.close();
            System.out.println("❌ Connection closed");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```