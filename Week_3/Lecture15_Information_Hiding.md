# Study notes for Programming In Java : Week 3 : : Lecture 15 : Information Hiding

## Introduction

Information hiding is a foundational principle in object-oriented programming, particularly in Java, that helps developers control the accessibility of data and methods within classes and across different components of a software system. This approach promotes encapsulation and ensures that implementation details are shielded from external access, thereby increasing modularity, security, and maintainability of code. The primary mechanism for information hiding in Java is the use of access modifiers, which restrict the scope of classes, methods, and data members according to the desired level of visibility. This guide explores the different Java access modifiers, their effects, usage contexts, nuances, and implications through detailed explanation and examples.

---

## Information Hiding in Java

Information hiding refers to the technique of hiding internal details of a class or module from the outside world, exposing only what is necessary for other parts of the system to use. This is essential for creating robust and modular programs.

### Motivations for Information Hiding
- Encapsulation: Bundles data and methods operating on the data within a class.
- Security: Prevents unauthorized or inadvertent modification of sensitive data.
- Flexibility: Allows internal changes without affecting dependent code.
- Maintainability: Limits the impact of changes and reduces bugs.
- Clarity: Users of a class need only to know what is essential, not how it is implemented.

## Access Modifiers in Java

Access modifiers control the visibility of class members (fields and methods) as well as classes themselves. There are four main types of access modifiers:
- `public`
- `protected`
- `private`
- (default) (also called package-private, when no modifier is specified)

### Overview Table of Access Modifiers

| Access Level        | Class | Package | Subclass | World (Any class) |
|--------------------|-------|---------|----------|-------------------|
| public             |  Yes  |   Yes   |   Yes    |      Yes          |
| protected          |  Yes  |   Yes   |   Yes    |      No           |
| default (no mod.)  |  Yes  |   Yes   |   No*    |      No           |
| private            |  Yes  |   No    |   No     |      No           |

*Default members are only accessible within the same package; subclasses outside the package do not have access.


## Default (Package-Private) Access Modifier

### Description
- When no access modifier is specified before a class, data member, or method, it is assigned the default access modifier.
- Members with default access are only accessible within classes that reside in the same package (commonly the same directory).

### Characteristics
- Applies to class declarations, fields, and methods.
- No explicit keyword for default access; simply omit public, protected, and private modifiers.

### Scope
- Accessible:
  - Within the same class
  - From other classes in the same package
- Not accessible:
  - From classes in a different package
  - From subclasses outside the package

#### Example
Suppose we have two files in the same directory:

```java
// A.java
default class A {
    void msg() { System.out.println("Hi I am in class A"); }
}

// B.java
class B {
    public static void main(String[] args) {
        A obj = new A();
        obj.msg();
    }
}
```
- No access modifier before `class A` or `void msg()`, so both use default access.
- If A.java and B.java are in the same directory/package, B can access A and its `msg` method.
- If B.java is placed in a different directory (different package), the code will result in a compilation error.

### Behavior in Java File Organization
- If both classes are defined in the same Java file, no access issues occur.
- If defined in separate files, they must reside in the same directory/package for access to succeed. Otherwise, errors will occur.

### Key Points
- Default access is package-restricted.
- Used for internal implementation details within a package.
- Avoids unnecessary exposure of class members beyond their intended boundary.


## Public Access Modifier

### Description
- The `public` modifier allows the broadest level of accessibility.
- Members or classes marked as public can be accessed from any other class or package.

### Characteristics
- Accessibility is global: accessible from everywhere.
- Suitable for APIs or methods/classes intended for widespread use.

### Scope Table
| Can Access Public Member? | Same Class | Same Package | Subclass (any package) | Any Class |
|--------------------------|------------|--------------|-----------------------|-----------|
| Yes                      |   Yes      |    Yes       |         Yes           |    Yes    |

### Usage Guidelines
- Used for methods, fields, and class declarations that are meant to be universally accessible.
- Public methods act as the interface for the class's functionality.
- All public classes and members can be imported and used in different packages.

#### Example
```java
// In pack1/A.java
public class A {
    public void msg() {
        System.out.println("Hello from public class A");
    }
}

// In pack2/B.java
class B {
    public static void main(String[] args) {
        A obj = new A();
        obj.msg();
    }
}
```
- Both classes in different packages.
- Since `A` and its `msg` method are public, `B` can access and instantiate `A`.

### Implications
- Anything marked public forms part of the publicly exposed API of your class or package.
- Changes to public API can affect many dependent classes, so they should be made carefully.
- Only make members public if necessary; otherwise, use more restrictive modifiers for better encapsulation.

### Special Notes
- If multiple classes are defined in the same file, only one can be public, and the file name must match the public class name.
- If all classes are in the same file, using the default access is advised.


## Private Access Modifier

### Description
- The `private` modifier limits access strictly to the class within which the member is declared.
- Most restrictive access control.

### Characteristics
- Used for fields, methods, and inner classes.
- Private members are not accessible from outside their own class, even by subclasses.

### Scope Table
| Can Access Private Member? | Same Class | Same Package | Subclass | World (Any Class) |
|---------------------------|------------|--------------|----------|-------------------|
| Yes                       | No         | No           | No       |

### Usage Guidelines
- Used to hide internal implementation details.
- Helps prevent accidental or malicious manipulation from outside the class.
- Encourages data integrity and security.

#### Example
```java
public class A {
    private int data = 10;
    public void showData() {
        System.out.println("Data: " + data);
    }
}

public class B {
    public static void main(String[] args) {
        A obj = new A();
        // System.out.println(obj.data); // ERROR: data is private
        obj.showData(); // OK: showData() is public
    }
}
```
- Field `data` is private; cannot be accessed directly outside class `A`.
- Public method `showData()` allows controlled access to `data`.

### Private Class
- You cannot declare a top-level class as private.
- Nested (inner) classes can be private and are then accessible only within the enclosing class.

### Private Constructor
- If a class's constructor is private, objects cannot be instantiated from outside the class.
- Used in singleton design patterns or utility classes where instance creation is to be controlled.

#### Example
```java
public class Singleton {
    private static Singleton instance;
    private Singleton() { }
    public static Singleton getInstance() {
        if (instance == null) { instance = new Singleton(); }
        return instance;
    }
}
```

### Indirect Access
- Private members can be accessed indirectly via public or protected methods defined in the same class.
- For secure design, avoid exposing sensitive data even indirectly if not appropriate.


## Protected Access Modifier

### Description
- The `protected` modifier provides access to members within the same package and also to subclasses, even if those subclasses are in different packages.
- Offers a middle ground between default/package access and public access.

### Characteristics
- Used mainly in inheritance hierarchies to allow subclasses to use or extend behaviors without exposing internals to everyone else.

### Scope Table
| Can Access Protected Member? | Same Class | Same Package | Subclass (any package) | World |
|-----------------------------|------------|--------------|-----------------------|-------|
| Yes                         | Yes        | Yes          | Yes                   | No    |

### Usage Guidelines
- Used for methods and fields that should be accessible to related classes (via inheritance) but hidden from the rest of the application.

#### Example
```java
// In src/pack1/A.java
public class A {
    protected void display() {
        System.out.println("This is protected");
    }
}

// In src/pack2/B.java
import pack1.A;
class B extends A {
    public static void main(String[] args) {
        B obj = new B();
        obj.display(); // works because B is a subclass
    }
}
```

### Key Points
- Accessible in the same package even by non-subclasses.
- Accessible in subclasses even if they are outside the package.
- Not accessible from non-subclasses outside the package.

### Method Overriding and Protected
- Overridden methods in subclasses can widen the access but cannot restrict it further (e.g., a protected method in a superclass cannot be overridden as private in a subclass).
- Attempting to do so leads to compilation errors.


## Combining Access Modifiers and Their Effects

### Practical Application
- Use `private` for all fields and methods that should not be accessed outside the class.
- Expose public methods for the interface you want other classes to use.
- Use `protected` to allow extensibility in inheritance hierarchies.
- Keep members package-private (default) when you want to restrict use to the same package.

### Example Rules
- If two classes are in the same file or package and use default access, they can interact with each other.
- If in different packages, only public members are visible, unless inheritance is used for protected members.
- Attempting to access private members from another class causes compilation errors.

### Compilation-Time Errors
- Java enforces access modifier rules during compilation.
- Violations of access policies block successful compilation, not runtime execution.

## Packages and Access Modifiers

### The Role of Packages
- Packages are groups of related classes and interfaces, physically represented as directories containing `.java` files.
- Packages help organize large projects, prevent naming conflicts, and set access boundaries.

### Access in Packages
| Modifier   | Accessible within same package | Accessible from other packages | Accessible in subclasses (any package) |
|------------|-------------------------------|-------------------------------|-----------------------------------------|
| public     | Yes                           | Yes                           | Yes                                     |
| protected  | Yes                           | No                            | Yes                                     |
| default    | Yes                           | No                            | No                                      |
| private    | No                            | No                            | No                                      |

- Classes with the same name can exist in different packages; full package names differentiate them.

### Example Question
- Is it possible for two classes with the same name, but in different packages, to be used in a program? 
- Yes, referencing them requires fully-qualified package names to distinguish.

---

## Conclusion

### Key Insights
- Information hiding is crucial for modularity, maintainability, and security in object-oriented programming.
- Java uses access modifiers (`public`, `protected`, `default`, `private`) to explicitly control the accessibility of classes, methods, and data members.
- Private is the most restrictive, followed by default (package-private), protected, and public as the least restrictive.
- Default access (package-private) restricts use to the same package, even for subclasses located outside the package.
- Public allows universal access, making members part of the public API.
- Protected is primarily intended for subclass and same-package access, supporting inheritance.
- Java enforces these access rules at compile time, preventing errors due to unauthorized access.
- Proper use of access modifiers enhances code clarity, reusability, and security.

### Key Terms
- **Information Hiding:** The principle of restricting access to internal object details.
- **Access Modifier:** Keyword in Java defining the visibility of classes, methods, or variables.
- **public:** Allows access from any class or package.
- **protected:** Allows access within the same package and from subclasses in other packages.
- **default (package-private):** Allows access within the same package; not explicitly declared.
- **private:** Restricts access to the declaring class only.
- **Package:** A namespace for organizing related Java classes, usually corresponding to a directory.
- **Encapsulation:** Wrapping data and methods within a class to restrict direct access from the outside.
- **Subclass:** A class that inherits from another (superclass) and can access protected members.
- **Compilation Error:** An error detected by the compiler due to violation of language rules, such as access restrictions.
- **Method Overriding:** Redefining a method in a subclass; governed by specific access rules.
