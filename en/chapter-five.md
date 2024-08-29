
---

### **Chapter 5: Object-Oriented Programming (OOP)**

---

Object-Oriented Programming (OOP) is a paradigm that organizes code using objects and classes. This chapter provides an in-depth exploration of OOP concepts in PHP, including classes, objects, inheritance, encapsulation, polymorphism, abstract classes, and interfaces. Each concept is illustrated with practical examples to facilitate understanding.

### **5.1 Introduction to Classes and Objects**

In OOP, a class is a blueprint for creating objects. Objects are instances of classes that contain both data (properties) and functions (methods).

#### **5.1.1 Defining a Class**

A class is defined using the `class` keyword, followed by the class name. Inside a class, you can define properties and methods.

**Example:**

```php
<?php
class Car {
    // Property
    public $color;

    // Method
    public function setColor($color) {
        $this->color = $color;
    }

    public function getColor() {
        return $this->color;
    }
}
?>
```

- **Properties**: Variables that belong to the class.
- **Methods**: Functions that belong to the class and operate on its properties.

#### **5.1.2 Creating an Object**

An object is an instance of a class created using the `new` keyword. Once created, you can access the object's properties and methods.

**Example:**

```php
<?php
// Create an object of the Car class
$myCar = new Car();

// Set the color property
$myCar->setColor("Red");

// Get and display the color property
echo "The color of the car is " . $myCar->getColor(); // Output: The color of the car is Red
?>
```

### **5.2 Inheritance**

Inheritance allows a class (child class) to inherit properties and methods from another class (parent class). This promotes code reuse and a hierarchical class structure.

#### **5.2.1 Extending a Class**

A child class extends a parent class using the `extends` keyword.

**Example:**

```php
<?php
// Parent class
class Vehicle {
    public $brand;

    public function setBrand($brand) {
        $this->brand = $brand;
    }

    public function getBrand() {
        return $this->brand;
    }
}

// Child class
class Car extends Vehicle {
    public $color;

    public function setColor($color) {
        $this->color = $color;
    }

    public function getColor() {
        return $this->color;
    }
}

// Create an object of the Car class
$myCar = new Car();
$myCar->setBrand("Toyota");
$myCar->setColor("Blue");

echo "The car brand is " . $myCar->getBrand(); // Output: The car brand is Toyota
echo "The car color is " . $myCar->getColor(); // Output: The car color is Blue
?>
```

- **Parent Class**: The class being inherited from.
- **Child Class**: The class that inherits from the parent class.

### **5.3 Encapsulation**

Encapsulation refers to the bundling of data (properties) and methods that operate on the data into a single unit (class). It also involves restricting access to some of the object's components to protect the integrity of the data.

#### **5.3.1 Visibility Keywords**

- **`public`**: Accessible from any context.
- **`protected`**: Accessible only within the class itself and by inheriting classes.
- **`private`**: Accessible only within the class itself.

**Example:**

```php
<?php
class Person {
    private $name; // Private property

    public function setName($name) {
        $this->name = $name;
    }

    public function getName() {
        return $this->name;
    }
}

$person = new Person();
$person->setName("Alice");
echo "The person's name is " . $person->getName(); // Output: The person's name is Alice
?>
```

### **5.4 Polymorphism**

Polymorphism allows objects of different classes to be treated as objects of a common superclass. It is achieved through method overriding and interfaces.

#### **5.4.1 Method Overriding**

Method overriding allows a subclass to provide a specific implementation of a method that is already defined in its parent class.

**Example:**

```php
<?php
class Animal {
    public function makeSound() {
        echo "Some generic animal sound";
    }
}

class Dog extends Animal {
    public function makeSound() {
        echo "Bark";
    }
}

$myDog = new Dog();
$myDog->makeSound(); // Output: Bark
?>
```

#### **5.4.2 Interfaces**

An interface defines a contract with methods that implementing classes must provide. Interfaces enable polymorphism by ensuring that different classes adhere to a common set of methods.

**Example:**

```php
<?php
interface AnimalInterface {
    public function makeSound();
}

class Cat implements AnimalInterface {
    public function makeSound() {
        echo "Meow";
    }
}

$myCat = new Cat();
$myCat->makeSound(); // Output: Meow
?>
```

### **5.5 Abstract Classes**

Abstract classes are classes that cannot be instantiated on their own. They are meant to be extended by other classes. Abstract classes can have abstract methods that must be implemented by any subclass.

**Example:**

```php
<?php
abstract class Shape {
    abstract public function area();

    public function describe() {
        echo "I am a shape.";
    }
}

class Circle extends Shape {
    private $radius;

    public function __construct($radius) {
        $this->radius = $radius;
    }

    public function area() {
        return pi() * pow($this->radius, 2);
    }
}

$circle = new Circle(5);
echo "The area of the circle is " . $circle->area(); // Output: The area of the circle is 78.539816339745
?>
```

### **5.6 Advanced OOP Concepts**

#### **5.6.1 Traits**

Traits are a mechanism for code reuse in single inheritance languages like PHP. Traits allow you to include methods in multiple classes.

**Example:**

```php
<?php
trait Logger {
    public function log($message) {
        echo "Log: " . $message;
    }
}

class User {
    use Logger;
}

$user = new User();
$user->log("User has logged in."); // Output: Log: User has logged in.
?>
```

#### **5.6.2 Namespaces**

Namespaces provide a way to group logically related classes, interfaces, functions, and constants. They help avoid name conflicts.

**Example:**

```php
<?php
namespace MyProject;

class MyClass {
    public function sayHello() {
        echo "Hello from MyClass!";
    }
}

$object = new MyClass();
$object->sayHello(); // Output: Hello from MyClass!
?>
```

### **5.7 Best Practices**

- **Keep Classes Focused:** Each class should have a single responsibility or purpose.
- **Use Interfaces and Traits:** To ensure that your classes remain flexible and adhere to design principles.
- **Encapsulate Implementation Details:** Hide the internal workings of a class from the outside world to reduce complexity and increase maintainability.

---

## **Exercises for Chapter 5**

1. **Class Definition Exercise:**
   Define a class called `Book` with properties for title, author, and publication year. Include methods to set and get these properties. Create an object and display the book details.

2. **Inheritance Exercise:**
   Create a parent class `Animal` with a method `makeSound()`. Extend this class with subclasses `Dog` and `Cat`, each providing their own implementation of `makeSound()`. Demonstrate polymorphism by calling the `makeSound()` method on instances of `Dog` and `Cat`.

3. **Encapsulation Exercise:**
   Create a class `BankAccount` with private properties for account number and balance. Provide public methods to deposit and withdraw funds. Ensure that the balance cannot be directly accessed or modified from outside the class. Demonstrate these methods with an example.

4. **Polymorphism Exercise:**
   Define an interface `PaymentMethod` with a method `processPayment()`. Implement this interface in classes `CreditCard` and `PayPal`, each providing a different implementation of `processPayment()`. Create objects and demonstrate the use of polymorphism.

5. **Abstract Class Exercise:**
   Define an abstract class `Vehicle` with an abstract method `getFuelEfficiency()`. Extend this class with concrete classes `Car` and `Truck`, each providing their own implementation of `getFuelEfficiency()`. Display the fuel efficiency of both types of vehicles.

6. **Trait Usage Exercise:**
   Create a trait `Logger` with a method `log()`. Use this trait in different classes, such as `User` and `Order`. Demonstrate how traits can be used to share methods across classes.

7. **Namespace Exercise:**
   Define a namespace `App\Models` and create a class `User` within it. Demonstrate how to use this class by creating an instance and calling its methods outside the namespace.

---

## **Summary of Chapter 5**

In this chapter, we explored Object-Oriented Programming (O

OP) in PHP in great detail. We covered fundamental concepts such as classes, objects, inheritance, encapsulation, polymorphism, and abstract classes. We also examined advanced topics like traits and namespaces. Mastery of these OOP principles will enable you to build well-structured, modular, and maintainable PHP applications.

---
