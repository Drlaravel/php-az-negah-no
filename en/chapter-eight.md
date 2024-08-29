
---

### Chapter 8: Working with Databases

---

Databases are a fundamental part of many web applications, allowing for the storage, retrieval, and management of data. In PHP, the most common database system used is MySQL. This chapter covers the basics of working with databases in PHP, including connecting to a database, performing CRUD (Create, Read, Update, Delete) operations, and handling errors.

### 8.1 Introduction to Databases

Databases store data in a structured format, typically using tables. PHP provides several methods for interacting with databases, with MySQL being the most popular. We will use MySQLi and PDO (PHP Data Objects) to interact with MySQL databases in this chapter.

### 8.2 Connecting to a Database

To perform operations on a database, you first need to establish a connection using either MySQLi or PDO.

#### 8.2.1 Connecting with MySQLi

MySQLi is an improved version of the original MySQL extension and supports both procedural and object-oriented programming.

**Example:**

```php
<?php
// Database configuration
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "test_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
```

#### 8.2.2 Connecting with PDO

PDO provides a consistent interface for multiple database systems and is more flexible than MySQLi.

**Example:**

```php
<?php
try {
    $conn = new PDO("mysql:host=localhost;dbname=test_db", "root", "");
    // Set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully";
} catch(PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

### 8.3 Creating a Database and Tables

Before performing operations, you need to create a database and tables.

#### 8.3.1 Creating a Database

**Example:**

```php
<?php
// Create connection
$conn = new mysqli($servername, $username, $password);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Create database
$sql = "CREATE DATABASE test_db";
if ($conn->query($sql) === TRUE) {
    echo "Database created successfully";
} else {
    echo "Error creating database: " . $conn->error;
}

$conn->close();
?>
```

#### 8.3.2 Creating Tables

**Example:**

```php
<?php
// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Create table
$sql = "CREATE TABLE users (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(30) NOT NULL,
    email VARCHAR(50),
    reg_date TIMESTAMP
)";

if ($conn->query($sql) === TRUE) {
    echo "Table created successfully";
} else {
    echo "Error creating table: " . $conn->error;
}

$conn->close();
?>
```

### 8.4 Performing CRUD Operations

CRUD operations involve creating, reading, updating, and deleting data in a database.

#### 8.4.1 Creating Records

**Example:**

```php
<?php
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "INSERT INTO users (name, email)
VALUES ('John Doe', 'john@example.com')";

if ($conn->query($sql) === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

$conn->close();
?>
```

#### 8.4.2 Reading Records

**Example:**

```php
<?php
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "SELECT id, name, email FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    // Output data of each row
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["name"]. " - Email: " . $row["email"]. "<br>";
    }
} else {
    echo "0 results";
}

$conn->close();
?>
```

#### 8.4.3 Updating Records

**Example:**

```php
<?php
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "UPDATE users SET email='newemail@example.com' WHERE id=1";

if ($conn->query($sql) === TRUE) {
    echo "Record updated successfully";
} else {
    echo "Error updating record: " . $conn->error;
}

$conn->close();
?>
```

#### 8.4.4 Deleting Records

**Example:**

```php
<?php
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "DELETE FROM users WHERE id=1";

if ($conn->query($sql) === TRUE) {
    echo "Record deleted successfully";
} else {
    echo "Error deleting record: " . $conn->error;
}

$conn->close();
?>
```

### 8.5 Handling Errors

Proper error handling is crucial for maintaining a robust application. Use try-catch blocks in PDO and error handling methods in MySQLi.

#### 8.5.1 Error Handling with MySQLi

**Example:**

```php
<?php
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "SELECT * FROM non_existing_table";
$result = $conn->query($sql);

if (!$result) {
    echo "Error: " . $conn->error;
}

$conn->close();
?>
```

#### 8.5.2 Error Handling with PDO

**Example:**

```php
<?php
try {
    $conn = new PDO("mysql:host=localhost;dbname=test_db", "root", "");
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    $stmt = $conn->prepare("SELECT * FROM non_existing_table");
    $stmt->execute();

    $result = $stmt->fetchAll();
} catch(PDOException $e) {
    echo "Error: " . $e->getMessage();
}

$conn = null;
?>
```

### 8.6 Best Practices

- **Use Prepared Statements**: To prevent SQL injection, use prepared statements with bound parameters.
- **Validate User Input**: Always validate and sanitize user input before using it in SQL queries.
- **Handle Errors Gracefully**: Provide meaningful error messages and handle exceptions properly.
- **Secure Database Connections**: Avoid using root credentials for application connections and use proper database permissions.

---

## Exercises for Chapter 8

1. **Create a Database and Table**: Write a PHP script that creates a database and a table with appropriate fields.

2. **Perform CRUD Operations**: Implement PHP scripts to perform Create, Read, Update, and Delete operations on a database table.

3. **Handle Errors**: Write PHP scripts to handle common database errors and display user-friendly messages.

4. **Implement Prepared Statements**: Modify your CRUD operations to use prepared statements with bound parameters.

5. **Database Security**: Implement security measures to protect your database from SQL injection and unauthorized access.

6. **Display Database Records**: Create a PHP script that retrieves and displays records from a database table in a user-friendly format.

---

## Summary of Chapter 8

In this chapter, we explored the fundamentals of working with databases in PHP. We covered how to connect to a database, create and manage tables, perform CRUD operations, and handle errors. By applying these techniques, you can effectively manage data in your PHP applications and ensure secure and efficient database interactions.

---
