# Study notes for Programming In Java : Week 1 : : Lecture 04 : Demonstration-I

## Introduction

This guide provides a comprehensive walkthrough of setting up a Java programming environment, editing and running Java programs from the command line, and understanding the fundamental process of writing, compiling, and executing basic to slightly advanced Java programs. It covers configuring system variables for the Java Development Kit (JDK), using text editors, working with project directories, error handling during compilation, and demonstrates Java programming concepts including array manipulation for both one-dimensional and three-dimensional arrays. The notes aim to provide clarity on each step, ensuring beginners can comfortably progress from setup to running their first Java programs and expanding into more complex constructs.

---

## Setting Up the Java Programming Environment

### Prerequisites for Java Programming
- Installation of the Java Development Kit (JDK), specifically recommended version 8 for compatibility.
- Ensuring the machine (laptop or PC) is properly configured to run Java programs, supporting efficient workflow from a chosen project directory.

### JDK Installation and Directory Structure
- JDK should typically be installed in the `Program Files` directoryâ€”commonly at `C://Program Files/Java/JDK 1.8.0_171`.
- All Java tools (compiler, runtime etc.), system libraries, and commands are located within this directory.

### Setting System Environment Variables
System environment variables are vital for enabling Java commands from any directory in the system. Key variables to configure:

| Variable Name | Value/Path | Description |
|---------------|---------------------------------------------------------------------------------------------|--------------------------------^{|
| JAVA_HOME     | C://Program Files/Java/JDK 1.8.0_171 | Main directory where JDK is installed; enables Java tools to be found. |
| Path          | %JAVA_HOME%/bin                    | Adds Java executable binaries (javac, java) to system-wide command path. |
| Classpath     | C://Program Files/Java/JDK 1.8.0_171/bin | Directory for Java class files; assists in locating runtime classes. |

#### Steps to Set Environment Variables (Windows Example)
1. Right-click on 'This PC/My Computer' and choose 'Properties'.
2. Go to 'Advanced settings'.
3. Select 'Environment Variables'.
4. Add a new system variable `JAVA_HOME` with the JDK installation path as the value.
5. Append `%JAVA_HOME%/bin` to the existing `Path` variable.
6. Set `Classpath` as needed, often mirroring the JDK bin path.

### Creating a Project Directory
- Essential for organizing all Java programs in a structured way.
- Example directory structure: `D:/NPTEL_Java/all_final/week1/code/demonstration1`.
- Directories can be created anywhere on the system for each project or week/module.

## Writing and Editing Java Programs

### Recommended Text Editors
- **Notepad++**: A lightweight, free text editor ideal for writing Java code, offering syntax highlighting and ease of use.
- Any other plain text editor (e.g., Sublime Text, VS Code), but Notepad++ is showcased for demonstration.

### Editing a Java Program
1. Open the text editor (e.g., Notepad++).
2. Type the Java program, ensuring correct syntax and naming conventions.
3. Save the file with a `.java` extension, matching the class name (case-sensitive) exactly.
4. Example: For a class `FirstJavaProgram`, the file **must** be saved as `FirstJavaProgram.java`.

#### Code Organization Tips
- Always give meaningful class names.
- Match file and class names precisely, as Java is case-sensitive.
- Save program files in the designated project directory for better organization.

## Compiling and Running Java Programs

### Compilation Process
- Use the command prompt (Windows) or terminal (Unix/Linux) for compilation and execution.
- Change the directory in the terminal to the project directory using `cd` command.

#### Compilation Command
```
javac FirstJavaProgram.java
```
- `javac` is the Java compiler.
- If no errors occur, compilation succeeds and creates a `.class` file (bytecode).
- The output file is named after the main class (e.g., `FirstJavaProgram.class`).

#### Execution Command
```
java FirstJavaProgram
```
- `java` is the Java runtime launcher.
- Provide only the class name (without the `.class` extension).
- The program executes and displays output as per the code's logic.

### Handling Compilation and Execution Errors
- If the class name and file name do not match (e.g., class is `FirstJavaProgram1` and the file is `FirstJavaProgram.java`), compilation usually fails.
- Always resolve such mismatches as Java expects exact correspondence between public class name and file name.
- Error messages guide in troubleshooting; common errors include syntax, naming, and missing files.

| Error Type                     | Cause                                                     | Solution                    |
|-------------------------------|-----------------------------------------------------------|-----------------------------|
| Compilation Class/File Mismatch| File name and public class name are different             | Rename either to match      |
| Command Not Found              | Path variable not set correctly                           | Check and reset Path        |
| Syntax Error                   | Code not written using correct Java syntax                | Review and correct code     |

## Demonstration of Basic Java Programs

### Example 1: First Java Program
- **Program Name:** `FirstJavaProgram`
- **Main Statement:** Prints a congratulatory message to the user.

#### Program Structure:
```java
public class FirstJavaProgram {
    public static void main(String[] args) {
        System.out.println("Congratulations, your first Java program runs successfully.");
    }
}
```
- Save as `FirstJavaProgram.java`.
- Use `javac` and `java` commands as described above.
- Expected output: `Congratulations, your first Java program runs successfully.`

### Example 2: HelloWorld Program
- **Program Name:** `helloworld`
- **Purpose:** Demonstrates basic printing to console and variations.

#### Key Concepts Demonstrated:
- Case sensitivity in file and class names (`helloworld.java` vs. `HelloWorld.java`).
- Multiple print statements:
    - `System.out.println("Hello, World");`
    - `System.out.println("Hi");`
    - Prints both messages on separate lines if using separate `println` statements.
    - Use of `System.out.print()` to print messages on the same line.

#### Example Variation:
```java
public class helloworld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
        System.out.println("Hi");
    }
}
```
- Demonstrates difference between `print` (no newline) and `println` (adds newline).
- Shows string concatenation for printing multiple values (e.g., `System.out.println("Hi" + " Debasis");`).

### Summary Table: Printing in Java
| Statement                          | Output Format                  |
|-------------------------------------|-------------------------------|
| System.out.println("message");      | Prints message with newline   |
| System.out.print("message");        | Prints message, no newline    |
| System.out.println(var1 + var2);    | Concatenates and prints with newline |

## Working with Arrays in Java

### One-Dimensional Arrays
- Demonstrated with a program named `TestArray`.
- Shows declaration, initialization, traversal, and value computation (like average).

#### Sample Code Snippet
```java
public class TestArray {
    public static void main(String[] args) {
        int[] a = {10, 20, 30, 40, 50};
        // Printing array elements
        for(int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.println(); // For new line

        // Calculating average
        float sum = 0;
        for(int i = 0; i < a.length; i++) {
            sum += a[i];
        }
        float average = sum / a.length;
        System.out.println("Average = " + average);
    }
}
```

#### Key Points
- Arrays are zero-indexed in Java.
- `.length` property gives array size.
- Use of loops (`for`) for traversal and calculations.
- Difference between `print` and `println` in output formatting.
- Inserting blank `System.out.println();` statements for better output formatting.

### Multi-dimensional Arrays: 3D Arrays
- Handled in a sample program called `3DArray`.
- Showcases declaration, memory allocation, initialization via nested loops, and printing.

#### Program Structure
- Declaring a 3D integer array: 
  `int[][][] my3DArray = new int[3][4][5];`
    - 3 pages (outer dimension), each with:
    - 4 rows (middle dimension), each with:
    - 5 columns (inner dimension).

- Initialization and traversal use nested for-loops:
    1. Outer loop for pages.
    2. Middle loop for rows.
    3. Inner loop for columns.
    4. Elements assigned using a function of indices, e.g., `my3DArray[i][j][k] = i * j * k;`.

- Printing follows the same nested loop structure, using `System.out.print()` for values and `System.out.println()` for formatting.

#### Representation Table
| Dimension | Size | Meaning                             |
|-----------|------|-------------------------------------|
| 1st       | 3    | Number of 2D arrays/pages            |
| 2nd       | 4    | Rows in each page                   |
| 3rd       | 5    | Columns in each row                 |

- Array elements are printed as separate 2D arrays (pages), each reflecting one depth/phase.
- Total elements: 3 * 4 * 5 = 60.

#### Program Sample Logic
```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 4; j++) {
        for (int k = 0; k < 5; k++) {
            my3DArray[i][j][k] = i * j * k;
        }
    }
}
// Printing follows same loops
```

### Best Practices & Output Formatting
- For clear, readable output, use spaces or blank lines (using additional `System.out.println();`).
- Favor meaningful variable names.
- Distinguish between array printing styles using `print` and `println` for line formatting.

## Hands-On Exercise
- As practical experience, repeat 3D array logic with 2D arrays (by removing one loop, reducing declaration to `new int[4][5];`).
- Initialize 2D arrays and print their contents similarly.
- Practice helps reinforce understanding of array indexing, multi-dimensional traversal, and output formatting.

## Error Handling and Troubleshooting
- Compilation errors (e.g., name mismatches, undeclared variables) highlighted, along with steps for resolution.
- Importance of case sensitivity for Java class and file naming re-emphasized.

---

## Conclusion

### Key Insights
- Proper setup of the Java environment and system variables is foundational for smooth Java programming.
- Consistency between class names and file names is compulsory in Java for successful compilation.
- Notepad++ and other text editors aid in writing and editing code comfortably, but output formatting depends on the Java code (choice of `print` vs `println`).
- Understanding of command-line operations (compile with `javac`, run with `java`) is essential for beginners to gain confidence with Java's workflow.
- Array operations (one-dimensional, multi-dimensional) demonstrate both language syntax and programming logic, providing a critical learning step from basic to advanced programming.
- Output formatting can be enhanced with careful use of printing statements and spacing, improving program presentation and user experience.

### Key Terms
- **JDK (Java Development Kit):** The software package containing tools, libraries, and runtime environments required to develop and run Java programs.
- **JAVA_HOME:** Environment variable pointing to the installation directory of the JDK; fundamental for system-wide Java command access.
- **Path Variable:** An environment variable listing directories for executable search; must include Java's `bin` directory.
- **Class File (.class):** The compiled Java bytecode file generated from a `.java` source file by the `javac` compiler.
- **javac:** Command-line Java compiler that converts source code files to bytecode.
- **java:** Java application launcher that runs bytecode files.
- **System.out.print / println:** Standard output methods for displaying messages to the console, with/without new lines.
- **Array:** A fixed-size, indexed data structure for storing elements of the same data type; may be one-dimensional or multi-dimensional.
- **Notepad++:** Popular free text editor for editing Java source code with enhanced features like syntax highlighting.
- **3D Array:** Multi-dimensional array structure in Java, represented as arrays of arrays, useful for managing complex data sets.
- **Loop/Nested Loop:** Control structures that repeat code execution; nested loops allow traversal of multidimensional arrays.
- **Concatenation:** Joining multiple strings or variables, typically using the `+` operator in Java.
