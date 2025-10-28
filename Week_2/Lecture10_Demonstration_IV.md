# Study notes for Programming In Java : Week 2 : : Lecture 10 : Demonstration-IV

## Introduction

This guide focuses on the core concepts and detailed demonstrations of input and output (I/O) mechanisms in Java programming. The content covers different ways to display data on the standard output (the screen), formatted output options, and various methods of accepting input from the user or command line. The Java approaches addressed include the use of System.out methods (print, println, and printf), command-line arguments, the Scanner class, and the DataInputStream class, illustrating how these tools facilitate communication between Java programs and their users.

---

## Java Output Techniques

Java provides multiple ways to display information to users, primarily through the standard output stream connected to the display. Understanding the functionality and differences among these output methods is foundational to Java programming.

### System.out Methods

#### The print() Method
- Prints data to the screen without moving the cursor to a new line.
- Allows continued output on the same line until a newline character or println() is used.

#### The println() Method
- Prints data to the screen and advances the cursor to the next line.
- Useful for outputting multiple lines, each starting from a new line.

#### The printf() Method
- Provides formatted output, allowing precise control over the appearance of strings, numbers, and other data types on the display.
- Syntax is similar to the C language's printf function, using format specifiers such as %d, %f, etc.

| Method       | Moves Cursor to Next Line | Formatting Capabilities |
|--------------|--------------------------|------------------------|
| print()      | No                       | Basic                 |
| println()    | Yes                      | Basic                 |
| printf()     | No                       | Advanced              |

### Illustrative Examples

#### Basic Output with print() and println()
- Initial statements such as System.out.println(1); & System.out.println(2); print '1' and '2' each on separate lines.
- System.out.print(3); System.out.print(4); display '3' and '4' on the same line.
- Newline characters (\n) within print statements can force line breaks, similar to C/C++.

**Example Output Flow**:
```
1
2
34
```

#### Using Concatenation and Variables
- Output can be customized by concatenating strings and variables using '+'.
- Example: System.out.println("Value of x is: " + x);
- Variables accessed directly in static main methods without object creation, provided they are declared appropriately in the context.

#### Advanced Formatting with printf()
- Accepts format specifiers to control decimal precision, alignment, padding, etc.
- Examples:
    - System.out.printf("%d", x);    // Prints variable x as an integer
    - System.out.printf("%.2f", pi); // Prints Pi value rounded to 2 decimal places
    - System.out.printf("%20.4f", value); // Prints a floating value in a field width of 20, with 4 digits after decimal

| Format Specifier | Output Purpose                |
|------------------|------------------------------|
| %d               | Integer (decimal)            |
| %f               | Floating point (default 6 dp)|
| %.2f             | Floating point (2 decimals)  |
| %n               | Platform-independent newline |

**Precision and Field Width**:
- Specifiers such as %4.8f or %6.2f control the number of digits before and after the decimal point, and the overall output width.
- Rounding and truncation are managed by the JVM as per specified formats.

#### Points on printf() Use
- Mixing up format specifiers or using an incorrect specifier will yield formatting errors or unexpected outputs.
- printf() is suitable for formatted reports, not just basic display.
- For simpler needs, print() or println() is sufficient.

---

## Input Methods in Java

Java programs often need to read user input. There are three primary ways to obtain input: command-line arguments, the Scanner class, and the DataInputStream class. Each has its context of use, advantages, and limitations.

### Command-Line Arguments

#### Concept
- When running a Java program, parameters following the class name in the execution command are passed as strings.
- Syntax: `java ClassName arg1 arg2 arg3 ...`
- In the main method: `public static void main(String[] args)`
    - 'args' is an array of strings storing each command-line input.

#### Accessing Command-Line Arguments
- Use a loop to iterate through the args array:
```java
for (int i = 0; i < args.length; i++) {
    System.out.println(args[i]);
}
```
- Each argument is accessible as a string; conversion to other types (int, float, etc.) is possible using parsing methods.

#### Practical Example
| Input Command                        | args Array Contents             |
|--------------------------------------|---------------------------------|
| java DemoClass hello world 123       | ["hello", "world", "123"]        |

- Printing each argument outputs each on a separate line.
- To convert an argument to an integer: `int x = Integer.parseInt(args[0]);`
- Non-numeric strings passed through Integer.parseInt will cause a runtime error (NumberFormatException).

#### Command-Line Argument Validation
- Check if any arguments are passed by testing args.length:
```java
if (args.length == 0) {
    System.out.println("No command line arguments found");
} else {
    // process args
}
```
- A robust Java program verifies valid input before processing.

#### Limitations
- Inputs are read only once at startup; real-time user interaction is not possible via command-line arguments.
- All inputs are received as strings; explicit parsing needed for numerical data.

### Scanner Class

#### Overview
- Provides a user-friendly, flexible, and straightforward way to read inputs from the keyboard at runtime.
- Part of `java.util` package. Must be imported explicitly: `import java.util.Scanner;`
- Can read various data types: nextInt(), nextFloat(), nextDouble(), next(), nextLine().

#### Example Usage
```java
Scanner sc = new Scanner(System.in);
System.out.print("Enter a number: ");
int num = sc.nextInt();
```
- The instance 'sc' of Scanner reads input from the keyboard due to the System.in parameter.
- Similar methods exist for other types: nextFloat(), nextDouble(), nextLine() for full lines, next() for single words.

| Scanner Method   | Reads              |
|------------------|-------------------|
| nextInt()        | Integer           |
| nextFloat()      | Float             |
| nextDouble()     | Double            |
| next()           | String (word)     |
| nextLine()       | String (line)     |

#### Input Flow Example
- Prompt user to enter two numbers:
    - Scanner asks for input, reads values, stores in variables (e.g., a and b).
    - Program logic processes these values (e.g., computes and displays the maximum).

**Sample Program**:
```java
Scanner sc = new Scanner(System.in);
System.out.print("Enter first number: ");
int a = sc.nextInt();
System.out.print("Enter second number: ");
int b = sc.nextInt();
System.out.println("The greater number is: " + (a > b ? a : b));
```

#### Reading Floating Point Inputs
- Use nextDouble() or nextFloat() for such values.
- Example: Reading a circle's radius, calculating area.

#### Advantages
- Accepts input at runtime, promoting interactivity.
- Can easily parse multiple data types.
- Intuitive and less error-prone compared to command-line arguments.

#### Limitations
- Scanner may sometimes encounter issues when mixing nextLine() with other next*() methods due to newline character handling.
- Does not provide robust line-based input reading for large, complex input streams as in file processing; that's where other stream classes may be needed.

### DataInputStream Class

#### Overview
- Provides methods to read primitive data types from a stream (keyboard or file) as raw byte streams.
- Located in `java.io` package. Import with `import java.io.*;`
- Often used for more fine-grained input control and is backward compatible with earlier Java versions.

#### Basic Usage
```java
DataInputStream in = new DataInputStream(System.in);
String tempString = in.readLine();
float value = Float.valueOf(tempString);
```
- Always reads input as a string, requiring manual conversion to needed data type.
- Primarily, used for handling file and stream input; less commonly used for keyboard input after the introduction of the Scanner class.

#### Example Application
- Reading multiple types of input (float, int, etc.) for a financial calculation (e.g., calculating interest):
    1. Prompt user for 'principal' (System.out.print), read value using in.readLine(), convert string to float.
    2. Repeat for 'rate of interest' and 'number of years'.
    3. Perform calculation and display the result.

#### Error Handling and try-catch
- In Java, methods that can throw exceptions (such as readLine()) require exception handling.
- Use try-catch blocks around DataInputStream input code to prevent runtime failures.
- Alternatively, declare 'throws Exception' in the method signature if not using a try-catch block.
- Omitting proper exception handling will result in compilation errors.

| Exception Approach         | Description                                    |
|---------------------------|------------------------------------------------|
| try-catch                 | Handles error inside method body               |
| throws Exception (method) | Signals error may propagate higher              |

#### Comparative Points
- Both Scanner and DataInputStream read input from the keyboard, but Scanner is considered more modern and user-friendly for most cases.
- DataInputStream can be used to read from files and network streams beyond basic keyboard interaction.

---

## Conclusion

### Key Insights
- Java provides a variety of output methods: print(), println(), and printf(); each serves distinct purposes for displaying data.
- Formatted output in Java is powerful with printf(), allowing tailored control over display, adopting conventions from C/C++.
- Inputs can enter a Java program through command-line arguments (start-time, string-based), Scanner class (runtime, datatype-flexible), or DataInputStream (raw streams, manual parsing required).
- Command-line arguments facilitate parameterized execution but always treat input as strings, requiring parsing and careful handling to avoid runtime errors (e.g., parsing a non-numeric string as an integer).
- Scanner class supports interactive and type-safe input collection, enhancing the user experience in CLI applications.
- DataInputStream allows low-level, buffered input, best used with robust error handling (try-catch) or by propagating exceptions with throws in the method.
- Exception handling is mandatory with DataInputStream; omitting try-catch or throws annotation triggers compilation errors.
- Print methods are easily controlled by the programmer to adapt output formatting to program needs. Use printf for formatting, but simple programs may benefit from the simplicity and reliability of println.

### Key Terms
- **System.out.print()**: Method for displaying text without appending a newline character at the end.
- **System.out.println()**: Prints text followed by a newline, moving the output cursor to the next line.
- **System.out.printf()**: Provides formatted output with C-style format specifiers for precision and padding.
- **Command-line arguments**: User-supplied input parameters accessed via the args array in the main method; always in string form.
- **Scanner class**: Utility in java.util for reading input from the keyboard or other sources, capable of parsing diverse data types.
- **DataInputStream**: Class from java.io for reading primitive data types from an input stream. Often requires converting input strings and handling exceptions.
- **try-catch block**: Java mechanism for handling exceptions and preventing runtime errors, especially when reading input prone to failures.
- **parseInt/String.valueOf/Float.valueOf**: Methods for converting string inputs to numerical types such as integer or float.
- **Standard output**: The display monitor or console where output statements in Java appear.
- **Standard input**: The default input device, typically the keyboard, from which user inputs are read.
