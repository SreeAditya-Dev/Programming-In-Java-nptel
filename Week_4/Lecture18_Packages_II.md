# Study notes for Programming In Java : Week 4 : : Lecture 18 : Packages-II

## Introduction

Java packages provide a structured way of organizing and accessing classes and interfaces. This topic covers how Java programs find and use packages, the mechanisms for specifying package locations, the differences between access specifiers in the context of packages, and practical examples for understanding package usage and access protection. A detailed understanding of packages is essential for modular programming, code reuse, and maintaining large codebases in Java.

---

## Methods of Accessing Packages in Java

A package is a namespace that organizes a set of related classes and interfaces. Packages are used to prevent naming conflicts, control access, and make code maintenance easier.

### How the Java Runtime Locates Packages
- When running a program, the Java runtime (interpreter) needs to know where referenced packages are located.
- This is managed by the `classpath`, a system environment variable that tells Java where to search for user-defined and built-in packages.
- `classpath` can be set in Windows, Unix, or MacOS according to the conventions of each operating system.

#### Three Methods to Specify Package Location
1. **Default Search (Working Directory)**
    - If no specific classpath is set, Java looks for packages in the current working directory.
    - The interpreter tries to find a directory that matches the package name specified in the import statement, under the working directory.
    - This is the simplest method, suitable for small projects or testing.

2. **Explicit Classpath Setting**
    - The classpath variable can be set to include any directory in the file system, not just the working directory.
    - Allows packages to be referenced from any location in the filesystem.
    - Example: Setting classpath as `C:\MyPrograms\Java` tells Java to search for packages in that directory tree.
    - Most practical for larger projects or when packages are stored in various locations.

3. **Specifying Package Location at Command Execution**
    - The package path can be specified directly when running `javac` or `java` commands.
    - Example: `javac abc.xyz.ClassName` will compile the class from the specified package structure directly.
    - Useful for ad-hoc compilation or running specific classes without modifying environment variables.

| Method                         | Description                                                        | Use case                        |
|------------------------------- |--------------------------------------------------------------------|----------------------------------|
| Default Search                 | Looks for package under current working directory                   | Small projects, quick demos      |
| Explicit Classpath Setting     | Sets classpath to any folder containing packages                    | Larger projects, multiple paths  |
| Command-Specific Package Path  | Specifies package on each invocation of `javac`/`java`              | One-off runs, special cases      |

### Example: Accessing a User-Defined Package
- Suppose you have a package `MyPack`.
- `MyPack` can be placed under the working directory or its path can be set in classpath, or invoked explicitly in Java commands.
- If path is set, Java will look into the specified directory for the package.
- If the package is not found, a 'package not found' or 'no class file available' error is reported.

#### Sample Steps
1. Place `MyPack` directly under the working directory.
2. Set classpath: `set CLASSPATH=C:\MyPrograms\Java` (for Windows).
3. Use `import MyPack.*;` in your code to import all classes from the package.
4. Compile and run your Java program; the interpreter checks the classpath.

## Importing Packages and Using Classes

### Import Statements
- The `import` keyword is used to make classes and interfaces from packages available to your program.
- Syntax: `import package_name.ClassName;` or `import package_name.*;` (imports all classes)

#### Examples with Standard Library
- `import java.util.Date;` - Imports the Date class from Java's util package.
- `import java.io.*;` - Imports all classes from Java's io package.

#### User-Defined Packages
- The same import mechanism applies to user-defined packages as to Java's API packages.
- No distinction: both use the same syntax and method for accessibility.

#### Import Paths
- If the classpath variable includes the root directory of the package, importing with the package name is sufficient.
- If not, you might need to specify the full path in the import statement.
- For nested packages or subpackages: `import package1.package2.ClassName;`

### Importing in Practice
- If all related Java files are placed in the same working directory, no explicit import or classpath is strictly necessary.
- If files are distributed across different directories, import statements and/or proper classpath settings become mandatory.

### Example Code Structure 
- Public class `Balance` in package `MyPack`:
    - Declared public for visibility.
    - Has public fields and methods (constructor and `show()` method).
    - Can be imported and used in any other Java program, just like built-in Java classes.

| File Name            | Contents                                      | Notes                        |
|--------------------- |----------------------------------------------|------------------------------|
| Balance.java         | package MyPack; public class Balance {...}    | Must be public               |
| AccountBalance.java  | (Imports and uses MyPack.Balance)             | Needs proper import/classpath|

## Access Specifiers and Package-Level Access Control

Access specifiers (modifiers) in Java allow fine-grained control over which parts of a class or package are visible and accessible in various scopes.

### Four Levels of Visibility in Java Packages
Java addresses visibility in four main scenarios regarding class members:
1. **Same package, subclass.**
2. **Same package, non-subclass.**
3. **Different package, subclass.**
4. **Different package, non-subclass.**

Each is affected differently by access specifiers.

### Java Access Specifiers
- **public**: Member accessible from anywhere (any class, package, or subclass).
- **protected**: Member accessible within the same package and by subclasses in any package.
- **default (no modifier)**: Member accessible only within the same package.
- **private**: Member accessible only within the defining class.

#### Default Access
- No explicit modifier.
- Used mainly for package-private visibility: only classes inside the same package have access.
- Not recommended for classes intended to be widely reused outside the package.

| Access Level    | Same Class | Same Package Subclass | Same Package Non-Subclass | Different Package Subclass | Different Package Non-Subclass |
|-----------------|------------|----------------------|---------------------------|----------------------------|-------------------------------|
| private         | Yes        | No                   | No                        | No                         | No                            |
| default         | Yes        | Yes                  | Yes                       | No                         | No                            |
| protected       | Yes        | Yes                  | Yes                       | Yes                        | No                            |
| public          | Yes        | Yes                  | Yes                       | Yes                        | Yes                           |

#### Explanation of Table:
- Private: Only accessible to the same class.
- Default: Accessible to all classes in the same package.
- Protected: Accessible to all classes in the same package, and to subclasses (even if in a different package).
- Public: Accessible from anywhere.

#### Example Scenarios
- **Same Class:** Any member can be accessed inside its own class.
- **Same Package Subclass:** Any member except private can be accessed.
- **Same Package Non-Subclass:** Default, protected, and public members accessible.
- **Different Package Subclass:** Only protected and public accessible.
- **Different Package Non-Subclass:** Only public accessible.

### Practical Examples

#### Example 1: Package Structure with Different Access Levels
- Two packages: `MyPackage1` and `MyPackage2`.
- Classes:
    - MyPackage1: `X` (base), `Y` (extends X), `A`.
    - MyPackage2: `Z` (extends X), `B`.

##### Class X (in MyPackage1)
- Fields:
    - `int n` (default)
    - `private int p` (private)
    - `protected int q` (protected)
    - `public int r` (public)
- Constructor: accesses all members (valid inside class)

##### Class Y (in MyPackage1, extends X)
- Constructor:
    - Can access: n (default), q (protected), r (public)
    - Cannot access: p (private)
- Attempting to access `p` leads to a compilation error.

##### Class A (in MyPackage1)
- Constructor:
    - Can access: n (default), r (public)
    - Cannot access: p (private), q (protected)
- Not a subclass; protected does not apply.

##### Class Z (in MyPackage2, extends X)
- Constructor:
    - Can access: q (protected), r (public)
    - Cannot access: n (default), p (private)

##### Class B (in MyPackage2)
- Constructor:
    - Can access: r (public)
    - Cannot access: n (default), p (private), q (protected)

##### Compilation Details
- Non-complying accesses (e.g., private from other classes) cause compilation errors.
- Only correct usages conforming to the access rules successfully compile.

##### Code Illustration Table
| Package/Class    | Accessed Member   | n (default) | p (private) | q (protected) | r (public) |
|------------------|------------------|-------------|-------------|---------------|------------|
| X (own class)    | Any              | Yes         | Yes         | Yes           | Yes        |
| Y (same pkg, sub)|                  | Yes         | No          | Yes           | Yes        |
| A (same pkg, non)|                  | Yes         | No          | No            | Yes        |
| Z (diff pkg, sub)|                  | No          | No          | Yes           | Yes        |
| B (diff pkg, non)|                  | No          | No          | No            | Yes        |

#### Key Observations
- **public** is necessary for classes and members that will be reused in other packages.
- Proper use of import and classpath ensures access to the desired classes.
- Misuse or omission of access specifiers leads to compilation error, enforcing encapsulation.

## Practical Tips for Package Usage

### Best Practices
- Place reusable classes in dedicated packages, declare as `public`.
- Use explicit classpath and import statements for larger projects spanning multiple directories.
- Restrict member visibility; do not default to `public` unnecessarily.
- Avoid placing `main` methods inside packages for classes intended only as library components.

### Common Pitfalls
- Failing to declare classes as public leads to inaccessibility outside the package.
- Not updating classpath leads to 'class not found' errors.
- Accessing private or default members outside intended packages causes compilation errors.

---

## Conclusion

### Key Insights
- Java provides three main ways to access packages â€“ default working directory, explicit classpath, and direct command invocation.
- Importing packages, both built-in and user-defined, requires careful management of the environment and correct syntax.
- Access specifiers (public, protected, default, private) strictly govern what can be accessed where, especially in a package context.
- Real-world examples clarify accessibility across packages and subclasses; public and protected are key for library development and inheritance respectively.
- Proper structuring of packages and class member accessibility helps in building modular, maintainable, and less error-prone Java applications.

### Key Terms
- **Classpath**: An environment variable or command-line parameter specifying paths where Java should search for classes and packages.
- **Package**: A mechanism in Java to group related classes and interfaces, avoid naming conflicts, and control access.
- **Import Statement**: A keyword (`import`) used to access classes and interfaces from packages.
- **Access Specifiers**: Java keywords (public, protected, default, private) that determine visibility of members and classes.
- **Public**: The member or class is accessible from any other class or package.
- **Protected**: The member is accessible in the package and to subclasses outside the package.
- **Default (package-private)**: The member is accessible only within its package.
- **Private**: The member is accessible only within its own class.
- **Subclass**: A class that extends another (superclass), inheriting its accessible members.
- **Compilation Error**: An error reported by the Java compiler due to violations of access rules, invalid syntax, or missing definitions.

---
