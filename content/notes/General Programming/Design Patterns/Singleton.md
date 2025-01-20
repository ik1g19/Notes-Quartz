#design-patterns 

Ensures a class has only one instance and provides a global access point to it 🔗[GfG](https://www.geeksforgeeks.org/singleton-design-pattern/)

![[Images/SINGLEton.png]]

- Single Instance: Singleton ensures that only *one instance* of the class exists throughout the application
- Global Access: Provide a *global point of access* to that instance
- Lazy or Eager Initialization: Support creating the instance either *when needed* (lazy) or *when* the class is *loaded* (eager)
- Thread Safety: Implement mechanisms to *prevent* multiple *threads* from *creating separate instances simultaneously*
- Private Constructor: Restrict direct instantiation by making the constructor private, forcing the use of the access point

# Private Constructor

The Singleton pattern incorporates a private constructor, which serves as a barricade against external attempts to create instances of the Singleton class

```java
// Private constructor to
// prevent external instantiation
class Singleton {

    // Making the constructor as Private
    private Singleton()
    {
        // Initialization code here
    }
}
```

# Static Factory Method

This method acts as a gateway, providing a global point of access to the Singleton object

When someone requests an instance, this method either creates a new instance (if none exists) or returns the existing instance to the caller

```java
// Static factory method for global access
public static Singleton getInstance()
{
    // Check if an instance exists
    if (instance == null) {
        // If no instance exists, create one
        instance = new Singleton();
    }
    // Return the existing instance
    return instance;
}

```

# Implementation

![[Images/Screenshot-2023-12-07-174635.png]] ^singleton-imp

```java
/*package whatever //do not write package name here */
import java.io.*;
class Singleton {
    // static class
    private static Singleton instance;
    private Singleton()
    {
        System.out.println("Singleton is Instantiated.");
    }
    public static Singleton getInstance()
    {
        if (instance == null)
            instance = new Singleton();
        return instance;
    }
    public static void doSomething()
    {
        System.out.println("Somethong is Done.");
    }
}

class GFG {
    public static void main(String[] args)
    {
        Singleton.getInstance().doSomething();
    }
}
```