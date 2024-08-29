
---

### Chapter 7: Working with Files

---

Working with files is an essential aspect of PHP programming. This chapter covers the various methods for handling files in PHP, including reading from and writing to files, file uploads, and file manipulation. We will explore functions and best practices for managing files effectively.

### 7.1 Introduction to File Handling

PHP provides a variety of functions to interact with files. These functions allow you to open, read, write, and close files, as well as perform other file operations such as deleting and renaming files.

### 7.2 Opening and Closing Files

Before performing operations on a file, you need to open it using the `fopen()` function. After completing the file operations, you should close the file using the `fclose()` function.

#### 7.2.1 Opening Files

The `fopen()` function opens a file or URL and returns a file handle that can be used for reading or writing.

**Example:**

```php
<?php
// Open a file for reading
$file = fopen("example.txt", "r");

if ($file) {
    // File opened successfully
    echo "File opened successfully.";
} else {
    // Error opening file
    echo "Error opening file.";
}
?>
```

#### 7.2.2 Closing Files

The `fclose()` function closes an open file.

**Example:**

```php
<?php
$file = fopen("example.txt", "r");

// Perform file operations

// Close the file
fclose($file);
?>
```

### 7.3 Reading from Files

You can read from files using several functions, including `fread()`, `fgets()`, and `file_get_contents()`.

#### 7.3.1 Reading Entire File

The `file_get_contents()` function reads an entire file into a string.

**Example:**

```php
<?php
$content = file_get_contents("example.txt");
echo $content; // Display the content of the file
?>
```

#### 7.3.2 Reading File Line by Line

The `fgets()` function reads a file line by line.

**Example:**

```php
<?php
$file = fopen("example.txt", "r");

while (($line = fgets($file)) !== false) {
    echo $line; // Display each line
}

fclose($file);
?>
```

### 7.4 Writing to Files

You can write to files using functions like `fwrite()`, `file_put_contents()`, and `fputs()`.

#### 7.4.1 Writing to a File

The `fwrite()` function writes data to an open file.

**Example:**

```php
<?php
$file = fopen("example.txt", "w");

if ($file) {
    fwrite($file, "Hello, world!\n");
    fclose($file);
    echo "Data written to file successfully.";
} else {
    echo "Error opening file.";
}
?>
```

#### 7.4.2 Writing to a File (Overwrite)

The `file_put_contents()` function writes data to a file, overwriting the file if it already exists.

**Example:**

```php
<?php
file_put_contents("example.txt", "New content");
echo "File updated successfully.";
?>
```

### 7.5 File Uploads

Uploading files from a client to a server is a common task in web development. PHP provides tools for handling file uploads securely.

#### 7.5.1 File Upload Form

Create an HTML form for file uploads:

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="fileToUpload">
    <input type="submit" value="Upload File">
</form>
```

#### 7.5.2 Handling File Uploads in PHP

In the `upload.php` script, handle the uploaded file using the `$_FILES` superglobal.

**Example:**

```php
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $target_dir = "uploads/";
    $target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
    $uploadOk = 1;

    // Check if file is an actual image or fake image
    $check = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
    if ($check !== false) {
        echo "File is an image - " . $check["mime"] . ".";
        $uploadOk = 1;
    } else {
        echo "File is not an image.";
        $uploadOk = 0;
    }

    // Check if file already exists
    if (file_exists($target_file)) {
        echo "Sorry, file already exists.";
        $uploadOk = 0;
    }

    // Check file size
    if ($_FILES["fileToUpload"]["size"] > 500000) {
        echo "Sorry, your file is too large.";
        $uploadOk = 0;
    }

    // Allow certain file formats
    $imageFileType = strtolower(pathinfo($target_file, PATHINFO_EXTENSION));
    if ($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg" && $imageFileType != "gif") {
        echo "Sorry, only JPG, JPEG, PNG & GIF files are allowed.";
        $uploadOk = 0;
    }

    // Check if $uploadOk is set to 0 by an error
    if ($uploadOk == 0) {
        echo "Sorry, your file was not uploaded.";
    // If everything is ok, try to upload file
    } else {
        if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], $target_file)) {
            echo "The file " . basename($_FILES["fileToUpload"]["name"]) . " has been uploaded.";
        } else {
            echo "Sorry, there was an error uploading your file.";
        }
    }
}
?>
```

### 7.6 File Manipulation

PHP provides various functions for manipulating files, such as renaming, deleting, and checking file existence.

#### 7.6.1 Renaming Files

The `rename()` function renames a file.

**Example:**

```php
<?php
rename("old_name.txt", "new_name.txt");
echo "File renamed successfully.";
?>
```

#### 7.6.2 Deleting Files

The `unlink()` function deletes a file.

**Example:**

```php
<?php
unlink("example.txt");
echo "File deleted successfully.";
?>
```

#### 7.6.3 Checking File Existence

The `file_exists()` function checks if a file exists.

**Example:**

```php
<?php
if (file_exists("example.txt")) {
    echo "File exists.";
} else {
    echo "File does not exist.";
}
?>
```

### 7.7 Best Practices

- **Validate Uploaded Files**: Ensure that uploaded files are properly validated and sanitized to prevent security issues.
- **Handle File Errors**: Always check for errors when performing file operations and provide user-friendly messages.
- **Secure File Uploads**: Use secure file upload practices to protect your server from malicious files.

---

## Exercises for Chapter 7

1. **File Reading Exercise**: Write a PHP script that reads the contents of a file and displays it on the web page.

2. **File Writing Exercise**: Create a PHP script that writes user input to a file and then displays the file contents.

3. **File Upload Exercise**: Create a file upload form and handle the file upload in a PHP script, including validation and error handling.

4. **File Manipulation Exercise**: Write PHP scripts to rename, delete, and check the existence of files.

5. **File Upload Security Exercise**: Implement security measures for file uploads, such as file type validation and size checks.

6. **File Operations Exercise**: Write a PHP script that demonstrates reading, writing, and appending to a file.

---

## Summary of Chapter 7

In this chapter, we covered various aspects of file handling in PHP. We explored how to open, read, write, and close files, as well as handle file uploads and perform file manipulation tasks. By mastering these file operations, you can effectively manage files in your PHP applications and ensure smooth file handling processes.

---
