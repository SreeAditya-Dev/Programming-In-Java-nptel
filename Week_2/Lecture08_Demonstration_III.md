# Study notes for Programming In Java : Week 2 : : Lecture 08 : Demonstration-III

## Introduction

Encapsulation is a foundational concept in object-oriented programming (OOP), serving as a technique for bundling data and methods that operate on that data within a single unit known as a class. This approach restricts direct access to internal object details, ensuring modifiability, maintainability, and security of code. In this set of notes, we delve into encapsulation through practical Java demonstrations. We will discuss the creation and initialization of classes and objects, usage and overloading of constructors, the concept of namespace collision and the resolution using the `this` keyword, and best practices in object initialization. A thorough exploration of these topics will enhance your understanding of how encapsulation structures robust Java programs.

---

## Creation and Initialization of Classes and Objects

### Defining Classes in Java
- A class is a blueprint for objects, defining which data (fields or attributes) and methods (functions or behaviors) are bundled together.
- Example: The `Circle` class with three double-type data fields: `x`, `y`, and `r` (representing coordinates and radius), and methods to calculate circumference and area.

#### Syntax Example:
```java
class Circle {
    double x, y, r;
    double circumference() { ... }
    double area() { ... }
}
```

### Creating Objects from Classes
- To use a class, you instantiate objects from it (creating an instance of the class).
- Standard procedure uses the `new` keyword and the class constructor:
  - `Circle c = new Circle();`
- Data members of the object (e.g., `x`, `y`, `r`) can be assigned values after object creation:
  - `c.x = 0.0; c.y = 0.0; c.r = 5.0;`

#### Example Code and Output
| Step                | Java Code                        | Description                 |
|---------------------|----------------------------------|-----------------------------|
| Define class        | `class Circle { ... }`           | Defines Circle class        |
| Create object       | `Circle c = new Circle();`       | Instantiates Circle         |
| Set attributes      | `c.x = 0.0;` etc.                | Sets object values          |
| Call method         | `c.circumference();`             | Uses object method          |

### Using Multiple Objects
- Multiple objects (instances) can be created from a single class.
- Each object maintains its own independent set of values for data members.
- Example:
  - `Circle c1 = new Circle(); c1.x = 3.0; c1.y = 4.0; c1.r = 5.0;`
  - `Circle c2 = new Circle(); c2.x = -4.0; c2.y = -8.0; c2.r = 10.0;`
- Each objectâ€™s methods use its own data.
- Running the program prints unique values for each objectâ€™s area and circumference.

### Multiple Classes in a Program
- Java allows the definition and use of several classes within a single program.
- Each class can have its own fields and methods.
- Example: Defining both `Circle` and `Box` classes.
  - `Box` may have `width`, `height`, `depth` as data fields and methods `area()` and `volume()`.
- The main method can create independent objects of each class and use their respective methods.

#### Example Code:
```java
class Box {
    double width, height, depth;
    double area() { ... }
    double volume() { ... }
}
```

| Class    | Data Fields                    | Methods                  |
|----------|------------------------------|--------------------------|
| Circle   | x, y, r                       | area(), circumference()  |
| Box      | width, height, depth           | area(), volume()         |


## Methods for Object Initialization

### Manual Initialization
- Commonly, object fields are assigned values after object creation:
  - Inefficient and error-prone, especially with many objects and fields.
- Automating initialization improves safety and reduces code duplication.

### Using Setter Methods for Initialization
- Add methods such as `setPoint()` to explicitly assign values to fields within the object.
- Advantages:
  - Groups initialization logic in one place
  - Improves code clarity
- Limitation:
  - If implemented as a method with fixed, hard-coded values, all objects initialized by it get the same values.

#### Example:
```java
class Point {
    int x, y;
    void setPoint(int a, int b) {
        x = a;
        y = b;
    }
}
```
- Allows for flexible initialization:
  - `p1.setPoint(15, 20);`
  - `p2.setPoint(0, 0);`
- Each object can have unique values assigned.

### Comparison Table: Initialization Methods
| Method                    | Flexibility | Convenience | Risk of Error |
|---------------------------|-------------|-------------|--------------|
| Direct field assignment   | High        | Low         | High         |
| Setter method (no params) | Low         | Moderate    | Moderate     |
| Setter with parameters    | High        | High        | Low          |
| Constructor (next section)| Highest     | High        | Lowest       |

## Constructors: Automatic Initialization

### Concept of Constructor
- A constructor is a special method invoked at the moment an object is instantiated.
- The constructor method:
  - Bears the same name as the class.
  - Has no return type (not even `void`).
  - Can have parameters to provide initialization values.

#### Example:
```java
class Circle {
    double x, y, r;
    Circle(double a, double b, double c) {
        x = a;
        y = b;
        r = c;
    }
}
```
- The object is created and initialized in one step:
  - `Circle c1 = new Circle(3.0, 4.0, 5.0);`


### Constructor Overloading
- Multiple constructors can be defined in a class, differing in the number or types of parameters (argument list differs).
- This flexibility allows objects to be created in different ways.

#### Examples of Overloaded Constructors:
```java
class Circle {
    double x, y, r;
    // Constructor with three parameters
    Circle(double a, double b, double c) { x = a; y = b; r = c; }
    // Constructor with one parameter
    Circle(double c) { x = 0; y = 0; r = c; }
    // Copy constructor
    Circle(Circle c) { x = c.x; y = c.y; r = c.r; }
    // Default constructor
    Circle() { x = 0; y = 0; r = 0; }
}
```

#### Table: Common Constructor Overloading Patterns
| Constructor Type         | Parameters             | Usage                                    |
|-------------------------|------------------------|-------------------------------------------|
| Full initialization     | (double, double, double)| All values specified                      |
| Only radius             | (double)               | Position defaults to (0,0), set only r    |
| Copy constructor        | (Circle)               | Duplicate another object's values         |
| Default                 | none                   | All values set to a default (e.g., 0)     |

#### Usage in Main Method:
```java
Circle c1 = new Circle(3.0, 4.0, 5.0); // 3-arg constructor
Circle c2 = new Circle(7.0);           // 1-arg constructor
Circle c3 = new Circle(c1);            // copy constructor
Circle c4 = new Circle();              // default constructor
```

---

## Namespace Collision and the `this` Keyword

### Problem: Name Clashes
- When method parameters have the same names as fields of a class, simple assignment (`rollno = rollno`) leads to ambiguity.
- Java resolves this using the `this` keyword.

### The `this` Keyword
- Refers to the current object.
- Distinguishes class fields from parameters or local variables of the same name.
- Syntax: `this.fieldName`.

#### Example: Student Class
```java
class Student {
    int rollno;
    String name, course;
    float marks;
    Student(int rollno, String name, String course, float marks) {
        this.rollno = rollno;
        this.name = name;
        this.course = course;
        this.marks = marks;
    }
}
```

### Additional Uses of `this`
- Accessing methods of the current class from within other methods:
  - `this.methodName();`
- Chaining constructors (calling one constructor from another within the same class):
  - `this();` or `this(params);`

#### Example of Constructor Chaining
```java
class Demo {
    int x;
    Demo() {
        this(5); // Calls parameterized constructor
    }
    Demo(int x) {
        this.x = x;
    }
}
```
- Here, the no-argument constructor calls the parameterized constructor, setting `x` to 5.

### Table: Main Uses of `this` in Java
| Use case                       | Example                              | Purpose                        |
|-------------------------------|--------------------------------------|-------------------------------|
| Resolve variable collisions    | `this.x = x;`                        | Distinguishes class fields     |
| Invoke current object methods  | `this.method();`                     | Reference objectâ€™s own methods |
| Call one constructor from another | `this(params);`                    | Constructor chaining           |

## Summary of Key Java Encapsulation Demonstrations

### Demonstration Review
1. **Single Class, Single Object**: Create a class, make an object, initialize variables, and call methods.
2. **Single Class, Multiple Objects**: Show that more than one object can be created from a class, each with independent data.
3. **Multiple Classes in a Program**: Define more than one class (e.g., Circle and Box). Each class has unrelated fields and methods.
4. **Initialization with Methods**: Use explicit setter methods for object field assignment.
5. **Parameterized Setter Methods**: Enhance flexibility by passing initialization values as arguments.
6. **Constructors and Overloading**: Employ constructors for guaranteed, automatic, and flexible object initialization. Support multiple initialization patterns with overloading.
7. **The `this` Keyword**: Resolve ambiguities and support method and constructor organization.

### Best Practices Highlighted
- Always initialize object fieldsâ€”preferably using constructors for safety and consistency.
- Use constructor overloading to support flexibility in object creation.
- Apply the `this` keyword to avoid variable name ambiguities and streamline internal class references.

---

## Conclusion

### Key Insights
- Java encapsulation is best achieved by grouping data and methods in classes, controlling access and modification through defined interfaces.
- Direct assignment of object fields after instantiation is possible but discouraged in favor of constructors, which guarantee object readiness upon creation.
- Constructors can be overloaded, allowing flexible object creation strategiesâ€”default, parameterized, and copy constructors cater to various initialization needs.
- The `this` keyword is vital for resolving variable name collisions (especially with method parameters) and for referring to the current object in method and constructor chains.
- Methods such as `setPoint()` offer explicit post-construction initialization, but parameterized constructors are the most robust solution for object state definition.
- In case of more than one class in a program, separate logic and data appropriately, and apply encapsulation principles throughout.

### Key Terms
- **Encapsulation**: The bundling of data and methods within a class, shielding internal state from outside intervention.
- **Class**: A Java template containing fields (attributes) and methods, defining the structure and behavior of all its objects.
- **Object**: A unique instance of a class, encapsulating its own state and capable of executing class methods.
- **Method**: A function defined in a class which operates on the objectâ€™s data.
- **Field/Data Member**: A variable belonging to a class, representing one aspect of object state.
- **Constructor**: A special method, same name as the class and no return type, invoked when creating an object. Used for initialization.
- **Constructor Overloading**: Defining multiple constructors with different parameter lists to permit varied ways of object creation.
- **Default Constructor**: A constructor without parameters, providing a default way of initializing the object.
- **Copy Constructor**: A constructor which takes another object of the same class as argument and copies its data.
- **Setter Method**: A method (such as `setPoint()`) designed to assign values to some or all fields of an object after its creation.
- **this Keyword**: A reference to the current object; vital for distinguishing instance variables from parameters and for constructor chaining.
- **Namespace Collision**: A situation where a parameter or local variable has the same name as a class field, resolved using `this`.
- **Constructor Chaining**: The process of calling one constructor from another in the same class using `this()`.
