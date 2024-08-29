
---

### **Chapter 3: Working with Arrays in PHP**

---

### **3.1 Introduction to Arrays**

Arrays in PHP are data structures that can store multiple values under a single name. Arrays can hold various types of data, such as strings, integers, and even other arrays. Arrays in PHP are dynamic, meaning you do not need to specify the size of the array in advance. Arrays can be indexed numerically or associatively.

#### **3.1.1 Types of Arrays in PHP**

PHP supports three types of arrays:

1. **Indexed Arrays:** Arrays with a numeric index.
2. **Associative Arrays:** Arrays with named keys.
3. **Multidimensional Arrays:** Arrays containing one or more arrays.

### **3.2 Indexed Arrays**

Indexed arrays use numeric indexes to store data. The index starts from `0` by default.

#### **3.2.1 Creating Indexed Arrays**

You can create an indexed array using the `array()` function or the short array syntax `[]`.

**Example:**

```php
<?php
$fruits = array("Apple", "Banana", "Orange");
$vegetables = ["Carrot", "Potato", "Tomato"];

echo $fruits[0]; // Output: Apple
echo $vegetables[1]; // Output: Potato
?>
```

#### **3.2.2 Adding and Removing Elements**

You can add elements to an indexed array using the `[]` syntax or `array_push()` function. To remove elements, you can use `unset()`.

**Example: Adding Elements**

```php
<?php
$fruits[] = "Mango"; // Adding element to the end
array_push($fruits, "Grapes"); // Another way to add element

print_r($fruits); // Output: Array ( [0] => Apple [1] => Banana [2] => Orange [3] => Mango [4] => Grapes )
?>
```

**Example: Removing Elements**

```php
<?php
unset($fruits[1]); // Removes "Banana"
print_r($fruits); // Output: Array ( [0] => Apple [2] => Orange )
?>
```

### **3.3 Associative Arrays**

Associative arrays use named keys that you assign to them to access their values. They are useful when you want to store data with a specific key, such as in a dictionary.

#### **3.3.1 Creating Associative Arrays**

You can create an associative array using the `array()` function or the short array syntax `[]`.

**Example:**

```php
<?php
$ages = array("John" => 25, "Jane" => 30, "Peter" => 35);
$grades = ["Alice" => "A", "Bob" => "B", "Charlie" => "C"];

echo $ages["John"]; // Output: 25
echo $grades["Alice"]; // Output: A
?>
```

#### **3.3.2 Adding and Removing Elements**

You can add elements to an associative array by specifying the key and value. To remove elements, you can use `unset()`.

**Example: Adding Elements**

```php
<?php
$ages["Mark"] = 40; // Adding a new element
print_r($ages); // Output: Array ( [John] => 25 [Jane] => 30 [Peter] => 35 [Mark] => 40 )
?>
```

**Example: Removing Elements**

```php
<?php
unset($ages["Jane"]); // Removes "Jane"
print_r($ages); // Output: Array ( [John] => 25 [Peter] => 35 [Mark] => 40 )
?>
```

### **3.4 Multidimensional Arrays**

Multidimensional arrays contain one or more arrays. They are useful for storing data in a tabular form or any hierarchical structure.

#### **3.4.1 Creating Multidimensional Arrays**

You can create multidimensional arrays by nesting arrays inside other arrays.

**Example:**

```php
<?php
$students = array(
    "Alice" => array("Math" => 90, "Science" => 85),
    "Bob" => array("Math" => 80, "Science" => 88),
);

echo $students["Alice"]["Math"]; // Output: 90
?>
```

#### **3.4.2 Adding and Removing Elements**

You can add or remove elements in a multidimensional array just like in any other array.

**Example: Adding Elements**

```php
<?php
$students["Charlie"] = array("Math" => 75, "Science" => 82); // Adding new student
print_r($students);
?>
```

**Example: Removing Elements**

```php
<?php
unset($students["Bob"]); // Removes "Bob" and his scores
print_r($students);
?>
```

### **3.5 Traversing Arrays**

Traversing an array means accessing each element of the array one by one. PHP provides several ways to traverse arrays, including `foreach` loops and other functions.

#### **3.5.1 Using `foreach` Loop**

The `foreach` loop is specifically designed for traversing arrays.

**Example: Traversing an Indexed Array**

```php
<?php
$fruits = ["Apple", "Banana", "Orange"];

foreach ($fruits as $fruit) {
    echo "Fruit: $fruit <br>";
}
?>
```

**Example: Traversing an Associative Array**

```php
<?php
$ages = ["John" => 25, "Jane" => 30, "Peter" => 35];

foreach ($ages as $name => $age) {
    echo "$name is $age years old. <br>";
}
?>
```

### **3.6 Useful Array Functions**

PHP provides many built-in functions for working with arrays. Some of the most commonly used functions are:

- **`count()`**: Returns the number of elements in an array.
- **`array_merge()`**: Merges two or more arrays into one.
- **`array_diff()`**: Computes the difference between arrays.
- **`array_keys()`**: Returns all the keys of an array.
- **`array_values()`**: Returns all the values of an array.
- **`sort()`**: Sorts an indexed array in ascending order.
- **`rsort()`**: Sorts an indexed array in descending order.
- **`array_reverse()`**: Returns an array with elements in reverse order.
- **`in_array()`**: Checks if a value exists in an array.
- **`array_search()`**: Searches an array for a value and returns the key.

#### **Examples of Array Functions**

**Example: Using `count()` and `array_merge()`**

```php
<?php
$fruits = ["Apple", "Banana"];
$vegetables = ["Carrot", "Potato"];

echo "Number of fruits: " . count($fruits); // Output: 2

$merged = array_merge($fruits, $vegetables);
print_r($merged); // Output: Array ( [0] => Apple [1] => Banana [2] => Carrot [3] => Potato )
?>
```

**Example: Using `array_diff()` and `in_array()`**

```php
<?php
$array1 = ["a", "b", "c", "d"];
$array2 = ["c", "d", "e", "f"];

$difference = array_diff($array1, $array2);
print_r($difference); // Output: Array ( [0] => a [1] => b )

if (in_array("a", $array1)) {
    echo "a is in array1";
}
?>
```

### **3.7 Exercises for Chapter 3**

1. **Create an Indexed Array and Traverse It:** Create an indexed array of five cities and display them using a `foreach` loop.
   
2. **Create an Associative Array and Perform Operations:** Create an associative array to store the names and ages of three people. Add a new person to the array, then remove one of them.
   
3. **Work with Multidimensional Arrays:** Create a multidimensional array to store student names and their grades in three subjects. Write a script to display each student’s average grade.
   
4. **Use Array Functions:** Write a script that uses `array_merge()`, `array_diff()`, and `array_search()` functions to manipulate two arrays.

### **3.8 Summary of Chapter 3**

In this chapter, you learned about arrays in PHP, including indexed arrays, associative arrays, and multidimensional arrays. You also explored how to add, remove, and traverse arrays and learned about some of the most useful array functions. Arrays are a fundamental part of PHP programming, allowing you to manage collections of data efficiently. In the next chapter, we will delve into string manipulation and functions in PHP, which are essential for processing text data.

