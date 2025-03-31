# C++ Tutorial

Written by Chris Shobe, 2025 (Updated for C++ 20).

## Table of Contents
[C++ Tutorial](cpp.md)
- Fundamentals
    - [Introduction](#introduction)
    - [Prerequisites](#prerequisites)
    - [Installing an IDE](#installing-an-ide)
        - [Compiler Flags](#compiler-flags)
    - [Basic Syntax and Structure](#basic-syntax-and-structure)
        - [Headers and Namespaces](#headers-and-namespaces)
        - [The `main()` Function](#the-main-function)
        - [Variables and Data Types](#variables-and-data-types)
        - [Type Modifers and Casting](#type-modifiers-and-casting)
        - [Input and Output](#input-and-output)
        - [New Lines](#new-lines)
        - [Semicolons (`;`)](#semicolons)
        - [Comments](#comments)
        - [Commonly Used Headers](#commonly-used-headers)
- [Control Flow](#control-flow)
    - Loops: [For](#for-loop-count-controlled-loop), [For-Each](#for-each-loop-range-based-loop), [While](#while-loop-condition-controlled-loop), [Do-While](#do-while-loop-runs-at-least-once)
    - [If-Else Statement](#if-else-statement)
    - [Dangling Else Problem](#dangling-else-problem)
    - [Switch Statement](#switch-statement)
    - [Ternary Operator](#ternary-operator)
    - [break](#break) / [continue](#continue) / [return](#return)
- [Functions](#functions)
    - [Definition and Calls](#function-definition-and-calls)
    - [Prototypes](#function-prototypes)
    - [Parameters (Pass by Value/Reference)](#function-parameters)
    - [Default Arguments](#default-arguments)
    - [Inline Functions](#inline-functions)
    - [Overloading](#function-overloading)
    - [Lambda Functions](#lambda-functions)
    - [Recursion](#recursion)
- [Templating](#templating)
    - [Function Templates](#function-templates)
    - [Class Templates](#class-templates)
    - [Template Specialization](#template-specialization)
- Data Structures
    - [Arrays](#arrays)
        - [Static Arrays](#static-arrays)
        - [Dynamic Arrays](#dynamic-arrays)
        - [Arrays of Objects](#arrays-of-objects)
        - [Operations](#array-operations)
    - [Vectors](#vectors)
        - [Essential Operations](#essential-vector-operations)
        - [Advanced Usage](#advanced-vector-usage)
        - [Performance Considerations](#vector-performance-considerations)
- [Memory Management](#memory-management)
    - [Stack vs Heap Memory](#stack-vs-heap-memory)
    - Pointers
        - [Basics](#pointer-basics)
        - [Arithmetic](#pointer-arithmetic)
        - [`this` Keyword](#the-this-keyword)
        - [Smart Pointers](#smart-pointers)
            - `unique_ptr` / `shared_ptr` / `weak_ptr`
- [Arrays vs Vectors vs Smart Pointers](#arrays-vs-vectors-vs-smart-pointers)
- [Object-Oriented Programming](#object-oriented-programming-oop)
    - [Four Principles](#four-major-principles-of-oop)
    - [Classes and Objects](#classes-and-objects)
    - [Constructors and Destructors](#constructors-and-destructors)
    - [Encapsulation](#encapsulation)
    - [Static Members](#static-members)
    - [Abstraction](#abstraction)
    - [Inheritance](#inheritance)
    - [Polymorphism](#polymorphism)
    - [Virtual Functions](#virtual-functions)
    - [Operator Overloading](#operator-overloading)
    - [Rule of Five](#rule-of-five)
    - [Friend Functions and Friend Classes](#friend-functions-and-friend-classes)

## Introduction

C++ was created by Bjarne Stroustrup in 1985 as "C with Classes." It has evolved through major standards:
- C++11 (Smart Pointers, auto)
- C++14/17 (FileSystem, Structured Bindings)
- C++20 (Ranges, Concepts)

**Motivation for Learning C++**:

- Used in game engines (Unreal), trading systems, embedded devices
- Combines high-level abstractions with low-level control
- Faster than Python/Java; more modern than C

**Hello World Example**
```cpp
#include <iostream>
int main() {
    std::cout << "Hello, C++20!\n";  // \n is faster than endl
    return 0;
}
```

## Prerequisites
- Basic programming knowledge (variables, loops)
- For absolute beginners: Start with our [C](c.md) or [Python](python.md) Tutorials

## Installing an IDE
* VS Code (Recommended for development): Requires calling GCC locally.
* OnlineGDB (Browser-based option).
* CLion (Best for large projects).
* Linux: Use SSH to connect to a remote machine instead of installing GCC locally.

### Compiler Flags
```cpp
g++ -std=c++20 -Wall -Wextra program.cpp -o program
```

**To see more information about installation, refer to our [C Tutorial](c.md).**

## Basic Syntax and Structure

### Headers and Namespaces
Typically, when you start a file there will be some headers and namespaces at the top.
* Headers provide declarations for standard functions and objects, enabling features such as input and output.
* Namespaces, like `std`, prevent naming conflicts by grouping related identifies, allowing shorthand usage.

**Example**
```cpp
#include <iostream>
using namespace std;
```

### The main() Function
The `main()` function is the entry point of every C++ program. Execution starts from `main()`, and it typically returns an integer value to indicate successful completion.

### Variables and Data Types
| Type | Description |
| - | - |
| int | An integer ranging from -(2^31-1) to 2^31-1. |
| char | A single character (1 byte). |
| float | A floating-point number with up to 6 decimal of precision. |
| double | A floating-point number with up to 15 decimal places of precision. |
| bool | A Boolean variable that holds true (1) or false (0). | 
| void | Represents 'no type'. Commonly used for functions that do not return a value and for generic pointers. |
| auto | Automatically deduces the type of a variable at compile time based on its assigned value. |
| const | Deduces the type of a variable at compile time based on its initializer. This improves flexibility but should be used carefully to maintain readability. |

### Type Modifiers and Casting
Type modifiers can change the size or sign of data types. Some common type modifiers include:
* `unsigned`: Specifies non-negative values only.
* `short`: Reduces the range of integer types (typically used for smaller integer values).
* `long and long long`: Extend the range of integers.

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

### Input and Output
```cpp
#include <iostream>  // for cin and cout
#include <iomanip>   // for formatting functions
using namespace std;

int main() {
    string x, line;
    
    cin >> x; // Input
    cout << "Hello, World" << endl; // Output with flush

    getline(cin, line); // Read full line
    
    cout << fixed << setprecision(2) << 3.14159 << endl; // Outputs 3.14

    // Example use of setw
    int num = 42;
    cout << setw(10) << num << endl; // Outputs "        42" (right-aligned, width 10)

    return 0; // indicates successful program execution
}
```
**If you do not add `using namespace std;`, you have to write `std::` in front of `cin` and `cout`.**

### New Lines
There are two ways to create new lines: `\n` and `endl`
| Feature | `\n` | `endl` |
| - | - | - |
| Syntax | `cout << "Hello\n";` | `cout << "Hello" << endl;` |
| Flushes Buffer | no | yes |
| Performance | faster | slower | 
| Best For | normal output (preferred for efficiency) | forcing immediate output (useful for debugging) |

### Semicolons
C++ requires a semicolon (`;`) at the end of most statements to indicate the end of an instruction. Forgetting a semicolon will result in a compilation error.

Needed:
* At the end of variable declarations (`int x = 5;`).
* At the end of expressions (`cout << "Hello";`).
* After return statements (`return x + y;`).
* In loops and conditional statements, semicolons are only used inside statements, not after curly braces `{}`.

### Comments
Comments are essential for code readability. You can write single-line comments using `//` and multi-line comments using `/* ... */`.
```cpp
// This is a single-line comment
/* This is a 
   multi-line comment */
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

## Control Flow
### For Loop (Count-Controlled Loop)
Used when the number of iterations is known beforehand.
```cpp
for (int i = 0; i < 5; i++) {
    cout << i << " ";  // Output: 0 1 2 3 4
}
```

### For-Each Loop (Range-Based Loop)
Used to iterate over elements in arrays, vectors, or other containers. The `auto` keyword can simplify the syntax.
```cpp
vector<int> nums = {1, 2, 3};
for (int n : nums) {  // By value (copy)
    cout << n << " ";
}
for (const auto& n : nums) {  // By const reference
    cout << n << " ";
}
```

### While Loop (Condition-Controlled Loop)
Used when the number of iterations is unknown and depends on a condition. The condition is checked before each iteration.
```cpp
int input;
do {
    cout << "Enter a positive number: ";
    cin >> input;
} while (input <= 0);  // Repeats until valid input
```

### Do-While Loop (Runs at Least Once)
Used when the loop should execute at least once, even if the condition is false. The condition is checked after each iteration.
```cpp
int number;
do {
    cout << "Enter a positive number: ";
    cin >> number;
} while (number <= 0);
```

Conditional statements like if-else, else-if, and switch allow programs to make decisions by executing different blocks of code based on specific conditions.

**Best Practice**: Always use braces {} to avoid the "dangling else" problem.

### If-Else Statement
```cpp
if (temperature > 30) {
    cout << "Hot day!";
} else if (temperature > 20) {
    cout << "Pleasant weather.";
} else {
    cout << "Cool or cold.";
}
```

### Dangling Else Problem
```cpp
// Potentially ambiguous
if (x > 0)
    if (x < 10)
        cout << "0-10";
else
    cout << "Negative?";  // Actually belongs to inner if!

// Clearer version
if (x > 0) {
    if (x < 10) {
        cout << "0-10";
    }
} else {
    cout << "Non-positive";
}
```

### Switch Statement
Used to compare a variable against multiple values. The `break` statement prevents fall-through, and the `default` case handles unexpected values. This only works with integral types (int, char, enum).
```cpp
enum Color {RED, GREEN, BLUE};
Color c = GREEN;

switch(c) {
    case RED: 
        cout << "Red";
        break;
    case GREEN:
        cout << "Green";
        break;
    case BLUE:
        cout << "Blue";
        break;
    default:
        cout << "Unknown";
}
```

### Ternary Operator
A shorthand for simple if-else statements.
```cpp
int max = (a > b) ? a : b;
```
In this example it asks if a is greater than b. If it is true, a is returned. If it is false, b is returned.

### break
The `break` statement immediately stops the execution of a loop or a `switch` case and moves to the next statement outside of it.

Using `break` in a Loop
```cpp
for (int i = 0; i < 10; i++) {
    if (i == 5) break;  // Exits loop when i reaches 5
    cout << i << " ";   // Output: 0 1 2 3 4
}
```

### continue
The `continue` statement skips the rest of the current loop iteration and moves to the next one.
* Used to skip certain iterations in a loop.
* Useful for filtering out specific values.
```cpp
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;  // Skips printing 2
    cout << i << " ";      // Output: 0 1 3 4
}
```
**Warning**: In while loops, ensure the loop variable updates:
```cpp
int i = 0;
while (i < 5) {
    if (i == 2) {
        i++;  // Essential to prevent infinite loop
        continue;
    }
    cout << i << " ";
    i++;
}
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

### Common Pitfalls
- Forgetting break in switch statements
- Using = instead of == in conditions
- Memory leaks from new without delete
- Array index out of bounds
- Uninitialized variables

## Functions
Functions encapsulate reusable logic into callable blocks, promoting modular programming. A function consists of:
* Return type (or void)
* Name
* Parameters (optional)
* Body containing executable code

### Function Definition and Calls
```cpp
// Function definition
int add(int a, int b) {    // Parameters a and b
    return a + b;          // Returns sum
}

int main() {
    int result = add(5, 3); // Function call (arguments 5 and 3)
    cout << result;         // Output: 8
    return 0;
}
```
**Key Components**
1. Return Type: int, double, string, void (no return value), auto (automatic type deduction)
2. Parameters: Passed by Value (copy) by default OR Passed by Reference (&)

### Function Prototypes
Allow calling functions before their definition:
```cpp
// Prototype (declaration)
double calculateInterest(double principal, int years);

int main() {
    cout << calculateInterest(1000, 5); // Works despite definition coming later
}

// Definition
double calculateInterest(double p, int y) { return p * y * 0.05; }
```

### Function Parameters
Functions can take parameters by value (copying the argument) or by reference (modifying the original value).

**Pass by Value (Default Behavior)**

The function receives a copy of the argument, and modifications inside the function do not affect the original variable.

```cpp
void incrementByValue(int x) {
    x++;  // Only modifies the local copy
    cout << "Inside function (by value): " << x << endl;
}
```

**Pass by Reference**

Using `&`, the function modifies the original variable directly.

```cpp
void incrementByReference(int &x) {
    x++;  // Modifies the original
    cout << "Inside function (by reference): " << x << endl;
}
```

**Pass by Const Reference**

The function recieves read-only access to the original variable. This is best practice for large objects.

```cpp
void printLargeData(const string &bigData) {
    // bigData[0] = 'A'; // COMPILER ERROR - can't modify
    cout << "Data (by const reference): " << bigData << endl;
}
```

**Comparison Table**

| Method | Example Call | Can Modify Original? | Memory Usage | Typical Use Case |
| - | - | - | - | - |
| Pass by Value | func(x) | No | Higher | Small Primitive Types |
| Pass by Reference | func(&x) | Yes | Lowest | Output Parameters |
| Pass by Const Ref | func(const &x) | No | Lowest | Large Read-Only Data |

### Default Arguments
C++ allows you to specify default values for function parameters. If no argument is provided during the function call, the default value is used.

```cpp
void log(string msg, bool timestamp = true) {
    if (timestamp) cout << "[LOG] " << time() << ": ";
    cout << msg;
}

log("Hello");       // Auto-adds timestamp
log("Error", false); // No timestamp
```

### Inline Functions
An inline function is a function whose code is inserted directly into the place where the function is called. This can reduce function call overhead and increase performance for small, frequently called functions.

```cpp
inline int square(int x) { return x*x; }
```
**Best Practice**: Use only for very small functions (1-3 lines)

### Function Overloading
C++ allows multiple functions with the same name as long as their parameter lists differ. The compiler determines which function to call based on argument types.

```cpp
void print(int i) { cout << "Integer: " << i; }
void print(double d) { cout << "Double: " << d; }
void print(const string& s) { cout << "String: " << s; }
```

### Lambda Functions
Lambda functions are anonymous functions that can be defined inline.
```cpp
auto sum = [](int a, int b) { return a + b; };
cout << sum(3, 4);  // 7

// With captures
int x = 10;
auto adder = [x](int y) { return x + y; };
cout << adder(5);  // 15
```

### Recursion
A function that calls itself is called a recursive function. Recursion is useful for problems that can be broken down into smaller, similar subproblems.

```cpp
int factorial(int n) {
    if (n <= 1) return 1;       // Base case
    return n * factorial(n-1);  // Recursive case
}
```
**Warning**: Deep recursion may cause stack overflow

## Templating
Templates enable generic programming by allowing functions/classes to operate with any data type. They are key to STL containers like vector<T>.

### Function Templates
```cpp
// Basic template
template <typename T>  // or 'class T'
T max(T a, T b) {
    return (a > b) ? a : b;
}

// Usage
std::cout << max(3, 5);      // int
std::cout << max(3.14, 2.5); // double
```
**Multiple Types**
```cpp
template <typename T, typename U>
auto mixedAdd(T a, U b) {
    return a + b;  // Return type deduced as decltype(a + b)
}
```

### Class Templates
```cpp
template <typename T>
class Box {
    T contents;
public:
    void set(const T& item) { contents = item; }
    T get() const { return contents; }
};

// Usage
Box<int> intBox;
intBox.set(42);
```
**Default Template Arguments**
```cpp
template <typename T = int>  // Defaults to 'int'
class Container { /*...*/ };

Container<> defaultContainer;  // Uses 'int'
```

### Template Specialization
Customize behavior for specific types:
```cpp
// General template
template <typename T>
class Printer {
public:
    void print(const T& value) {
        std::cout << "Value: " << value << '\n';
    }
};

// Specialization for bool
template <>
class Printer<bool> {
public:
    void print(bool value) {
        std::cout << "Bool: " << (value ? "true" : "false") << '\n';
    }
};
```

### Best Practices
- Prefer typename over class in templates (more readable).
- Use constraints (C++20) instead of static_assert.
- Avoid complex metaprogramming unless necessary.
- Document template requirements (e.g., "T must be comparable").

### Common Pitfalls
- Missing Definitions: Template code must be in headers.
- Opaque Errors: Use static_assert for clearer messages.
- Bloat: Each instantiation creates new code—avoid excessive types.

## Arrays
Arrays are used to store multiple values of the same type in a single variable. There are two main types of arrays in C++: **Static Arrays** and **Dynamic Arrays**.

### Static Arrays
Static arrays have a fixed size determined at compile time. The size cannot be changed after declaration, which makes them efficient but inflexible. They are stack-allocated memory with no bounds checking.
```cpp
// Declaration and initialization
int numbers[5];               // Uninitialized array (contains garbage values)
int primes[] = {2, 3, 5, 7};  // Size automatically determined (4 elements)
int matrix[2][3] = {          // 2D array
    {1, 2, 3},
    {4, 5, 6}
};

// Best practices:
1. Always initialize arrays to avoid undefined behavior
int safeArray[5] = {};  // All elements zero-initialized

2. Use sizeof() to get array size (only works for stack arrays)
size_t size = sizeof(primes)/sizeof(primes[0]);

3. Prefer std::array for fixed-size arrays (type-safe, bounds checking)
#include <array>
std::array<int, 4> modernArray = {1, 2, 3, 4};
```

### Dynamic Arrays
Dynamic arrays, on the other hand, are allocated at runtime. They are useful when the size of the array cannot be known in advance and needs to be changed dynamically. Dynamic arrays are managed through pointers, and require manual memory management to prevent memory leaks.
```cpp
// Traditional C-style (not recommended)
int* dynArray = new int[10];  // Allocate
dynArray[0] = 42;             // Access
delete[] dynArray;            // Must manually delete

// Modern C++ approach (recommended)
#include <memory>
auto smartArray = std::make_unique<int[]>(10);  // Automatically managed
smartArray[0] = 42;  // No delete needed

// Multi-dimensional dynamic arrays
// Preferred approach:
std::vector<std::vector<int>> matrix(rows, std::vector<int>(cols));

// Alternative:
auto matrix = std::make_unique<int*[]>(rows);
for (int i = 0; i < rows; ++i) {
    matrix[i] = std::make_unique<int[]>(cols);
}
```

**Best Practice**: Use Smart Pointers: automatically manage memory, preventing leaks.
```cpp
#include <memory>
using namespace std;

int main() {
    unique_ptr<int> uPtr = make_unique<int>(10); //exclusive ownership
    shared_ptr<int> sPtr = make_shared<int>(20); //shared ownership with reference counting
    weak_ptr<int> wPtr = sPtr; //weak reference to avoid circular dependencies
    if (auto locked = wPtr.lock()) {
        cout << *locked << endl; // Safely access the shared object
    }
}
```

### Arrays of Objects
Arrays can store objects, allowing you to manipulate multiple instances of a class.

```cpp
class Person {
    string name;
    int age;
public:
    Person(string n, int a) : name(n), age(a) {}
};

// Static array
Person people[3] = {
    Person("Alice", 30),
    Person("Bob", 25),
    Person("Charlie", 35)
};

// Dynamic array
Person* dynPeople = new Person[2]{
    Person("Dave", 40),
    Person("Eve", 28)
};

delete[] dynPeople;
```

### Array Operations
```cpp
// Searching
bool found = false;
for (int i = 0; i < size; ++i) {
    if (arr[i] == target) {
        found = true;
        break;
    }
}

// Or use standard algorithms:
#include <algorithm>
bool found = std::find(arr, arr+size, target) != arr+size;

// Sorting
std::sort(arr, arr+size);  // For C-style arrays
std::sort(modernArray.begin(), modernArray.end());  // For std::array
```

### Common Pitfalls
* Bounds Violations: everything starts at 0, so even though the size may be 5, the last item is at index 4.
* Memory Leaks: remember `delete[]`
* Dangling Pointers: after deleting a pointer, set it to `nullptr` for extra safety

**Best Practices**
- Prefer array for fixed-size
- Always initialize pointers to `nullptr`
- Use smart pointers for dynamic arrays
- Document ownership of raw pointers 

## Vectors
Vectors in C++ are dynamic arrays provided by the Standard Library. They can grow and shrink in size as needed and handle memory management automatically.

### Essential Vector Operations
Vectors can be initialized in several ways:
```cpp
#include <vector>
using namespace std;

// Initialization
vector<int> v1;                 // Empty
vector<int> v2(5, 10);          // 5 elements, all 10
vector<int> v3 = {1, 2, 3};     // Initializer list
vector<int> v4(v3);             // Copy constructor

// Accessing elements
cout << v3[0];       // No bounds checking (faster)
cout << v3.at(0);    // With bounds checking (safer)
cout << v3.front();  // First element
cout << v3.back();   // Last element

// Modifying
v3.push_back(4);     // Add to end
v3.pop_back();       // Remove from end
v3.insert(v3.begin() + 1, 5);  // Insert at position
v3.erase(v3.begin());          // Remove first element
v3.clear();         // Remove all elements

// Capacity management
v3.reserve(100);    // Preallocate memory
v3.shrink_to_fit(); // Reduce capacity to fit size
```
### Advanced Vector Usage
```cpp
// Vector of objects
class Person {
    string name;
    int age;
public:
    Person(string n, int a) : name(n), age(a) {}
};

vector<Person> people;
people.emplace_back("Alice", 30);  // More efficient than push_back
people.emplace_back("Bob", 25);

// Iterating through vectors
for (const auto& p : people) {  // Range-based for loop
    cout << p.name << endl;
}

for (auto it = people.begin(); it != people.end(); ++it) {  // Iterator
    cout << it->name << endl;
}

// Algorithm operations
#include <algorithm>
sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
    return a.age < b.age;
});

auto result = find_if(people.begin(), people.end(), [](const Person& p) {
    return p.name == "Alice";
});
```

### Vector Performance Considerations
- Use `reserve()` when you know the eventual size to avoid reallocations
- Prefer `emplace_back()` over `push_back()` for complex objects
- `shrink_to_fit()` can reduce memory usage after large removals
- vectors are contiguous - excelent for cache locality

### Common Pitfalls
* Out-of-Bounds Access: Use `at()` for bounds checking to avoid undefined behavior.
* Inefficient Resizing: Use `reserve()` to preallocate memory and avoid frequent reallocations.

## Memory Management
### Stack vs Heap Memory
**Stack**: Stores local variables. Memory is automatically managed and automatically deallocated when the variable goes out of scope. It's generally faster but limited in size.
**Heap**: Stores dynamically allocated memory. You must manually allocate and deallocate memory using `new` and `delete`. It offers more flexibility but requires careful memory management to avoid leaks.

### Pointer Basics
A pointer is a variable that stores the memory address of another variable.

**Declaration**: `int* ptr = &x;`
* `ptr` stores the address of `x`.

**Dereferencing**: `cout << *ptr;`
* This accesses the value stored at the address `ptr` points to.


### Pointer vs Reference
- `int* ptr`: Pointer to an integer.
- `int** ptr`: Pointer to a pointer to an integer (used in multi-level indirection).
- `int& ref`: Reference to an integer (alias for an existing variable).
```cpp
int x = 10;
int* ptr = &x;
int** ptr2 = &ptr;
int& ref = x;
```

### Smart Pointers
```cpp
#include <memory>

// 1. Unique pointer (exclusive ownership)
auto uptr = std::make_unique<int>(10);
// Automatically deleted when out of scope

// 2. Shared pointer (shared ownership)
auto sptr = std::make_shared<int>(20);
auto sptr2 = sptr;  // Reference count increases

// 3. Weak pointer (non-owning reference)
std::weak_ptr<int> wptr = sptr;
if (auto locked = wptr.lock()) {  // Convert to shared_ptr temporarily
    cout << *locked;
}
```

### Pointer Arithmetic
Pointers can be incremented or decremented to traverse arrays.

```cpp
int arr[] = {10, 20, 30, 40, 50};
int* ptr = arr;

cout << *ptr;      // 10
cout << *(ptr+2);  // 30 (pointer arithmetic)
ptr++;
cout << *ptr;      // 20
```

### The this Keyword
The `this` pointer refers to the current object in a member function.

```cpp
class MyClass {
public:
    int x;
    MyClass(int x) { this->x = x; } // 'this->x' refers to the member variable
};
```
* `this->x` refers to the member variable, while `x` refers to the constructor parameter

### Pointer Best Practices
- Prefer smart pointers over raw pointers
- Use `make_unique`/`make_shared` instead of `new`
- For arrays, prefer `std::vector` or `std::array`
- If using raw pointers, always
    - Initialize to `nullptr`
    - Check the null before deferencing
    - Document ownership semantics

### Common Pitfalls
* Memory Leaks: use smart pointers to prevent
* Dangling Pointers: set pointers to nullptr after deletion
* Double Deletion: use smart pointers
* Buffer Overflows: use vectors with bounds checking
* Shallow vs Deep Copy: understand the difference when copying objects with pointers

## Arrays vs Vectors vs Smart Pointers
| Feature | C-Style Arrays | std:array | std::vector | Smart Pointers |
| - | - | - | - | - |
| size | fixed at compile-time | fixed at compile-time | dynamic (grows/shrinks) | dynamic (grows/shrinks) |
| memory management | manual (need to free memory) | automatic (managed internally) | automatic | automatic |
| resizable | no | no | yes | no
| modern c++ | avoid | preferred for fixed size | preferred for dynamic size | preferred for heap allocation | 
| pass to functions | decays to pointer | by value/reference | by reference | by value/move |

## Object-Oriented Programming (OOP)
Object-Oriented Programming (OOP) organizes code around objects rather than actions and data rather than logic. It promotes efficient, modular, and reusable code by structuring programs into entities known as objects.

### Four Major Principles of OOP
1. [Encapsulation](#encapsulation): Hiding implementation details by using private variables and public accessor (getter) and mutator (setter) methods.
2. [Data Abstraction](#abstraction): Focuses on the "what" an object does rather than "how" it does it.
3. [Inheritance](#inheritance): Defines relationships between objects, where one class can inherit properties and behaviors from another.
4. [Polymorphism](#polymorphism): Allows one function or operator to work in multiple ways based on context (e.g., function overloading, overriding, and operator overloading).

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
* **Public**: Accessible by any part of the program.
* **Private**: Accessible only within the class itself (for encapsulation).
* **Protected**: Accessible within the class and its derived classes (used in inheritance).

### Constructors and Destructors
**Constructors**: Special member functions used to initialize objects.

**Example Constructor**:
```cpp
class Person {
    string name;
    int age;
public:
    // Use initialization lists
    Person(string n, int a) : name(n), age(a) {}
    
    // Make single-argument constructors explicit
    explicit Person(int a) : age(a) {}
};
```

**Copy Constructor**: Creates a new object as a copy of an existing object.
```cpp
Person(const Person &other) {
    name = other.name;
    age = other.age;
}
```

**Destructors**: Called when an object is destroyed to release resources.
```cpp
~Person() {
    cout << "Destructor called for " << name << endl;
}
```

### Encapsulation
Encapsulation ensures that the internal state of an object is protected from unintended modifications.

**Getters**: Functions used to retrieve the values of private member variables. 

**Setters**: Functions used to set the values of private member variables.

```cpp
class BankAccount {
private:  // Implementation hiding
    double balance;
    string accountNumber;
    
public:  // Public interface
    BankAccount(string num, double initial) 
        : accountNumber(num), balance(initial) {}
        
    // Accessors (getters)
    double getBalance() const { return balance; }
    
    // Mutators (setters) with validation
    bool deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return true;
        }
        return false;
    }
    
    bool withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }
};
```

### Static Members
Static data members are shared by all objects of a class. Static member functions can access only static data members.

```cpp
class Employee {
    static int count;  // Declaration
    int id;
    
public:
    Employee() : id(++count) {}
    
    static int getCount() { return count; }
    
    // Static utility function
    static bool isValidId(int testId) {
        return testId > 0 && testId <= count;
    }
};

int Employee::count = 0;  // Definition
```

### Abstraction
```cpp
class DatabaseConnection {
public:
    virtual void connect() = 0;  // Pure virtual - implementation hidden
    virtual void query(const string& sql) = 0;
    virtual ~DatabaseConnection() = default;  // Virtual destructor
};

// Concrete implementation
class MySQLConnection : public DatabaseConnection {
    // Implementation details hidden
    void connect() override { /* MySQL specific */ }
    void query(const string& sql) override { /* MySQL specific */ }
};
```

### Inheritance
Inheritance allows a new class to inherit properties and methods from an existing class.
```cpp
// Base class
class Shape {
protected:
    string color;
public:
    Shape(string c) : color(c) {}
    virtual double area() const = 0;  // Pure virtual
    virtual ~Shape() = default;
};

// Derived class
class Circle : public Shape {
    double radius;
public:
    Circle(string c, double r) : Shape(c), radius(r) {}
    
    double area() const override {
        return 3.14159 * radius * radius;
    }
    
    // Additional functionality
    double circumference() const {
        return 2 * 3.14159 * radius;
    }
};
```

### Polymorphism
Polymorphism enables the same method to perform different actions depending on the object.
```cpp
void printArea(const Shape& shape) {
    cout << "Area: " << shape.area() << endl;
}

int main() {
    Circle circle("Red", 5.0);
    printArea(circle);  // Works through polymorphism
}
```

### Virtual Functions
Virtual functions enable polymorphism - allowing derived classes to provide their own implementations of base class functions.
 **Basic Virtual Function Example**
```cpp
class Animal {
public:
    virtual void speak() {  // Virtual function
        cout << "Animal sound!" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {  // Override base version
        cout << "Woof!" << endl;
    }
};

// Usage:
Animal* myPet = new Dog();
myPet->speak();  // Outputs "Woof!" (calls Dog's version)
```

**Key Rules**:
- Use when:
    - need different behavior in derived classes
    - using base class pointers to access objects
    - creating interfaces (with pure virtual functions)
- Always make detructors virtual in base classes
- Use `override` keyword to be explicit
- Avoid virtual functions when:
    - Performance is critical
    - The class won't be inherited from
    - For very small, simple functions

**Pure Virtual Functions (Interfaces)**
```cpp
class Shape {  // Abstract class
public:
    virtual double area() = 0;  // Pure virtual (must be implemented)
};

class Circle : public Shape {
    double radius;
public:
    double area() override { return 3.14 * radius * radius; }
};
```

### Pointer Member Variables
Classes may have pointer member variables, which require careful memory management (allocation and deallocation) to avoid memory leaks.
```cpp
class MyClass {
    int* data;
public:
    MyClass(int val) : data(new int(val)) {}
    ~MyClass() { delete data; }
};
```
* The `data` pointer is dynamically allocated in the constructor.
* The destructor ensures that the allocated memory is properly deallocated when the object is destroyed.

### Operator Overloading
Operator overloading allows custom behaviors for operators.
```cpp
class Complex {
    double real, imag;
    
public:
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
    
    // Prefix ++
    Complex& operator++() {
        ++real;
        return *this;
    }
    
    // Postfix ++
    Complex operator++(int) {
        Complex temp = *this;
        ++(*this);
        return temp;
    }
    
    // Stream insertion
    friend ostream& operator<<(ostream& os, const Complex& c) {
        return os << c.real << " + " << c.imag << "i";
    }
};
```

### Smart Pointers for Member Variables
```cpp
class Document {
    unique_ptr<Content> content;  // Exclusive ownership
    
public:
    Document(unique_ptr<Content> c) : content(std::move(c)) {}
    
    void process() {
        if (content) {
            content->render();
        }
    }
    
    // Factory method
    static Document createFromFile(const string& filename) {
        return Document(make_unique<FileContent>(filename));
    }
};
```

### Rule of Five
```cpp
class ResourceHolder {
    int* resource;
public:
    // Constructor
    ResourceHolder(int size) : resource(new int[size]) {}
    
    // Destructor
    ~ResourceHolder() { delete[] resource; }
    
    // Copy constructor
    ResourceHolder(const ResourceHolder& other) {
        resource = new int[/*size*/];
        std::copy(/*...*/);
    }
    
    // Move constructor
    ResourceHolder(ResourceHolder&& other) noexcept 
        : resource(other.resource) {
        other.resource = nullptr;
    }
    
    // Copy/move assignment operators...
};
```

### Friend Functions and Friend Classes
A friend function or class has access to the private and protected members of another class.
```cpp
class Box {
private:
    double width;

public:
    Box(double w) : width(w) {}
    friend void printWidth(const Box &b);
};

void printWidth(const Box &b) {
    cout << "Width: " << b.width << endl;
}
```