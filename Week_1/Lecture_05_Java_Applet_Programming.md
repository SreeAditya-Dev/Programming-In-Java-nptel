# Study notes for Programming In Java : Week 1 : : Lecture 05 : Java Applet Programming

## Introduction

Java offers two main programming paradigms: applications and applets. While Java applications are similar to stand-alone programs run from the command line, applets are specially designed to embed graphical content within web pages, enabling interactive graphical user interface (GUI) experiences inside browsers or using applet viewers. This guide provides a detailed exploration of Java applet programming, covering what applets are, their structure, the process of creating, compiling, and executing applet code, the critical methods used in applets, means for handling user input, and careful comparison between applets and traditional applications. Practical examples, such as displaying a message or drawing shapes based on external input, will clarify essential steps and differences.

---

## Understanding Java Applet Programming

### Java Applications vs Java Applets
- **Java Applications**:
  - Stand-alone programs (like those written in C, C++, or Python)
  - Run using the `java` command (JVM interpreter)
  - Can read input directly from keyboard, files, etc.
  - Uses a `main` method as the execution entry point
  - Allows user-defined methods and class structures

- **Java Applets**:
  - Small Java programs embedded in web pages or run by applet viewers
  - Specifically designed for GUIs and interactive content
  - No `main` method; execution is managed by browser or applet viewer
  - Heavily rely on a set of predefined methods (`init`, `start`, `stop`, `destroy`, `paint`)
  - Requires embedding within an HTML file
  - Input is passed through HTML, not directly via standard means
- **Naming convention:**
  - Applications and applets both use class names as file names, but HTML file names embedding applets can differ from the class name

### What is an Applet?
- An applet is a small Java program primarily for GUI interaction
- Renders graphical content inside a rectangular area within a window (the "applet window")
- Typical visual elements include:
  - Title bar
  - Display area (for images, text, components such as buttons, text fields, etc.)
- Example applets: calculator GUIs, interactive demos, drawing areas

### Java Packages and Import Statements
- Java applets depend on two critical packages:
  - `java.applet` (for applet-specific classes)
  - `java.awt` (for Abstract Window Toolkit; provides GUI classes like Graphics, Button, and Layouts)
- Using imports:
  - Specific class import:
    - `import java.applet.Applet;`
    - `import java.awt.Graphics;`
  - Wildcard (import all classes):
    - `import java.applet.*;`
    - `import java.awt.*;`
- These must be included at the beginning of the source file

### General Structure of a Java Applet

#### Standard Applet Skeleton
- Import required packages (`java.applet`, `java.awt`)
- Define applet class, extending `Applet`:
  - `public class ClassName extends Applet { ... }`
- Implement essential methods (paint, init, etc.)
- All data fields and methods are defined inside the class
- Example:
  ```java
  import java.applet.Applet;
  import java.awt.Graphics;

  public class HelloWorldApplet extends Applet {
      public void paint(Graphics g) {
          g.drawString("Hello, World", 150, 150);
      }
  }
  ```
- No `main` method, unlike applications
- Braces (`{ ... }`) encompass all variable, method, and data definitions

### Anatomy of the Applet Window
- Title/Page bar: Provided by browser or applet viewer
- Display area: Customizable with text, buttons, images, or other GUI elements
- Can house multiple components (e.g., calculator buttons, display text fields)

### Compiling and Running an Applet
#### Source and Destination Files
- Source code saved as `ClassName.java` (e.g., `HelloWorldApplet.java`)
- Compilation using `javac` results in a `.class` file (e.g., `HelloWorldApplet.class`)

#### Embedding in HTML
- An applet cannot run stand-alone; it must be embedded in an HTML page using special tags
- Typical HTML for embedding:
  ```html
  <html>
    <body>
      <applet code="HelloWorldApplet.class" width="300" height="300"></applet>
    </body>
  </html>
  ```
- The HTML file can be named arbitrarily (must have `.html` extension)
- Parameters `width` and `height` define the on-screen size of the applet display window

#### Running via Applet Viewer
- Compile using: `javac HelloWorldApplet.java`
- Generates: `HelloWorldApplet.class`
- To execute:
  - `appletviewer HTMLFileName.html` (e.g., `appletviewer HelloApplet.html`)
- Output will be visible in a window of the specified size

| Step           | File Type        | Command/Tool       | Description                                 |
|----------------|-----------------|--------------------|---------------------------------------------|
| Write code     | .java           | Editor (Notepad)   | Edit source code, ensure correct class name  |
| Compile code   | .class          | javac              | Compile source into bytecode                 |
| Embed in HTML  | .html           | Editor             | Create HTML file with applet tag             |
| Run applet     | .html/.class    | appletviewer       | Launch applet using viewer and HTML file     |

#### Example: Displaying "Hello World" in an Applet
- Import necessary packages
- Define the applet class, extending Applet
- Implement the paint method using `g.drawString()` to render text
- The coordinates `[x, y]` (e.g., `[150, 150]`) define where the string appears within the applet window

### Structure Recap
- **Three required steps:**
  1. Write applet code in Java (`.java` file), compile to `.class`
  2. Create and edit HTML file embedding the class
  3. Run via `appletviewer` (or browser with Java support)
- Applet class file can be embedded in any HTML file with any name, provided it uses the correct syntax

## Core Methods in Java Applet Programming

### Overview of Applet Life Cycle Methods
Applets rely on a specific set of lifecycle-related methods, which are invoked by the applet viewer or browser rather than the programmer directly.

| Method   | Purpose                                        | Invoked When                                                 |
|----------|------------------------------------------------|--------------------------------------------------------------|
| init     | Initialization code (single execution)         | Applet is loaded/instantiated                                |
| start    | Preparation for running; called multiple times | Applet becomes active/running (page shown/restored)          |
| stop     | Clean-up actions; can run multiple times       | Applet is stopped (page hidden or user leaves the page)      |
| destroy  | Final clean-up before resource release         | Applet is destroyed (browser closes/explicit killing)        |
| paint    | Rendering visual graphics (including text)     | Whenever repaint/refresh/redraw required (e.g., resize)      |

- **Note:** Only these methods are allowed; users cannot create additional lifecycle methods with arbitrary names
- The actual method bodies (code inside) can be customized

### Method Details

#### The `init()` Method
- Runs when the applet is first loaded
- Used for initialization (variable setup, size adjustments, reading HTML parameters, etc.)
- Place for setting up the appletâ€™s initial environment
- Example usages:
  - Adjusting applet window size using `resize(width, height)`
  - Getting input values from HTML parameters

#### The `paint(Graphics g)` Method
- Fundamental for rendering the applet's display
- Receives a `Graphics` object `g` for drawing operations
- Typical uses:
  - Drawing strings: `g.drawString("text", x, y)`
  - Rendering shapes: `g.drawRect(x, y, w, h)`
  - Painting images or custom graphics
- Invoked whenever the display needs repainting (e.g., resize, exposure, changes)
- Example:
  ```java
  public void paint(Graphics g) {
      g.drawString("This is my rectangle", 60, 100);
      g.drawRect(20, 40, 150, 100);
  }
  ```

#### The `start()` and `stop()` Methods
- `start()` runs when applet becomes active again (e.g., after being stopped; tab switch, window activation)
- `stop()` is called when the applet is suspended (e.g., page hidden, window minimized)
- Used for tasks such as starting/stopping background animation or threads

#### The `destroy()` Method
- Called once before applet instance is destroyed
- Place for releasing non-memory resources, closing files, terminating connections
- Rarely used in simple examples

### Passing Input to Applets: HTML Parameters
- Applets can read user input or configuration from the HTML code that embeds them
- Values are passed as `<param>` tags inside the HTMLâ€™s `<applet>` tag
- Applet code uses the `getParameter(String name)` method inside `init()` to retrieve these values

| HTML param example          | Java retrieval                       |
|----------------------------|--------------------------------------|
| `<param name="xval" value="20">` | `String s = getParameter("xval");`        |
|                            | `int x = Integer.parseInt(s);`       |

- This technique allows dynamic alteration of applet behavior without changing Java source code

#### Example: Drawing a Rectangle Based on Input
- In the applet:
  - Use `getParameter("xval")`, etc. to retrieve numeric inputs from HTML
  - Parse and use these values in graphical rendering (e.g., `g.drawRect(x, y, w, h);`)
- In HTML:
  ```html
  <param name="xval" value="30">
  <param name="yval" value="50">
  <param name="wval" value="100">
  <param name="hval" value="60">
  ```
- Changing these values in HTML alters the applet display without touching the Java code

### Resizing the Applet Window
- Java applet window size usually set within the HTML (`width`, `height` attributes)
- Programmers can override dimensions inside `init()` using `resize(newWidth, newHeight)`
- Use-case: If you want the appletâ€™s display area to be different from the HTML-defined area

#### Example:
- In HTML: `<applet code="MyApplet.class" width="300" height="300"></applet>`
- In Java `init()`: `resize(200, 200);` â€” this updates the appletâ€™s display area to 200x200 pixels at runtime, regardless of the HTML values

### Full Structure Summary
- **Essential Steps for Developing a Java Applet:**
  1. Import necessary packages
  2. Define a public class that extends `Applet`
  3. Optionally declare variables
  4. Implement allowed methods (`init`, `start`, `stop`, `destroy`, `paint`)
  5. Compile code, embed in HTML, run with viewer
- **Lifecycle management:** The environment (browser/app applet viewer) handles start/stop/init/destroy; programmer fills in their code for each step as needed

## Comparison: Java Applications vs Applets

| Aspect         | Java Application                | Java Applet                                   |
|----------------|--------------------------------|-----------------------------------------------|
| Main Method    | Required (`public static void main`) | Not used; special methods (`init`, etc.)     |
| Entry Point    | User defines                    | Applet viewer/browser manages                 |
| Execution Tool | Command line (`java`), IDE      | Applet viewer/browser + HTML                  |
| I/O            | Direct: keyboard, file, network | Indirect: via HTML `<param>` or user GUI input|
| User Methods   | Any name/number                 | Only predefined allowed (fixed lifecycle)     |
| Embedding      | Stand-alone/external execution  | Must be in HTML file as `<applet>`            |
| Communication  | Can exchange data across network and other apps | Cannot communicate outside sandbox         |
| System Access  | Full (potentially restricted by security) | Highly restricted for security reasons    |
| Interfacing    | Can call/run programs in other languages | Cannot interface with programs in other languages |
| Example Code   | Uses main(), arbitrary structure| Uses `init()`, `paint()`, class extends Applet|

#### Key Design Differences
- Applets are sandboxed for web security
- Applets do not have arbitrary entry points; only the environment triggers code execution
- Stand-alone applications are unrestricted in design; applets have fixed lifecycle and methods

### Example: Structure Differences

| Java Application                       | Java Applet                                    |
|----------------------------------------|------------------------------------------------|
| public class HelloApp {                | public class HelloApplet extends Applet {      |
|     public static void main(...){ ... } |     public void paint(Graphics g) { ... }      |
|                                        |                                                |
| }                                      | }                                              |

- Applications: user manages control/flow, can use arbitrary data input/output
- Applets: program structure and interactions are controlled by HTML and the viewer

---

## Conclusion

### Key Insights
- Applets are a special Java program type embedded in web pages or run by applet viewers, mainly for GUI or interactive visual content
- Applet development involves unique steps: code writing, compiling, HTML embedding, and running with a dedicated viewer
- Applet structure is highly regulated, requiring inheritance from Applet class and restricting to predefined lifecycle methods (`init`, `start`, `stop`, `destroy`, `paint`)
- Inputs to applets are provided via HTML; applets lack direct keyboard or file I/O
- Applet display areas can be dynamically manipulated both through static HTML attributes and runtime Java code
- Clear distinctions exist between Java applets and applications, with deep implications regarding entry points, permissions, communication, and program design

### Key terms
- **Applet**: A small Java program designed to be embedded in a web page or run by an applet viewer, usually to provide GUI features
- **Application**: A stand-alone Java program with a `main` method, capable of system-level operations and direct I/O
- **Applet Viewer**: A Java tool (command-line or browser) for running applet programs via HTML files
- **init()**: Applet method for initialization; executed once when the applet is loaded
- **paint(Graphics g)**: Applet method responsible for drawing and rendering visual content
- **start()/stop()**: Methods controlling the appletâ€™s active/suspended state, called by browsers/viewers
- **destroy()**: Method executed to clean up resources before applet is destroyed
- **resize(w, h)**: Method for programmatically setting the appletâ€™s display area
- **getParameter(String)**: Method for retrieving input from HTML parameter tags
- **HTML param tag**: `<param name="name" value="value">` â€” used to pass values from HTML to an applet
- **AWT (Abstract Window Toolkit)**: Java package (`java.awt`) providing UI components and drawing primitives

---
