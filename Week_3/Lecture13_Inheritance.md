# Study notes for Programming In Java : Week 3 : : Lecture 13 : Inheritance

## Introduction

Inheritance is a fundamental concept within object-oriented programming that enables new classes to acquire the properties and behaviors of existing classes. This paradigm supports the creation of reusable, maintainable, and extensible code structures. The following notes provide an in-depth exploration of inheritance, focusing specifically on its implementation and implications within the Java programming language. Covered topics include the hierarchy of inheritance, the use of the `extends` keyword, method overriding, the role of the `super` keyword, special types of classes (abstract and final), and dynamic method resolution (runtime polymorphism). Multiple real-world and code-based examples are provided to clarify these concepts.

---

## Inheritance in Object-Oriented Programming

Inheritance facilitates the creation of new classes (subclasses) based on existing ones (superclasses), sharing their fields and methods and allowing for further specialization.

### Fundamental Concepts
- **Definition**: Inheritance describes a relationship where one class (the child or subclass) derives characteristics (fields and methods) from another class (the parent or superclass).
- **IS-A Relationship**: Inheritance is often explained through the IS-A relationship, where the subclass can be considered a specialized form of the superclass, e.g., "a Lion IS-A Animal".
- **Reusability**: Inheritance promotes code reuse, enabling common features to be coded once in the superclass and inherited by all subclasses.

#### Biological Analogy
- Just as children inherit traits from their parents, subclasses inherit properties from superclasses.
- Supports single inheritance (one parent class), and in some languages, multiple inheritance (more than one parent class).

### Types of Inheritance

Inheritance can be structured in several ways, creating a class hierarchy:

| Type of Inheritance            | Description                                                         | Example                                          |
|-------------------------------|---------------------------------------------------------------------|--------------------------------------------------|
| Single Inheritance            | One subclass inherits from one superclass.                          | Class B extends Class A                          |
| Multiple Single Inheritance   | More than one subclass inherits from the same superclass.           | Class B, Class C extend Class A                  |
| Multi-level Inheritance       | A subclass derives from another subclass, forming a chain.          | Class C extends Class B extends Class A          |
| Multiple Inheritance          | A class inherits from more than one superclass.                     | Not supported directly in Java                   |
| Hybrid Inheritance            | Combination of two or more types (single + multiple, etc.).         | Not supported directly in Java                   |

**Java supports single, multiple single, and multi-level inheritance. It does not support multiple or hybrid inheritance using classes due to ambiguity and complexity (the "diamond problem").**

### Hierarchical Example: Animal Class
- `Animal` (general superclass)
    - `Herbivore` (subclass of Animal)
    - `Carnivore` (subclass of Animal)
        - `Lion` (subclass of Carnivore)
        - `Hyena` (subclass of Carnivore)

Here, `Lion` and `Hyena` are more specialized subclasses, but both can be considered an `Animal` through the IS-A relationship.

### Java Implementation of Inheritance

#### The `extends` Keyword
- Used to create a subclass that inherits from a superclass.
- Basic Syntax:
  ```java
  class SubclassName extends SuperclassName {
      // Additional fields and methods
  }
  ```
- All public and protected members of the superclass become available in the subclass.

#### Example: Vehicles
- `Vehicle` (superclass)
    - `Car`, `Truck` (subclasses of Vehicle)
    - `FireTruck` (subclass of Truck)

#### Benefits
- Promotes **code reuse**: Common features are defined in one place.
- Simplifies **maintainability**: Changes in the superclass can propagate to subclasses.
- Supports **extensibility**: Easy to add specialized behaviors.

### Simple Inheritance Example in Java

#### 2D and 3D Point
- **Superclass**: `Point2D` with integer fields `x` and `y` and a `display()` method.
- **Subclass**: `Point3D` extends `Point2D`, adds `z` as a new field and can override `display()`.

**Diagram:**
| Class      | Fields      | Methods          |
|------------|-------------|-----------------|
| Point2D    | x, y        | display()       |
| Point3D    | x, y, z     | display()*      |

*`Point3D` can override `display()` or add new methods as needed.

#### Code Snippet
```java
class Point2D {
    int x, y;
    void display() {
        // Implementation for 2D point
    }
}

class Point3D extends Point2D {
    int z;
    void display() { // Overrides Point2D's display
        // Implementation for 3D point
    }
}
```

### Access and Overriding
- All public/protected methods and variables of `Point2D` are accessible in `Point3D` unless overridden.
- If a subclass defines a method with the same signature as its superclass, it **overrides** that method (method overriding).

### Inheritance Hierarchy Patterns

#### Multiple Single Inheritance
- Several subclasses inherit from the same superclass.
- Example:
    - `Person` (superclass)
        - `Student` (subclass)
        - `Employee` (subclass)

In both `Student` and `Employee`, the fields and methods of `Person` are inherited and can be extended or overridden.

#### Multi-Level Single Inheritance
- A subclass derived from another subclass (a class hierarchy chain).
- Example:
    - `Person` â†’ `Employee` â†’ `RegularEmployee` / `TemporaryEmployee`.

#### Unsupported Patterns in Java
- **Multiple Inheritance:** A class cannot inherit from multiple superclasses.
- **Hybrid Inheritance:** Combination of multiple and single inheritance is also unsupported with classes.

### Hierarchical Example: Geometrical Objects
- Generalization: `GeoObject` (superclass)
    - `OneDObject`, `TwoDObject`, `ThreeDObject` (subclasses)
        - Further specialization (e.g., `TwoDObject` â†’ `Triangle`, `Quadrilateral` â†’ `Rectangle`, `Parallelogram`)
- Special attributes and methods specific to each subclass can be added iteratively.

### Method Overriding and Overloading

**Method Overriding**
- Occurs when a subclass implements a method with the same name, return type, and parameters as a method in its superclass, thus replacing the superclass's version.
- Syntax:
  ```java
  class SuperClass {
      void display() {
          // ...
      }
  }

  class SubClass extends SuperClass {
      @Override
      void display() {
          // ... (overrides SuperClass's display)
      }
  }
  ```
- Necessary for dynamic binding/runtime polymorphism.

**Method Overloading**
- Occurs when two or more methods in the same class share the same name but have different parameters (type and/or number).
- Overloading is allowed both within a class and across inherited classes, but distinct from overriding.

#### Example Table: Overriding vs. Overloading
| Feature    | Overriding                    | Overloading                   |
|------------|------------------------------|-------------------------------|
| Class      | Across superclass/subclass   | Within same class or inheritance hierarchy |
| Signature  | Must be identical            | Must differ (parameters)      |
| Purpose    | Replace superclass method    | Provide multiple forms        |

### Dynamic Binding (Runtime Polymorphism)
- The method to be executed is determined at runtime based on the actual subclass object.
- Enables arrays or references of a superclass type to store objects of different subclasses and correctly invoke overridden methods.
- Example:
  ```java
  Bike b = new Splendor();
  b.run(); // Will call Splendor's run()
  ```

### Type Casting and Access
- Upcasting: Storing a subclass object in a superclass reference.
    - Allows generalized storage and manipulation, but overridden methods are still called (due to dynamic binding).
- Downcasting: Casting back to the subclass type (explicitly), usually to access subclass-specific methods not present in the superclass.

### Accessing Members
- Subclass instances can access superclass fields and methods unless they are private or overridden.
- Superclass references cannot access subclass-specific fields/methods.

### The `super` Keyword in Java

The `super` keyword provides several important mechanisms for interacting with superclass features from the subclass:

#### Purposes of `super`
1. **Referencing Instance Variables**: Access superclass fields when they are hidden by subclass fields of the same name.
2. **Invoking Superclass Methods**: Call a method in the superclass that has been overridden by the subclass.
3. **Invoking Superclass Constructors**: Call a constructor from the superclass explicitly from within the subclass constructor.

#### Example 1: Accessing Superclass Field
```java
class Animal {
    String color = "white";
}
class Dog extends Animal {
    String color = "black";
    void printColor() {
        System.out.println(color);        // prints black (subclass variable)
        System.out.println(super.color);  // prints white (superclass variable)
    }
}
```

#### Example 2: Invoking Superclass Method
```java
class Animal {
    void eat() { System.out.println("eating"); }
}
class Dog extends Animal {
    void eat() { System.out.println("eating bread"); }
    void work() {
        super.eat();    // Calls Animal's eat()
        bark();         // Calls Dog's bark()
        eat();          // Calls Dog's eat() (overridden)
    }
    void bark() { System.out.println("barking"); }
}
```

#### Example 3: Invoking Superclass Constructor
```java
class Animal {
    Animal() { System.out.println("Animal created"); }
}
class Dog extends Animal {
    Dog() {
        super();            // invokes superclass constructor
        System.out.println("Dog created");
    }
}
```

#### Constructor Selection with Arguments
- If the superclass defines multiple constructors, the subclass can choose which to call by passing arguments to `super()`.
- The constructor whose parameters match is invoked.

### Abstract Classes

#### Abstract Class
- Defined with the `abstract` keyword.
- Can contain abstract methods (declared without implementations) as well as fully implemented, concrete methods.
- Cannot be instantiated directly; objects cannot be created from abstract classes.
- Serves as a template for subclasses.

#### Properties
- Abstract methods must be implemented in concrete subclasses.
- Abstract classes can also have final methods (cannot be overridden) and variables.
- Example:

```java
abstract class Shape {
    abstract void draw();
    void print() { System.out.println("This is a shape"); }
}
```

### Final Classes and the `final` Keyword

#### The `final` Keyword
- Can be applied to classes, methods, and variables.
    - **Final class**: Cannot be subclassed. No class can extend a final class.
    - **Final method**: Cannot be overridden in subclasses.
    - **Final variable**: Value cannot be changed once assigned.

- Example:

```java
final class Bike {}
class SportsBike extends Bike {} // Error: cannot inherit from final class
```

### Rules, Limitations, and Best Practices

#### Inheritance Rules
- Subclass inherits all accessible (public/protected/default) fields and methods except:
    - Constructors are not inherited (need explicit calls with `super`).
    - Private members are not accessible directly in the subclass.
- Java only allows one direct superclass for each class (no multiple inheritance with classes).
- Inheritance supports polymorphismâ€”reference of superclass can point to any subclass object.

#### Encapsulation and Inheritance
- Inheritance should not break encapsulation; use protected access for members that are to be inherited and accessed by subclasses.

#### Best Practices
- Use inheritance to represent IS-A relationships; prefer composition (HAS-A) for other relationships.
- Do not overuse inheritance; consider interfaces or composition if multiple behaviors are needed.
- Override methods where subclass behavior should differ, but call `super.method()` if base class logic is still required.

---

## Conclusion

### Key Insights
- Inheritance is a core concept of object-oriented programming that allows code reuse and the structuring of class hierarchies.
- Java supports only single, multi-level, and multiple single inheritance (not true multiple or hybrid inheritance in classes).
- The use of the `extends` keyword creates subclasses that inherit fields and methods from superclasses.
- Method overriding enables polymorphic behavior and dynamic method resolution, vital for flexible, maintainable code.
- The `super` keyword is fundamental for controlling superclass access, especially for variables, methods, and constructors.
- Abstract classes provide templates for generalized behaviors, while final classes prevent further specialization.

### Key Terms
- **Inheritance:** Mechanism allowing a new class to acquire members (fields and methods) from an existing class.
- **Superclass/Parent Class:** The class being inherited from.
- **Subclass/Child Class:** The class that inherits from the superclass.
- **IS-A Relationship:** Relationship between a subclass and a superclass (e.g., "Lion is-an Animal").
- **Single Inheritance:** Subclass inherits from one superclass only.
- **Multiple Inheritance:** Subclass inherits from multiple superclasses (not allowed in Java classes).
- **Multi-level Inheritance:** Forming a chain of inheritance, subclassing another subclass.
- **Method Overriding:** Redefining a superclass's method in a subclass with the same signature.
- **Method Overloading:** Providing multiple methods with the same name but different parameters.
- **Dynamic Binding/Runtime Polymorphism:** Method calls resolved at runtime based on actual object type.
- **Upcasting:** Assigning a subclass object to a superclass reference.
- **super Keyword:** Used to access superclass members (variables, methods, constructors) from a subclass.
- **Abstract Class:** Cannot be instantiated, may define abstract methods serving as templates for subclasses.
- **Final Class:** Class marked final cannot be extended, and methods/variables marked final cannot be overridden/modified in subclasses.
