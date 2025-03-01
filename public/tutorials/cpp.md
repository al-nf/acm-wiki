# C++ Tutorial

Written by Chris Shobe, 2025.

## Table of Contents
[C++ Tutorial](#c++-tutorial)
- [Table of Contents](#table-of-contents)
- Introduction
    - [What is C++?](#what-is-c++)
    - [How to run C++](#how-to-run-c++)
- [Basic Syntax and Structure](#basic-syntax-and-structure)
    - [Headers and Namespaces](#headers-and-namespaces)
    - [Commonly Used Header](#)
    - [Variables and Data Types](#variables-and-data-types)
- [Control Flow](#control-flow)
- [Loops](#loops)

## What is C++?

C++ was developed as an extension of C, sharing similar syntax but introducing Object-Oriented Programming (OOP) through classes and objects. This guide covers key differences, OOP principles, memory management, templating, and advanced C++ features.

## How to run C++ (Install an IDE)
* VS Code (Recommended for development): Requires calling GCC locally.
* OnlineGDB (Browser-based option).
* Linux: Use SSH to connect to a remote machine instead of installing GCC locally.

**To see more information about insallation. Go to our C Tutorial**

## Basic Syntax and Structure
### Headers and Namespaces
```cpp
#include <iostream>
using namespace std;
// includes all C++ Standard Library items
// instead of std::cout, you can simply use cout
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

### Input & Output
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

## Variables and Data Types
| Type | Description |
| - | - |
| int | An integer ranging from -(2^31-1) to 2^31-1. |
| char | A single character (1 byte). |
| float | A floating-point number with up to 6 decimal of precision. |
| double | A floating-point number with up to 15 decimal places of precision. |
| bool | A Boolean variable that holds true (1) or false (0). | 
| void | A data type of "no type". Usually used for functions and pointers. |

## Control Flow
### If-Else Statement
```cpp
//Standard statement with brackets
if(x > 0) {
    //code executes if x is greater than 0
} else {
    //code executes if x is not greater than 0
}

//If the condition controls only ONE statement, the brackets {} can be omitted.
//You can write the one statement on the same line or the line below the if statement.
//Best Practice: always use {}
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
        break; //Exits the switch to prevent fall-through
    case 2:
        cout << "x is two" << endl;
        break;
    default: //Executes if none of the cases match
        cout << "x is neither one nor two\n";
        break;
}
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

## Loop Control Statements
### break
### continue
### return

## Functions
### Function Definition
A function is defined with a return type, a name, and optional parameters.
```cpp
int add(int a, int b) {
    return a + b;
}
```
`int add(int a, int b)`: Declares a function named `add` that takes two integer parameters (`a` and `b`).
`return a + b;`: Returns the sum of `a` and `b` to the caller.

### Function Call
To execute a function, you need to call it with appropriate arguments.
```cpp
int result = add(5,3); //result = 8
```

### Void Function (No Return Value)
A `void` function peforms an action but does not return a value.
```cpp
void printMessage() {
    cout << "Hello from function !\n";
}
```
The function `printMessage()` has a `void` return type. Instead of returning something, it simply prints a message when called.
This is useful for tasks like displaying messages, modifying global variables, or performing actions without needing a return value.