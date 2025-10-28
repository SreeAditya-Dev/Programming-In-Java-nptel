# Study notes for Programming In Java : Week 4 : : Lecture 19 : Demonstration-VIII

## Introduction

Packages are foundational constructs in Java that assist in creating modular, organized, and reusable code. This guide provides a detailed demonstration of Java package usage, covering built-in API imports, creation and management of user-defined packages, package access controls, handling name collisions, and the use of packages in inheritance. The nuances of visibility modifiersâ€”public, private, protected, and defaultâ€”within the context of packages are also unraveled, giving a clear view into practical considerations for real-world Java programming.

---

## Java Packages and Built-In API Imports

Packages in Java serve as containers for classes and interfaces, grouping related types to streamline code management and namespace division. Java offers a robust standard library with numerous built-in packages.

### Importing Built-In API Packages

- Java comes with many standard (API) packages (e.g., java.lang, java.util).
- The `import` statement is used to bring classes or entire packages into a Java program.

#### The `import` Statement
- Syntax: `import packageName.ClassName;` â€” imports a single class
- Syntax: `import packageName.*;` â€” imports all classes in the package
- Example: `import java.lang.Math;` or `import java.lang.*;`

#### Accessing Package Members
- After importing, classes and their public members are directly accessible.
- Example: `Math.sqrt(20.0)` computes the square root using the static method `sqrt()` in the `Math` class from java.lang.

| Import Statement                   | Classes Available              | Usage Example      |
|-------------------------------------|-------------------------------|-------------------|
| import java.lang.*;                 | All classes in java.lang       | Math.sqrt(4)      |
| import java.util.Vector;            | Only Vector class              | new Vector()      |
| import java.util.*;                 | All classes in java.util       | new ArrayList()   |

#### Importing Specific Classes
- Importing an entire package can increase load time unnecessarily.
- Good practice: import only what is needed (e.g., `import java.util.Vector;`).
- Classes can also be referenced with their fully qualified name (e.g., `java.util.ArrayList list = new java.util.ArrayList();`) without an import statement.

### Importing Multiple Packages
- Multiple classes from different packages can be imported in a single program (e.g., both `Vector` and `ArrayList` from `java.util`).
- Use of `import java.util.*;` brings all relevant classes into scope.

## User-Defined Packages

User-defined packages allow the logical grouping of custom classes. Organization not only improves clarity and maintainability but also enables access protection and namespace management.

### Creating a Package
1. Declare the package at the top of the Java source file using `package packageName;` (e.g., `package myPackage;`).
2. Place the source file in a directory named after the package (`myPackage/`).
3. The public class in the file should have the same name as the file (class `MyClass` in `MyClass.java`).
4. Compile the file so that the `.class` file is stored in the corresponding directory.

#### Example Process
- Directory structure: `myPackage/MyClass.java`
- File content:
  ```java
  package myPackage;
  public class MyClass {
      // Class content
  }
  ```
- Compilation stores `MyClass.class` in `myPackage/`.

### Accessing User-Defined Packages
- Import using `import myPackage.MyClass;` or `import myPackage.*;`, then instantiate or use as needed.
- Ensure that the root package directory is in the classpath for the runtime to locate classes.

#### Class Access Example
```java
import myPackage.MyClass;
...
MyClass obj = new MyClass();
```

#### Multiple Classes in a Package
- A package can house multiple class files (e.g., `myPackage/MyClass1.java`, `myPackage/MyClass2.java`).
- Import all with `import myPackage.*;` to access all classes.

### Access Control and Visibility in Packages

Visibility modifiers have critical roles in determining accessibility among classes within and outside packages.

#### Access Specifiers:
| Modifier    | Same Class | Subclass (Same pkg) | Non-subclass (Same pkg) | Subclass (Other pkg) | Non-subclass (Other pkg) |
|-------------|------------|---------------------|-------------------------|----------------------|--------------------------|
| public      | Yes        | Yes                 | Yes                     | Yes                  | Yes                      |
| protected   | Yes        | Yes                 | Yes                     | Yes                  | No                       |
| no modifier | Yes        | Yes                 | Yes                     | No                   | No                       |
| private     | Yes        | No                  | No                      | No                   | No                       |

- **public**: Visible everywhere
- **protected**: Visible in package and subclasses (even if in different package)
- **no modifier (default)**: Visible only within the package
- **private**: Visible only within the declaring class

### Fully Qualified Class Names and Name Collisions

#### Same Class Name in Multiple Packages
- Different packages can contain classes with identical names (e.g., `myPackage1.MyClass` and `myPackage2.MyClass`).
- Issue: Importing both can lead to a naming collision; Java does not allow two classes of the same name imported from different packages in the same file.
- Solution: Use fully qualified names to instantiate objects:
  ```java
  myPackage1.MyClass a = new myPackage1.MyClass();
  myPackage2.MyClass b = new myPackage2.MyClass();
  ```

### Inheritance Across Packages

Classes in packages may serve as superclasses for classes in the same or other packages.

#### Requirements:
- The superclass must be `public` so it is accessible outside its package.
- The subclass must import the package or use a fully qualified name.
- Only accessible members (public, protected) can be inherited and accessed.

| Superclass Member Type | Accessible in Subclass (Other Pkg)? |
|-----------------------|--------------------------------------|
| public                | Yes                                  |
| protected             | Yes                                  |
| (default/package)     | No                                   |
| private               | No                                   |

#### Example:
Suppose `myPackage.Balance` is `public`, and fields are at least `protected`.
A class `Savings` in another file can `extends Balance` and access all eligible members.

#### Method Overriding
- Overriding a method (like `show()`) in the subclass offers extended or modified functionality semantics.
- If the original method is `public` or `protected`, the subclass can override it.

### Explicit Package Reference Without `import`

- Classes can still be instantiated using the complete package path (fully qualified name), even when not imported:
  ```java
  myPackage.Balance obj = new myPackage.Balance(...);
  ```
- Useful when class names would otherwise collide, or to reduce namespace pollution/export.

## Access Modification Demonstrated

A comprehensive example may involve two packages (`myPackage1`, `myPackage2`) and classes demonstrating all four types of access control.

### Example Breakdown:
1. **Class `X` (in `myPackage1`)**
    - Members: `n` (default), `p` (private), `q` (protected), `r` (public)
    - All members accessible within the class itself
2. **Class `Y` (extends `X`, same package)**
    - Can access `n` (default), `q` (protected), `r` (public); **cannot** access `p` (private)
3. **Class `A` (uses `X`)**
    - Can access `n` (default), `r` (public); not `p` or `q`
4. **Class `Z` (extends `X`, different package `myPackage2`)**
    - Can access `q` (protected), `r` (public); not `n` (default/package), nor `p` (private)
5. **Class `B` (uses `X` in a different package)**
    - Only `r` (public) accessible

#### Table Summary
| Class Relationship                 | Access Default | Access Private | Access Protected | Access Public |
|------------------------------------|:-------------:|:--------------:|:---------------:|:------------:|
| Same class                         |      Yes      |      Yes       |      Yes        |     Yes      |
| Subclass same package              |      Yes      |      No        |      Yes        |     Yes      |
| Non-subclass same package          |      Yes      |      No        |      Yes        |     Yes      |
| Subclass different package         |      No       |      No        |      Yes        |     Yes      |
| Non-subclass different package     |      No       |      No        |      No         |     Yes      |

## Best Practices and Common Mistakes

- Always declare classes as `public` if they need to be accessed from other packages.
- Keep classes and packages organized in the correct directory structure.
- Avoid importing packages or classes unnecessarilyâ€”minimize the imported scope for performance and clarity.
- Use fully qualified names judiciously to avoid naming collisions.
- Understand and apply proper access controls for encapsulation and the principle of least privilege.

## Advanced Concepts: Packages as Information Hiding

- Packages offer an additional information hiding layer, controlling visibility across module boundaries.
- Combining packages with proper access modifiers leads to more secure and maintainable code.
- Inheritance can be managed more robustly by controlling protected and public access properly.

---

## Conclusion

### Key Insights
- Java packages provide powerful modularization and namespace management.
- Import statements streamline reference to external classes, but the simplest or most explicit form should be used for clarity.
- User-defined packages enforce logical separation, enhance maintainability, and secure code via access control.
- Fully qualified names resolve naming conflicts when two classes have the same name in different packages.
- Inheritance across packages is straightforward if visibility modifiers (public/protected) are used correctly.
- Access specifiers determine the scope of class members, requiring thorough understanding when designing shared libraries or frameworks.
- Advanced use of packages leads to improved encapsulation and information hiding, which are pivotal in large-scale software development.

### Key Terms
- **Package**: A grouping of related Java classes and interfaces providing namespace management.
- **Import Statement**: A Java statement used to include classes or an entire package namespace for easy access.
- **Access Specifier/Modifier**: Keywords in Java (public, private, protected, default) that determine accessibility of classes and class members.
- **Fully Qualified Class Name**: Complete reference to a class, including its package (e.g., `java.util.ArrayList`).
- **Inheritance**: Mechanism by which a class can inherit fields and methods from a superclass, even across packages if visibility allows.
- **Information Hiding**: Principle of restricting access to the internal state and implementation details of a class or package.
- **Namespace Collision**: Conflict that occurs when two imported classes with the same name cause ambiguity; resolved via fully qualified names.
- **Public**: Accessible everywhere.
- **Private**: Accessible only within the class where declared.
- **Protected**: Accessible within the package and subclasses, even outside package.
- **Default (Package-Private)**: Accessible only within classes in the same package.

---
