
---

### **Chapter 2: Control Structures and Functions in PHP**

---

### **2.1 Introduction to Control Structures**

Control structures are fundamental to any programming language. They allow you to control the flow of execution based on conditions. PHP provides several control structures such as `if`, `else`, `switch`, `for`, `while`, and more, which help in making decisions, repeating tasks, and managing the flow of your code.

#### **2.1.1 The `if` Statement**

The `if` statement is the most basic control structure that executes a block of code if a specified condition is true.

**Example:**

```php
<?php
$number = 10;

if ($number > 5) {
    echo "The number is greater than 5.";
}
?>
```

#### **2.1.2 The `if-else` Statement**

The `if-else` statement allows you to execute one block of code if the condition is true and another block if it is false.

**Example:**

```php
<?php
$number = 3;

if ($number > 5) {
    echo "The number is greater than 5.";
} else {
    echo "The number is not greater than 5.";
}
?>
```

#### **2.1.3 The `if-elseif-else` Statement**

The `if-elseif-else` statement allows you to test multiple conditions. It is useful when you have more than two possible outcomes.

**Example:**

```php
<?php
$day = "Monday";

if ($day == "Saturday") {
    echo "It's a weekend!";
} elseif ($day == "Sunday") {
    echo "It's still a weekend!";
} else {
    echo "It's a weekday.";
}
?>
```

#### **2.1.4 The `switch` Statement**

The `switch` statement is another way to perform conditional logic. It is used when you want to compare the same expression with different values.

**Example:**

```php
<?php
$color = "red";

switch ($color) {
    case "blue":
        echo "The color is blue.";
        break;
    case "red":
        echo "The color is red.";
        break;
    default:
        echo "Unknown color.";
}
?>
```

### **2.2 Loops in PHP**

Loops are used to execute a block of code repeatedly as long as a specified condition is true. PHP provides several types of loops, such as `for`, `while`, `do-while`, and `foreach`.

#### **2.2.1 The `for` Loop**

The `for` loop is used when the number of iterations is known. It consists of three parts: initialization, condition, and increment/decrement.

**Example:**

```php
<?php
for ($i = 0; $i < 5; $i++) {
    echo "The number is: $i <br>";
}
?>
```

#### **2.2.2 The `while` Loop**

The `while` loop repeats a block of code as long as a specified condition is true.

**Example:**

```php
<?php
$i = 0;

while ($i < 5) {
    echo "The number is: $i <br>";
    $i++;
}
?>
```

#### **2.2.3 The `do-while` Loop**

The `do-while` loop is similar to the `while` loop, but it executes the code block at least once, even if the condition is false.

**Example:**

```php
<?php
$i = 0;

do {
    echo "The number is: $i <br>";
    $i++;
} while ($i < 5);
?>
```

#### **2.2.4 The `foreach` Loop**

The `foreach` loop is used to iterate over arrays. It is the easiest way to loop through the elements of an array.

**Example:**

```php
<?php
$fruits = array("Apple", "Banana", "Orange");

foreach ($fruits as $fruit) {
    echo "Fruit: $fruit <br>";
}
?>
```

### **2.3 Introduction to Functions**

Functions are a block of code that can be reused multiple times. Functions help to make code more modular, reusable, and organized. PHP provides many built-in functions, and you can also define your own custom functions.

#### **2.3.1 Defining a Function**

A function is defined using the `function` keyword followed by the function name and a pair of parentheses `()`.

**Example:**

```php
<?php
function greet() {
    echo "Hello, World!";
}

greet(); // Calling the function
?>
```

#### **2.3.2 Function Parameters**

Functions can take parameters, which are variables passed to the function when it is called.

**Example:**

```php
<?php
function greet($name) {
    echo "Hello, $name!";
}

greet("Alice");
?>
```

#### **2.3.3 Return Values from Functions**

Functions can return values using the `return` keyword. This allows you to store the result of a function call in a variable.

**Example:**

```php
<?php
function add($a, $b) {
    return $a + $b;
}

$sum = add(5, 10);
echo "The sum is: $sum";
?>
```

#### **2.3.4 Default Parameters**

PHP functions support default parameter values. If no value is passed for a parameter, the default value is used.

**Example:**

```php
<?php
function greet($name = "Guest") {
    echo "Hello, $name!";
}

greet(); // Output: Hello, Guest!
greet("Alice"); // Output: Hello, Alice!
?>
```

### **2.4 Variable Scope in PHP**

The scope of a variable is the context within which it is defined. PHP has three types of variable scope:

1. **Local Scope:** A variable declared within a function has local scope and is accessible only within that function.
2. **Global Scope:** A variable declared outside any function has global scope and is accessible anywhere in the script, except inside functions unless specified.
3. **Static Scope:** A static variable retains its value even after the function execution ends.

**Example of Local Scope:**

```php
<?php
function myFunction() {
    $x = 5; // Local scope
    echo "The value of x inside function: $x";
}

myFunction();
echo "The value of x outside function: $x"; // Error: Undefined variable
?>
```

**Example of Global Scope:**

```php
<?php
$y = 10; // Global scope

function myFunction() {
    global $y; // Access global variable
    echo "The value of y inside function: $y";
}

myFunction();
echo "The value of y outside function: $y";
?>
```

### **2.5 Recursive Functions**

A recursive function is a function that calls itself. Recursion is useful for solving problems that can be broken down into smaller, similar problems.

**Example: Factorial Calculation using Recursion**

```php
<?php
function factorial($n) {
    if ($n <= 1) {
        return 1;
    } else {
        return $n * factorial($n - 1);
    }
}

echo "Factorial of 5 is: " . factorial(5);
?>
```

### **2.6 Anonymous Functions and Closures**

Anonymous functions, also known as closures, are functions that have no specified name. They are often used as callback functions or when a function is needed only once.

**Example: Anonymous Function**

```php
<?php
$greet = function($name) {
    echo "Hello, $name!";
};

$greet("Alice"); // Output: Hello, Alice!
?>
```

### **2.7 Exercises for Chapter 2**

1. **Control Structures Practice:** Write a PHP script that checks if a number is even or odd using `if-else`.
   
2. **Loop Practice:** Create a PHP script that prints the multiplication table of a given number using a `for` loop.
   
3. **Function Practice:** Write a function that calculates the sum of all elements in an array.
   
4. **Recursive Function Practice:** Implement a recursive function to calculate the Fibonacci sequence up to a given number.
   
5. **Anonymous Functions and Closures:** Write a script that uses an anonymous function to filter an array of integers, returning only the even numbers.

### **2.8 Summary of Chapter 2**

In this chapter, you learned about control structures and functions in PHP, which are essential for writing effective and efficient code. You explored various types of loops, conditionals, and the concept of functions, parameters, and return values. Understanding these concepts is crucial for building more complex and dynamic applications. In the next chapter, we will dive deeper into working with arrays and advanced data manipulation in PHP.

---
