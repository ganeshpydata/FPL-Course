# C Programming — Detailed Notes (Unit 3)
## Decision Making, Branching and Looping

---

# PART A: DECISION MAKING AND BRANCHING

By default, a C program executes statements **sequentially**, one after another. **Decision-making (branching) statements** allow the program to choose between different paths of execution based on whether a condition is true or false.

---

## 1. Simple `if` Statement

The simplest decision-making statement. It executes a block of code **only if** the given condition is true. If the condition is false, the block is simply skipped.

**Syntax:**
```c
if (condition) {
    // statements executed only if condition is true
}
```

**Flow:**
```
        ┌───────────┐
        │ Condition │
        └─────┬─────┘
        True  │  False
    ┌─────────┘  └─────────┐
┌───▼────┐              ┌──▼──────────┐
│ Execute │              │ Skip block  │
│  block  │              │             │
└───┬────┘              └──┬──────────┘
    └───────────┬───────────┘
                ▼
          Next statement
```

**Example Program:**
```c
#include <stdio.h>
int main() {
    int age;
    printf("Enter your age: ");
    scanf("%d", &age);

    if (age >= 18) {
        printf("You are eligible to vote.\n");
    }

    printf("Program ends.\n");   // always executes
    return 0;
}
```
**Output (age = 20):**
```
Enter your age: 20
You are eligible to vote.
Program ends.
```
**Output (age = 15):**
```
Enter your age: 15
Program ends.
```

---

## 2. If-Else Statement

Executes **one block if the condition is true**, and a **different block if it is false**. Provides a two-way branch.

**Syntax:**
```c
if (condition) {
    // executed if condition is true
} else {
    // executed if condition is false
}
```

**Example Program:**
```c
#include <stdio.h>
int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (num % 2 == 0) {
        printf("%d is Even\n", num);
    } else {
        printf("%d is Odd\n", num);
    }
    return 0;
}
```
**Output (num = 7):**
```
Enter a number: 7
7 is Odd
```

---

## 3. Else-If Ladder (Nested if-else)

Used when there are **multiple conditions** to check in sequence. Each condition is tested in order; as soon as one is true, its block executes and the rest are skipped.

**Syntax:**
```c
if (condition1) {
    // block 1
} else if (condition2) {
    // block 2
} else if (condition3) {
    // block 3
} else {
    // default block (none of the conditions matched)
}
```

**Example Program: Grading System**
```c
#include <stdio.h>
int main() {
    int marks;
    printf("Enter marks (0-100): ");
    scanf("%d", &marks);

    if (marks >= 90) {
        printf("Grade: A\n");
    } else if (marks >= 75) {
        printf("Grade: B\n");
    } else if (marks >= 60) {
        printf("Grade: C\n");
    } else if (marks >= 40) {
        printf("Grade: D\n");
    } else {
        printf("Grade: F (Fail)\n");
    }
    return 0;
}
```
**Output (marks = 82):**
```
Enter marks (0-100): 82
Grade: B
```

**Nested if (if inside another if):**
```c
#include <stdio.h>
int main() {
    int a = 10, b = 20, c = 15;
    if (a > b) {
        if (a > c)
            printf("A is largest\n");
        else
            printf("C is largest\n");
    } else {
        if (b > c)
            printf("B is largest\n");
        else
            printf("C is largest\n");
    }
    return 0;
}
// Output: B is largest
```

---

## 4. Switch Statement

Used as an alternative to a long `else-if` ladder when comparing **one variable against multiple fixed (constant) values**. More readable for such cases.

**Syntax:**
```c
switch (expression) {
    case value1:
        // statements
        break;
    case value2:
        // statements
        break;
    ...
    default:
        // statements if no case matches
}
```

**Key rules:**
- `expression` must evaluate to an integer or character (not float/string).
- `case` values must be constants and unique.
- `break` exits the switch; without it, execution **"falls through"** into the next case.
- `default` is optional and executes when no case matches.

**Example Program: Simple Calculator**
```c
#include <stdio.h>
int main() {
    char op;
    float a, b;

    printf("Enter operator (+,-,*,/): ");
    scanf(" %c", &op);
    printf("Enter two numbers: ");
    scanf("%f %f", &a, &b);

    switch (op) {
        case '+':
            printf("Result = %.2f\n", a + b);
            break;
        case '-':
            printf("Result = %.2f\n", a - b);
            break;
        case '*':
            printf("Result = %.2f\n", a * b);
            break;
        case '/':
            if (b != 0)
                printf("Result = %.2f\n", a / b);
            else
                printf("Error: Division by zero\n");
            break;
        default:
            printf("Invalid operator\n");
    }
    return 0;
}
```
**Output (op='*', a=4, b=5):**
```
Enter operator (+,-,*,/): *
Enter two numbers: 4 5
Result = 20.00
```

**Example illustrating "fall-through" (missing break):**
```c
#include <stdio.h>
int main() {
    int day = 2;
    switch (day) {
        case 1:
        case 2:
        case 3:
        case 4:
        case 5:
            printf("Weekday\n");
            break;
        case 6:
        case 7:
            printf("Weekend\n");
            break;
        default:
            printf("Invalid day\n");
    }
    return 0;
}
// Output: Weekday
// (cases 1-5 share the same block because there's no break between them)
```

**Switch vs If-Else Ladder:**

| Switch | If-Else Ladder |
|---|---|
| Compares one variable to constant values | Can test any complex/relational condition |
| Faster for many discrete values | Can be slower for many conditions |
| Cannot use ranges or floats directly | Can handle ranges, floats, multiple variables |

---

## 5. Goto Statement

Used to transfer control **unconditionally** to a labeled statement anywhere within the same function. Considered poor programming practice in general since it breaks structured flow, but occasionally used for breaking out of deeply nested loops.

**Syntax:**
```c
goto label;
...
label:
    statement;
```

**Example Program:**
```c
#include <stdio.h>

int main() {
    int i = 1;

    start:                      // label: goto jumps back to here
    if (i <= 5) {               // check the condition each time we arrive
        printf("%d ", i);       // print the current value of i
        i++;                    // increase i by 1
        goto start;             // jump back to the label "start"
    }
    printf("\nDone\n");         // runs only when i > 5 (condition is false)
    return 0;
}

/* How it runs:
   Step 1: i = 1 -> 1 <= 5 true  -> print 1, i = 2, goto start
   Step 2: i = 2 -> 2 <= 5 true  -> print 2, i = 3, goto start
   Step 3: i = 3 -> 3 <= 5 true  -> print 3, i = 4, goto start
   Step 4: i = 4 -> 4 <= 5 true  -> print 4, i = 5, goto start
   Step 5: i = 5 -> 5 <= 5 true  -> print 5, i = 6, goto start
   Step 6: i = 6 -> 6 <= 5 false -> skip the if block, print Done
*/

// Output:
// 1 2 3 4 5
// Done
```

**Example: using goto to break out of nested loops:**
```c
#include <stdio.h>
int main() {
    for (int i = 1; i <= 3; i++) {
        for (int j = 1; j <= 3; j++) {
            if (i == 2 && j == 2)
                goto end;   // jump straight out of both loops
            printf("i=%d j=%d\n", i, j);
        }
    }
    end:
    printf("Loop exited\n");
    return 0;
}
```

> **Why avoid goto?** It makes code harder to read, debug, and maintain since control can jump anywhere, breaking the natural top-to-bottom logical flow. Modern C style prefers loops, functions, and `break`/`continue` instead.

---

# PART B: DECISION MAKING AND LOOPING

**Loops** allow a block of statements to be executed **repeatedly** as long as a given condition holds true. This avoids writing the same code multiple times.

---

## 6. While Statement (Entry-controlled loop)

The condition is checked **before** the loop body executes. If the condition is false initially, the body **never executes** — hence called an **entry-controlled** (pre-test) loop.

**Syntax:**
```c
while (condition) {
    // loop body
}
```

**Example Program: Print numbers 1 to 5**
```c
#include <stdio.h>
int main() {
    int i = 1;
    while (i <= 5) {
        printf("%d ", i);
        i++;
    }
    return 0;
}
// Output: 1 2 3 4 5
```

**Example Program: Sum of digits of a number**
```c
#include <stdio.h>
int main() {
    int num = 1234, sum = 0, digit;

    while (num != 0) {
        digit = num % 10;   // extract last digit
        sum += digit;
        num /= 10;          // remove last digit
    }
    printf("Sum of digits = %d\n", sum);   // 1+2+3+4 = 10
    return 0;
}
```

---

## 7. Do-While Statement (Exit-controlled loop)

The condition is checked **after** the loop body executes. This guarantees the body executes **at least once**, even if the condition is false from the start — hence called an **exit-controlled** (post-test) loop.

**Syntax:**
```c
do {
    // loop body
} while (condition);   // note the semicolon
```

**Example Program:**
```c
#include <stdio.h>
int main() {
    int i = 1;
    do {
        printf("%d ", i);
        i++;
    } while (i <= 5);
    return 0;
}
// Output: 1 2 3 4 5
```

**Example showing the key difference (condition false from the start):**
```c
#include <stdio.h>
int main() {
    int i = 10;

    // while loop - body never runs
    while (i <= 5) {
        printf("while: %d\n", i);
        i++;
    }

    // do-while loop - body runs once, then checks condition
    do {
        printf("do-while: %d\n", i);   // prints once: 10
        i++;
    } while (i <= 5);

    return 0;
}
// Output: do-while: 10
```

**While vs Do-While:**

| While | Do-While |
|---|---|
| Condition checked **before** execution | Condition checked **after** execution |
| Entry-controlled loop | Exit-controlled loop |
| Body may execute 0 times | Body executes **at least once** |
| `while (condition) { }` | `do { } while (condition);` |

---

## 8. For Statement

The most compact looping construct, ideal when the **number of iterations is known** in advance. It combines initialization, condition-checking, and increment/decrement in a single line.

**Syntax:**
```c
for (initialization; condition; update) {
    // loop body
}
```

**Execution order:** initialization (once) → check condition → execute body → update → check condition again → ... until condition is false.

**Example Program:**
```c
#include <stdio.h>
int main() {
    for (int i = 1; i <= 5; i++) {
        printf("%d ", i);
    }
    return 0;
}
// Output: 1 2 3 4 5
```

**Example Program: Factorial of a number**
```c
#include <stdio.h>
int main() {
    int n = 5;
    long fact = 1;

    for (int i = 1; i <= n; i++) {
        fact *= i;
    }
    printf("Factorial of %d = %ld\n", n, fact);   // 120
    return 0;
}
```

**Variations of the for loop:**
```c
// Multiple initializations/updates using comma operator
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i=%d j=%d\n", i, j);
}

// Infinite loop (no condition) - needs break to exit
for (;;) {
    printf("This runs forever unless broken\n");
    break;   // stops after first iteration here
}

// Decrementing for loop
for (int i = 5; i >= 1; i--) {
    printf("%d ", i);
}
// Output: 5 4 3 2 1
```

**Nested for loop — Pattern printing:**
```c
#include <stdio.h>
int main() {
    for (int i = 1; i <= 4; i++) {
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        printf("\n");
    }
    return 0;
}
// Output:
// *
// **
// ***
// ****
```

**Comparison of all three loops:**

| Loop | Best Used When | Condition Check | Guarantees Execution |
|---|---|---|---|
| `while` | Number of iterations unknown | Before body | Not guaranteed |
| `do-while` | Body must run at least once (e.g., menus) | After body | Guaranteed once |
| `for` | Number of iterations known | Before body | Not guaranteed |

---

## 9. Break Statement

Used to **immediately terminate** the nearest enclosing loop (`for`, `while`, `do-while`) or `switch` statement, transferring control to the statement right after it.

**Syntax:**
```c
break;
```

**Example Program: Stop loop when a value is found**
```c
#include <stdio.h>
int main() {
    for (int i = 1; i <= 10; i++) {
        if (i == 6) {
            break;   // exit loop when i equals 6
        }
        printf("%d ", i);
    }
    return 0;
}
// Output: 1 2 3 4 5
```

**Example Program: Searching in an array**
```c
#include <stdio.h>
int main() {
    int arr[] = {4, 8, 15, 16, 23, 42};
    int key = 16, found = 0;

    for (int i = 0; i < 6; i++) {
        if (arr[i] == key) {
            found = 1;
            printf("Found %d at index %d\n", key, i);
            break;   // no need to keep searching
        }
    }
    if (!found)
        printf("Not found\n");
    return 0;
}
// Output: Found 16 at index 3
```

> In **nested loops**, `break` exits only the **innermost** loop it is placed in — not all enclosing loops.

---

## 10. Continue Statement

Used to **skip the rest of the current iteration** of a loop and move directly to the **next iteration** (re-checking the loop condition), without exiting the loop entirely.

**Syntax:**
```c
continue;
```

**Example Program: Print only odd numbers, skipping even ones**
```c
#include <stdio.h>
int main() {
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue;   // skip even numbers
        }
        printf("%d ", i);
    }
    return 0;
}
// Output: 1 3 5 7 9
```

**Example Program: Sum of numbers excluding multiples of 3**
```c
#include <stdio.h>
int main() {
    int sum = 0;
    for (int i = 1; i <= 10; i++) {
        if (i % 3 == 0) {
            continue;   // skip this iteration, don't add to sum
        }
        sum += i;
    }
    printf("Sum = %d\n", sum);   // 1+2+4+5+7+8+10 = 37
    return 0;
}
```

**Break vs Continue:**

| Break | Continue |
|---|---|
| Terminates the loop completely | Skips only the current iteration |
| Control moves **after** the loop | Control moves to the loop's next condition check |
| Used to exit early | Used to skip unwanted cases |

---

## Quick Revision Summary

| Concept | One-line takeaway |
|---|---|
| Simple if | Executes a block only when condition is true |
| If-else | Two-way branching: true block or false block |
| Else-if ladder | Tests multiple conditions in sequence, top to bottom |
| Switch | Compares one variable against multiple constant values; needs `break` |
| Goto | Unconditional jump to a label; generally avoided in structured code |
| While | Entry-controlled loop; condition checked before body runs |
| Do-while | Exit-controlled loop; body runs at least once |
| For | Compact loop with init/condition/update; best when iterations are known |
| Break | Immediately exits the nearest loop or switch |
| Continue | Skips current iteration, jumps to next loop check |

---
*End of Unit 3 Notes*
