# Study notes for Programming In Java : Week 4 : : Lecture 20 : Interface-I

## Introduction

Interfaces form a cornerstone of Javaâ€™s structured and modular approach to software design. This session examines interfaces in detail, positioning them as a distinguishing feature that enhances Java's suitability for complex, large-scale, and maintainable projects. The notes begin by revisiting abstract classes as a foundation and then contrast their features and limitations with interfaces, especially regarding inheritance and polymorphism. After understanding the syntax and semantics of interfaces, practical examples illustrate their use and how they enable object-oriented design patterns like multiple inheritance and contract-driven development. The section also covers interface inheritance and implementation rules, ending with a summary of key insights and terminology.

---

## Abstract Classes in Java

### Definition and Characteristics
- An abstract class in Java is declared with the `abstract` keyword and may include abstract methods (without body) or concrete (implemented) methods.
- Abstract classes cannot be instantiated directly.

### Example Structure
- Abstract class example: `Geometry` placed in a package `MyShape`.
- Members:
  - `PI`: `static` and `final` (constant).
  - Abstract methods: `area()` and `circumference()` (declared without a body).

```java
package MyShape;
public abstract class Geometry {
    static final double PI = 3.14159;
    public abstract double area();
    public abstract double circumference();
}
```

### Inheriting Abstract Classes
- Subclasses such as `Circle`, `Rectangle`, and `Ellipse` can inherit from `Geometry`.
- Each subclass must implement all abstract methods from the superclass or be declared abstract itself.

#### Circle Example
- `Circle` provides logic for both `area()` and `circumference()`.
- It introduces its own constructors and possibly additional specific methods.

#### Rectangle Example
- Member variables such as length `l` and width `w` (often `protected` for subclass access).
- Implements required methods from `Geometry` and may include its own.

#### Ellipse Example
- Provides its rendering and calculation logic for the inherited abstract methods.
- May include properties unique to ellipses.

### Abstract Classes and Instantiation
- Objects cannot be directly created from an abstract class.
- Objects are instead created from concrete subclasses that implement all inherited abstract methods.

#### Example of Usage
- Program creates an array of `Geometry` references.
- Stores instances of `Circle`, `Rectangle`, and `Ellipse` in this array.
- Polymorphic behavior: Each objectâ€™s overridden methods are called at runtime according to its actual type (dynamic binding).

#### Code Sketch
```java
Geometry[] geoObjects = new Geometry[3];
geoObjects[0] = new Circle(...);
geoObjects[1] = new Rectangle(...);
geoObjects[2] = new Ellipse(...);
double totalArea = 0;
for (Geometry obj : geoObjects) {
    totalArea += obj.area();
}
```

#### Key Takeaways
- Abstract classes define design templates or blueprints, guiding subclass implementations.
- Subclasses must fully define inherited abstract methods to be concrete (instantiable).
- Abstract classes support single inheritance only.

## Multiple Inheritance and Interfaces

### The Limitation of Single Inheritance
- Java classes (including abstract ones) can only extend one superclass (single inheritance).
- Sometimes, a class needs features from more than one parent typeâ€”a scenario known as multiple inheritance.

### The Role of Interfaces
- Java does not allow multiple inheritance of classes but achieves similar functionality via interfaces.
- Interfaces offer a way to define contracts (method signatures) that multiple classes can adopt, allowing polymorphic behavior across unrelated classes.

### Interface Definition and Syntax
#### Basic Declaration
- Declared with the `interface` keyword:
```java
public interface Drawable {
    void draw();
    void resize(int size);
}
```
- Methods listed in an interface are implicitly `public` and `abstract`â€”keyword optional.
- Variables in interfaces are implicitly `public`, `static`, and `final` (constants).

| Aspect      | Abstract Class            | Interface                       |
|-------------|--------------------------|---------------------------------|
| Inheritance | Single                   | Multiple (implements multiple)  |
| Methods     | Abstract and/or Concrete | All abstract (pre-Java 8)       |
| Variables   | Any, with any modifier   | Public, static, final only      |
| Instantiation | No                      | No                              |

#### Example:
```java
interface Shape {
    double PI = 3.14159;
    double area(); // implicitly public abstract
}
```

#### Implementing Interfaces in Classes
- Any class can `implement` one or more interfaces:
```java
class Circle implements Shape {
    private double radius;
    public double area() {
        return PI * radius * radius;
    }
}
```

- A class can implement multiple interfaces, separated by commas.

#### Interface Inheritance
- Interfaces themselves can extend one or more other interfaces:
```java
interface Curves extends Circle, Ellipse {
    void smoothness();
}
```

### Key Differences: Abstract Class vs Interface

| Feature               | Abstract Class                  | Interface                                        |
|-----------------------|----------------------------------|--------------------------------------------------|
| Modifiers on Methods  | Can be any (abstract or concrete)| All are abstract/public by default                |
| Static Methods        | Allowed                         | Not allowed (until Java 8), only constants allowed|
| Implementation        | Members may have logic           | Only method signatures (pre-Java 8, default added in later versions)|
| Inheritance           | Only single                     | Multiple via implements                          |
| Object Instantiation  | Not allowed                     | Not allowed                                      |

### Utilizing Interfaces: Purpose and Advantage
- Serve as templates or contractsâ€”specify what methods a class must implement.
- Enable loose coupling and development flexibility.
- Permit a form of multiple inheritance, allowing classes to adopt behaviors from many sources.
- Classes that implement the same interface can be handled polymorphically.

### Syntax and Diagrammatic Structure
- Interfaces declared with the `interface` keyword.
- Signature for implementing multiple interfaces:

```java
class MultiFeature implements Interface1, Interface2 {
    // Implement all methods from both interfaces
}
```

- Interface variables are constants and cannot be changed by implementing classes.
- All interface methods have no bodyâ€”semicolon immediately follows signature.

### Example: Practical Use Case

#### Defining an Interface
```java
interface GeoAnalyzer {
    double area();
    double perimeter();
}
```

#### Implementing Multiple Classes
- `Circle`, `Ellipse`, and `Rectangle` each `implement` GeoAnalyzer.
- Each provides logic for `area()` and `perimeter()`.

#### Demonstration Code
```java
GeoAnalyzer[] shapes = {
    new Circle(...),
    new Ellipse(...),
    new Rectangle(...)
};
for (GeoAnalyzer item : shapes) {
    System.out.println(item.area());
}
```
- The interface type variable (`GeoAnalyzer`) can point to any implementing object.
- Polymorphic/late binding (run-time resolution of method calls).

### Multiple Interfaces Implementation Example
```java
interface Drawable {
    void draw();
}
interface Resizable {
    void resize();
}
class Line implements Drawable, Resizable {
    public void draw() { /* logic */ }
    public void resize() { /* logic */ }
}
```
- `Line` adopts contracts from both `Drawable` and `Resizable`.

#### Interface Inheritance Example
- One interface can inherit another:
```java
interface Constants {
    int MAX = 100;
}
interface Chemistry extends Constants {
    void chemicalProcess();
}
```
- `Chemistry` includes all constants from `Constants` and adds its own methods.

### Rules and Restrictions for Interfaces
- All methods are implicitly `public` and `abstract`.
- No static methods (pre-Java 8).
- All variables are `public`, `static`, and `final`.
- Methods cannot be `final` (as they must be implemented by subclasses).
- A class can `extend` one class and `implement` multiple interfaces:

```java
class Demo extends Shape implements Drawable, Serializable {
    // ...
}
```

- Interfaces can extend multiple interfaces but cannot implement classes or other interfaces.
- Objects of an interface cannot be instantiated directly.
- Interface types can be used as reference types pointing to objects of implementing classes, facilitating polymorphism.

### Summary Table of Key Interface Properties
| Principle                                         | Interface Specification       |
|---------------------------------------------------|------------------------------|
| Declaration keyword                               | interface                    |
| Can a class extend multiple interfaces?           | Yes (via implements)         |
| Can interfaces extend multiple interfaces?         | Yes                          |
| Are interface methods implicitly public/abstract? | Yes                          |
| Are variables implicitly public/static/final?     | Yes                          |
| Can interfaces have constructors?                 | No                           |
| Can interface declare static methods?             | No (before Java 8)           |
| Object instantiation possible?                    | No                           |

### Example: Interface and Class Implementation
```java
interface Measurement {
    double getValue();
}
class Temperature implements Measurement {
    private double temp;
    public double getValue() { return temp; }
}
```
- `Temperature` provides a concrete implementation of `getValue()`.

### Interface Usage Pattern
- Define protocol/contract for families of related or unrelated classes.
- Enable grouping of classes (e.g., all objects that have area calculations).
- Achieve code flexibilityâ€”implement interface in any class as needed.

### Polymorphism with Interfaces
- Variables of interface type can reference objects of any class that implements the interface.
- Enables dynamic (run-time) method binding.

#### Example:
```java
Measurement m;
m = new Temperature();
System.out.println(m.getValue());
```

### Inheritance Among Interfaces
- Interface may extend one or more interfaces to compound their contracts.
- Syntax:
```java
interface Physics extends Constants, Chemistry {
    void someLaw();
}
```

### Best Practices
- Use interfaces to define clear method contracts when method implementation is expected to vary across different classes.
- Prefer interfaces for loose coupling and when multiple unrelated classes share capabilities.
- Abstract classes are preferred when shared code/behavior is to be inherited, but only one superclass is necessary.

---

## Conclusion

### Key Insights
- Abstract classes define shared templates and allow partial implementation. Only single inheritance is supported for classes.
- Interfaces define method contracts without implementation, allowing multiple types to share behavior regardless of class hierarchy.
- Variables in interfaces are constants, and methods are always abstract and public unless declared otherwise (from Java 8, interfaces can have `default` methods and `static` methods, but this is not covered in classic interface usage).
- Interfaces enable multiple inheritance in Java, which is otherwise restricted at the class level, by letting classes implement several interfaces.
- Both abstract classes and interfaces cannot be instantiated directly. Classes inheriting abstract classes or implementing interfaces must implement all abstract methods unless they are declared abstract themselves.
- Interfaces promote code flexibility, reusability, and stronger architectural contracts.

### Key Terms
- **Abstract Class**: A class with the `abstract` modifier that cannot be instantiated directly and may have both abstract and concrete methods.
- **Abstract Method**: A method without a body, meant to be implemented by subclasses.
- **Interface**: A special Java type, declared with `interface`, that defines a contract of method signatures and constants for implementing classes. Supports multiple inheritance.
- **Implements**: Java keyword used in class definitions to adopt the contract provided by one or more interfaces.
- **Extends**: Used to inherit from a class (for classes) or inherit from another interface (for interfaces).
- **Polymorphism**: The ability of references of a superclass or interface type to point to objects of different subclasses or implementing classes, enabling dynamic method binding at runtime.
- **Multiple Inheritance**: The concept where a type (class/interface) inherits features from more than one parent. This is achieved in Java for behaviors only via interfaces.
- **Public/Static/Final**: Modifiers automatically applied to variables in interfaces, making them constants accessible in all implementing classes.

---
