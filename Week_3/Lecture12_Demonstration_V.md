# Study notes for Programming In Java : Week 3 : : Lecture 12 : Demonstration-V

## Introduction

This set of notes covers several foundational programming concepts in Java, with a focus on demonstrating control structures (while, do-while, for loops), decision structures (if-else and switch-case), scope rules (static, block, and variable scopes), object-oriented aspects (instance vs. class variables and methods), and writing recursive functions. The explanations are supported with example scenarios, emphasizing the understanding of the flow of program execution, variable visibility, and recursive design patterns. These concepts are critical for developing robust and error-free Java programs.

---

## Loop Structures in Java

Loops are control structures that repeatedly execute a block of code as long as a condition remains true.

### The while Loop
- A pre-test loop; checks the condition before executing the loop body.
- Syntax: `while (condition) { /* block of statements */ }`
- The loop body may never execute if the condition is initially false.
- Common use case: Indeterminate or input-driven loops.
- Example:
    - Print the first ten odd numbers using a while loop.
    - Initialization: `count = 0`.
    - Condition: `count < 11`.
    - Inside the loop: Print current odd number, then increment count.

### The do-while Loop
- A post-test loop; executes the loop body at least once before checking the condition.
- Syntax: `do { /* block of statements */ } while (condition);`
- Guarantees at least one execution of the body.
- Example:
    - Print the first ten even numbers using a do-while loop.
    - Initialization is before the loop.
    - Condition is checked after executing the loop body.

**Difference between while and do-while:**
| Feature              | while                     | do-while                              |
|----------------------|--------------------------|---------------------------------------|
| Condition check      | Before loop body         | After loop body                       |
| Execution guarantee  | 0 or more times          | At least once                         |

### The for Loop
- Suitable when the number of iterations is known beforehand.
- Syntax: `for (initialization; condition; update) { /* block */ }`
- Packs initialization, condition, and update in one line.
- Example:
    - Print integers from 1 to 10.
    - All control over `i` (loop variable) is managed in the for statement.
- Behavior mirrors while/do-while in functionality but structure is more concise for count-based iterations.

#### Three Elements of For Loop
1. Initialization: Variable setup (e.g., `int i=1;`)
2. Condition: Continuation check (e.g., `i<11;`)
3. Update: Progression of iteration (e.g., `i++`)

### Loop Control Statements

#### continue Statement
- When encountered, skips the remaining loop body and proceeds to the next iteration.
- Usage example:
    - Skip printing even numbers in a for loop.
    - If `i` is even, execute `continue`, so printing occurs only for odd `i`.

#### break Statement
- Exits the loop prematurely, regardless of the loop condition.
- Typically used with a runtime condition.
- Example:
    - Infinite for loop (`for(;;)`) but ends when `i` reaches a multiple of 10 using `break`.
- Key point: `break` allows terminating both definite and indefinite loops under special conditions.

---

## Decision Structures

### if-else Statement
- Used to decide which block of code to execute among two alternatives based on a condition.
- Syntax straightforward from C/C++.
- Enables binary branching logic.

### switch-case Statement
- Selects one among many code blocks to execute.
- Useful for multi-way branching based on a single variable's value.
- Syntax:
    ```java
    switch (expression) {
        case value1:
            // actions
            break;
        case value2:
            // actions
            break;
        ...
        default:
            // actions
    }
    ```
- Each case ends with a `break` to prevent fall-through.
- Example usage:
    - Continuously prompt the user in a `do-while` until a valid choice (1-5) is provided.
    - Based on input, execute different code blocks for each case.
- Exiting the loop requires entering a value outside the specified range.

#### Multi-Condition Decision Example
- Demonstrated by a program that checks if a number is prime:
    - For loop checks divisibility from 2 to half of the number.
    - Boolean flag indicates primality.
    - Early exit using `break` once a divisor is found.
    - Showcases combined use of for loop and if statement for complex checks.

---

## Scope Rules in Java

Scope determines where in the code a variable can be accessed or modified. Understanding scope rules prevents common programming errors and improves code robustness.

### Block Scope
- Variables declared inside `{}` are valid only within that block.
- Accessing these variables outside the block leads to compile-time errors.
- Example:
    - Declaring `int x=10;` inside an inner block.
    - `System.out.println(x);` is valid inside but not outside the block.
    - Attempting to use `x` outside the block causes a compilation error.

### Loop Variable Scope
- Declaring a variable in a loop statement (e.g., `for(int x=0; ...)`) limits its visibility to the loop.
- Attempting to use the loop variable after the loop's body ends in a compilation error.
- If the variable is declared outside the loop, it remains accessible after the loop as well.

#### Table: Scope Examples
| Declaration Location           | Scope                                              |
|-------------------------------|---------------------------------------------------|
| Inside main method block       | Throughout main method                             |
| Inside an inner block          | Within the inner block only                        |
| Inside a for loop statement    | Inside the for loop body only                      |
| Outside the for loop           | From point of declaration to end of containing block |

### Static Scope in Java
- Also known as lexical scope.
- Variable visibility is determined at compile time, not at runtime.
- Variables declared at class level (fields) are accessible throughout the class (if access modifier allows).
- Java does not support true global variables; everything is within a class.

### Instance vs. Class Variables
#### Instance Variables
- Belong to individual objects of a class.
- Declared without `static` keyword.
- Each object has its own copy of the variable.

#### Class Variables (Static Variables)
- Declared using the `static` keyword.
- Shared across all objects of the class.
- Example: `static int circleCount;`
- Modifying a static variable through any object or directly through the class affects the value for all instances.

#### Example:
1. Three objects (`c1`, `c2`, `c3`) of class `Circle` are created.
2. Each object's construction increments the static variable `circleCount`.
3. Printing `c1.circleCount`, `c2.circleCount`, and `c3.circleCount` gives the same value (latest count).

| Variable Type           | Belongs to             | Initialized via       | Shared?   |
|------------------------|------------------------|-----------------------|-----------|
| Instance variable      | Object                 | Object constructor    | No        |
| Class (static) variable| Class                  | Class (static context)| Yes       |

---

## Class and Instance Methods

### Instance Methods
- Require an object to be invoked.
- Operate on the instance variables and can use `this` keyword.
- Invoked via object reference, e.g., `obj.methodName()`.
- Example: Determining if one circle is bigger than another using instance method.

### Class (Static) Methods
- Declared with the `static` keyword.
- Can be called using the class name; do not require object creation.
- Cannot access instance variables directly (unless via object passed as argument).
- Used for utility or helper methods or operations that don't depend on object state.
- Example: A method that compares two objects and returns the larger one.

#### Difference Summary Table
| Feature        | Instance Method         | Class (Static) Method |
|----------------|------------------------|----------------------|
| Invocation     | Object required         | Class name or object |
| Access         | Can access instance and static variables | Can only access static variables |
| Use case       | Object-specific logic   | Utility/shared logic |

#### Usage Example:
- Two overloaded methods `bigger`: one as instance method (`public Circle bigger(Circle c)`), another static (`public static Circle bigger(Circle a, Circle b)`).
- Static method invoked as `Circle.bigger(a, b)`, instance method as `a.bigger(b)`.

---

## Recursive Program Writing in Java

Recursion involves a function calling itself to solve smaller subproblems of the same task. Each recursive function should have:
1. A base (termination) case.
2. A recursive case that breaks the task into simpler instances.

### Factorial Calculation
- Recursive definition: `fact(n) = n * fact(n-1)` with base case `fact(0) = 1`.
- Recursive method defined in a class; called with user input.
- Demonstrates terminating condition and recursive multiplication.
- Limitation: Stack overflow or integer overflow for very large `n`. Use `long` if higher limits are needed.

### Fibonacci Sequence Generation
- Recursive definition: `fib(n) = fib(n-1) + fib(n-2)` with `fib(0) = 0`, `fib(1) = 1`.
- Prints the sequence up to a user-defined number.
- Contains two base cases and a recursive call.
- Inefficient for large values due to repeated calculations; iterative version or memoization preferred for large `n`.

### GCD Calculation (Euclidâ€™s Algorithm)
- Recursive definition:
    - If `n == 0`, GCD is `m`.
    - Otherwise, return `gcd(n, m % n)`.
- Handles several termination conditions (e.g., if either value is 0).
- Demonstrates robust recursive structure with input checking.
- Only accepts integer inputs; non-integer produces runtime error.

#### Important Points in Recursive Programs
- Every recursive method must define at least one termination (base) case to avoid infinite recursion.
- Each call creates a new stack frame; improper base case leads to stack overflow.
- Useful for problems naturally broken into smaller subproblems: factorial, Fibonacci, GCD, tree traversal, etc.

#### Example: Recursively Printing Numbers
- A method that prints a counter before and after the recursive call to demonstrate call stack unwinding.

#### Table: Recursion vs. Iteration
| Aspect              | Recursion             | Iteration                |
|---------------------|-----------------------|--------------------------|
| Termination         | Base case             | Loop condition           |
| Performance         | May use more memory (due to stack frames) | Often better (no stack frames) |
| Clarity             | Clear for divide-and-conquer | Sometimes less expressive |
| Risk                | Stack overflow        | Infinite loop if not careful |

---

## Conclusion

### Key Insights
- Java offers three primary loop constructs: while, do-while, and for. Understanding their nuances helps select the appropriate control structure for a given problem.
- Break and continue statements allow finer control over loop execution, enabling early termination or skipping steps as needed.
- Scope rules in Java are based on where variables are declared. Access outside of scope results in compile-time errors.
- Java does not permit global variables in the C/C++ sense. Instead, static variables at the class level act as shared data among instances.
- Instance methods require objects for invocation; class (static) methods can be called on the class itself and do not have access to instance variables unless passed explicitly.
- Recursive programming is a powerful paradigm available in Java, but requires careful handling of base cases and understanding of stack-based execution.
- Most iterative (loop-based) problems can also be solved recursively, and vice versa, but they may differ in performance and applicability.

### Key Terms
- **while loop**: A control structure that checks its continuation condition before executing its body.
- **do-while loop**: Loop structure that executes at least once before checking the continuation condition.
- **for loop**: Loop with initialization, condition-check, and update in one statement, ideal for count-based iteration.
- **break statement**: Ends loop execution prematurely.
- **continue statement**: Skips the current loop body and proceeds with the next iteration.
- **if-else statement**: Allows for binary decisions within code based on conditions.
- **switch-case statement**: Provides multi-way branching based on the value of a single variable.
- **scope**: The area of the code in which a variable is accessible.
- **block scope**: Scope limited to the block (enclosed by `{}`) where a variable is defined.
- **instance variable**: A field defined in a class and possessed individually by each object of the class.
- **static (class) variable**: A field defined with the `static` keyword; shared among all instances of the class.
- **instance method**: A method that operates on instance variables, requiring object reference for invocation.
- **class (static) method**: Declared with the `static` keyword; called on the class without a specific object.
- **recursion**: The process in which a method calls itself to solve subdivided instances of a problem.
- **base case**: The stopping condition for a recursive method.
- **stack overflow**: Runtime error caused by excessive function calls without proper termination, typically in recursive methods.
