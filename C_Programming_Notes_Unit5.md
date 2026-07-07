# C Programming — Detailed Notes (Unit 5)
## User-Defined Functions and Structures

---

# PART A: USER-DEFINED FUNCTIONS

## 1. Need for User-Defined Functions

A **function** is a self-contained block of code that performs a specific, well-defined task. C allows programmers to define their own functions in addition to using built-in library functions (like `printf`, `scanf`, `sqrt`).

**Why use user-defined functions?**

- **Modularity** – Large problems can be broken into smaller, manageable sub-problems, each handled by its own function.
- **Reusability** – A function written once can be called multiple times from different parts of the program (or even other programs), avoiding code duplication.
- **Readability & Maintainability** – Code organized into logically-named functions is easier to read, debug, and modify.
- **Abstraction** – A function can be *used* without knowing its internal implementation details, as long as its purpose (interface) is clear.
- **Easier debugging & testing** – Each function can be tested and debugged independently.

**Example without functions (repetitive code):**
```c
#include <stdio.h>
int main() {
    int a = 5, b = 10, sum1;
    sum1 = a + b;
    printf("Sum1 = %d\n", sum1);

    int c = 20, d = 30, sum2;
    sum2 = c + d;
    printf("Sum2 = %d\n", sum2);
    return 0;
}
```

**Same task using a function (cleaner, reusable):**
```c
#include <stdio.h>

int add(int x, int y) {   // reusable function
    return x + y;
}

int main() {
    printf("Sum1 = %d\n", add(5, 10));
    printf("Sum2 = %d\n", add(20, 30));
    return 0;
}
```

---

## 2. A Multi-Function Program

A C program can (and usually does) consist of **multiple functions**. Execution always begins from the `main()` function, which may call other user-defined functions, which in turn may call others.

**Example: Multi-function program**
```c
#include <stdio.h>

void greet();              // function declaration (prototype)
int square(int n);          // function declaration
void displayResult(int n, int sq);

int main() {
    greet();
    int num = 6;
    int result = square(num);
    displayResult(num, result);
    return 0;
}

void greet() {
    printf("Welcome to the Square Calculator!\n");
}

int square(int n) {
    return n * n;
}

void displayResult(int n, int sq) {
    printf("Square of %d is %d\n", n, sq);
}
```
**Output:**
```
Welcome to the Square Calculator!
Square of 6 is 36
```
Here, `main()` acts as the controller, calling `greet()`, `square()`, and `displayResult()` in sequence — this is the essence of modular, multi-function program design.

---

## 3. Elements of User-Defined Functions

Every user-defined function in C involves **three key elements**:

| Element | Purpose |
|---|---|
| **Function Declaration (Prototype)** | Tells the compiler the function's name, return type, and parameter types before it is used |
| **Function Definition** | Contains the actual body/code of the function |
| **Function Call** | The statement that invokes/executes the function |

**Visual overview:**
```c
int add(int a, int b);     // 1. Declaration (prototype) - ends with ;

int main() {
    int result = add(3, 4); // 3. Function Call
    printf("%d", result);
    return 0;
}

int add(int a, int b) {    // 2. Function Definition
    return a + b;
}
```

---

## 4. Definition of Functions

The **function definition** contains the actual body — the set of statements that define what the function does when called.

**Syntax:**
```c
return_type function_name(parameter_list) {
    // local variable declarations
    // statements
    return value;   // optional, depends on return_type
}
```

**Example:**
```c
int multiply(int a, int b) {   // header
    int result;                 // body
    result = a * b;
    return result;               // returns the result to the caller
}
```

- `return_type` – the data type of the value the function sends back (`int`, `float`, `void`, etc.)
- `function_name` – identifier used to call the function
- `parameter_list` – variables that receive values passed by the caller (also called **formal parameters**)
- `return` statement – sends a value back to the caller and exits the function immediately (omitted entirely if `return_type` is `void`)

---

## 5. Return Values and Their Types

A function can return **at most one value** directly, using the `return` statement. The type of this value must match the function's declared `return_type`.

**Rules:**
- If `return_type` is `void`, the function returns nothing, and `return;` (with no value) is optional.
- The `return` statement immediately terminates the function, even if more code follows it.
- A function can have multiple `return` statements (e.g. in different branches), but only one executes per call.

**Example Program: Different return types**
```c
#include <stdio.h>

int getInt() {
    return 42;             // returns an int
}
float getFloat() {
    return 3.14f;           // returns a float
}
char getChar() {
    return 'A';              // returns a char
}
void showMessage() {
    printf("Hello from void function\n");
    return;                   // optional, just exits
}

int main() {
    printf("%d\n", getInt());
    printf("%.2f\n", getFloat());
    printf("%c\n", getChar());
    showMessage();
    return 0;
}
```
**Output:**
```
42
3.14
A
Hello from void function
```

**Example: Multiple return statements (only one executes):**
```c
int checkSign(int n) {
    if (n > 0)
        return 1;      // positive
    else if (n < 0)
        return -1;     // negative
    else
        return 0;      // zero
}
```

---

## 6. Function Calls

A **function call** is a statement that invokes/executes a function, optionally passing values (**arguments**) to it and optionally receiving a returned value.

**Syntax:**
```c
function_name(argument_list);
```

**Example:**
```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int main() {
    int result = square(5);   // function call, 5 is the argument
    printf("Square = %d\n", result);   // Square = 25
    return 0;
}
```

**Two ways parameters can be passed to functions:**

| Method | Description |
|---|---|
| **Call by Value** | A copy of the argument's value is passed; changes inside the function do NOT affect the original variable |
| **Call by Reference** | The address of the argument is passed (using pointers); changes inside the function DO affect the original variable |

**Example — Call by Value (default in C):**
```c
#include <stdio.h>
void modify(int x) {
    x = x + 10;   // only changes the local copy
}
int main() {
    int a = 5;
    modify(a);
    printf("a = %d\n", a);   // a = 5 (unchanged!)
    return 0;
}
```

**Example — Call by Reference (using pointers):**
```c
#include <stdio.h>
void modify(int *x) {
    *x = *x + 10;   // modifies the actual variable via its address
}
int main() {
    int a = 5;
    modify(&a);        // passing address of a
    printf("a = %d\n", a);   // a = 15 (changed!)
    return 0;
}
```

---

## 7. Function Declaration (Prototype)

A **function declaration (prototype)** informs the compiler about a function's name, return type, and parameter types **before** it is defined or called — usually placed above `main()`. This lets the function be called anywhere in the file, even if its full definition appears later.

**Syntax:**
```c
return_type function_name(parameter_type1, parameter_type2, ...);
```

**Example:**
```c
#include <stdio.h>

int add(int, int);          // function declaration/prototype

int main() {
    printf("%d\n", add(3, 4));   // function can be called before its definition
    return 0;
}

int add(int a, int b) {      // function definition (later in the file)
    return a + b;
}
```

> Without a prototype, if a function is called before it's defined, older compilers may assume default types and generate warnings or incorrect behavior. Prototypes prevent such mismatches and enable the compiler to check argument types at each call site.

---

## 8. Category of Functions

Based on whether a function accepts **arguments** and whether it **returns a value**, functions fall into **four categories**.

### 8.1 No Arguments and No Return Value
The function neither receives data from the caller nor sends any data back. Typically used for simple tasks like displaying a message.

```c
#include <stdio.h>
void greet() {
    printf("Hello, welcome!\n");
}
int main() {
    greet();     // no arguments passed, nothing returned
    return 0;
}
```

### 8.2 Arguments but No Return Value
The function receives data via parameters but does not send any result back (return type `void`). Useful for performing an action (like printing) based on input.

```c
#include <stdio.h>
void printSquare(int n) {
    printf("Square of %d is %d\n", n, n * n);
}
int main() {
    printSquare(6);   // argument passed: 6; nothing returned
    return 0;
}
// Output: Square of 6 is 36
```

### 8.3 Arguments with Return Value
The function receives input data and also returns a computed result. This is the **most common and most useful** category, since it behaves like a true reusable "black box."

```c
#include <stdio.h>
int add(int a, int b) {
    return a + b;
}
int main() {
    int sum = add(15, 25);   // arguments passed, value returned
    printf("Sum = %d\n", sum);   // Sum = 40
    return 0;
}
```

### 8.4 No Arguments but Returns a Value
The function takes no input but still computes and returns a value — often used when the value doesn't depend on external input (e.g., a constant calculation, or reading global data).

```c
#include <stdio.h>
int getPiApprox() {
    return 3;   // simplistic - just for illustration
}
float getPiValue() {
    return 3.14159;
}
int main() {
    printf("Value: %.5f\n", getPiValue());   // Value: 3.14159
    return 0;
}
```

**Summary Table:**

| Category | Takes Arguments? | Returns Value? | Typical Use |
|---|---|---|---|
| No args, no return | No | No | Print a fixed message |
| Args, no return | Yes | No | Display something based on input |
| Args, with return | Yes | Yes | Compute and return a result (most common) |
| No args, with return | No | Yes | Return a fixed/global/computed value |

---

## 9. Functions That Return Multiple Values

In C, a function's `return` statement can send back **only one value directly**. To effectively "return" multiple values, we use:

**Method 1 — Pointers (call by reference):** Pass addresses of variables as arguments; the function modifies them directly.
```c
#include <stdio.h>
void minMax(int arr[], int size, int *min, int *max) {
    *min = *max = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] < *min) *min = arr[i];
        if (arr[i] > *max) *max = arr[i];
    }
}
int main() {
    int arr[] = {12, 45, 3, 67, 29, 8};
    int min, max;
    minMax(arr, 6, &min, &max);
    printf("Min = %d, Max = %d\n", min, max);   // Min = 3, Max = 67
    return 0;
}
```

**Method 2 — Using a structure to bundle multiple values into one returnable unit:**
```c
#include <stdio.h>
struct Result {
    int min;
    int max;
};
struct Result minMax(int arr[], int size) {
    struct Result r;
    r.min = r.max = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] < r.min) r.min = arr[i];
        if (arr[i] > r.max) r.max = arr[i];
    }
    return r;   // returns a struct containing both values
}
int main() {
    int arr[] = {12, 45, 3, 67, 29, 8};
    struct Result res = minMax(arr, 6);
    printf("Min = %d, Max = %d\n", res.min, res.max);
    return 0;
}
```

---

## 10. Nesting of Functions

C allows a function to **call another function** from within its body — this is called **nesting of functions**. (Note: C does not allow defining one function's body literally *inside* another's braces, but it does allow one function to *call* another during execution.)

**Example:**
```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int sumOfSquares(int a, int b) {
    return square(a) + square(b);   // nested call to square()
}

int main() {
    int result = sumOfSquares(3, 4);   // main calls sumOfSquares, which calls square
    printf("Sum of squares = %d\n", result);   // 9 + 16 = 25
    return 0;
}
```

**Flow of control:**
```
main() 
   └──> calls sumOfSquares(3, 4)
              └──> calls square(3) --> returns 9
              └──> calls square(4) --> returns 16
              └──> returns 9 + 16 = 25
   <──  receives 25
```

---

## 11. Recursion

**Recursion** occurs when a function **calls itself**, either directly or indirectly, to solve a problem by breaking it into smaller sub-problems of the same type.

**Every recursive function must have:**
1. **Base case** – a condition under which the function stops calling itself (prevents infinite recursion).
2. **Recursive case** – the function calls itself with a smaller/simpler version of the problem, moving toward the base case.

**Example Program: Factorial using recursion**
```c
#include <stdio.h>

long factorial(int n) {
    if (n == 0 || n == 1) {   // base case
        return 1;
    }
    return n * factorial(n - 1);   // recursive case
}

int main() {
    printf("Factorial of 5 = %ld\n", factorial(5));   // 120
    return 0;
}
```

**How recursion unfolds for `factorial(5)`:**
```
factorial(5) = 5 * factorial(4)
factorial(4) = 4 * factorial(3)
factorial(3) = 3 * factorial(2)
factorial(2) = 2 * factorial(1)
factorial(1) = 1                     <- base case reached

Unwinding back:
factorial(2) = 2 * 1  = 2
factorial(3) = 3 * 2  = 6
factorial(4) = 4 * 6  = 24
factorial(5) = 5 * 24 = 120
```

**Example Program: Fibonacci series using recursion**
```c
#include <stdio.h>

int fibonacci(int n) {
    if (n == 0) return 0;      // base case 1
    if (n == 1) return 1;      // base case 2
    return fibonacci(n - 1) + fibonacci(n - 2);   // recursive case
}

int main() {
    for (int i = 0; i < 8; i++) {
        printf("%d ", fibonacci(i));
    }
    return 0;
}
// Output: 0 1 1 2 3 5 8 13
```

**Recursion vs Iteration (loop-based):**

| Recursion | Iteration |
|---|---|
| Function calls itself | Uses loop constructs (for/while) |
| Uses call stack — more memory overhead | Generally uses less memory |
| Often more elegant/readable for naturally recursive problems (trees, factorial) | Often faster and more efficient |
| Risk of **stack overflow** if base case is missing or too deep | No such risk |

> **Caution:** Every recursive function must eventually reach its base case; otherwise, it results in **infinite recursion**, leading to a stack overflow and program crash.

---

# PART B: STRUCTURES

## 12. What is a Structure?

A **structure** is a **user-defined data type** that groups together **variables of different data types** under a single name. Unlike arrays (which hold elements of the *same* type), a structure can bundle related but *differently-typed* data into one logical unit.

**Why use structures?**
- To represent a **real-world entity** with multiple attributes (e.g., a Student has a name, roll number, and marks — different types, one entity).
- To pass a group of related values to/from functions as a single unit.
- Foundation for more advanced data structures (linked lists, trees, etc.)

**Real-world example:** A `Student` record naturally has a name (string), roll number (int), and percentage (float) — a structure lets us group all three under one type.

---

## 13. Structure Type Declarations

Before a structure variable can be created, the **structure type** itself must be declared using the `struct` keyword — this defines the "template" or "blueprint."

**Syntax:**
```c
struct structure_name {
    data_type member1;
    data_type member2;
    ...
};
```

**Example:**
```c
struct Student {
    char name[30];
    int rollNo;
    float percentage;
};
```
> This declaration alone does **not** create any variable or allocate memory — it only defines the *type* `struct Student`, which can now be used to create actual variables.

---

## 14. Structure Declarations (Declaring Structure Variables)

Once the structure type is defined, variables of that type can be declared in several ways.

**Method 1 — Declare variables separately, after defining the structure:**
```c
struct Student {
    char name[30];
    int rollNo;
    float percentage;
};

struct Student s1, s2;   // declaring two structure variables
```

**Method 2 — Declare variables at the same time as the structure definition:**
```c
struct Student {
    char name[30];
    int rollNo;
    float percentage;
} s1, s2;                 // variables declared here directly
```

**Method 3 — Using `typedef` for convenience (avoids repeating `struct` keyword):**
```c
typedef struct {
    char name[30];
    int rollNo;
    float percentage;
} Student;

Student s1, s2;   // no need to write 'struct' each time
```

---

## 15. Referencing Structure Members

Individual members of a structure variable are accessed using the **dot (`.`) operator**.

**Syntax:**
```c
structure_variable.member_name
```

**Example Program:**
```c
#include <stdio.h>
#include <string.h>

struct Student {
    char name[30];
    int rollNo;
    float percentage;
};

int main() {
    struct Student s1;

    strcpy(s1.name, "Amit Sharma");   // assigning to a char array member
    s1.rollNo = 101;
    s1.percentage = 87.5;

    printf("Name: %s\n", s1.name);
    printf("Roll No: %d\n", s1.rollNo);
    printf("Percentage: %.2f\n", s1.percentage);

    return 0;
}
```
**Output:**
```
Name: Amit Sharma
Roll No: 101
Percentage: 87.50
```

**Accessing structure members via a pointer — uses the arrow (`->`) operator:**
```c
#include <stdio.h>
struct Student {
    char name[30];
    int rollNo;
};
int main() {
    struct Student s1 = {"Riya", 102};
    struct Student *ptr = &s1;

    printf("%s\n", ptr->name);      // arrow operator (equivalent to (*ptr).name)
    printf("%d\n", ptr->rollNo);
    return 0;
}
```

---

## 16. Referencing Whole Structures

An entire structure variable (all its members together) can be:

**1. Assigned to another variable of the same type in one statement:**
```c
struct Student s1 = {"Amit", 101, 87.5};
struct Student s2;
s2 = s1;   // copies ALL members of s1 into s2 at once
```

**2. Passed to a function (by value or by reference):**
```c
#include <stdio.h>
struct Student {
    char name[30];
    int rollNo;
};

void display(struct Student s) {   // passed by value (a copy)
    printf("%s - %d\n", s.name, s.rollNo);
}

int main() {
    struct Student s1 = {"Amit", 101};
    display(s1);   // whole structure passed at once
    return 0;
}
```

**3. Returned from a function (as seen earlier in Section 9, Method 2):**
```c
struct Student getDefaultStudent() {
    struct Student s = {"Unknown", 0};
    return s;   // entire structure returned
}
```

**4. Compared** — Note: unlike simple variables, **structures cannot be directly compared using `==`**; each member must be compared individually, or `memcmp()` can be used carefully (with caveats around padding bytes).

---

## 17. Initialization of Structures

Structure variables can be initialized at the time of declaration, similar to arrays.

**Method 1 — Initializer list, in order of members:**
```c
struct Student {
    char name[30];
    int rollNo;
    float percentage;
};

struct Student s1 = {"Priya", 105, 91.5};
```

**Method 2 — Designated initializers (C99 and later) — specify member names explicitly, order-independent:**
```c
struct Student s1 = {.rollNo = 105, .name = "Priya", .percentage = 91.5};
```

**Method 3 — Partial initialization (remaining members set to 0 / empty):**
```c
struct Student s1 = {"Priya"};   // rollNo = 0, percentage = 0.0
```

**Example Program: Array of structures (common real-world pattern)**
```c
#include <stdio.h>

struct Student {
    char name[30];
    int rollNo;
    float percentage;
};

int main() {
    struct Student students[3] = {
        {"Amit", 101, 87.5},
        {"Priya", 102, 91.2},
        {"Rahul", 103, 78.9}
    };

    for (int i = 0; i < 3; i++) {
        printf("%s | Roll: %d | %.2f%%\n",
               students[i].name, students[i].rollNo, students[i].percentage);
    }
    return 0;
}
```
**Output:**
```
Amit | Roll: 101 | 87.50%
Priya | Roll: 102 | 91.20%
Rahul | Roll: 103 | 78.90%
```

---

## Quick Revision Summary

| Concept | One-line takeaway |
|---|---|
| Need for functions | Enables modularity, reusability, readability, easier debugging |
| Multi-function program | `main()` coordinates calls to other user-defined functions |
| Elements of a function | Declaration (prototype), Definition, Call |
| Function definition | Header + body containing the actual logic |
| Return values | `return` sends back at most one value matching the declared type |
| Function calls | Invokes a function; C uses call-by-value by default (call-by-reference via pointers) |
| Function declaration | Prototype informs compiler of signature before use |
| Categories of functions | Combinations of (no/with) arguments × (no/with) return value |
| Multiple return values | Achieved via pointers (out-parameters) or returning a structure |
| Nesting of functions | One function calls another during execution |
| Recursion | Function calls itself; needs a base case + recursive case |
| Structure | User-defined type grouping different data types under one name |
| Structure type declaration | `struct Name { members };` defines the blueprint |
| Structure declaration | Creates actual variables of a structure type |
| Referencing members | Dot (`.`) operator for variables, arrow (`->`) for pointers |
| Referencing whole structures | Assign, pass, or return an entire structure as one unit |
| Initialization of structures | Ordered list, designated initializers, or partial init |

---
*End of Unit 5 Notes*
