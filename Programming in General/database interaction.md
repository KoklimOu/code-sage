 - Relational Databases: Structured into tables with predefined schemas, uses SQL for operations. Examples include MySQL and PostgreSQL.
 - Non-Relational Databases (NoSQL): Includes various data models (document, key-value, graph, etc.), typically more flexible and scalable. Examples include MongoDB and Redis.
 - SQL: Language used for managing and querying relational databases.
 - NoSQL: A broad category of database technologies that are not solely reliant on SQL and offer flexible schema and scalability options.

### Techniques for Interacting with Databases

1. **ORM (Object-Relational Mapping)**
   - **Description:** Maps application objects to database tables in a relational database.
   - **Purpose:** Simplifies data manipulation by abstracting SQL queries into method calls.
   - **Example Libraries:** Hibernate, JPA (Java Persistence API), Entity Framework.

2. **ODM (Object-Document Mapping)**
   - **Description:** Maps application objects to documents in a document-oriented NoSQL database.
   - **Purpose:** Provides an abstraction for working with documents in a schema-less or flexible schema environment.
   - **Example Libraries:** Mongoose (for MongoDB), Morphia (for MongoDB), Spring Data MongoDB.

3. **Direct SQL**
   - **Description:** Directly writing and executing SQL queries using database-specific drivers.
   - **Purpose:** Provides complete control over database interactions and optimizations.
   - **Example Tools:** JDBC (Java Database Connectivity), ADO.NET (for .NET).

4. **Query Builders**
   - **Description:** Provide a programmatic way to construct SQL queries using a fluent API.
   - **Purpose:** Simplifies dynamic query generation while avoiding raw SQL.
   - **Example Libraries:** jOOQ (Java), QueryDSL (Java), Knex.js (JavaScript).

5. **Micro ORM**
   - **Description:** Lightweight ORMs that focus on minimal abstraction, offering simpler and faster operations compared to full-fledged ORMs.
   - **Purpose:** Combine the simplicity of direct SQL with some convenience of ORM.
   - **Example Libraries:** Dapper (for .NET), SQLAlchemy Core (Python), Sequelize (Node.js).

6. **Database Abstraction Layers**
   - **Description:** Abstract the database interactions to allow switching between different databases with minimal code changes.
   - **Purpose:** Increase portability and flexibility of the application.
   - **Example Libraries:** SQLAlchemy (Python), TypeORM (TypeScript/JavaScript), Hibernate (with support for multiple databases).

7. **Active Record Pattern**
   - **Description:** Combines data access logic with domain logic in the same class.
   - **Purpose:** Simplifies CRUD operations by embedding database interaction logic within the domain model.
   - **Example Libraries:** ActiveRecord (Ruby on Rails), Laravel Eloquent (PHP).

8. **Data Mapper Pattern**
   - **Description:** Separates data access logic from business logic by mapping objects to database data in separate classes.
   - **Purpose:** Promotes separation of concerns and testability.
   - **Example Libraries:** Doctrine ORM (PHP), Hibernate (Java).

9. **Stored Procedures and Functions**
   - **Description:** Encapsulate database logic in SQL stored procedures and functions that reside on the database server.
   - **Purpose:** Improve performance and security by reducing the amount of data transferred between application and database.
   - **Example Use Cases:** Complex transactions, batch processing.

10. **GraphQL for Databases**
    - **Description:** Use GraphQL to interact with databases, often with custom resolvers mapping GraphQL queries to database queries.
    - **Purpose:** Provide a flexible query language that can aggregate and fetch data from multiple sources.
    - **Example Tools:** Hasura (GraphQL Engine for PostgreSQL), Prisma (GraphQL ORM for Node.js).

11. **CQRS (Command Query Responsibility Segregation)**
    - **Description:** Separates read and write operations into different models, optimizing for different usage patterns.
    - **Purpose:** Improves scalability and performance by tailoring data structures to specific needs.
    - **Example Use Cases:** Event sourcing, microservices architectures.

### Examples

**Direct SQL with JDBC:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class JdbcExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/yourdatabase";
        String username = "yourusername";
        String password = "yourpassword";

        try (Connection conn = DriverManager.getConnection(url, username, password)) {
            // Read example
            String selectSQL = "SELECT id, name, email FROM customers WHERE id = ?";
            try (PreparedStatement pstmt = conn.prepareStatement(selectSQL)) {
                pstmt.setInt(1, 1); // setting the parameter
                ResultSet rs = pstmt.executeQuery();

                while (rs.next()) {
                    int id = rs.getInt("id");
                    String name = rs.getString("name");
                    String email = rs.getString("email");
                    System.out.println("ID: " + id + ", Name: " + name + ", Email: " + email);
                }
            }

            // Create example
            String insertSQL = "INSERT INTO customers (name, email) VALUES (?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
                pstmt.setString(1, "Jane Doe");
                pstmt.setString(2, "jane.doe@example.com");
                pstmt.executeUpdate();
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### Conclusion

There are numerous techniques for interacting with databases, each offering different levels of abstraction, control, and ease of use. ORM and ODM are popular techniques for object-oriented interaction with relational and document databases, respectively. However, other techniques like direct SQL, query builders, micro ORMs, and database abstraction layers provide alternatives that might be better suited for certain applications or developer preferences.

## More about ORM

- **ORM as a Technique:** At its core, Object-Relational Mapping (ORM) is a programming technique. It defines a way to bridge the gap between object-oriented programming and relational databases. This technique involves defining how object properties map to database table columns and how object methods translate to database queries.

- **ORM as a Tool:** In practice, ORMs are often implemented as software libraries or frameworks that automate this technique. These tools provide pre-built functionality for object-to-relitional mapping, query building, and data manipulation. They essentially take the manual work out of implementing the ORM technique.