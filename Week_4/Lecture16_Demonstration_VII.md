# Study notes for Programming In Java : Week 4 : : Lecture 16 : Demonstration-VII

## Introduction

Information hiding is a cornerstone of object-oriented programming, ensuring that the internal details of classes are shielded from external access and modification. Java provides robust mechanisms for information hiding through access specifiers: `default`, `public`, `private`, and `protected`. This guide delves into their practical workings, supported by hands-on examples covering object creation, accessibility, and nuances surrounding class members, methods, constructors, inheritance, and method overriding. By examining code behaviors, errors, and best practices, these notes will provide clarity on using Java's access specifiers for effective information hiding.

---

## Java Access Specifiers and Information Hiding

Access specifiers in Java determine the accessibility of classes, methods, and variables. They play a crucial role in ensuring information hiding, safeguarding class integrity, and controlling the exposure of implementation details.

### Overview of Access Specifiers
- **Default**: No keyword; applies if no other access modifier is provided.
- **Public**: Most open, allowing access from any location.
- **Private**: Most restrictive, limiting access strictly within the class.
- **Protected**: Allows access within the same package and from subclasses (even if in different packages in some contexts).

#### Table: Java Access Specifiers - Access Levels

| Specifier  | Same Class | Same Package | Subclass | Other Packages |
|------------|------------|--------------|----------|---------------|
| public     | Yes        | Yes          | Yes      | Yes           |
| protected  | Yes        | Yes          | Yes      | No*           |
| default    | Yes        | Yes          | No       | No            |
| private    | Yes        | No           | No       | No            |

*Protected is accessible in subclasses even if they are in other packages.

### Importance in Information Hiding
- Restricts access to sensitive data and methods.
- Encourages encapsulation and modularity.
- Promotes security, code maintenance, and clarity in interactions between components.

## Demonstrations of Access Specifiers in Java

This section provides practical insights, illustrated through code examples, on how access specifiers affect the usage of classes, methods, and data members.

### Default Access Modifier

#### Behavior
- A class, method, or member with no explicit specifier is given default (package-private) access.
- Accessible only within the same package.

#### Demonstration
##### Example 1: Two Classes, Same File (Default Access)
- Both class `A` and the main class are in a single file (e.g., `demonstration_71.java`).
  - Access and execution are smooth since both are within the same package (directory).
- Good practice: Store different classes in separate files, naming the file after the class if it is public.

##### Example 2: Two Classes, Separate Files, Same Directory
- Class `A` in `A.java`; main class in `demonstration_72.java`.
- Both files reside in the same directory.
- Default access still allows object creation and method access across these classes.

##### Example 3: Two Classes in Different Directories
- Class `A` is placed in one directory, the main class in another.
- Attempting to access the default class or its members from the main class in another directory results in a compilation error (`cannot find symbol`), demonstrating the limitation of default access.

#### Key Points for Default Access
- Members/classes are accessible within the same package (directory).
- Moving a class or member to a different package or directory blocks access.

### Public Access Modifier

#### Behavior
- Public members/classes are accessible from any location, across different directories and packages.

#### Demonstration
##### Example 4: Public Class in a Package Accessed from Another Package
- Class `A` is declared as `public` and stored under `pack1/A.java`.
- Main class is in `pack2/demonstration_74.java` and accesses `A` via an import statement.
- Compilation and execution succeed, as public classes/members are accessible across packages.

##### Example 5: Method Access Within Public Classes
- If class `A` is public but its method (like `message`) is default, access from different packages fails.
- Changing the method's access to public rectifies the error.

#### Key Points for Public Access
- Public classes must be stored in files matching the class name.
- Public members are accessible everywhere; both their class and member need to be public for external access.

### Private Access Modifier

#### Behavior
- Private members or methods are accessible only within their own class.

#### Demonstration
##### Example 6: Private Data Member in a Class
- Class `A` defines a private data member (e.g., `private int data`) and a public method.
- Attempting to access `data` from outside class `A` (even in the same file) produces a compile-time error, demonstrating strict encapsulation.

##### Example 7: Private Members and Indirect Access
- Class `A` has a private member and a public method.
- The public method, when called from another class, internally uses the private dataâ€”this is allowed.
- Direct external access is forbidden, but indirect access via a public method is permitted.

#### Restrictions on Private in Main Class
- Java does not allow class members in the main method/class to be declared private or public when in the same file if not in their own separate class files.
- Attempting to mark a member as public/private in such context results in a compile-time error. Only default access is allowed for class members directly in the main class in these cases.

#### Private Constructors
##### Example 8: Private Constructor
- If a class's constructor is declared private, object creation is blocked outside the class.
- Attempting to instantiate such a class from another class leads to a compilation error.
- Removing the private modifier (or making the constructor public or default) restores the ability to create objects.

#### Key Points for Private Access
- Used for encapsulation and restricting access.
- Often used in singleton patterns (private constructor), though with controlled object creation internally.

### Protected Access Modifier

#### Behavior
- Accessible within the same package and by subclasses, even if those subclasses are in other packages.

#### Demonstration
##### Example 9: Protected Members in Same File
- Protected data members and methods in a class (`protected int rollNo; protected void message()`) are accessible by other classes within the same file.
- If classes are placed in different files (and possibly different packages), direct access is blocked unless through inheritance.

##### Example 10: Protected Members and Inheritance
- Superclass with protected members; subclass (possibly in another package) accesses these members via inheritance.
- If a member is private in the superclass, it remains inaccessible in the subclass even if in the same package.
- Changing the private member to protected enables access in the subclass.

#### Table: Accessibility of Protected Members
| Context                      | Can Access? |
|------------------------------|-------------|
| Same file, different class   | Yes         |
| Same package, different file | Yes         |
| Subclass (same/different pkg)| Yes         |
| Non-subclass, other package  | No          |

### Summary Table: Access Specifiers for Classes and Members

| Usage                            | Default | Public | Private | Protected |
|----------------------------------|---------|--------|---------|-----------|
| Class in same package            | Yes     | Yes    | No      | Yes*      |
| Class in another package         | No      | Yes    | No      | Yes*      |
| Subclass in same package         | Yes     | Yes    | No      | Yes       |
| Subclass in different package    | No      | Yes    | No      | Yes       |
| Outside package, No Inheritance  | No      | Yes    | No      | No        |

*For protected, only through inheritance, not by object reference unless in the same package.

## Cases and Rules Regarding Class Declarations

### File Name Restrictions
- Only one public class per file; file name must match the public class name.
- Multiple classes can reside in one file only if none are public (default access required).
- Attempting to declare more than one public class in a single file or mismatching the file name for a public class yields a compile-time error.

### Members in Main Class
- In files with multiple classes (none public), all member variables and methods must have default access; others yield compilation errors.

## Working with Constructors and Access Modifiers

### Private Constructors
- Prevent external instantiation; used to restrict object creation (e.g., singleton patterns).
- Public or default constructors allow object creation externally.

### Access Modifiers in Inheritance and Overriding

#### Overriding Methods and Access Levels
- A subclass can override a superclass's method only if the overriding method has equal or more accessible (weaker) access.
    - `public` may be overridden with `public` or `protected` or default.
    - `protected` can be overridden with `protected` or default.
    - `private` methods are not inherited and cannot be overridden.
    - Subclass cannot reduce accessibility of the overridden method.

#### Example Scenario
- Superclass method is `protected`.
    - Overriding it with `public` in a subclass is allowed.
    - Overriding it with `private` is not.

### Examples: Overriding Access Table

| Superclass Method Access | Allowed Subclass Overriding Access |
|-------------------------|-------------------------------------|
| public                  | public, protected, default           |
| protected               | protected, default                   |
| default                 | default                              |
| private                 | (Cannot be overridden)               |

### Hierarchy of Access
- `private` > `protected` > `default` > `public` (from most to least restrictive)

## Comprehensive Example: Multiple Modifiers in One Program

A class might have members with mixed access levels (public/private/protected/default), demonstrating their individual behaviors:
- Public members/methods: universally accessible.
- Private: encapsulated strictly within the class.
- Protected: accessible to subclasses or within package.
- Default: accessible only within the same package.

Typical code patterns involve attempting various valid/invalid accesses to observe compile-time successes/errors and behavior in inheritance or package contexts.

## Error Handling and Compilation

Java's compiler rigorously enforces access specifications:
- Invalid or illegitimate accesses yield compilation errors.
- Developers are guided via error messages to fix access-level violations.
- This automatic enforcement supports code safety and modularity.

---

## Conclusion

### Key Insights
- Java provides four main access specifiers (`default`, `public`, `private`, and `protected`) for granular control of program structure and information hiding.
- `Default` limits access to within the package; often used when no keyword is specified.
- `Public` offers the broadest access; but comes with the requirement that public classes must be alone in files named after them.
- `Private` restricts access to the defining class, ensuring complete encapsulation.
- `Protected` extends visibility to subclasses and, within packages, to other classes.
- Attempting to access members outside their permitted scope leads to compilation errors, guiding best practices for encapsulation.
- Inheritance and method overriding bring additional nuances, as overriding methods cannot tighten (reduce) visibility compared to parent methods.
- Constructors can be private to control object creation, but this blocks instantiation from outside the class.
- For multiple classes in one source file, only one may be public, and the rest must use default access.
- Regular practice with these concepts, including purposely introducing errors, helps cement understanding of Java's access control mechanisms.

### Key Terms
- **Access Specifier**: Keyword determining the visibility and accessibility of Java classes, methods, and variables.
- **Default Access**: No explicit modifier is used; accessible only within the same package.
- **Public**: Accessible from any location (any class, any package).
- **Private**: Accessible only from within the defining class.
- **Protected**: Accessible within the same package and by subclasses (even across packages through inheritance).
- **Package**: A namespace grouping related classes; also maps to folders in the filesystem.
- **Encapsulation**: The object-oriented principle of bundling data and restricting access to internal states.
- **Information Hiding**: Concealing the inner workings or data of objects from outside interference and misuse.
- **Constructor**: Special method for initializing new objects; can be privatized to restrict instantiation.
- **Method Overriding**: Providing a new implementation for a superclass method in a subclass, subject to access compatibility.
- **Compilation Error**: An error flagged by the Java compiler when access rules or other syntax constraints are violated.

---
