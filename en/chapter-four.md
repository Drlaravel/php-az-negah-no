در فصل چهارم، به مبحث کار با رشته‌ها (Strings) در PHP خواهیم پرداخت. رشته‌ها یکی از پرکاربردترین انواع داده‌ها در برنامه‌نویسی هستند و PHP مجموعه‌ای از توابع قدرتمند برای کار با رشته‌ها ارائه می‌دهد. در این فصل، به بررسی نحوه تعریف و استفاده از رشته‌ها، توابع مختلف برای دستکاری رشته‌ها، و روش‌های پیشرفته‌تر مانند جستجو و جایگزینی در رشته‌ها خواهیم پرداخت.

---

### **Chapter 4: Working with Strings in PHP**

---

### **4.1 Introduction to Strings**

A string in PHP is a sequence of characters enclosed within single quotes (`'`) or double quotes (`"`). Strings are one of the most commonly used data types and can store anything from a single character to long blocks of text.

#### **4.1.1 Defining Strings**

Strings can be defined in two ways: using single quotes or double quotes.

- **Single-quoted strings:** Simple strings with minimal processing.
- **Double-quoted strings:** Allow variable interpolation and escape sequences.

**Example:**

```php
<?php
$single_quoted = 'Hello, World!';
$double_quoted = "Hello, $single_quoted";

echo $single_quoted; // Output: Hello, World!
echo $double_quoted; // Output: Hello, Hello, World!
?>
```

### **4.2 String Concatenation**

String concatenation is the process of joining two or more strings together. In PHP, the concatenation operator (`.`) is used to join strings.

**Example:**

```php
<?php
$greeting = "Hello";
$name = "John";
$welcome = $greeting . ", " . $name . "!";
echo $welcome; // Output: Hello, John!
?>
```

### **4.3 String Functions in PHP**

PHP provides a wide range of built-in functions for working with strings. Some of the most commonly used functions are:

#### **4.3.1 `strlen()` - String Length**

The `strlen()` function returns the length of a string.

**Example:**

```php
<?php
$length = strlen("Hello, World!");
echo "The length of the string is: $length"; // Output: 13
?>
```

#### **4.3.2 `strtoupper()` and `strtolower()` - Changing Case**

The `strtoupper()` function converts all characters in a string to uppercase, while `strtolower()` converts them to lowercase.

**Example:**

```php
<?php
$original = "Hello, World!";
$upper = strtoupper($original);
$lower = strtolower($original);

echo $upper; // Output: HELLO, WORLD!
echo $lower; // Output: hello, world!
?>
```

#### **4.3.3 `substr()` - Substring Extraction**

The `substr()` function returns a portion of a string, defined by a starting position and optionally a length.

**Example:**

```php
<?php
$text = "Hello, World!";
$substring = substr($text, 7, 5); // Extracts "World"
echo $substring; // Output: World
?>
```

#### **4.3.4 `strpos()` and `strrpos()` - Finding a Substring**

The `strpos()` function finds the position of the first occurrence of a substring in a string. `strrpos()` finds the position of the last occurrence.

**Example:**

```php
<?php
$haystack = "I love PHP, I really love PHP!";
$position = strpos($haystack, "PHP"); // First occurrence
$last_position = strrpos($haystack, "PHP"); // Last occurrence

echo "First occurrence: $position"; // Output: 7
echo "Last occurrence: $last_position"; // Output: 24
?>
```

#### **4.3.5 `str_replace()` - Replacing Substrings**

The `str_replace()` function replaces all occurrences of a substring within a string with another substring.

**Example:**

```php
<?php
$text = "I love PHP!";
$new_text = str_replace("PHP", "programming", $text);

echo $new_text; // Output: I love programming!
?>
```

### **4.4 Advanced String Functions**

PHP also provides more advanced functions for working with strings, such as formatting, splitting, and joining strings.

#### **4.4.1 `implode()` and `explode()` - Joining and Splitting Strings**

- **`implode()`**: Joins array elements into a single string.
- **`explode()`**: Splits a string into an array based on a delimiter.

**Example:**

```php
<?php
$words = ["I", "love", "PHP"];
$sentence = implode(" ", $words);
echo $sentence; // Output: I love PHP

$sentence = "I love PHP";
$words = explode(" ", $sentence);
print_r($words); // Output: Array ( [0] => I [1] => love [2] => PHP )
?>
```

#### **4.4.2 `trim()` - Trimming Whitespace**

The `trim()` function removes whitespace (or other characters) from the beginning and end of a string.

بله، ادامه می‌دهیم:

---

```php
<?php
$text = "  Hello, World!  ";
$trimmed = trim($text); // Removes whitespace from both ends
echo $trimmed; // Output: Hello, World!
?>
```

### **4.5 String Formatting**

String formatting in PHP allows you to create formatted strings using functions like `printf()` and `sprintf()`.

#### **4.5.1 `printf()` - Formatted Output**

The `printf()` function outputs a formatted string. You can use format specifiers to format numbers, strings, and other data types.

**Example:**

```php
<?php
$number = 123.456;
printf("Formatted number: %.2f", $number); // Output: Formatted number: 123.46
?>
```

#### **4.5.2 `sprintf()` - Formatted String**

The `sprintf()` function returns a formatted string without outputting it. This is useful when you want to store the formatted string in a variable.

**Example:**

```php
<?php
$number = 123.456;
$formatted = sprintf("Formatted number: %.2f", $number);
echo $formatted; // Output: Formatted number: 123.46
?>
```

### **4.6 String Manipulation Examples**

Here are some practical examples of string manipulation:

#### **4.6.1 Checking String Length**

```php
<?php
$text = "Check the length of this string.";
if (strlen($text) > 20) {
    echo "The string is quite long.";
} else {
    echo "The string is short.";
}
?>
```

#### **4.6.2 Replacing Words in a String**

```php
<?php
$sentence = "The quick brown fox jumps over the lazy dog.";
$modified = str_replace("fox", "cat", $sentence);
echo $modified; // Output: The quick brown cat jumps over the lazy dog.
?>
```

#### **4.6.3 Extracting Substrings**

```php
<?php
$full_name = "John Doe";
$first_name = substr($full_name, 0, strpos($full_name, " "));
echo $first_name; // Output: John
?>
```

### **4.7 Common Pitfalls and Best Practices**

#### **4.7.1 Avoiding Common Pitfalls**

- **Encoding Issues:** Ensure that strings are handled in the correct character encoding (e.g., UTF-8) to avoid unexpected results.
- **Escape Sequences:** Be cautious with escape sequences in double-quoted strings. Use `addslashes()` if necessary to escape special characters.

#### **4.7.2 Best Practices**

- **Use Single Quotes When Possible:** Use single quotes for strings that do not require variable interpolation or special escape sequences for better performance.
- **Sanitize User Input:** Always sanitize and validate user input to avoid security vulnerabilities such as SQL injection and XSS (Cross-Site Scripting).

---
### **Chapter 4: Strings (Continued)**

---

### **4.8 String Encoding and Multibyte Strings**

PHP handles strings in various encodings. The default encoding is typically UTF-8, which supports a wide range of characters. However, when dealing with multibyte character encodings (like UTF-8), you need to use specific functions to handle these properly.

#### **4.8.1 Handling UTF-8 Strings**

When working with UTF-8 encoded strings, it's important to use functions that are aware of multibyte characters to avoid issues with string manipulation.

**Example:**

```php
<?php
// Set the internal encoding to UTF-8
mb_internal_encoding("UTF-8");

// Example UTF-8 string
$utf8_string = "こんにちは";

// Get the length of the UTF-8 string
$length = mb_strlen($utf8_string);
echo "The length of the string is: $length"; // Output: The length of the string is: 5
?>
```

#### **4.8.2 Multibyte String Functions**

PHP provides a set of functions for handling multibyte strings:

- **`mb_strlen()`**: Returns the number of characters in a string.
- **`mb_substr()`**: Returns part of a string specified by start and length parameters.
- **`mb_strpos()`**: Finds the position of the first occurrence of a substring in a string.

**Example:**

```php
<?php
$utf8_string = "こんにちは";

// Find the position of a character
$position = mb_strpos($utf8_string, "に");
echo "The position of 'に' is: $position"; // Output: The position of 'に' is: 2

// Extract a substring
$substring = mb_substr($utf8_string, 1, 2);
echo "Substring: $substring"; // Output: Substring: ちに
?>
```

### **4.9 String Manipulation with Regular Expressions**

Regular expressions (regex) are powerful tools for pattern matching and manipulation in strings. PHP uses the `preg_` functions to work with regular expressions.

#### **4.9.1 Matching Patterns**

**Example:**

```php
<?php
$text = "The quick brown fox jumps over the lazy dog.";
$pattern = "/fox/";
if (preg_match($pattern, $text)) {
    echo "The pattern 'fox' was found!";
} else {
    echo "The pattern 'fox' was not found.";
}
?>
```

#### **4.9.2 Replacing Patterns**

**Example:**

```php
<?php
$text = "The quick brown fox jumps over the lazy dog.";
$pattern = "/fox/";
$replacement = "cat";
$result = preg_replace($pattern, $replacement, $text);
echo $result; // Output: The quick brown cat jumps over the lazy dog.
?>
```

### **4.10 Common Issues and Best Practices**

#### **4.10.1 Handling Special Characters**

When dealing with special characters in strings, you may need to escape them. Use `addslashes()` or `htmlspecialchars()` to handle special characters properly.

**Example:**

```php
<?php
$text = "Hello, I'm a PHP developer!";
$escaped = addslashes($text);
echo $escaped; // Output: Hello, I\'m a PHP developer!
?>
```

#### **4.10.2 Avoiding SQL Injection**

When inserting strings into SQL queries, always use prepared statements to avoid SQL injection attacks. PHP’s PDO or MySQLi provides ways to handle this securely.

**Example:**

```php
<?php
// Using PDO for prepared statements
$pdo = new PDO('mysql:host=localhost;dbname=test', 'user', 'password');
$sql = 'SELECT * FROM users WHERE username = :username';
$stmt = $pdo->prepare($sql);
$stmt->execute(['username' => $username]);
$results = $stmt->fetchAll();
?>
```

---

## **Exercises for Chapter 4**

1. **UTF-8 String Length Exercise:**
   Create a UTF-8 string containing several multibyte characters and calculate its length using `mb_strlen()`.

2. **Multibyte Substring Exercise:**
   Given a UTF-8 string, extract and display a substring using `mb_substr()`.

3. **Regex Pattern Matching Exercise:**
   Write a program to check if a given text contains a specific pattern using `preg_match()`.

4. **Regex Replacement Exercise:**
   Create a string and replace all occurrences of a specified pattern using `preg_replace()`.

5. **Special Characters Handling Exercise:**
   Create a string with special characters and use `addslashes()` or `htmlspecialchars()` to escape these characters.

6. **SQL Injection Prevention Exercise:**
   Write a script that connects to a database and performs a query using prepared statements to prevent SQL injection.

---

## **Summary of Chapter 4**

In this chapter, we explored advanced string handling techniques in PHP, including UTF-8 encoding, multibyte string functions, and regular expressions. We covered how to handle special characters, avoid common pitfalls, and ensure that your string operations are secure. Understanding these advanced string manipulation techniques will help you work with textual data more effectively and build robust PHP applications.

---
