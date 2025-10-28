# Study notes for Programming In Java : Week 3 : : Lecture 14 : Demonstration-VI

## Introduction

This guide presents an in-depth exploration of inheritance in Java, focusing on practical demonstrations and nuanced concepts. Key topics include the basic mechanisms of inheritance, the distinction between simple and multi-level inheritance, the use of the `super` keyword, method overriding, and the application of Java's `abstract` and `final` keywords. These concepts are explained through illustrative code examples, real usage scenarios, and clarifications on behaviors like variable name collisions, constructor initialization, and runtime polymorphism. By following these notes, learners gain a comprehensive understanding of how Java's inheritance model supports the creation of robust, extensible, and well-structured object-oriented applications.

---

## Inheritance Basics in Java

Inheritance allows one class (the subclass) to acquire the properties and behaviors (fields and methods) of another class (the superclass). This foundational object-oriented principle promotes code reuse and organized program structure.

### Simple Inheritance
- In simple inheritance, a single subclass extends a superclass.
- The subclass gets direct access to all public and protected members of the superclass.
- Subclasses can also define their own additional fields and methods.

#### Example Structure:
| Class | Fields (Members)       | Methods              |
|-------|-----------------------|----------------------|
| A     | int i, int j          | void showIJ()        |
| B     | int k (new)           | void showK(), sum()  |

- Object creation demonstrates that subclass objects can access inherited superclass members as well as their own.
- Access control: Default access (no modifier) permits subclass access within the same package.

### Initialization Using Superclass Constructors
- Subclasses can be initialized using constructors defined in the superclass.
- The `super` keyword allows calling a superclass constructor from the subclass constructor, passing needed arguments for proper initialization.
- Demonstrated with a `Box` superclass (fields: width, height, depth) and a `BoxWeight` subclass (adds: weight).

**Example Table for Constructor Initialization:**
| Operation                            | Code Example                          |
|--------------------------------------|---------------------------------------|
| Superclass initialization            | `Box myBox1 = new Box(2,3,4);`        |
| Subclass initialization (via super)  | `BoxWeight myBox2 = new BoxWeight(2,3,4,0.076);` |

- If the subclass does not explicitly call a superclass constructor, Java inserts a call to the default superclass constructor.
- Subclass constructors can specify which superclass constructor to invoke by using `super(arg1,arg2,...)`. 

### Referencing Subclass Objects via Superclass References
- Java allows a subclass object to be referenced by a superclass variable (e.g., `Superclass ref = new Subclass();`).
- This is a legal operation, and such a reference can only access members declared in the superclass.
- Method calls on such references resolve at runtime (dynamic binding).
- Example: A `Box` variable can refer to a `BoxWeight` object.

## The super Keyword in Detail

The `super` keyword serves several important purposes in Java's inheritance mechanism.

### Avoiding Variable Name Collision
- When a subclass declares a field with the same name as one in the superclass, a name collision or hiding occurs.
- The subclass field hides the superclass field within its context.
- To reference the superclass field explicitly, use `super.fieldName`.

**Code Illustration:**
```java
class A { int i; }
class B extends A { int i; // hides A's i   }
// In B's constructor or method:
super.i = a; // accesses A's i
this.i = b;  // accesses B's i
```

### Invoking Superclass Constructors
- Use `super()` or `super(arg1, arg2)` as the first statement in a subclass constructor to invoke a specific superclass constructor.
- Ensures that the superclass part of the object is properly initialized.

### Access to Superclass Methods and Variables
- `super.methodName()` calls a method defined in the superclass, even if overridden in the subclass.
- Useful for extending superclass behavior while customizing in the subclass.

### Demonstration Table
| Use Case                        | Syntax Example           | Purpose                                        |
|----------------------------------|-------------------------|------------------------------------------------|
| Reference superclass variable    | `super.i`               | Avoid variable hiding/collision                |
| Call superclass constructor      | `super(a, b, c)`        | Initialize inherited members                   |
| Call superclass method           | `super.display()`       | Invoke overridden superclass method            |

## Method Overriding

Method overriding enables a subclass to provide a specific implementation for a method already defined in its superclass.
- The subclass method must have the same signature as the superclass method.
- Enables dynamic (runtime) polymorphism.
- Calls to overridden methods resolve based on the actual object, not the reference type.

### Overriding in Practice
- Example: `class Cat` with method `speak()`, subclass `PetCat` overrides `speak()`.
- When calling `speak()` on a `PetCat` object, the overridden version in `PetCat` is executed.

#### Multi-level Overriding
- When another subclass, e.g., `MagicCat`, extends `Cat` and further overrides `speak()`, it can selectively use `super.speak()` to call the parentâ€™s implementation as needed.

### Dynamic Binding (Runtime Polymorphism)
- The version of an overridden method that gets called is determined at runtime based on the actual object type.
- This allows flexible and extensible program design.

## Types of Inheritance

### Single (Simple) Inheritance
- One subclass derives directly from one superclass.
- Promotes clear hierarchical relationships and code reuse.

### Multi-level Inheritance
- A subclass is derived from a derived class, creating a chain (e.g., `Box` â†’ `BoxWeight` â†’ `Shipment`).
- Each class in the chain can extend/add new functionalities and fields.

**Example: Multi-level Chain**
| Level      | Class Name  | Extends           | Distinct members      |
|------------|-------------|-------------------|----------------------|
| Level 1    | Box         | Object (implicit) | width, height, depth |
| Level 2    | BoxWeight   | Box               | weight               |
| Level 3    | Shipment    | BoxWeight         | cost                 |

### Multiple Inheritance
- Java does **not** support multiple inheritance for classes directly (one class cannot extend more than one class).
- Can be simulated using interfaces.

## Abstract Classes and Methods

### Abstract Classes
- Declared with the `abstract` keyword; cannot be instantiated directly.
- May contain abstract methods (no implementation) and concrete methods (with implementation).
- Serve as blueprints for subclasses; subclasses must implement all abstract methods unless declared abstract themselves.

#### Rules for Abstract Classes
1. Cannot create objects directly: `Base b = new Base(); // Error if Base is abstract.`
2. Can have constructors, but only for use by subclasses during object instantiation.
3. Abstract classes can have non-abstract methods and fields.
4. Subclasses must implement abstract methods, or themselves be abstract.

#### Example:
```java
abstract class Base {
  Base() { System.out.println("Base constructor"); }
  abstract void fun();
  void nonAbstract() { System.out.println("Non-abstract method"); }
}

class Derived extends Base {
  void fun() { System.out.println("Fun defined"); }
}
```

### Abstract Methods
- Declared with only the method signature, ending with a semicolon; the `abstract` keyword must be present.
- Cannot have a body in the abstract class.
- Must be implemented in a concrete subclass.

#### Table: Features of Abstract Concepts
| Concept           | Abstract Class            | Abstract Method                |
|-------------------|--------------------------|---------------------------------|
| Instantiation     | Not allowed              | Not applicable                 |
| Declaration       | Use `abstract class`     | Use `abstract` in method decl. |
| Implementation    | May have none            | Must be implemented by subclass|

### Constructors in Abstract Classes
- Abstract classes can have constructors.
- Their constructors are invoked by subclass constructors using `super()`, to initialize inherited fields.
- Cannot invoke them directly via the `new` operator.

### Accessing Superclass Methods in Subclasses
- Subclasses can call superclass (concrete or abstract) methods using `super.methodName()`.
- Overridden methods in a subclass can still invoke the parent implementation for additional or extended behavior.

## The final Keyword

### Usage of final
- The `final` keyword imposes strict restrictions to safeguard class design.
- It can be applied to variables, methods, and classes.

#### final Classes
- Declaring a class as `final` (e.g., `final class Bike`) prevents it from being subclassed.
- Attempting to extend a final class yields a compile-time error.

#### final Methods
- A `final` method cannot be overridden by subclasses.
- Ensures that the methodâ€™s implementation remains constant throughout the inheritance hierarchy.
- Useful for utility methods or implementation details that should not be customized.

#### final Variables
- A `final` variable becomes a constant (cannot be reassigned after initialization).
- Ensures data integrity.

### Demonstrations and Compilation Behavior
- Java's compiler enforces final class and method restrictions.
- Attempting to extend a final class or override a final method results in errors such as "cannot inherit from final ClassName" or "cannot override final methodName in ClassName".

## Summary Table: Inheritance Features Demonstrated
| Feature                    | Example/Usage                        | Notes                                               |
|----------------------------|--------------------------------------|-----------------------------------------------------|
| Simple Inheritance         | `class B extends A`                  | Subclass inherits members and methods from superclass|
| Multi-level Inheritance    | `Shipment extends BoxWeight extends Box` | Inheritance "chain"                               |
| super keyword              | `super.i`, `super()`                 | Resolving name collision, constructor invocation     |
| Method Overriding          | Subclass re-defines superclass method| Enables dynamic (runtime) polymorphism              |
| Abstract Class/Method      | `abstract class`, `abstract void fun()` | Cannot be instantiated; must be implemented      |
| final Keyword              | `final class`, `final void fun()`    | Prevents further extension or override              |

## Practical Exercises Advised
- Experiment with provided example codes:
  - Implement and modify simple and multi-level inheritance hierarchies.
  - Practice overriding methods and see runtime behavior.
  - Use `super` for both variable/method reference and constructor chaining.
  - Try declaring classes, variables, and methods as `final`.
  - Create abstract classes and concrete subclasses as shown.
- Observe compiler feedback when violating inheritance restrictions.

---

## Conclusion

### Key Insights
- Java's inheritance mechanics provide powerful code reuse and extensibility but require careful handling of hierarchy, constructor chaining, and access control.
- The `super` keyword is essential for managing inherited state, resolving ambiguity, and invoking parent class logic.
- Method overriding enables runtime polymorphism, allowing Java programs to behave flexibly according to object types at execution.
- Abstract classes and methods provide templates for subclassing but cannot be instantiated directly, and may include both abstract and concrete elements.
- The `final` keyword enforces inheritance restrictions, protecting classes, methods, or variables from being extended or modified, thereby increasing code safety and maintainability.

### Key Terms
- **Inheritance** : Object-oriented mechanism where a class acquires properties and methods of another class.
- **super (keyword)** : Used to refer to superclass variables, methods, or constructors in subclass.
- **Constructor Chaining** : Process where a subclass constructor invokes the constructor of its superclass.
- **Name Collision/Variable Hiding** : When a subclass declares a member with the same name as in a superclass.
- **Method Overriding** : Defining a method in a subclass with the same signature as in the superclass; enables polymorphism.
- **Abstract Class** : A class that cannot be instantiated and may contain abstract (unimplemented) methods.
- **Abstract Method** : A method with no implementation, to be defined in subclasses.
- **final (keyword)** : Restricts inheritance or method overriding, or prevents variable value reassignment.
- **Dynamic Binding/Polymorphism** : Method call resolution at runtime based on actual object class.
- **Multi-level Inheritance** : A chain of inheritance; subclass extends another subclass.
- **Access Specifiers** : Keywords in Java (public, protected, default, private) that determine member accessibility.
