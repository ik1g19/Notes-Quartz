#java

---


| **Feature**                       | **Interface**                                                                            | **Abstract Class**                                                                    |
| --------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Definition**                    | A blueprint that can be implemented by classes to achieve multiple inheritance.          | A class that cannot be instantiated and may contain abstract or non-abstract methods. |
| **Multiple Inheritance**          | Supports multiple inheritance (a class can implement multiple interfaces).               | Does not support multiple inheritance (a class can extend only one abstract class).   |
| **Default Method Implementation** | Methods are abstract by default, but Java 8 introduced `default` and `static` methods.   | Can have both abstract methods (no body) and concrete methods (with body).            |
| **Constructor**                   | Cannot have constructors.                                                                | Can have constructors.                                                                |
| **Access Modifiers for Methods**  | All methods are `public` or implicitly `public`.                                         | Methods can have any access modifier (`public`, `protected`, `private`).              |
| **Fields/Variables**              | Can only have `public`, `static`, and `final` variables (constants).                     | Can have instance variables (both `static` and non-`static`).                         |
| **Inheritance Type**              | Used to define a contract that other classes must follow.                                | Used for code reuse and defining a base class for subclasses.                         |
| **Extending/Implementing**        | A class can implement multiple interfaces.                                               | A class can extend only one abstract class.                                           |
| **When to Use**                   | Use when you need to define a contract that different classes can implement differently. | Use when you want to provide a common base class with shared functionality.           |
