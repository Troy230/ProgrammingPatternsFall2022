# 1. Database Connection

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.*;

/**
 *
 * @author cstuser
 */
public class MyProject {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) throws SQLException {
        String url = "jdbc:mysql://localhost:3306/university";
        String uname = "root";
        String password = "1234";
        String query = "Select * from student";

        try {
            Connection con = DriverManager.getConnection(url, uname, password);
            Statement statement = con.createStatement();
            ResultSet result = statement.executeQuery(query);
            ResultSetMetaData resultMD = result.getMetaData();

            while(result.next()) {
                String universityData = "";

                for(int i = 1; i <= resultMD.getColumnCount(); i++) {
                    universityData += result.getString(i) + " : ";
                }

                System.out.println(universityData);
            }

        } catch(SQLException e) {
            e.printStackTrace();
        }
    }

}
```
