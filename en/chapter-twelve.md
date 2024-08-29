---

### Chapter 12: File Handling and Manipulation

---

File handling is a crucial skill in web development, allowing you to create, read, write, and manipulate files on the server. PHP provides various functions for file handling, enabling you to perform tasks such as uploading files, reading file contents, and modifying file data. This chapter covers the essentials of file handling in PHP.

### 12.1 Introduction to File Handling

File handling involves interacting with files stored on the server. PHP provides functions to perform various file operations, such as creating, opening, reading, writing, and closing files.

### 12.2 Opening and Closing Files

To work with files, you need to open them first. PHP provides functions to open files in different modes (read, write, append).

#### 12.2.1 Opening Files

**Example:**

```php
<?php
$file = fopen("example.txt", "r"); // Open file for reading
if ($file) {
    // File opened successfully
} else {
    echo "Unable to open file.";
}
?>
```

#### 12.2.2 Closing Files

**Example:**

```php
<?php
fclose($file); // Close the file when done
?>
```

### 12.3 Reading from Files

You can read the contents of a file using PHP functions. You can read files line-by-line or in chunks.

#### 12.3.1 Reading the Entire File

**Example:**

```php
<?php
$content = file_get_contents("example.txt");
echo $content;
?>
```

#### 12.3.2 Reading Line-by-Line

**Example:**

```php
<?php
$file = fopen("example.txt", "r");
while (($line = fgets($file)) !== false) {
    echo $line . "<br>";
}
fclose($file);
?>
```

### 12.4 Writing to Files

You can write data to a file by opening it in write or append mode. Be cautious as writing in write mode will overwrite the existing content.

#### 12.4.1 Writing Data

**Example:**

```php
<?php
$file = fopen("example.txt", "w"); // Open file for writing
if ($file) {
    fwrite($file, "Hello, World!");
    fclose($file);
} else {
    echo "Unable to open file.";
}
?>
```

#### 12.4.2 Appending Data

**Example:**

```php
<?php
$file = fopen("example.txt", "a"); // Open file for appending
if ($file) {
    fwrite($file, "Appended text.");
    fclose($file);
} else {
    echo "Unable to open file.";
}
?>
```

### 12.5 Uploading Files

Uploading files involves receiving files from a user and saving them to the server.

#### 12.5.1 Handling File Uploads

**HTML Form:**

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="fileToUpload">
    <input type="submit" value="Upload File">
</form>
```

**PHP Script (upload.php):**

```php
<?php
$target_dir = "uploads/";
$target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
$uploadOk = 1;

if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], $target_file)) {
    echo "The file " . basename($_FILES["fileToUpload"]["name"]) . " has been uploaded.";
} else {
    echo "Sorry, there was an error uploading your file.";
}
?>
```

### 12.6 File Permissions and Security

File permissions control access to files. It is essential to set correct permissions and handle files securely to avoid unauthorized access.

#### 12.6.1 Setting File Permissions

**Example:**

```php
<?php
chmod("example.txt", 0644); // Set file permissions to read/write for owner, read-only for others
?>
```

#### 12.6.2 Secure File Handling

- **Validate File Types**: Ensure uploaded files are of expected types.
- **Limit File Sizes**: Set restrictions on file sizes to avoid large uploads.
- **Store Files Securely**: Avoid storing sensitive files in publicly accessible directories.

### 12.7 Best Practices

- **Validate Inputs**: Always validate and sanitize file inputs to prevent security issues.
- **Handle Errors**: Implement proper error handling for file operations.
- **Use File Locks**: Use file locking mechanisms if concurrent file access is a concern.
- **Limit Access**: Restrict access to files based on user roles and permissions.

---

## Exercises for Chapter 12

1. **Open and Close Files**: Write PHP scripts to open, read, and close files.

2. **Read and Write Files**: Create scripts to read from and write data to files.

3. **File Uploads**: Implement a file upload system and handle file uploads securely.

4. **File Permissions**: Set and modify file permissions using PHP.

5. **Handle

 Errors**: Write code to handle errors during file operations and provide user feedback.

---

## Summary of Chapter 12

In this chapter, we covered the basics of file handling in PHP. We explored opening, reading, writing, and closing files. We also discussed handling file uploads and setting file permissions. Understanding file handling is essential for managing data on the server and implementing features that involve file manipulation.

---
