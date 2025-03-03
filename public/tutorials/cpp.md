# C++ Tutorial

Written by Chris Shobe, 2025.

## Table of Contents
[C++ Tutorial](#c++-tutorial)
- [Table of Contents](#table-of-contents)
- [What is C++?](#introduction)
- [How to run C++](#installing-an-ide)
- [Basic Syntax and Structure](#basic-syntax-and-structure)
    - [Preprocessor Directives](#preprocessor-directives)
    - [Headers and Namespaces](#headers-and-namespaces)
    - [Commonly Used Headers](#commonly-used-headers)
    - [Comments](#comments)
    - [Input and Output](#input-and-output)
    - [New Lines](#new-lines)
    - [Variables and Data Types](#variables-and-data-types)
- [Loops](#loops)
    - for, for-each, while, do-while
- [Control Statements](#control-statements)
    - if-else, else-if, switch, break, continue, return
- [Functions](#function-calls)
    - [Function Definition](#function-definition)
    - [Function Calls](#function-calls)
    - [Void Functions](#void-functions)
    - [Function Parameters](#function-parameters)
    - [Function Overloading](#function-overloading)
- [Arrays](#arrays)
    - [Static Arrays](#static-arrays)
    - [Dynamic Arrays](#dynamic-arrays)
    - [Arrays of Objects](#arrays-of-objects)
    - [Searching Arrays of Objects](#searching-arrays-of-objects)
- [Vectors](#vectors)
    - [Accessing a Vector at an Index](#accessing-a-vector-at-an-index)
    - [Modifying Vectors](#modifying-vectors)
    - [Arrays vs Vectors](#arrays-vs-vectors)
- [Pointers and Memory Management](#pointers-and-memory-management)
    - [Stack vs Heap Memory](#stack-vs-heap-memory)
    - [Pointer Basics](#pointer-basics)
    - [Dynamic Memory Allocation](#dynamic-memory-allocation)
    - [Smart Pointers](#smart-pointers)
    - [Pointer Arithmetic](#pointer-arithmetic)
    - [The this Keyword](#the-this-keyword)
- [Object-Oriented Programming(OOP)](#object-oriented-programming-oop)
    - [Pointer Member Variables](#pointer-member-variables)

## Introduction

C++ was developed as an extension of C, sharing similar syntax but introducing Object-Oriented Programming (OOP) through classes and objects. This guide covers key differences between C++ and C, OOP principles, memory management, templating, and advanced C++ features.

**Motivation for Learning C++**:

Learning C++ can open doors to a wide range of applications. It's commonly used in system programming, game development, real-time simulations, and performance-critical applications due to its high efficiency and control over hardware. Whether you're building operating systems, game engines, or applications requiring high performance, C++ is a vital skill for developers.

**Comparison with Other Languages**:

C++ offers more control over system resources than higher-level languages like Python, Java, or C#. It provides direct memory manipulation and low-level features, making it a go-to choice for performance-critical and hardware-level tasks. While Python and Java are easier to use and focus more on developer productivity, C++ offers greater performance and flexibility, especially in resource-constrained environments.

## Installing an IDE
* VS Code (Recommended for development): Requires calling GCC locally.
* OnlineGDB (Browser-based option).
* Linux: Use SSH to connect to a remote machine instead of installing GCC locally.

**To see more information about insallation, refer to our C Tutorial. (add link here)**

## Basic Syntax and Structure

### Preprocessor Directives
Preprocessor directives are commands that are processed before the actual compilation starts.
* `#include` is used to include header files, making functions and objects available in your program.
* `#define` is used for defining constants or macros.

### Headers and Namespaces
Typically, when you start a file there will be some headers and namespaces at the top.
* Headers provide delcarations for standard functions and objects, enabling features such as input and output.
* Namespaces, like `std`, prevent naming conflicts by grouping related identifies, allowing shorthand usage.

**Example**
```cpp
#include <iostream>
using namespace std;
```
### Commonly Used Headers
| Header | Functionality |
| - | - |
| `<iostream>` | Input (`cin`), output (`cout`), error (`cerr`) |
| `<iomanip>` | Formatting output (`setprecision`, `setw`, `fixed`) |
| `<fstream>` | File I/O (`ifstream`, `ofstream`, `fstream`) |
| `<algorithm>` | Sorting, searching (`sort()`, `reverse()`, `binary_search()`) |
| `<cmath>` | Math functions (`sqrt()`, `pow()`, `abs()`) |
| `<cstdlib>` | Random numbers (`rand()`), conversions (`atoi()`, `atof()`) |
| `<vector>` | Dynamic Arrays |
| `<string>` | String Manipulation |

For a complete list and more, visit https://cplusplus.com/reference/.

### Comments
Comments are essential for code readability. You can write single-line comments using `//` and multi-line comments using `/* ... */`.
```cpp
// This is a single-line comment
/* This is a 
   multi-line comment */
```

### Input and Output
```cpp
cin >> x; //Input
cout << "Hello" << endl; //Output with flush
getline(cin, line); // Read full line
```
**If you do not add `using namespace std;`, you have to write `std::` in front of `cin` and `cout`.**

### Semicolons (`;`) in C++
C++ requires a semicolon (`;`) at the end of most statements to indicate the end of an instruction. Forgetting a semicolon will result in a compilation error.

Needed:
* At the end of variable declarations (`int x = 5;`).
* At the end of expressions (`cout << "Hello";`).
* After return statements (`return x + y;`).
* In loops and conditional statements, semicolons are only used inside statements, not after curly braces `{}`.

Not Needed:
* After function headers (`int add(int a, int b) {` → No semicolon).
* After control structures (`if`, `for`, `while`, `switch`, etc.).
* Before a block of code `{ ... }`.

### New Lines
There are two ways to create new lines: `\n` and `endl`
| Feature | `\n` | `endl` |
| - | - | - |
| Syntax | `cout << "Hello\n";` | `cout << "Hello" << endl;` |
| Flushes Buffer | no | yes |
| Performance | faster | slower | 
| Best For | normal output | immediate flushing (debugging, logging) |

### Variables and Data Types
| Type | Description |
| - | - |
| int | An integer ranging from -(2^31-1) to 2^31-1. |
| char | A single character (1 byte). |
| float | A floating-point number with up to 6 decimal of precision. |
| double | A floating-point number with up to 15 decimal places of precision. |
| bool | A Boolean variable that holds true (1) or false (0). | 
| void | A data type of "no type". Usually used for functions and pointers. |
| auto | Automatically deduces the type of a variable at compile time based on its assigned value. |
| const | A qualifier that makes a variable unmodifiable after initialization. Used for constant values. |

### Type Modifiers
Type modifiers can change the size or sign of data types. Some common type modifiers include:
* `unsigned`: Specifies non-negative values only.
* `short`: Reduces the range of integer types (typically used for smaller integer values).
* `long and long long`: Extend the range of integers.

### Type Casting
Type casting is the process of converting one data type to another.
* Implicit casting (or coercion) happens automatically when you assign a smaller data type to a larger one (e.g., int to double).
```cpp
int x = 10;
double y = x; // Implicit casting from int to double
```
* Explicit casting is done manually by the programmer using a cast operator.
```cpp
double x = 10.5;
int y = (int) x; // Explicit casting from double to int
```

## Loops
### For Loop (Count-Controlled Loop)
Used when the number of iterations is known beforehand.
```cpp
for (int i = 0; i < N; i++) {
    //Content
}
```

### For-Each Loop (Range-Based Loop)
Used to iterate over elements in arrays, vectors, or other containers.
```cpp
for (int x : v) {
    //Content
}
```

### While Loop (Condition-Controlled Loop)
Used when the number of iterations is unknown and depends on a condition.
```cpp
int i = 0;
while (i < N) {
    // Content
}
```

### Do-While Loop (Runs at Least Once)
Used when the loop should execute at least once, even if the condition is false.
```cpp
int i = 0;
do {
    // Content
} while (i < N);
```

## Control Statements
Conditional statements like if-else, else-if, and switch allow programs to make decisions by executing different blocks of code based on specific conditions.

**A Note About `{}`**
* If the condition controls only ONE statement, the brackets {} can be omitted.
* You can write the one statement on the same line or the line below the if statement.
* Best Practice: always use {}

### If-Else Statement
```cpp
//Standard statement with brackets
if(x > 0) {
    //code executes if x is greater than 0
} else {
    //code executes if x is not greater than 0
}
```

### Else-If Statement
```cpp
if (x > 0) {
    //content
} else if (x == 0) {
    //content
} else {
    //content
}
```
### Switch Statement
```cpp
switch(x) {
    case 1:
        cout << "x = one\n";
    case 2:
        cout << "x is two" << endl;
    default: //Executes if none of the cases match
        cout << "x is neither one nor two\n";
}
```

### break
The `break` statement immediately stops the execution of a loop or a `switch` case and moves to the next statement outside of it.

Using `break` in a Loop
```cpp
for (int i = 0; i < 10; i++) {
    if (i == 5) break; // Loop stops when i == 5
    cout << i << " ";
}
// Output: 0 1 2 3 4
```

Using `break` in a Switch Case
* Stops loop execution when a condition is met
* Prevents fall-through in `switch` statements
```cpp
switch (x) {
    case 1:
        cout << "x is one\n";
        break; // Exits the switch to prevent fall-through
    case 2:
        cout << "x is two\n";
        break;
    default:
        cout << "x is neither one nor two\n";
        break;
}
```

### continue
The `continue` statement skips the rest of the current loop iteration and moves to the next one.
* Used to skip certain iterations in a loop.
* Useful for filtering out specific values.
```cpp
for (int i = 0; i < 5; i++) {
    if (i == 2) continue; // Skips the iteration when i == 2
    cout << i << " ";
}
// Output: 0 1 3 4
```

### return
The `return` statement is used to exit a function and optionally return a value.
* Used in functions to return values.
* Can be used for early exit if a condition is met.
```cpp
int add(int a, int b) {
    return a + b; // Exits the function and sends the sum back to the caller
}
```

## Functions
Functions allow code reuse and modular programming by encapsulating logic into callable blocks. A function consists of a return type, a name, parameters (optional), and a body.

### Function Definition
A function is defined with a return type, a name, and optional parameters.
```cpp
int add(int a, int b) {
    return a + b;
}
```
* `int add(int a, int b)`: Declares a function named `add` that takes two integer parameters (`a` and `b`).
* `return a + b;`: Returns the sum of `a` and `b` to the caller.

### Function Calls
To execute a function, you need to call it with appropriate arguments.
```cpp
int result = add(5,3); //result = 8
```

### Void Functions
A `void` function peforms an action but does not return a value.
```cpp
void printMessage() {
    cout << "Hello from function !\n";
}
```
* The function `printMessage()` has a `void` return type. 
* Instead of returning something, it simply prints a message when called.
* This is useful for tasks like displaying messages, modifying global variables, or performing actions without needing a return value.

### Function Parameters
Functions can take parameters by value (copying the argument) or by reference (modifying the original value).

**Pass by Value (Default Behavior)**

The function receives a copy of the argument, and modifications inside the function do not affect the original variable.

```cpp
void increment(int num) {
    num += 1; // Only modifies the local copy
}
int main() {
    int x = 5;
    increment(x);
    cout << x; // Output: 5 (unchanged)
}
```

**Pass by Reference**

Using `&`, the function modifies the original variable directly.

```cpp
void incrementRef(int &num) {
    num += 1;
}
int main() {
    int x = 5;
    incrementRef(x);
    cout << x; // Output: 6 (modified)
}
```

### Default Arguments
C++ allows you to specify default values for function parameters. If no argument is provided during the function call, the default value is used.

```cpp
int add(int a, int b = 5) {
    return a + b;
}
```
**Function Call**:
```cpp
int result1 = add(10); // result1 = 10 + 5 = 15
int result2 = add(10, 20); // result2 = 10 + 20 = 30
```

### Inline Functions
An inline function is a function whose code is inserted directly into the place where the function is called. This can reduce function call overhead and increase performance for small, frequently called functions.

```cpp
inline int square(int x) {
    return x * x;
}
```
Use inline functions for small tasks where the overhead of a function call would be relatively expensive, but for larger functions, the performance gain may be negligible.

### Function Overloading
C++ allows multiple functions with the same name as long as their parameter lists differ. The compiler determines which function to call based on argument types.

```cpp
int multiply(int a, int b) {
    return a * b;
}

double multiply(double a, double b) {
    return a * b;
}

int main() {
    cout << multiply(3, 4);   // Calls int version: Output 12
    cout << multiply(2.5, 3); // Calls double version: Output 7.5
}
```

## Arrays
There are two main types of arrays in C++: **Static Arrays** and **Dynamic Arrays**.

### Static Arrays
Static arrays have a fixed size determined at compile time. The size cannot be changed after declaration, which makes them efficient but inflexible. Static arrays are typically used for small, fixed-size data structures.
```cpp
int array[5]; //creates an array that can contain 5 integers
```
* **Size**: Fixed at compile time, e.g., `array[5]`.
* **Memory Allocation**: Done at compile time, no runtime overhead.

### Dynamic Arrays
Dynamic arrays, on the other hand, are allocated at runtime. They are useful when the size of the array cannot be known in advance and needs to be changed dynamically. Dynamic arrays are managed through pointers, and require manual memory management to prevent memory leaks.
```cpp
int *array = new int[5]; //creates an array that can contain 5 integeers
delete[] array; //deallocates memory to prevent memory leaks
```
* **Size**: Can be dynamically changed.
* **Memory Allocation**: Done at runtime using `new` and `delete`.
* **Manual Management**: You need to manually allocate and deallocate memory.

### Arrays of Objects
An array of objects is an array where each element is an instance of a class. It can be used to store multiple instances of a class, allowing you to manipulate and access them as needed.
```cpp
class Person {
public:
    string name;
    int age;

    // Constructor to initialize Person objects
    Person(string n, int a) : name(n), age(a) {}
};

int main() {
    // Creating an array of 3 Person objects
    Person people[3] = {{"Alice", 30}, {"Bob", 25}, {"Charlie", 35}};

    // Accessing elements in the array
    cout << people[0].name << " is " << people[0].age << " years old.\n"; // Alice, 30
    cout << people[1].name << " is " << people[1].age << " years old.\n"; // Bob, 25
}
```
**Note: If you're unfamiliar with what a class is, make sure to check out the "Classes" section of this tutorial, where we explain the fundamentals of classes constructors, and object-oriented programming.**

### Searching Arrays of Objects
To search an array of objects, you can use a loop or algorithms like std::find_if. This allows you to search for a specific object based on one of its attributes.

Example using a loop:
```cpp
for (int i = 0; i < 3; ++i) {
    if (people[i].name == "Bob") {
        cout << "Found " << people[i].name << ", Age: " << people[i].age << endl;
    }
}
```

## Vectors
Vectors in C++ are dynamic arrays provided by the Standard Library. They can grow and shrink in size as needed and handle memory management automatically.
```cpp
#include <iostream> // Needed for cout
#include <vector> // Required to use vectors

using namespace std; // To avoid prefixing std::

vector<int> v; // Creates a vector of integers
v = {1, 2, 3, 4, 5}; // Initializes the vector with 5 integers
cout << v.front(); // Prints 1 (the first element)
cout << v.back();  // Prints 5 (the last element)
```
* **Automatic Size Management**: Vectors can change size dynamically.
* **Conveience**: Handles memory management automatically.

### Accessing a Vector at an Index
There are two ways to access elements in a vector:
| Feature | `v[i]` | `v.at()` |
| - | - | - |
| bounds checking | no | yes |
| speed | faster | slightly slower |
| safety | unsafe | safe |
| use case | when index is known to be valid | when safety is more important than speed |
```cpp
cout << v[0]; // Accesses the first element, no bounds checking
cout << v.at(0); // Accesses the first element, with bounds checking
```

### Modifying Vectors
You can modify vectors in various ways using built-in functions.
| Feature | Description |
| - | - |
| `v.push_back(10);`| adds an element (10) to the end of the vector |
| `v.pop_back();`| remove last element from the vector |
| `v.clear();`| remove all elements from the vector |
| `sort(v.begin(), v.end());`| sorts the vector in ascending order |

**Example**

```cpp
v.push_back(6); // Adds 6 to the end
v.pop_back();   // Removes the last element (5)
sort(v.begin(), v.end()); // Sorts the vector in ascending order
```
### Arrays vs Vectors
| Feature | Static Arrays | Vectors |
| - | - | - |
| size | fixed at compile-time | dynamic (grows/shrinks) |
| memory management | manual (need to free memory) | automatic (managed internally) |
| flexibility | inflexible | flexible, can resize |
| ease of use | more manual (e.g., no bounds checking) | easier to use, with bounds checking |

## Pointers and Memory Management
### Stack vs Heap Memory
**Stack**: Stores local variables. Memory is automatically managed and automatically deallocated when the variable goes out of scope. It's generally faster but limited in size.
**Heap**: Stores dynamically allocated memory. You must manually allocate and deallocate memory using `new` and `delete`. It offers more flexibility but requires careful memory management to avoid leaks.

### Pointer Basics
A pointer is a variable that stores the memory address of another variable.

**Declaration**: `int* ptr = &x;`
* `ptr` stores the address of `x`.

**Dereferencing**: `cout << *ptr;`
* This accesses the value stored at the address `ptr` points to.

**Example**
```cpp
int x = 10;
int* ptr = &x; // Pointer to x
cout << *ptr;   // Dereferencing the pointer to print the value of x, which is 10
```

### Dynamic Memory Allocation
In C++, memory for variables can be allocated dynamically at runtime using `new` and deallocated using `delete`. This is done on the heap.

**Single Variable**:
```cpp
int* ptr = new int;   // Dynamically allocate memory for a single integer
*ptr = 5;             // Assign value 5 to the dynamically allocated integer
delete ptr;           // Deallocate memory
```

**Array**:
```cpp
int* arr = new int[5]; // Dynamically allocate memory for an array of 5 integers
delete[] arr;          // Deallocate memory for the array
```

**Note: Failing to `delete` dynamically allocated memory results in memory leaks, which can slow down or crash your program due to excessive memory usage.**

### Smart Pointers
Smart pointers are wrappers around raw pointers that help manage memory automatically, preventing memory leaks. Examples include:
* unique_ptr: Manages a single object and automatically deletes it when it goes out of scope.
* shared_ptr: Allows shared ownership of an object; the object is deleted when the last shared_ptr goes out of scope.
* weak_ptr: Does not affect the reference count, used to avoid circular references.

### Pointer Arithmetic
Pointers in C++ can be incremented or decremented, allowing you to traverse arrays and other data structures directly.

**Example**
```cpp
int arr[] = {1, 2, 3, 4, 5};
int* ptr = arr;    // Pointer points to the first element of the array

cout << *ptr;      // Dereference to print 1
ptr++;             // Move pointer to the next element
cout << *ptr;      // Dereference to print 2
```

### The this Keyword
The `this` pointer is a special pointer that refers to the current object in a member function. It's often used to differentiate between member variables and parameters with the same name.

```cpp
class MyClass {
public:
    int x;
    MyClass(int x) { this->x = x; } // 'this->x' refers to the member variable
};
```
* `this->x` refers to the member variable, while `x` refers to the constructor parameter

## Object-Oriented Programming (OOP)
Object-Oriented Programming (OOP) is organized around objects rather than actions and data rather than logic. It allows for more efficient, modular, and reusable code by structuring the program into different entities known as objects.

Four Major Principles of OOP:
1. **Encapsulation**: Hiding implementation details by using private variables and public accessor (getter) and mutator (setter) methods.
2. **Data Abstraction**: Focuses on the "what" an object does rather than "how" it does it.
3. **Polymorphism**: Allows one function or operator to work in multiple ways based on context. This can be achieved via function overloading or overriding, and operator overloading.
4. **Inheritance**: Defines relationships between objects, where one class can inherit properties and behaviors from another.

### Classes and Objects
**Class Definition**: A class serves as a blueprint for creating objects. It defines the properties and behaviors common to all objects of that class.
```cpp
class Person {
public:
    string name;
    int age;
    void introduce() {
        cout << "Hello, my name is " << name << " and I am " << age << " years old." << endl;
    }
};
```

**Creating an Object**: An object is an instance of a class.
```cpp
Person p;
p.name = "Alice";
p.age = 30;
p.introduce();
```

**Access Modifiers in Classes**
1. **Public**: Accessible by any part of the program.
2. **Private**: Accessible only within the class itself (for encapsulation).
3. **Protected**: Accessible within the class and its derived classes (used in inheritance).

### Constructors and Destructors
**Constructors**: Special member functions used to initialize objects when they are created. Constructors have the same name as the class and are called automatically when an object is created.

**Example Constructor**:
```cpp
class Person {
public:
    string name;
    int age;

    // Constructor to initialize name and age
    Person(string n, int a) {
        name = n;
        age = a;
    }
};
```

**Copy Constructor**: A special constructor used to create a new object as a copy of an existing object.
```cpp
Person(const Person &other) {
    name = other.name;
    age = other.age;
}
```

**Destructors**: Special member functions called when an object is destroyed. They are used to release resources, such as memory, when an object is no longer needed.
```cpp
~Person() {
    cout << "Destructor called for " << name << endl;
}
```

### Encapsulation
Encapsulation ensures that the internal state of an object is protected from unintended or harmful modifications.

**Getters**: Functions used to retrieve the values of private member variables. 

**Setters**: Functions used to set the values of private member variables.

**Example with Getters and Setters**:
```cpp
class Person {
private:
    string name;
    int age;

public:
    // Getter for name
    string getName() {
        return name;
    }

    // Setter for name
    void setName(string n) {
        name = n;
    }

    // Getter for age
    int getAge() {
        return age;
    }

    // Setter for age
    void setAge(int a) {
        age = a;
    }

    void introduce() {
        cout << "Hello, my name is " << name << " and I am " << age << " years old." << endl;
    }
};
```

### Operator Overloading
Operator overloading allows you to define custom behaviors for operators like `+`, `-`, etc., when used with objects of user-defined types.

**Example Operator Overloading (`+` for adding two `Person` objects)**: 
```cpp
class Person {
public:
    string name;
    int age;

    // Constructor
    Person(string n, int a) {
        name = n;
        age = a;
    }

    // Overloading the + operator
    Person operator+(const Person &other) {
        Person result(name + " & " + other.name, age + other.age);
        return result;
    }
};
```

### Inheritance
Inheritance allows you to create a new class based on an existing class. The new class (derived class) inherits properties and methods from the base class.
```cpp
class Animal {
public:
    string species;
    void speak() {
        cout << "Animal sound!" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() {
        cout << "Bark!" << endl;
    }
};

Dog d;
d.speak();  // Outputs: "Bark!"
```

### Polymorphism
Polymorphism allows objects of different classes to be treated as objects of a common base class. This enables the same method to perform different actions based on the object type.

Virtual functions allow for dynamic dispatch and enable runtime polymorphism. They make it possible to override a method in a derived class and call the overridden method through a base class pointer or reference. Without virtual functions, polymorphism would only be possible at compile-time (static polymorphism), not at runtime.

For the following examples the speak() method is defined in both the base class (Animal) and the derived classes (Dog and Cat), so calling speak() on an object will invoke the version of the method corresponding to the actual class of the object. This is **method overloading**.

**Example with Virtual Functions**:
```cpp
class Animal {
public:
    virtual void speak() {  // Virtual function
        cout << "Animal sound!" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {  // Override the base class function
        cout << "Bark!" << endl;
    }
};

Animal *a = new Dog();
a->speak();  // Outputs: "Bark!" because Dog's version of speak() is called
```

**Example without Virtual Functions**:
```cpp
class Animal {
public:
    void speak() {
        cout << "Animal sound!" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() {
        cout << "Bark!" << endl;
    }
};

class Cat : public Animal {
public:
    void speak() {
        cout << "Meow!" << endl;
    }
};

int main() {
    Animal a;
    Dog d;
    Cat c;

    a.speak();  // Outputs: "Animal sound!"
    d.speak();  // Outputs: "Bark!"
    c.speak();  // Outputs: "Meow!"
    
    return 0;
}
```

### Abstract Data Types (ADTs) and Classes
An Abstract Data Type (ADT) defines a data structure by its behavior (what it does) rather than how it does it. ADTs are often implemented using abstract classes and pure virtual functions.

**Example of an ADT using an abstract class**:
```cpp
class Shape {
public:
    virtual void draw() = 0;  // Pure virtual function, making Shape an abstract class
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle." << endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing a square." << endl;
    }
};
```
### Pointer Member Variables
Classes may have pointer member variables, which require careful memory management (allocation and deallocation) to avoid memory leaks.

**Example**
```cpp
class MyClass {
    int* data; // Pointer member variable
public:
    MyClass(int val) { data = new int(val); } // Dynamically allocate memory in constructor
    ~MyClass() { delete data; }               // Deallocate memory in destructor
};
```
* The `data` pointer is dynamically allocated in the constructor.
* The destructor ensures that the allocated memory is properly deallocated when the object is destroyed.

### Using Objects in Arrays
In OOP, you may need to store objects in arrays for efficient management of multiple instances. In addition to statically allocating arrays, you can also dynamically allocate memory for arrays of objects, which gives you more control over the memory usage and size of the array.

**Static Arrays of Objects**

As shown in the Arrays section, static arrays of objects are straightforward, but they are fixed in size. You create them with a predetermined number of elements:
```cpp
Person people[3]; // Static array of 3 Person objects
```

**Dynamic Arrays of Objects**
You can store objects in arrays, but keep in mind that arrays of objects may not be as flexible as vectors for dynamic resizing.

```cpp
Person people[3];  // Array of objects

people[0].name = "Alice";
people[0].age = 30;

people[1].name = "Bob";
people[1].age = 25;
```