# C Programming — Detailed Notes (Unit 4)
## Arrays, Character Arrays and Strings

---

# PART A: ARRAYS

An **array** is a collection of a **fixed number of elements** of the **same data type**, stored in **contiguous memory locations**, and referred to by a common name. Individual elements are accessed using an **index (subscript)**, which in C always starts from **0**.

**Why use arrays?**
- Storing multiple values of the same type without declaring separate variables for each (e.g., marks of 50 students).
- Efficient, indexed access to data.
- Foundation for more complex data structures (matrices, strings, stacks, etc.)

---

## 1. One-Dimensional Arrays

A **one-dimensional (1-D) array** is a simple list of elements, all of the same type, arranged linearly in memory.

### 1.1 Declaration of One-Dimensional Arrays

**Syntax:**
```c
data_type array_name[size];
```

- `data_type` – type of elements the array will hold (int, float, char, etc.)
- `array_name` – identifier following normal variable-naming rules
- `size` – total number of elements (must be a positive integer constant)

**Examples:**
```c
int marks[5];       // array of 5 integers: marks[0] to marks[4]
float price[10];     // array of 10 floats
char name[20];       // array of 20 characters
```

**Memory representation of `int marks[5];`:**
```
Index:   0     1     2     3     4
       ┌─────┬─────┬─────┬─────┬─────┐
marks: │  ?  │  ?  │  ?  │  ?  │  ?  │
       └─────┴─────┴─────┴─────┴─────┘
```
> Indexing always starts at **0** and ends at **size − 1**. Accessing `marks[5]` for an array of size 5 is **out of bounds** and leads to undefined behavior (a common bug).

### 1.2 Initialization of One-Dimensional Arrays

**Method 1 — Initialization at declaration:**
```c
int marks[5] = {90, 85, 78, 92, 88};
```

**Method 2 — Size can be omitted if initializer list is given (compiler counts elements):**
```c
int marks[] = {90, 85, 78, 92, 88};   // size automatically becomes 5
```

**Method 3 — Partial initialization (remaining elements default to 0):**
```c
int marks[5] = {90, 85};   // marks = {90, 85, 0, 0, 0}
```

**Method 4 — Element-by-element assignment (after declaration):**
```c
int marks[5];
marks[0] = 90;
marks[1] = 85;
marks[2] = 78;
marks[3] = 92;
marks[4] = 88;
```

**Method 5 — Using a loop (commonly used for input from user):**
```c
int marks[5];
for (int i = 0; i < 5; i++) {
    scanf("%d", &marks[i]);
}
```

**Example Program: Read and display array elements, find sum & average**
```c
#include <stdio.h>
int main() {
    int marks[5], sum = 0;
    float avg;

    printf("Enter 5 marks: ");
    for (int i = 0; i < 5; i++) {
        scanf("%d", &marks[i]);
        sum += marks[i];
    }

    avg = (float) sum / 5;

    printf("Marks entered: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", marks[i]);
    }

    printf("\nSum = %d\n", sum);
    printf("Average = %.2f\n", avg);
    return 0;
}
```
**Sample Output:**
```
Enter 5 marks: 90 85 78 92 88
Marks entered: 90 85 78 92 88
Sum = 433
Average = 86.60
```

**Example Program: Find the largest element in an array**
```c
#include <stdio.h>
int main() {
    int arr[6] = {12, 45, 3, 67, 29, 8};
    int largest = arr[0];

    for (int i = 1; i < 6; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    printf("Largest element = %d\n", largest);   // 67
    return 0;
}
```

---

## 2. Two-Dimensional Arrays

A **two-dimensional (2-D) array** stores data in a **rows-and-columns (matrix/table)** format. It can be thought of as an "array of arrays."

**Syntax:**
```c
data_type array_name[rows][columns];
```

**Example:**
```c
int matrix[3][4];   // 3 rows, 4 columns => 12 total elements
```

**Memory representation of `int matrix[2][3];` (conceptually, as a table):**
```
           col0   col1   col2
row0:    [ 1  ]  [ 2  ]  [ 3  ]
row1:    [ 4  ]  [ 5  ]  [ 6  ]
```
Accessed as: `matrix[0][0]=1, matrix[0][1]=2, ... matrix[1][2]=6`

> Internally, C stores 2-D arrays in **row-major order** — meaning all elements of row 0 are stored first, then row 1, and so on, in one continuous block of memory.

### 2.1 Initialization of Two-Dimensional Arrays

**Method 1 — Full initialization (row-wise, recommended for readability):**
```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

**Method 2 — Initialization without inner braces (still works, less readable):**
```c
int matrix[2][3] = {1, 2, 3, 4, 5, 6};
```

**Method 3 — Row size can be omitted (column size cannot):**
```c
int matrix[][3] = {
    {1, 2, 3},
    {4, 5, 6}
};   // number of rows (2) is inferred automatically
```

**Method 4 — Partial initialization (missing values default to 0):**
```c
int matrix[2][3] = {
    {1, 2},      // becomes {1, 2, 0}
    {4}          // becomes {4, 0, 0}
};
```

**Method 5 — Using nested loops (typical for input from the user):**
```c
int matrix[2][3];
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        scanf("%d", &matrix[i][j]);
    }
}
```

**Example Program: Read and display a 2-D matrix**
```c
#include <stdio.h>
int main() {
    int matrix[2][3];

    printf("Enter 6 elements (2x3 matrix):\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }

    printf("Matrix:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
**Sample Output:**
```
Enter 6 elements (2x3 matrix):
1 2 3 4 5 6
Matrix:
1 2 3
4 5 6
```

**Example Program: Addition of two matrices**
```c
#include <stdio.h>
int main() {
    int a[2][2] = {{1, 2}, {3, 4}};
    int b[2][2] = {{5, 6}, {7, 8}};
    int sum[2][2];

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            sum[i][j] = a[i][j] + b[i][j];
        }
    }

    printf("Sum matrix:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", sum[i][j]);
        }
        printf("\n");
    }
    return 0;
}
// Output:
// 6 8
// 10 12
```

**1-D vs 2-D Arrays:**

| One-Dimensional Array | Two-Dimensional Array |
|---|---|
| Linear list of elements | Table (rows × columns) of elements |
| `int a[5];` | `int a[3][4];` |
| Accessed with one index: `a[i]` | Accessed with two indices: `a[i][j]` |
| Used for simple lists | Used for matrices, grids, tables |

---

# PART B: CHARACTER ARRAYS AND STRINGS

In C, there is **no separate built-in string data type**. A **string** is simply an **array of characters terminated by a special null character `\0`** (ASCII value 0), which marks the end of the string.

---

## 3. Declaration and Initialization of String Variables

**Declaration:**
```c
char name[size];
```
The size should be **at least one more** than the maximum number of characters expected, to leave room for the terminating `\0`.

**Initialization Methods:**

**Method 1 — String literal (compiler adds `\0` automatically):**
```c
char name[6] = "Hello";   // stored as 'H','e','l','l','o','\0'
```

**Method 2 — Character-by-character (must add `\0` manually):**
```c
char name[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

**Method 3 — Size omitted (compiler calculates it):**
```c
char name[] = "Hello";   // size becomes 6 automatically (5 letters + '\0')
```

**Important note:** `char name[5] = "Hello";` is **invalid/unsafe** — "Hello" needs 6 bytes (5 letters + `\0`), so there is no room left for the null terminator, causing undefined behavior.

**How a string looks in memory:**
```
char city[6] = "Delhi";

Index:   0    1    2    3    4    5
       ┌────┬────┬────┬────┬────┬────┐
city:  │ D  │ e  │ l  │ h  │ i  │ \0 │
       └────┴────┴────┴────┴────┴────┘
```

---

## 4. Reading Strings from the Terminal

**Method 1 — Using `scanf("%s", ...)`:** Reads a string but **stops at the first whitespace** (space/tab/newline). No `&` is needed since an array name already represents its address.
```c
#include <stdio.h>
int main() {
    char name[30];
    printf("Enter your name: ");
    scanf("%s", name);         // stops at first space
    printf("Hello, %s!\n", name);
    return 0;
}
```
**Output (input: "John Smith"):**
```
Enter your name: John Smith
Hello, John!        <- only "John" captured, "Smith" is left out
```

**Method 2 — Using `gets()` (reads full line including spaces) — DEPRECATED/unsafe, avoid in modern code:**
```c
char name[30];
gets(name);   // reads until Enter; no bounds checking - can overflow buffer
```

**Method 3 — Using `fgets()` (safe, recommended way to read a full line with spaces):**
```c
#include <stdio.h>
int main() {
    char name[30];
    printf("Enter your full name: ");
    fgets(name, sizeof(name), stdin);   // reads including spaces, bounds-checked
    printf("Hello, %s", name);
    return 0;
}
```
**Output:**
```
Enter your full name: John Smith
Hello, John Smith
```
> `fgets` also captures the newline character (`\n`) if it fits within the buffer, which is why it's common to strip it afterward if needed.

---

## 5. Writing Strings to the Screen

**Method 1 — Using `printf("%s", ...)`:**
```c
char city[] = "Mumbai";
printf("City: %s\n", city);   // City: Mumbai
```

**Method 2 — Using `puts()`:** Prints the string followed automatically by a newline. Simpler and slightly faster than `printf` for plain string output.
```c
char city[] = "Mumbai";
puts(city);   // Mumbai   (newline added automatically)
```

**Example Program comparing both:**
```c
#include <stdio.h>
int main() {
    char msg[] = "Welcome to C Programming";

    printf("%s\n", msg);   // using printf
    puts(msg);             // using puts (adds its own newline)

    return 0;
}
```

---

## 6. Putting Strings Together (String Concatenation)

Combining two strings into one is called **concatenation**, done using the `strcat()` function from `<string.h>`.

**Syntax:**
```c
strcat(destination, source);
// appends 'source' to the end of 'destination'
// destination MUST have enough space to hold the combined result
```

**Example Program:**
```c
#include <stdio.h>
#include <string.h>
int main() {
    char first[20] = "Good";
    char second[] = "Morning";

    strcat(first, " ");        // append a space
    strcat(first, second);     // append second string

    printf("Combined: %s\n", first);   // Combined: Good Morning
    return 0;
}
```

> **Caution:** `first` must be declared large enough to hold the final combined string plus the null terminator, or it will overflow into adjacent memory (undefined behavior).

**`strncat()` — safer, limits number of characters appended:**
```c
char first[20] = "Hello";
strncat(first, " World, this is long", 6);   // appends only 6 characters
printf("%s\n", first);   // Hello World,
```

---

## 7. Comparison of Two Strings

Strings **cannot** be compared using `==` (that would compare memory addresses, not content). Instead, C provides `strcmp()` from `<string.h>`.

**Syntax:**
```c
int result = strcmp(str1, str2);
```

**Return value meaning:**

| Return Value | Meaning |
|---|---|
| `0` | Strings are exactly equal |
| `< 0` (negative) | `str1` comes before `str2` alphabetically |
| `> 0` (positive) | `str1` comes after `str2` alphabetically |

**Example Program:**
```c
#include <stdio.h>
#include <string.h>
int main() {
    char str1[] = "apple";
    char str2[] = "banana";
    char str3[] = "apple";

    printf("%d\n", strcmp(str1, str2));   // negative ('a' < 'b')
    printf("%d\n", strcmp(str2, str1));   // positive ('b' > 'a')
    printf("%d\n", strcmp(str1, str3));   // 0 (equal)

    if (strcmp(str1, str3) == 0) {
        printf("str1 and str3 are the same\n");
    }
    return 0;
}
```

**`strncmp()` — compares only the first `n` characters:**
```c
#include <string.h>
int result = strncmp("hello123", "hello456", 5);   // compares only "hello" vs "hello"
printf("%d\n", result);   // 0 (first 5 characters match)
```

---

## 8. Introduction to String Handling Functions

All the following functions are declared in the header file **`<string.h>`**, which must be included to use them.

| Function | Purpose | Example | Result |
|---|---|---|---|
| `strlen(s)` | Returns length of string (excludes `\0`) | `strlen("Hello")` | 5 |
| `strcpy(dest, src)` | Copies `src` string into `dest` | `strcpy(a, "Hi")` | `a` becomes "Hi" |
| `strncpy(dest, src, n)` | Copies only first `n` characters | `strncpy(a, "Hello", 3)` | `a` becomes "Hel" |
| `strcat(dest, src)` | Appends `src` to end of `dest` | `strcat(a, "!")` | appends "!" |
| `strncat(dest, src, n)` | Appends only first `n` characters of `src` | — | — |
| `strcmp(s1, s2)` | Compares two strings | `strcmp("a","b")` | negative |
| `strncmp(s1, s2, n)` | Compares first `n` characters | — | — |
| `strchr(s, ch)` | Finds first occurrence of a character in string | `strchr("Hello",'l')` | pointer to first 'l' |
| `strstr(s1, s2)` | Finds first occurrence of one string inside another | `strstr("Hello","ll")` | pointer to "llo" |
| `strrev(s)` | Reverses a string (non-standard, compiler-specific) | `strrev("abc")` | "cba" |
| `strlwr(s)` | Converts string to lowercase (non-standard) | `strlwr("ABC")` | "abc" |
| `strupr(s)` | Converts string to uppercase (non-standard) | `strupr("abc")` | "ABC" |

**Example Program using multiple string functions:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[50] = "Hello World";
    char copy[50];

    printf("Length of str: %lu\n", strlen(str));     // 11

    strcpy(copy, str);
    printf("Copied string: %s\n", copy);              // Hello World

    if (strstr(str, "World") != NULL) {
        printf("'World' found inside str\n");
    }

    char *pos = strchr(str, 'W');
    printf("First 'W' found at: %s\n", pos);          // World

    return 0;
}
```
**Output:**
```
Length of str: 11
Copied string: Hello World
'World' found inside str
First 'W' found at: World
```

> **Note:** `strrev()`, `strlwr()`, and `strupr()` are **not part of the ANSI C standard** — they're compiler extensions (common in Turbo C / older Windows compilers) and may not be available on GCC/Linux. Portable alternatives use loops with `tolower()`/`toupper()` from `<ctype.h>`.

**Example Program: Manual string reversal (portable way)**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello";
    int len = strlen(str);

    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - 1 - i];
        str[len - 1 - i] = temp;
    }

    printf("Reversed: %s\n", str);   // olleH
    return 0;
}
```

---

## Quick Revision Summary

| Concept | One-line takeaway |
|---|---|
| One-Dimensional Array | Linear list of same-type elements, indexed from 0 |
| Declaration (1-D) | `data_type array_name[size];` |
| Initialization (1-D) | List `{...}` at declaration, loop, or element-by-element |
| Two-Dimensional Array | Matrix/table of elements: `array[rows][columns]` |
| Initialization (2-D) | Row-wise braces `{{...},{...}}` or nested loops |
| String | Character array terminated by `\0` (null character) |
| Declaring/Initializing Strings | `char name[size] = "text";` — size must include room for `\0` |
| Reading Strings | `scanf("%s",...)` (stops at space); `fgets()` for full lines (safe) |
| Writing Strings | `printf("%s",...)` or `puts()` (auto newline) |
| Concatenation | `strcat(dest, src)` — dest must have enough space |
| Comparison | `strcmp(s1, s2)` — returns 0 if equal, else negative/positive |
| String Functions | `strlen, strcpy, strncpy, strcat, strcmp, strchr, strstr` from `<string.h>` |

---
*End of Unit 4 Notes*
