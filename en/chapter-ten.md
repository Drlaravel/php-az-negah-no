---

### Chapter 10: Interacting with Databases

---

Databases are crucial for storing, retrieving, and managing data in web applications. PHP provides various methods to interact with databases, allowing developers to perform operations like querying, inserting, updating, and deleting data. In this chapter, we will explore how to work with databases in PHP, using both MySQLi and PDO (PHP Data Objects).

### 10.1 Introduction to Databases

Databases are systems that store data in a structured format. PHP often interacts with relational databases, where data is organized into tables with rows and columns.

### 10.2 Connecting to a Database

To interact with a database, you first need to establish a connection. PHP provides two primary extensions for database interaction: MySQLi and PDO.

#### 10.2.1 Using MySQLi

**Example:**

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "my_database";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
```

#### 10.2.2 Using PDO

**Example:**

```php
<?php
$dsn = "mysql:host=localhost;dbname=my_database";
$username = "root";
$password = "";

try {
    $pdo = new PDO($dsn, $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully";
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

### 10.3 Performing Database Operations

Once connected, you can perform various database operations such as querying, inserting, updating, and deleting data.

#### 10.3.1 Querying Data

**MySQLi Example:**

```php
<?php
$sql = "SELECT id, name, email FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["name"]. " - Email: " . $row["email"]. "<br>";
    }
} else {
    echo "0 results";
}
?>
```

**PDO Example:**

```php
<?php
$sql = "SELECT id, name, email FROM users";
$stmt = $pdo->query($sql);

while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
    echo "id: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
}
?>
```

#### 10.3.2 Inserting Data

**MySQLi Example:**

```php
<?php
$sql = "INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com')";

if ($conn->query($sql) === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}
?>
```

**PDO Example:**

```php
<?php
$sql = "INSERT INTO users (name, email) VALUES (:name, :email)";
$stmt = $pdo->prepare($sql);

$stmt->bindParam(':name', $name);
$stmt->bindParam(':email', $email);

$name = 'John Doe';
$email = 'john@example.com';

if ($stmt->execute()) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->errorInfo()[2];
}
?>
```

#### 10.3.3 Updating Data

**MySQLi Example:**

```php
<?php
$sql = "UPDATE users SET email='john.doe@example.com' WHERE name='John Doe'";

if ($conn->query($sql) === TRUE) {
    echo "Record updated successfully";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}
?>
```

**PDO Example:**

```php
<?php
$sql = "UPDATE users SET email = :email WHERE name = :name";
$stmt = $pdo->prepare($sql);

$stmt->bindParam(':email', $email);
$stmt->bindParam(':name', $name);

$email = 'john.doe@example.com';
$name = 'John Doe';

if ($stmt->execute()) {
    echo "Record updated successfully";
} else {
    echo "Error: " . $stmt->errorInfo()[2];
}
?>
```

#### 10.3.4 Deleting Data

**MySQLi Example:**

```php
<?php
$sql = "DELETE FROM users WHERE name='John Doe'";

if ($conn->query($sql) === TRUE) {
    echo "Record deleted successfully";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}
?>
```

**PDO Example:**

```php
<?php
$sql = "DELETE FROM users WHERE name = :name";
$stmt = $pdo->prepare($sql);

$stmt->bindParam(':name', $name);

$name = 'John Doe';

if ($stmt->execute()) {
    echo "Record deleted successfully";
} else {
    echo "Error: " . $stmt->errorInfo()[2];
}
?>
```

### 10.4 Prepared Statements

Prepared statements help prevent SQL injection by separating SQL logic from data.

#### 10.4.1 Using MySQLi

**Example:**

```php
<?php
$stmt = $conn->prepare("SELECT id, name, email FROM users WHERE email = ?");
$stmt->bind_param("s", $email);
$email = 'john@example.com';
$stmt->execute();
$result = $stmt->get_result();

while ($row = $result->fetch_assoc()) {
    echo "id: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
}
?>
```

#### 10.4.2 Using PDO

**Example:**

```php
<?php
$sql = "SELECT id, name, email FROM users WHERE email = :email";
$stmt = $pdo->prepare($sql);
$stmt->bindParam(':email', $email);
$email = 'john@example.com';
$stmt->execute();

while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
    echo "id: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
}
?>
```

### 10.5 Handling Errors

Proper error handling is essential for robust applications.

#### 10.5.1 MySQLi Error Handling

**Example:**

```php
<?php
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

#### 10.5.2 PDO Error Handling

**Example:**

```php
<?php
try {
    $pdo = new PDO($dsn, $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

### 10.6 Best Practices

- **Use Prepared Statements**: Protect against SQL injection.
- **Handle Errors Gracefully**: Provide meaningful error messages and log errors for troubleshooting.
- **Close Connections**: Properly close database connections to free up resources.
- **Sanitize and Validate Data**: Always sanitize and validate data before using it in SQL queries.

---

## Exercises for Chapter 10

1. **Create a Database Connection**: Write a PHP script to connect to a MySQL database using MySQLi and PDO.

2. **Query Data**: Write scripts to query and display data from a `users` table using both MySQLi and PDO.

3. **Insert Data**: Write scripts to insert new records into a `users` table using both MySQLi and PDO.

4. **Update Data**: Write scripts to update existing records in the `users` table using both MySQLi and PDO.

5. **Delete Data**: Write scripts to delete records from the `users` table using both MySQLi and PDO.

6. **Use Prepared Statements**: Modify your scripts to use prepared statements for querying data.

---

## Summary of Chapter 10

In this chapter, we covered how to interact with databases using PHP. We explored connecting to a database, performing CRUD operations (Create, Read, Update, Delete), and using prepared statements to enhance security. We also discussed handling errors and best practices for database interactions. Understanding how to manage database operations effectively is crucial for developing dynamic and data-driven web applications.

