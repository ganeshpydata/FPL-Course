# C Programming — Detailed Notes (Unit 1)

---

## 1. Program Design Tools

Before writing actual code, a programmer designs the logic of a solution. The two most common tools for this are **Algorithms** and **Flowcharts**.

### 1.1 Algorithm

An **algorithm** is a step-by-step, finite set of instructions written in plain (natural) language to solve a specific problem. It is independent of any programming language — the same algorithm can later be implemented in C, Python, Java, etc.

**Characteristics of a good algorithm:**
- **Finiteness** – must terminate after a finite number of steps.
- **Definiteness** – each step must be clear and unambiguous.
- **Input** – zero or more well-defined inputs.
- **Output** – one or more well-defined outputs.
- **Effectiveness** – each step must be basic enough to be carried out.

**Example: Algorithm to find the sum of two numbers**
```
Step 1: Start
Step 2: Read two numbers, A and B
Step 3: Compute SUM = A + B
Step 4: Print SUM
Step 5: Stop
```

**Example: Algorithm to find the largest of three numbers**
```
Step 1: Start
Step 2: Read A, B, C
Step 3: If A > B and A > C, then Largest = A
Step 4: Else if B > C, then Largest = B
Step 5: Else Largest = C
Step 6: Print Largest
Step 7: Stop
```

### 1.2 Flowchart

A **flowchart** is a pictorial/graphical representation of an algorithm using standard symbols. It shows the flow of control from one step to another and makes the logic easier to visualize, especially for beginners.

**Standard Flowchart Symbols:**

| Symbol | Name | Purpose |
|---|---|---|
| Oval | Terminal (Start/Stop) | Marks beginning and end |
| Parallelogram | Input/Output | Used for reading input or printing output |
| Rectangle | Process | Used for calculations/assignments |
| Diamond | Decision | Used for conditional (yes/no) branching |
| Arrow | Flow line | Shows direction of execution |
| Circle | Connector | Joins parts of flowchart on the same/different page |

**Example: Flowchart for Sum of Two Numbers (described)**
```
        ┌───────┐
        │ Start │
        └───┬───┘
            │
     ┌──────▼───────┐
     │ Read A, B     │
     └──────┬───────┘
            │
     ┌──────▼───────┐
     │ SUM = A + B   │
     └──────┬───────┘
            │
     ┌──────▼───────┐
     │ Print SUM     │
     └──────┬───────┘
            │
        ┌───▼───┐
        │ Stop  │
        └───────┘
```

**Example: Flowchart for Largest of Two Numbers (described)**
```
        Start
          │
     Read A, B
          │
     Is A > B? ──Yes──► Print A
          │
          No
          │
       Print B
          │
        Stop
```

**Algorithm vs Flowchart:**

| Algorithm | Flowchart |
|---|---|
| Textual representation | Graphical/pictorial representation |
| Easier to write, harder to visualize for complex logic | Easier to visualize, harder to draw for large programs |
| Uses plain steps | Uses standard symbols |
| No fixed notation | Follows fixed standard symbols (ANSI) |

---

## 2. Overview of C

### 2.1 History of C

- Developed by **Dennis Ritchie** at **Bell Laboratories (AT&T)** in **1972**.
- Evolved from two earlier languages:
  - **BCPL** (Basic Combined Programming Language) by Martin Richards (1967)
  - **B language** by Ken Thompson (1970) — used to create early Unix
- C was originally developed to **re-write the UNIX operating system**, which was earlier written in assembly language.
- In **1978**, Brian Kernighan and Dennis Ritchie published *"The C Programming Language"*, informally called **K&R C**, which became an unofficial standard.
- **ANSI (American National Standards Institute)** standardized C in **1989**, known as **ANSI C** or **C89**.
- **ISO** adopted it in 1990 as **C90**.
- Later versions: **C99**, **C11**, **C17**, **C23** added new features (like inline functions, better type support, etc.)

### 2.2 Importance / Features of C

1. **Middle-level language** – combines features of both high-level (readability) and low-level (direct hardware access) languages.
2. **Structured programming language** – programs are divided into functions/modules, making code modular and easy to debug.
3. **Portability** – a C program written on one machine can run on another with little or no modification.
4. **Rich set of operators and built-in functions**.
5. **Fast execution speed** – close to assembly language in performance.
6. **Foundation language** – many languages (C++, Java, C#, Python interpreter itself) are influenced by or built using C concepts.
7. Supports **pointers**, giving direct memory access and manipulation.
8. Extensible using **libraries** (stdio.h, stdlib.h, math.h, etc.).
9. Widely used in **system software** – operating systems, compilers, embedded systems, device drivers.

---

## 3. Character Set of C

The character set is the set of valid characters that a C compiler can recognize. It includes:

| Category | Characters |
|---|---|
| **Letters** | A–Z, a–z |
| **Digits** | 0–9 |
| **Special Symbols** | `~ ! @ # % ^ & * ( ) _ - + = { } [ ] : ; " ' < > , . ? / \ |` |
| **White Spaces** | blank space, tab, newline |
| **Escape Sequences** | `\n`, `\t`, `\\`, `\'`, `\"`, `\0`, `\r`, `\b`, `\a` etc. |

**Example — Escape sequences in use:**
```c
#include <stdio.h>
int main() {
    printf("Hello\tWorld\n");   // \t = tab, \n = newline
    printf("She said \"C is fun\"\n");
    return 0;
}
```
**Output:**
```
Hello   World
She said "C is fun"
```

---

## 4. C Tokens

A **token** is the smallest individual unit in a C program that the compiler recognizes. C has **6 types of tokens**:

1. **Keywords** – e.g., `int`, `for`, `while`
2. **Identifiers** – e.g., `sum`, `total_marks`
3. **Constants** – e.g., `10`, `3.14`, `'A'`
4. **Strings** – e.g., `"Hello"`
5. **Operators** – e.g., `+`, `-`, `*`, `==`
6. **Special Symbols** – e.g., `{ }`, `( )`, `;`, `,`

**Example program identifying tokens:**
```c
#include <stdio.h>          // preprocessor directive
int main() {                // keyword 'int', identifier 'main'
    int a = 10, b = 20;      // keywords, identifiers, constants, operator
    int sum = a + b;         // identifier, operator '+'
    printf("Sum = %d", sum); // string, identifier
    return 0;                // keyword, constant
}
```

---

## 5. Keywords and Identifiers

### 5.1 Keywords

- Keywords are **reserved words** that have a predefined meaning in C.
- They **cannot** be used as variable names, function names, or identifiers.
- C (ANSI C) has **32 keywords**.

**List of C Keywords:**
```
auto      break     case      char      const
continue  default   do        double    else
enum      extern    float     for       goto
if        int       long      register  return
short     signed    sizeof    static    struct
switch    typedef   union     unsigned  void
volatile  while
```

### 5.2 Identifiers

- Identifiers are **user-defined names** given to variables, functions, arrays, structures, etc.

**Rules for naming identifiers:**
1. Can contain letters (A–Z, a–z), digits (0–9), and underscore (`_`).
2. Must **begin with a letter or underscore**, not a digit.
3. Cannot be a **keyword**.
4. No spaces or special symbols (`@`, `#`, `%`, etc.) allowed.
5. Case-sensitive: `Sum` and `sum` are different identifiers.
6. Length may vary by compiler, but generally first 31 characters are significant.

**Valid identifiers:** `total`, `_marks`, `student1`, `avg_score`
**Invalid identifiers:** `1total` (starts with digit), `total marks` (space), `float` (keyword)

**Example:**
```c
int _age = 25;      // valid
int roll1 = 101;     // valid
// int 1roll = 101; // invalid - starts with digit
```

---

## 6. Constants

A **constant** is a value that does not change during program execution.

### Types of Constants in C:

| Type | Example | Description |
|---|---|---|
| **Integer constant** | `10`, `-25`, `0`, `017` (octal), `0x1A` (hex) | Whole numbers |
| **Floating-point constant** | `3.14`, `-0.001`, `2.5e3` | Numbers with decimal or exponent |
| **Character constant** | `'A'`, `'9'`, `'\n'` | Single character enclosed in single quotes |
| **String constant** | `"Hello"`, `"C Program"` | Sequence of characters enclosed in double quotes |

**Example:**
```c
#include <stdio.h>
int main() {
    int a = 100;          // integer constant
    float pi = 3.14159;    // floating point constant
    char grade = 'A';      // character constant
    char name[] = "Amit";  // string constant
    printf("%d %f %c %s", a, pi, grade, name);
    return 0;
}
```

---

## 7. Variables

A **variable** is a named location in memory used to store a value that **can change** during program execution.

**Rules for variable names** are the same as identifier rules (see Section 5.2).

**Example:**
```c
int marks;        // declaration
marks = 90;        // assignment
marks = 95;        // value changed - this is why it's called a "variable"
```

---

## 8. Data Types

Data types specify the **type of data** a variable can hold, and how much memory it occupies.

### 8.1 Classification of Data Types

| Category | Examples |
|---|---|
| **Primary (Basic)** | int, char, float, double, void |
| **Derived** | array, pointer, function, structure |
| **User-defined** | struct, union, enum, typedef |

### 8.2 Basic Data Types with Size & Range (typical, 32-bit system)

| Data Type | Size (bytes) | Format Specifier | Range (approx.) |
|---|---|---|---|
| `char` | 1 | `%c` | -128 to 127 |
| `int` | 2 or 4 | `%d` | -32,768 to 32,767 (or larger) |
| `float` | 4 | `%f` | 3.4E−38 to 3.4E+38 |
| `double` | 8 | `%lf` | 1.7E−308 to 1.7E+308 |
| `void` | 0 | — | represents "no value" |

**Modifiers** can be applied to basic types: `short`, `long`, `signed`, `unsigned`.

**Example:**
```c
#include <stdio.h>
int main() {
    int age = 20;
    float height = 5.9;
    double distance = 384400.65;
    char grade = 'A';
    printf("Age: %d\n", age);
    printf("Height: %.1f\n", height);
    printf("Distance: %.2lf\n", distance);
    printf("Grade: %c\n", grade);
    return 0;
}
```

---

## 9. Declaration of Variables

**Syntax:**
```c
data_type variable_name;
data_type variable1, variable2, ...;
```

- A declaration tells the compiler the **name and type** of the variable so it can allocate appropriate memory.
- Every variable **must be declared before use** in C.

**Examples:**
```c
int a;                 // single declaration
int x, y, z;            // multiple declaration, same type
float price, discount;  // multiple declaration
char grade = 'B';       // declaration with initialization
```

---

## 10. Storage Classes

A **storage class** defines the **scope** (visibility), **lifetime**, and **default initial value** of a variable.

C has **4 storage classes**:

| Storage Class | Keyword | Storage Location | Default Value | Scope | Lifetime |
|---|---|---|---|---|---|
| **Automatic** | `auto` | RAM/Stack | Garbage | Local to block | Within the block |
| **External** | `extern` | RAM | Zero | Global | Whole program |
| **Static** | `static` | RAM | Zero | Local to block | Retains value between function calls |
| **Register** | `register` | CPU register | Garbage | Local to block | Within the block |

### Examples:

**auto (default for local variables):**
```c
void func() {
    auto int x = 5;   // same as: int x = 5;
}
```

**static (retains value across function calls):**
```c
#include <stdio.h>
void counter() {
    static int count = 0;  // initialized only once
    count++;
    printf("Count = %d\n", count);
}
int main() {
    counter();  // Count = 1
    counter();  // Count = 2
    counter();  // Count = 3
    return 0;
}
```

**extern (used to access a global variable across files/functions):**
```c
int x = 10;  // global variable
void display() {
    extern int x;  // refers to the global x
    printf("%d", x);
}
```

**register (requests variable be stored in CPU register for faster access):**
```c
void loopFunc() {
    register int i;   // fast-access loop counter
    for (i = 0; i < 10; i++) {
        printf("%d ", i);
    }
}
```

---

## 11. Assigning Values to Variables

Values can be assigned to variables in the following ways:

**1. Using the assignment operator (`=`):**
```c
int a;
a = 10;
```

**2. At the time of declaration (initialization):**
```c
int a = 10;
float pi = 3.14;
```

**3. Using an input function (`scanf`):**
```c
int age;
scanf("%d", &age);
```

**4. Multiple assignment:**
```c
int a, b, c;
a = b = c = 5;   // all three variables get value 5
```

**5. Using expressions:**
```c
int a = 5, b = 10;
int sum = a + b;   // sum = 15
```

---

## 12. Defining Symbolic Constants

A **symbolic constant** is a name given to a constant value using the preprocessor directive `#define`. It improves readability and makes the program easier to maintain (change the value in one place).

**Syntax:**
```c
#define NAME value
```

**Example:**
```c
#include <stdio.h>
#define PI 3.14159
#define MAX_MARKS 100

int main() {
    float radius = 5;
    float area = PI * radius * radius;
    printf("Area = %.2f\n", area);
    printf("Max marks possible = %d\n", MAX_MARKS);
    return 0;
}
```

**Key points:**
- No semicolon at the end of `#define`.
- No memory is allocated; it is simply a **text substitution** done by the preprocessor before compilation.
- By convention, symbolic constants are written in **UPPERCASE**.

---

## 13. Declaring a Variable as Constant

The `const` keyword is used to declare a variable whose **value cannot be modified** after initialization. Unlike `#define`, `const` variables **do** occupy memory and are **type-checked** by the compiler.

**Syntax:**
```c
const data_type variable_name = value;
```

**Example:**
```c
#include <stdio.h>
int main() {
    const float PI = 3.14159;
    printf("PI = %.2f\n", PI);
    // PI = 3.14;   // ERROR: assignment of read-only variable
    return 0;
}
```

**`const` vs `#define`:**

| `const` | `#define` |
|---|---|
| Handled by compiler | Handled by preprocessor |
| Occupies memory | No memory allocation (simple substitution) |
| Has a data type | No data type |
| Can be checked/debugged | Cannot be debugged (invisible to debugger) |
| Follows scope rules | Global by default (valid till end of file, or #undef) |

---

## 14. Declaring a Variable as Volatile

# `volatile` in C — Beginner Notes

## 1. What is `volatile`?

`volatile` is a **type qualifier** in C. It tells the compiler that a variable's value may change unexpectedly, outside the normal flow of the code.

Because of this, the compiler must respect accesses to the variable instead of assuming its value stays the same.

It is commonly used with:

- Hardware registers in embedded systems
- Variables updated by interrupt service routines (ISRs)
- Memory-mapped input/output

> **Remember:** `volatile` does not make a variable thread-safe or atomic. It does not prevent race conditions.

## 2. Syntax

```c
volatile int flag;
```

These declarations mean the same thing:

```c
volatile int value;
int volatile value;
```

## 3. Basic example

```c
#include <stdio.h>

int main(void)
{
    volatile int number = 10;

    printf("Initial value: %d\n", number);

    number = 20;

    printf("Updated value: %d\n", number);

    return 0;
}
```

### Output

```text
Initial value: 10
Updated value: 20
```




**Where `volatile` is commonly used:**
- Variables shared with **hardware registers**.
- Variables modified inside an **Interrupt Service Routine (ISR)**.
- Variables shared between **multiple threads**.

**Combining const and volatile:**
```c
const volatile int sensor_value;  
// Value can change externally (hardware), but program itself cannot modify it.
```

---

## Quick Revision Summary

| Concept | One-line takeaway |
|---|---|
| Algorithm | Step-by-step language-independent solution |
| Flowchart | Graphical representation of algorithm using symbols |
| C History | Created by Dennis Ritchie, 1972, Bell Labs, for UNIX |
| Character Set | Letters, digits, special symbols, whitespace |
| Tokens | Smallest units: keywords, identifiers, constants, strings, operators, symbols |
| Keywords | 32 reserved words, cannot be used as names |
| Identifiers | User-defined names following naming rules |
| Constants | Fixed values: integer, float, char, string |
| Variables | Named memory locations whose value can change |
| Data Types | int, char, float, double, void + derived/user-defined |
| Declaration | Tells compiler the type & name before use |
| Storage Classes | auto, extern, static, register — control scope & lifetime |
| Assigning Values | `=`, initialization, `scanf`, chained assignment |
| Symbolic Constants | `#define NAME value` — preprocessor substitution |
| const | Compiler-enforced, memory-occupying constant |
| volatile | Prevents compiler optimization; value may change externally |

---
*End of Unit 1 Notes*
