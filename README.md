## JDBC Transaction Management Project

This project demonstrates how to manually manage transactions using JDBC (Java Database Connectivity). It showcases the use of:

* setAutoCommit(false) to disable auto-commit;
* commit() to confirm the transaction when everything succeeds;
* rollback() in the catch block to undo changes if something goes wrong.

## How Transactions Work

By default, JDBC commits each SQL statement automatically. In this project, that behavior is changed to manual control, giving you full transactional integrity over multiple related operations.

## Transaction Control Flow

```java
Connection conn = null;

try {
    // Establish connection
    conn = DriverManager.getConnection(DB_URL, USER, PASS);

    // Disable auto-commit to manually control the transaction
    conn.setAutoCommit(false);

    // Perform multiple related operations here
    // For example: insert a customer and their order

    // If all operations succeed, commit the transaction
    conn.commit();

} catch (SQLException e) {
    // If an error occurs, rollback the transaction
    if (conn != null) {
        try {
            conn.rollback();
            System.out.println("Transaction rolled back due to error.");
        } catch (SQLException rollbackEx) {
            rollbackEx.printStackTrace();
        }
    }
    e.printStackTrace();

} finally {
    // Close the connection
    if (conn != null) {
        try {
            conn.close();
        } catch (SQLException closeEx) {
            closeEx.printStackTrace();
        }
    }
}
```
