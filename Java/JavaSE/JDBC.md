# Java Database Connectivity API

* [Oracle JDBC Trail](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html)
* [java.sql module documentation](https://docs.oracle.com/javase/9/docs/api/java.sql-summary.html)
* [java.sql package documentation](https://docs.oracle.com/javase/9/docs/api/java/sql/package-summary.html)
* [javax.sql package documentation - Java EE?](https://docs.oracle.com/javase/9/docs/api/javax/sql/package-summary.html)

## Drivers

There are four types of drivers, because of course:

* Type 1: JDBC-ODBC bridge - from the late 90s, using ODBC, the Open Database Connectivity Protocol, which was the dominant DB connection protocol at the time
* Type 2: JDBC & Native API driver - more performant than JDBC-ODBC bridge, but also not all Java
* Type 3: JDBC API & Type 3 driver - client driver is all Java, additional middleware driver that it communicates to on the server
* Type 4: 100% Java thing driver - a single driver, downside here is a different driver is needed for each database type

The typical driver used will be the Type 4 MySQL JDBC driver, coordinates: `mysql:mysql-connector-java:5.1.45`

## Example Connection Code

```Java
private final String USERNAME = "dbuser";
private final String PASSWORD = "dbpassword";
private final String CONN_STRING = "jdbc:mysql://localhost/explorecalifornia";

public Connection connect() throws SQLException {

    Connection connection = null;
    try {
        connection = DriverManager.getConnection(CONN_STRING, USERNAME, PASSWORD);
        System.out.println("Connection successful.");
        retun connection;
    } catch (SQLException e) {
        System.out.println(e.getMessage());
        return null;
    } finally {
        if (connection != null) {
            connection.close();
        }
    }
}
```

Example code isn't necessarily good code.

## Example Query Code

```Java
Statement statement = connection.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY);
ResultSet resultSet = statement.executeQuery("SELECT * FROM states");
resultSet.last();
System.out.println("Number of rows: " + resultSet.getRow());

if (resultSet != null) {
    resultSet.close();
}
if (statement != null) {
    statement.close();
}
if (connection != null) {
    connection.close();
}
```

Example code isn't necessarily good code, sacrficises try-catch for readability.

## Working with a ResultSet

Result sets can either be forward read only, or scrollable.

A result set that can only be read forward is commonly read using a while loop like so:

Whereas a scrollable result set has more options for how to read it, here are some of the methods:

* Methods that move the cursor:
  * `resultSet.beforeFirst();`
  * `resultSet.first();`
  * `resultSet.last();`
  * `resultSet.afterLast();`
  * `resultSet.absolute(int row);`
* Methods that return a boolean:
  * `resultSet.isBeforeFirst();`
  * `resultSet.isFirst();`
  * `resultSet.isLast();`
  * `resultSet.isAfterLast();`