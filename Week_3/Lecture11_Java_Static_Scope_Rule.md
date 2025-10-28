# Study notes for Programming In Java : Week 3 : : Lecture 11 : Java Static Scope Rule

## Introduction

Understanding scope rules is vital in programming as it affects variable visibility, memory, and behavior throughout a program. In Java, scope determines how variables, methods, and classes are accessed and managed. This module examines the static scope rule in detail, including the distinctions between instance and class variables, class and instance methods, the concept of nested classes, and provides programming examples illustrating these concepts. The notes also introduce recursion in Java, covering how static scope interacts with recursive methods and demonstrating with classic algorithm examples: factorial, Fibonacci series, and greatest common divisor (GCD).

---

## Static and Dynamic Scoping Concepts in Java

Java, like most modern programming languages, primarily employs the static (or lexical) scope rule. Understanding how scope is established in Java forms the basis for robust, predictable, and maintainable code.

### Static Scope
- **Definition**: Static scope (also known as lexical scope) refers to determining the scope of variables based on their location within the source code.
- **Resolution**: Variable and method references are resolved by the structure of the program text, not the runtime call stack.
- **Identification**: What a variable name refers to can be determined just by inspecting the source code.

### Dynamic Scope
- **Definition**: Variables are resolved at runtime based on the program's call stack (less common in modern programming languages like Java).
- **Java Usage**: Java strictly enforces static scope; dynamic scope is not a native feature.

#### Static Scope in Practice
Consider the following class structure:

```java
class Box {
    float x, y, w;
    float area() { ... }
}
class Circle {
    float x, y, r;
    float area() { ... }
}
```
- The variables `x` and `y` in `Box` and `Circle` are local to their respective classes. 
- `Box.x` is independent of `Circle.x`, even though both have the same name and type.

### Example: Scope Resolution in Main Program
Suppose there is a main class named `GeoClass`:

```java
class GeoClass {
    int x = 50;
    int y = 60;
    ...
}
```
- `GeoClass` has `x` and `y` as its own members.
- When objects of `Box` and `Circle` are created within `GeoClass`, say `Box b` and `Circle c`, `b.x` refers to `Box.x`, and `c.x` refers to `Circle.x`.
- Scope is resolved using the object name and the class definition.

#### Table: Illustration of Variable Scopes
| Class/Object         | Variable Name | Value      | Scope                 |
|---------------------|--------------|------------|-----------------------|
| GeoClass            | x            | 50         | GeoClass only         |
| GeoClass            | y            | 60         | GeoClass only         |
| Box (object b)      | x            | float      | Box only              |
| Circle (object c)   | x            | float      | Circle only           |

- Variables of the same name but declared in different classes/objects are distinct due to static scoping.

### Block Scope in Methods
Variables declared within a method or a block (`{ ... }`) have scope only within that block.

Example:
```java
public static void main(String[] args) {
    int x = 20; // Scope: Entire main method
    {
        int y = 20; // Scope: This inner block only
    }
    y = 100; // Compilation error: y not in scope
}
```
- `x` is accessible throughout `main`.
- `y` is not accessible outside its block.

---

## Instance and Class (Static) Variables in Java

Understanding how variables are scoped at the object and class level is crucial in Java. Java provides both instance variables and class (static) variables, each with different behavior and lifetime.

### Instance Variables
- **Definition**: Variables declared within a class but outside any method, constructor, or block, without the `static` keyword.
- **Scope and Lifetime**: Each object of the class gets its own copy of instance variables. The scope is within the class, and for the object's lifetime.
- **Memory**: Separate storage for each object.

#### Example:
```java
class Box {
    float x, y, w;
}
Box b1 = new Box();
Box b2 = new Box();
```
- `b1.x`, `b2.x`, etc., are all distinct; changes to one object's instance variable donâ€™t affect others.

### Class (Static) Variables
- **Definition**: Declared within a class using the `static` keyword.
- **Scope and Lifetime**: Single copy shared by all instances of the class. Lifetime is for the duration of the program.
- **Memory**: Stored in the class area; not tied to specific object instances.

#### Example:
```java
class Box {
    static float w;
    float x, y;
}
Box.w = 20; // Accessible via the class
```

- All objects of `Box` share the same `w`. Changing `Box.w` affects all instances.

| Type of Variable | Declaration Example      | Lifetime             | Scope                | Number of Copies      |
|------------------|------------------------|----------------------|----------------------|----------------------|
| Instance         | float x;               | Objectâ€™s lifetime    | Belongs to object    | One per object       |
| Class (Static)   | static float w;        | Program's lifetime   | Belongs to class     | One per class        |

### Accessing Variables: Syntax
- **Instance Variable**: `objectName.instanceVar`
- **Class Variable**: `ClassName.classVar` or `objectName.classVar` (both legal but the class name is preferred)

---

## Class (Static) and Instance Methods

Java methods, like variables, can be instance (non-static) or class (static) methods, influencing how and when they are used.

### Instance Methods
- **Definition**: Regular methods without `static` keyword.
- **Access Requirements**: Need an object to invoke.
- **Typical Use**: Methods that operate on instance variables.

#### Example:
```java
class Circle {
    double r;
    double area() { return Math.PI * r * r; }
}
Circle c = new Circle();
c.area();
```

### Static Methods
- **Definition**: Defined with the `static` keyword.
- **Access Requirements**: Can be called without any object. Invoked using the class name.
- **Typical Use**: Utility or helper functions; modifying static variables.

#### Example:
```java
class MathHelper {
    static int max(int a, int b) { return a > b ? a : b; }
}
MathHelper.max(5, 7);
```

### Overloading with Static and Instance Methods
- Java allows method overloading, i.e., multiple methods with the same name but different parameters.
- Static and instance methods with the same name can coexist, but their context of invocation and usage differ.

#### Example:
```java
class Circle {
    double r;
    Circle bigger(Circle c) { ... } // instance method
    static Circle bigger(Circle a, Circle b) { ... } // static method
}
```
- `c1.bigger(c2)` calls an instance method.
- `Circle.bigger(c1, c2)` calls a static method.

---

## Nested Classes in Java

A nested class is defined within another class's scope. This influences its visibility and applicability.

### Types of Nested Classes
1. **Static Nested Class**: Declared with the `static` modifier. Associated with its outer class (not its outer class's instance).
2. **Non-Static (Inner) Class**: Tied to an instance of the enclosing class; cannot have static declarations within.

### Properties and Usage
- Nested classes are used to logically group classes only used in one place.
- They help in encapsulation and improve code readability.
- Access: A nested class is more restricted in access than top-level classes.

### Example: Static Nested Class
```java
class Circle {
    static class Point {
        int x, y;
        void display() { ... }
    }
}
```
- Here, `Point` is local to `Circle` â€“ cannot be used outside unless via `Circle.Point`.

#### Table: Summary of Nested Class Properties
| Nested Class Type | Static/Non-Static | Access to Outer Instance | Usage               |
|-------------------|-------------------|-------------------------|---------------------|
| Static            | Yes               | No                      | Utility, grouping   |
| Inner             | No                | Yes                     | Stateful logic      |

### Example Program Using Nested Class
- The nested `Point` class is used only for defining helper points inside a `Circle`.
- This increases encapsulation: only code inside `Circle` can use `Point` directly.
- Accessing a nested class externally is restricted; for static nested class: `Circle.Point pt = new Circle.Point();`.

---

## Recursion in Java: Concepts and Applications

Recursion is a process where a method calls itself to solve subproblems. Static scoping ensures that each recursive call gets its own scope for local variables.

### Definition of Recursion
- A method that calls itself directly or indirectly
- Two key requirements:
    1. **Base (Termination) Case**: When to stop
    2. **Recursive Case**: How the problem breaks into smaller subproblems

### Example: Factorial Calculation
- **Mathematical Definition:**
    - n! = n Ã— (n-1)! for n > 0
    - 0! = 1

#### Recursive Implementation in Java:
```java
int factorial(int n) {
    if (n == 0) return 1; 
    else return n * factorial(n - 1); 
}
```
- Each function call has its own variable scope due to static scoping rules.

#### Iterative Version for Comparison:
```java
int factorial(int n) {
    int result = 1;
    for(int i = 1; i <= n; i++) result *= i;
    return result;
}
```

| Approach    | Memory Usage           | Clarity           | Stack Depth    |
|-------------|-----------------------|-------------------|---------------|
| Recursive   | Function call stack   | Closer to math    | n+1           |
| Iterative   | Local variables only  | More explicit     | 1             |

### Example: Fibonacci Series
- **Mathematical Definition:**
    - F(0) = 0; F(1) = 1
    - F(n) = F(n-1) + F(n-2) for n > 1

#### Recursive Implementation:
```java
int fibonacci(int n) {
    if (n == 0) return 0;
    else if (n == 1) return 1;
    else return fibonacci(n-1) + fibonacci(n-2);
}
```
- Note: Recursive Fibonacci is elegant but inefficient for large n due to repeated calculations.

#### Iterative Implementation:
```java
int fibonacci(int n) {
    int a = 0, b = 1, c;
    for (int i = 2; i <= n; i++) {
        c = a + b;
        a = b; b = c;
    }
    return b;
}
```
- This is memory efficient and avoids repeated subtraction.

### Example: GCD (Greatest Common Divisor) using Recursion
- **Euclidâ€™s Algorithm:**
    - GCD(a, b) = GCD(b, a % b) for b â‰  0
    - GCD(a, 0) = a

#### Recursive Implementation
```java
int gcd(int a, int b) {
    if (b == 0) return a;
    else return gcd(b, a % b);
}
```
- Each recursive call is resolved according to the static scope rules.

#### Table: Recursion vs Iteration
| Problem           | Recursive Approach                       | Iterative Approach               |
|-------------------|------------------------------------------|----------------------------------|
| Factorial         | Call stack grows to n                    | Simple loop                      |
| Fibonacci         | Exponential calls for n                  | Linear time with previous values |
| GCD               | Logarithmic calls                        | While loop                       |
- Recursive solutions are elegant for many problems, but iteration can be more efficient in practice.

---

## Conclusion

### Key Insights
- **Static scope is fundamental to Java:** Variable and method binding is determined lexically, not at runtime.
- **Instance vs Class Variables:** Instance variables are object-specific; class (static) variables are shared across all instances.
- **Method Scope:** Instance methods need an object; static methods can be invoked via the class.
- **Nested Classes:** Allow encapsulating helper classes within classes, adding structure and hiding implementation details.
- **Recursion:** Static scope supports recursive methods by ensuring each function callâ€™s variables are isolated, and recursion solves many algorithms elegantly.

### Key Terms
- **Static Scope:** Compile-time binding of variable/method references based on code structure.
- **Dynamic Scope:** Runtime binding via call stack (not used in Java).
- **Instance Variable:** Variable unique to each object instance.
- **Class Variable (Static Variable):** Shared variable among all class instances, defined with `static` keyword.
- **Instance Method:** Non-static method requiring an object to invoke.
- **Static Method (Class Method):** Method declared with `static` keyword, invocable via class name.
- **Nested Class:** Class declared within another class, scope limited to enclosing class or block.
- **Recursion:** Technique where a function calls itself to solve problems by dividing them into subproblems.
- **Base Case (in Recursion):** Condition under which recursive calls end.
- **Fibonacci Sequence:** Numeric sequence where each term is the sum of its two predecessors, often used to illustrate recursion.
- **GCD (Greatest Common Divisor):** The largest number dividing two numbers, commonly calculated using recursion with Euclidâ€™s algorithm.
