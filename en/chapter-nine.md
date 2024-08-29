
---

### Chapter 9: Handling Forms and Web Interactions

---

Forms are a fundamental part of web applications, allowing users to input data and interact with your website. In PHP, handling forms involves receiving user input, validating it, and then processing or storing it. This chapter covers the basics of handling forms in PHP, including form methods, validation, and working with form data.

### 9.1 Introduction to Forms

Forms are used to collect data from users. They are typically created using HTML and submitted to a server for processing. PHP processes the submitted form data and can perform various operations such as storing the data in a database or sending emails.

### 9.2 Creating and Handling Forms

Forms are created using HTML and submitted using the `GET` or `POST` methods. PHP retrieves and processes the submitted data.

#### 9.2.1 HTML Form Basics

**Example:**

```html
<form method="post" action="process_form.php">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <input type="submit" value="Submit">
</form>
```

#### 9.2.2 Handling Form Data in PHP

When a form is submitted, PHP retrieves the data from the `$_POST` or `$_GET` superglobal arrays.

**Example (process_form.php):**

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Collect and sanitize form data
    $name = htmlspecialchars($_POST['name']);
    $email = htmlspecialchars($_POST['email']);
    
    echo "Name: $name<br>";
    echo "Email: $email<br>";
}
?>
```

### 9.3 Validating Form Data

Validation ensures that the data submitted by users meets specific criteria before processing. This step helps prevent invalid or malicious data from being processed.

#### 9.3.1 Server-Side Validation

Server-side validation is performed on the server after form submission. It ensures that the data is correctly formatted and meets the required criteria.

**Example:**

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = trim($_POST['name']);
    $email = trim($_POST['email']);
    $errors = [];

    // Validate name
    if (empty($name)) {
        $errors[] = "Name is required.";
    }

    // Validate email
    if (empty($email)) {
        $errors[] = "Email is required.";
    } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Invalid email format.";
    }

    // Display errors or process data
    if (empty($errors)) {
        echo "Name: $name<br>";
        echo "Email: $email<br>";
    } else {
        foreach ($errors as $error) {
            echo "$error<br>";
        }
    }
}
?>
```

### 9.4 Handling Form Submissions

Handling form submissions involves processing the data after it has been validated. This may include storing data in a database, sending an email, or performing other actions.

#### 9.4.1 Storing Form Data in a Database

**Example:**

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = htmlspecialchars($_POST['name']);
    $email = htmlspecialchars($_POST['email']);
    
    // Database connection
    $conn = new mysqli($servername, $username, $password, $dbname);
    
    // Check connection
    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }
    
    // Prepare and bind
    $stmt = $conn->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
    $stmt->bind_param("ss", $name, $email);
    
    // Execute and check
    if ($stmt->execute()) {
        echo "Record saved successfully.";
    } else {
        echo "Error: " . $stmt->error;
    }
    
    // Close connection
    $stmt->close();
    $conn->close();
}
?>
```

#### 9.4.2 Sending Form Data via Email

**Example:**

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = htmlspecialchars($_POST['name']);
    $email = htmlspecialchars($_POST['email']);
    $to = "recipient@example.com";
    $subject = "Form Submission";
    $message = "Name: $name\nEmail: $email";
    $headers = "From: $email";

    if (mail($to, $subject, $message, $headers)) {
        echo "Email sent successfully.";
    } else {
        echo "Error sending email.";
    }
}
?>
```

### 9.5 Using PHP Superglobals

PHP provides several superglobal arrays to handle form data and other global variables.

#### 9.5.1 `$_POST` and `$_GET`

- `$_POST`: Collects data submitted via the POST method.
- `$_GET`: Collects data submitted via the GET method.

**Example:**

```php
<?php
// Access POST data
$name = $_POST['name'];
$email = $_POST['email'];

// Access GET data
$search = $_GET['search'];
?>
```

#### 9.5.2 `$_REQUEST`

`$_REQUEST` combines `$_GET`, `$_POST`, and `$_COOKIE` data.

**Example:**

```php
<?php
$request_data = $_REQUEST;
echo "Name: " . $request_data['name'] . "<br>";
echo "Email: " . $request_data['email'] . "<br>";
?>
```

### 9.6 Security Considerations

Handling forms involves various security considerations to prevent attacks such as XSS (Cross-Site Scripting) and CSRF (Cross-Site Request Forgery).

#### 9.6.1 Preventing XSS

Sanitize user input to prevent XSS attacks by using `htmlspecialchars()`.

**Example:**

```php
<?php
$name = htmlspecialchars($_POST['name']);
$email = htmlspecialchars($_POST['email']);
?>
```

#### 9.6.2 Preventing CSRF

Use CSRF tokens to protect against cross-site request forgery attacks.

**Example:**

```php
<?php
session_start();
if (empty($_SESSION['token'])) {
    $_SESSION['token'] = bin2hex(random_bytes(32));
}
?>

<form method="post" action="process_form.php">
    <input type="hidden" name="token" value="<?php echo $_SESSION['token']; ?>">
    <!-- Other form fields -->
    <input type="submit" value="Submit">
</form>
```

**Processing the token:**

```php
<?php
session_start();
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    if (hash_equals($_SESSION['token'], $_POST['token'])) {
        // Process the form data
    } else {
        echo "Invalid CSRF token.";
    }
}
?>
```

### 9.7 Best Practices

- **Always Sanitize Input**: Protect against XSS by sanitizing user input.
- **Validate Data**: Ensure that the data meets required formats and constraints.
- **Use Prepared Statements**: Protect against SQL injection by using prepared statements for database interactions.
- **Implement CSRF Protection**: Use CSRF tokens to protect form submissions.
- **Secure File Uploads**: If handling file uploads, validate file types and sizes to prevent security issues.

---

## Exercises for Chapter 9

1. **Create a Form**: Build an HTML form that collects user information and submits it to a PHP script for processing.

2. **Validate Form Data**: Implement server-side validation for the form data and display any errors to the user.

3. **Store Data in a Database**: Modify your form processing script to store form data in a database.

4. **Send Form Data via Email**: Create a PHP script that sends form data via email to a specified recipient.

5. **Implement CSRF Protection**: Add CSRF protection to your form and validate the CSRF token in your PHP script.

6. **Sanitize User Input**: Ensure all user input is properly sanitized before processing.

---

## Summary of Chapter 9

In this chapter, we covered the basics of handling forms in PHP. We learned how to create and process forms, validate user input, and store or send form data. We also explored PHP superglobals for handling form data and discussed security considerations to protect against common web vulnerabilities. Mastering form handling is essential for developing interactive and secure web applications.

---
