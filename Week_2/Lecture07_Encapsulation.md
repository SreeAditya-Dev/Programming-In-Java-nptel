# Study notes for Programming In Java : Week 2 : : Lecture 07 : Encapsulation

## Introduction

Encapsulation is a core concept in object-oriented programming, particularly in Java. This principle refers to the practice of bundling data and the methods that operate on this data into a single unit known as a class. Encapsulation plays a foundational role in defining and managing the structure and behavior of objects within Java applications. The following guide explores the concept of encapsulation, the structure and components of classes in Java, including fields, methods, and constructors, and demonstrates practical use cases like single and multiple class declarations, construction and use of objects, and the special role of constructors, overloading, and the 'this' keyword within class definitions.

---

## The Concept of a Class in Java and Encapsulation

### Basics of Classes
- A class is the fundamental building block in Java, acting as a template or blueprint for creating objects.
- Each class provides the structure (data and behavior) an object will have.
- Classes are user-defined and can be customized according to program requirements.
- The elements that make up a class typically include fields (data variables), methods (functions), constructors (special methods for initialization), blocks, nested classes, and interfaces.

#### Primary Elements in a Class
1. **Fields (Member Variables):** 
   - Hold the state or attributes of an object (e.g., for a Circle class: radius, x, y coordinates).
   - Can be of primitive data types (int, float, etc.) or object references.

2. **Methods:**
   - Define the operations (functions) that manipulate or utilize the fields.
   - Allow objects to exhibit behaviors (e.g., calculating area, circumference).

3. **Constructors:**
   - Special functions for initializing new objects, often with default or specific values.

4. **Blocks, Nested Classes, Interfaces:**
   - Advanced elements extending the functionality and organization of classes (only briefly mentioned).

### Encapsulation: Definition and Mechanism
- Encapsulation means combining a classâ€™s data (fields) and its behavior (methods) into a single unit.
- This separation helps in managing complexity and improves security by restricting direct access to some of the object's components.
- The outside code interacts with the fields via methods rather than accessing them directly.
- In Java, encapsulation is achieved by:
   - Declaring fields as private
   - Providing public methods (getters, setters) for controlled access

#### Encapsulation Table
| Aspect        | Description                       |
|--------------|-----------------------------------|
| Data         | Fields/Attributes (e.g., x, y, r) |
| Operations   | Methods (e.g., area(), circumference()) |
| Encapsulation| Data + Operations in one class    |

---
## Defining a Class: Structure and Example

### General Class Structure
- A class is defined with the `class` keyword, a user-defined name, variables, and methods.
- Syntax (pseudo-code):
  ```java
  class ClassName {
      // Fields
      // Methods
      // Constructors
  }
  ```

### Example: Defining a Circle Class
#### Defining Fields
- For a Circle, fields might be:
  - `float r;` // radius
  - `float x;` // x-coordinate
  - `float y;` // y-coordinate

#### Defining Methods
- Functions relevant to a circle:
  - `float circumference()`: returns the circumference using `2 * Math.PI * r`
  - `float area()`: returns the area using `Math.PI * r * r`

#### Combined Class Definition
```java
class Circle {
    float r;
    float x;
    float y;
    float circumference() {
        return 2 * Math.PI * r;
    }
    float area() {
        return Math.PI * r * r;
    }
}
```

#### Features
- Encapsulates data (r, x, y) and operations (circumference, area).

---
## Using Classes and Objects

### Object Creation and Initialization
- To use a class, declare and initialize objects from it:
  ```java
  Circle c = new Circle();
  c.x = 0.0f;
  c.y = 0.0f;
  c.r = 5.0f;
  ```
- Objects are instances of classes, each with their own field values.

### Accessing Fields and Methods
- Access fields using dot notation, e.g., `c.x`, `c.y`, and `c.r`
- Call methods using the same syntax, e.g., `c.circumference()`, `c.area()`
- Example:
  ```java
  System.out.println(c.circumference());
  System.out.println(c.area());
  ```

### Creating Multiple Objects
- Multiple objects can be instantiated from the same class:
  ```java
  Circle c1 = new Circle();
  Circle c2 = new Circle();
  c1.x = 3.0f; c1.y = 4.0f; c1.r = 5.0f;
  c2.x = -4.0f; c2.y = -8.0f; c2.r = 10.0f;
  ```
- Each object maintains its own state.

#### Table: Examples of Circle Objects
| Object | x    | y    | r    |
|--------|------|------|------|
| c1     | 3.0  | 4.0  | 5.0  |
| c2     | -4.0 | -8.0 | 10.0 |

---
## Multiple Classes in Programs

### Declaring and Using Multiple Classes
- It's common to define several classes in one Java program (file), each representing a different type of object.
- Example: Along with `Circle`, define a `Box` class:
  ```java
  class Box {
      float width, height, depth;
      float area() { /* code */ }
      float volume() { /* code */ }
  }
  ```
- Objects of different classes can be created and manipulated within the program:
  ```java
  Circle c = new Circle();
  Box b = new Box();
  ```

### Program with Multiple Classes
- The main program (class with the main method) can create and use multiple objects:
  ```java
  public class MulticlassDemo {
      public static void main(String[] args) {
          Circle c = new Circle();
          Box b = new Box();
          // Initialize and use objects...
      }
  }
  ```
- All class definitions and the main class can reside in the same `.java` file (named after the main class).

#### Important Points
- Only one class should include the `main` method per file; this is the entry point for execution.
- Attempting to execute a Java program without a main class (having `main`) will lead to a compilation error.
- Filename must match the main class name.

---
## Initialization and Constructors

### Methods for Initializing Objects
- Objects require initialization to set up their internal state (field values).
- Can be done by explicitly assigning values after creation, via methods, or automatically using constructors.

#### Initialization via Method (e.g., setCircle)
- A method can be added to initialize all fields at once:
  ```java
  void setCircle(float a, float b, float c){
      x = a;
      y = b;
      r = c;
  }
  ```
- Usage:
  ```java
  c1.setCircle(3.0f, 4.0f, 5.0f);
  c2.setCircle(-4.0f, 8.0f, 10.0f);
  ```

#### Initialization Using Constructors
- A constructor is a special method automatically invoked when an object is created.
- Characteristics:
  - Same name as the class
  - No return type (not even void)
- Used to ensure the object begins with a specified state.

##### Example of a Constructor:
```java
class Circle {
    float x, y, r;
    Circle(float a, float b, float c) {
        x = a;
        y = b;
        r = c;
    }
}
```
- Usage:
  ```java
  Circle c1 = new Circle(3.0f, 4.0f, 5.0f);
  Circle c2 = new Circle(-4.0f, 8.0f, 10.0f);
  ```

### The `this` Keyword
- Used to distinguish between instance variables and parameters with the same name.
- In constructors and methods, `this.x` refers to the current object's field, `x` to the parameter.
- Example:
  ```java
  Circle(float x, float y, float r) {
      this.x = x;
      this.y = y;
      this.r = r;
  }
  ```
- Also used to invoke another constructor from the current constructor within the same class.

---
## Constructor Overloading (Multiple Constructors)

### Definition
- Java allows more than one constructor in a class, each with different parameters.
- Facilitates initialization flexibility (e.g., providing all, some, or no initial values).

#### Example of Overloaded Constructors
```java
class Circle {
    float x, y, r;
    // Constructor 1: three parameters
    Circle(float x, float y, float r) {
        this.x = x;
        this.y = y;
        this.r = r;
    }
    // Constructor 2: only radius
    Circle(float r) {
        this(0, 0, r);
    }
    // Constructor 3: copy constructor
    Circle(Circle c) {
        this(c.x, c.y, c.r);
    }
    // Constructor 4: default
    Circle() {
        this(0, 0, 1);
    }
}
```

#### Usage Scenarios
1. All properties specified:
   ```java
   Circle c1 = new Circle(3.0f, 4.0f, 5.0f);
   ```
2. Only radius specified:
   ```java
   Circle c2 = new Circle(7.0f);
   ```
3. Copying another Circle:
   ```java
   Circle c3 = new Circle(c1);
   ```
4. No parameters (defaults):
   ```java
   Circle c4 = new Circle();
   ```

##### Table: Constructor Forms
| Constructor            | Usage Example           | Description                                     |
|------------------------|------------------------|-------------------------------------------------|
| Three parameters       | Circle(3, 4, 5)        | Full initialization                             |
| One parameter (radius) | Circle(7)              | Default center at (0,0), radius=7               |
| Copy constructor       | Circle(existingCircle)  | Cloning an existing object's state              |
| Default                | Circle()               | Center (0,0), radius=1                          |

### The `this` Keyword in Constructor Chaining
- `this()` can be used in a constructor to call another constructor from the same class.
- Helps reuse initialization code and ensures consistency.
- Example:
  ```java
  Circle(float r) {
      this(0, 0, r); // calls the other constructor
  }
  ```

### Namespace Resolution with `this`
- Prevents ambiguity when field names and parameters are the same in constructors or methods.
- Ensures correct assignment to the objectâ€™s fields.

---
## Conclusion

### Key Insights
- Encapsulation is the integration of data (fields) and operations (methods) in a class, providing structure and control in Java programs.
- Objects are instances of classes and maintain independent states, governed by the values of their fields.
- Java allows for both single and multiple objects from the same class, as well as coexistence of multiple classes within a single program file.
- Constructors enable automatic and flexible object initialization, supporting various initialization scenarios via overloading.
- The `this` keyword is vital in resolving naming conflicts and supporting constructor chaining, enhancing code clarity and reliability.
- Every Java application needs a main class (with the main method) as the programâ€™s entry point, and the source file should be named accordingly.

### Key Terms
- **Encapsulation:** The bundling of data and methods operating on the data within a class, restricting direct access to some components and providing controlled interfaces.
- **Class:** A template or blueprint for creating objects, encapsulating data (fields) and behavior (methods).
- **Object:** An instance of a class with its own unique state (field values).
- **Field/Member Variable:** A variable defined in a class representing an attribute of an object.
- **Method:** A function defined inside a class that can operate on the data fields and perform actions.
- **Constructor:** Special method with the same name as the class; automatically called on object creation for initialization; has no return type.
- **Constructor Overloading:** The practice of defining multiple constructors with different parameter lists to provide flexible object initialization.
- **this Keyword:** Refers to the current object. Used to resolve ambiguity between instance variables and parameters and to chain constructors.
- **Main Class:** The class containing the `public static void main(String[] args)` method, serving as the entry point for Java programs.
- **Namespace Resolution:** The process of distinguishing between parameters and fields with the same name using the `this` keyword.
- **Dot Notation:** The syntax for accessing fields and methods of an object (e.g., `object.field`, `object.method()`).
