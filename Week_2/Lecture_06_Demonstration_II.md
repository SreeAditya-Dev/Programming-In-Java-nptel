# Study notes for Programming In Java : Week 2 : : Lecture 06 : Demonstration-II

## Introduction

Java applet programming enables developers to create small, interactive applications that run within a web browser or applet viewer. This set of notes guides you through the essential steps of writing, compiling, and executing Java applets, demonstrates how applets are embedded into HTML files, explores the interaction between applets and HTML parameters, describes applet methods such as `init()` and `paint()`, and discusses best practices around file organization and runtime execution in Java applet development.

---

## Getting Started with Java Applets

### Overview of Java Applets
- Java applets are Java programs designed to be embedded within web pages or run in an applet viewer.
- Unlike standalone Java applications, applets are managed by the browser or viewer, and interact with the user through a graphical interface.

### Required Packages and Classes
To create a Java applet, two main packages must be imported:
- `java.applet.Applet`: Provides the base Applet class necessary for applet functionality.
- `java.awt.*`: Contains the Abstract Window Toolkit classes for GUI components and graphics.

From these packages, two commonly used classes are:
- `Applet`: The superclass for all applet classes.
- `Graphics`: Provides the context for drawing on the applet window.

### The Structure of a Basic Applet Program
- The applet program is defined as a Java class that extends `Applet`.
- At a minimum, it overrides the `paint(Graphics g)` method for drawing on the appletâ€™s surface.

#### Example Structure
```java
import java.applet.Applet;
import java.awt.Graphics;

public class ExampleApplet extends Applet {
    public void paint(Graphics g) {
        g.drawString("Hello, Applet!", 150, 150);
    }
}
```

### Compiling and Running an Applet
- Save the Java source file with the `.java` extension, using the same name as the public class.
- Compile with the Java compiler (`javac`). For example:
  - `javac ExampleApplet.java` â†’ produces `ExampleApplet.class`.
- Running requires embedding the class in an HTML file and viewing with an applet viewer.

### The HTML File for Embedding Applets
- The HTML file uses the `<applet>` tag to specify the class file and the size of the display area.

#### Example HTML
```html
<html>
  <body>
    <applet code="ExampleApplet.class" width="300" height="300"></applet>
  </body>
</html>
```
- Filename can be any valid name, e.g., `AppletExample.html`.
- The `width` and `height` attributes define the size in pixels.

### Running the Applet
- The applet can be run using the command:
  - `appletviewer AppletExample.html`
- This opens the applet window displaying the graphical output.

---

## Understanding Applet Program Behavior

### The Paint Method
- The `paint(Graphics g)` method handles all content rendering for the appletâ€™s window.
- Example usage: `g.drawString("Welcome", 150, 150);` draws text at coordinates (150, 150).
- Modifying text/location in `drawString` reflects instantly upon compiling and reloading.

### Modifying Applet Appearance via HTML
- Changing the `<applet>` tagâ€™s `width` and `height` in HTML resizes the applet's display area.
- No need to recompile the Java class when only the HTML is changed (e.g., resizing the applet window).
- Example changes:
  - Change `width="300"` and `height="300"` to `width="200"` and `height="200"` for a smaller area.
  - Increase `width` or `height` for larger display.
- Position given to `drawString` should align with display area size for visible output.

### Multiple String Outputs
- Drawing multiple strings is possible by calling `g.drawString` with different parameters.
- Example:
  ```java
  g.drawString("Kharagpur", 50, 20);
  g.drawString("Welcome NPTEL Java", 150, 150);
  ```
  - Each string appears at the specified coordinates.

### Customizing the Title Bar
- The `<title>` tag in HTML specifies the windowâ€™s title.
- Changing this tag affects the applet viewerâ€™s window title when not in appletviewer.
- Example:
  ```html
  <head><title>Hello World Applet</title></head>
  ```
- In appletviewer, some title features may not be fully supported, but in standard browsers, it changes the page/app view title.

---

## Applet Lifecycle and Methods

### Key Applet Methods
- **init()**: Called once when the applet is first loaded. Used for initialization.
- **start()**: Called after `init()`, and whenever the applet is restarted.
- **paint(Graphics g)**: Called to redraw the applet window.
- **stop()**: Called when the applet is stopped.
- **destroy()**: Called when the applet is terminated.

### Demonstrating the init() Method
- The `init()` method is ideal for setting up properties such as:
  - Window size (using `resize(w, h)`)
  - Background color (using `setBackground(Color color)`)
- Example usage:
  ```java
  public void init() {
    resize(300, 300);
    setBackground(Color.YELLOW);
  }
  ```
- `resize()` adjusts the programmatic size of the applet window, possibly overriding HTML-specified size.
- `setBackground(Color color)` changes the background color of the applet; color values (like `Color.YELLOW`) are defined in the `Color` class of the `java.awt` package.

#### Table: Common Color Constants in Java AWT
| Color Constant    | Visual Color      |
|------------------|------------------|
| Color.WHITE      | White            |
| Color.YELLOW     | Yellow           |
| Color.RED        | Red              |
| Color.GREEN      | Green            |
| Color.BLUE       | Blue             |
| Color.BLACK      | Black            |
| Color.GRAY       | Gray             |

### Combining init() Functionality
- The `init()` method may include both resizing and background color statements, affecting display as soon as the applet loads.

### Compilation and Execution
- If `init()` logic is changed, recompile the Java file before rerunning. If only HTML parameters change, no recompilation needed.

---

## Passing Input to Applets via HTML Parameters

### Applet Input Limitations
- Applets cannot receive input directly from:
  - Keyboard
  - Mouse (for general data; exceptions exist for GUI events)
  - Files or network sources (without explicit permission)
- To supply input, HTML `<param>` tags are used in the embedding HTML file.

### Using <param> Tags
- Syntax:
  ```html
  <applet ...>
    <param name="msg" value="HELLO WORLD">
    <param name="x_position" value="20">
    <param name="y_position" value="50">
  </applet>
  ```
- These tags pass values to the applet during initialization.

### Retrieving Parameter Values in Applet Code
#### Example Implementation
```java
public class DemoInputApplet extends Applet {
    int x, y;
    String msg;
    public void init() {
        x = Integer.parseInt(getParameter("x_position"));
        y = Integer.parseInt(getParameter("y_position"));
        msg = getParameter("msg");
    }
    public void paint(Graphics g) {
        g.drawString(msg, x, y);
    }
}
```
- `getParameter(String name)`: Reads a parameter value passed via HTML `<param>`.
- If parsing integers, use `Integer.parseInt()` as parameters are retrieved as strings.

#### Table: Parameter Retrieval
| Parameter Type | HTML Tag Example                     | Java Retrieval Example                     |
|---------------|---------------------------------------|--------------------------------------------|
| String        | <param name="msg" value="Hi">         | msg = getParameter("msg");                |
| Integer       | <param name="x" value="20">           | x = Integer.parseInt(getParameter("x"));   |

### Modifying Parameter Values
- Updating values in `<param>` tags (e.g., a new message or different position) alters applet output with no need for recompilation.
- Executing the HTML after changing parameters produces different results as per supplied values.

---

## Practical File Management for Applets

### Managing File Names
- Java file (`.java`): Must match the public class name, e.g., `DemoApplet.java` for `class DemoApplet`.
- Compiled file (`.class`): Automatically named after the compiled class.
- HTML file: Can have any name; it is not required to match the class name.
- While not required, keeping consistent and descriptive naming helps in project organization.

### HTML File Embedding Options
- Applet HTML code is usually placed in a separate `.html` file.
- Alternatively, some developers embed the HTML code as commented text at the end of the Java source file. Compilation ignores any lines within Java comments, and the HTML can be copied from there when needed.

#### Example: HTML Embedded as Comments
```java
/*
<html>
  <body>
    <applet code="DemoApplet.class" width="300" height="300">
    </applet>
  </body>
</html>
*/
```
- This practice helps keep both code and its HTML reference together.
- The applet viewer can execute by referencing the Java file if the HTML tag is present at the end within comments.

### Executing Applets Directly from .java Files with Embedded HTML
- The applet viewer can be invoked as:
  - `appletviewer DemoApplet.java`
- The viewer extracts the embedded HTML and executes the applet accordingly.
- This can serve as a shortcut during development, but best practice is generally to separate Java and HTML code for clarity and reusability.

### Differences Between Java and Applet Viewer Execution
- Java command: Runs standard Java applications by interpreting bytecode.
- Appletviewer: Specifically interprets HTML `<applet>` tags and executes the referenced applet class.
- When given a `.java` file with an embedded HTML applet tag, appletviewer locates the HTML segment and executes according to the tagâ€™s parameters.

---

## Key Takeaways and Best Practices

### General Applet Development Tips
- Always ensure the Java class name matches the `.java` filename.
- Parameters for the appletâ€™s visual layout (width, height, background color) can be controlled both by HTML and by the applet code (`resize()`, `setBackground()`).
- Custom input values are best supplied via HTML `<param>` and read in the appletâ€™s `init()` method.
- File naming between Java and HTML is flexible but should be managed prudently to avoid confusion.
- HTML files must be referenced by their exact filenames in appletviewer; partial or incorrect names result in errors.
- Embedded HTML in Java source is convenient but should be used judiciously for simple use-cases or documentation.

### Troubleshooting Common Applet Issues
| Symptom                               | Likely Cause                          | Solution                           |
|----------------------------------------|---------------------------------------|------------------------------------|
| Applet fails to display                | Incorrect file/class name             | Check class/HTML file names        |
| Nothing appears, or window is blank    | Mismatched coordinates/size           | Adjust drawString location/size    |
| Parameter values not picked up         | Incorrect HTML <param> or name        | Check parameter names in HTML/Java |
| Cannot run applet via appletviewer     | Wrong file extension or file missing  | Use correct .html/.java filename   |

---

## Conclusion

### Key Insights
- Java applets are simple to create but require proper setup of both Java class code and embedding HTML.
- The interplay between applet code and HTML enables developers to set display properties, pass input data, and control the applet lifecycle.
- The `init()` method is pivotal for initializing applet properties such as size and color, while the `paint()` method takes care of rendering elements.
- Input to applets is best handled through HTML `<param>` tags and the `getParameter()` method inside the applet code.
- Applet projects often benefit from clear naming conventions for source, class, and HTML files, although strict matching is not required.
- Embedding HTML directly in Java comments can be convenient for rapid testing, but standard practice favors using separate HTML and Java files for maintainability.

### Key Terms
- **Applet**: A small Java program that runs within a web page or applet viewer, extending the `Applet` class.
- **Appletviewer**: A utility for running and testing Java applets outside standard browsers.
- **paint(Graphics g)**: The method responsible for rendering graphics and text on the appletâ€™s canvas.
- **init()**: Method called once at applet startup for initial setup, including reading parameters and configuring UI.
- **resize()**: An applet method used to set or change the dimensions of the applet display window.
- **setBackground(Color c)**: Method to alter the background color of an appletâ€™s canvas.
- **getParameter(String name)**: Retrieves values supplied via HTML `<param>` tags, allowing external data to be used in the applet.
- **<applet> tag**: HTML element for embedding and configuring a Java applet inside a web page.
- **<param> tag**: HTML element nested inside `<applet>` for passing parameters to the applet code.
- **javac**: Java compiler, translates Java source files into bytecode (`.class` files).
- **Class file**: The compiled version of a Java program (with `.class` extension), executable by JVM or applet viewers.
- **AWT (Abstract Window Toolkit)**: Javaâ€™s original platform-independent windowing, graphics, and user-interface widget toolkit.
