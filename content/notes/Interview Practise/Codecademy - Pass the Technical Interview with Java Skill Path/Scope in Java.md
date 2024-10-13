# Concepts

#java #codecademy

---

### Intro to Scope

In Java, _scope_ defines where a certain variable or method is accessible in a program. Variables can be defined as having one of three types of scope:

1. **Class level scope** (instance variables): any variable declared within a class is accessible by all methods in that class. Depending on its _access modifier_ (ie. `public` or `private`), it can sometimes be accessed outside the class.

```java
public class Car {
    public String color;
    private int speed;

    public Car(String color, int speed) {
        // Variables color and speed accessible here
    }

    public void drive(boolean fourWheel) {
        // Variables color and speed accessible here
    }
}

public class BuyCar {
    public static void main(String[] args) {
        Car carObject = new Car("blue", 70);
        // Can access the public variable, color, in this class
        String carColor = carObject.color;
        // Can’t access the private variable, speed, in this class
        // int carSpeed = carObject.speed -- This results in an error, can’t access speed here
    }
}
```

1. **Method level scope** (local variables): any variable declared within a method, arguments included, is NOT accessible outside that method.

```java
public class Car {
    public String color;
    private int speed;

    public void drive(boolean fourWheel) {
        String tires = "wide";
        // fourWheel and tires are only accessible here
        // fourWheel and tires are destroyed after drive() finishes
    }

    public void paint(String newColor, String oldColor) {
        // newColor and oldColor are only accessible here
        // newColor and oldColor are destroyed after paint() finishes
    }
}

public class PaintCar {
    // The only variable from Car accessible in this class is color
    // None of the variables declared in Car methods are accessible in this class
}
```

1. **Block scope** (loop variables): any variable declared in a `for` loop condition is not accessible after the loop, unless you defined it beforehand.

```java
public class Car {
    public void changeTires() {
        int numTires = 4;
        int changedTires = 0;
        for (int i = 0; i < numTires; i++) {
            changedTires += 1;
        }
        // numTires and changedTires are accessible here, i is not
    }
}
```

### Access Modifiers

In Java, there are four _access modifiers_ that restrict the accessibility of the method or variable to which the modifier is applied. They are only used within classes, not within methods. `public` and `private` are the most relevant modifiers to our work, but we will briefly discuss all of them.

- `private`: The **most** restrictive modifier. It limits access to methods and variables to the class in which they are declared. `private` is chosen when there is no need to use certain methods or variables outside the class.
- `default`: Allows access only from within the current package. If there is no specified access modifier, the method or variable will take on this one. Learn more about the [default modifier](https://javarevisited.blogspot.com/2012/10/difference-between-private-protected-public-package-access-java.html).
- `protected`: Allows access to a method or variable only from within the current package, unless it is accessed through a child class outside of the package. Learn more about the [protected modifier](https://javarevisited.blogspot.com/2012/10/difference-between-private-protected-public-package-access-java.html).
- `public`: The **least** restrictive modifier. It allows access to a class, method or variable not only from within the class in which it is declared, but outside as well. This is the modifier we will most commonly use, but to understand the scenarios in which to use the others, check out the [Oracle documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html).

Min-heaps are a data structure that keeps track of the minimum element in a dataset. We haven’t covered them in Java quite yet, but we can look at the `MinHeap` class to help us understand `private` vs. `public`.

The `.bubbleUp()` method is `private` because “bubbling up”, or adjusting a heap after adding an element, is an internal process, not something that needs to be performed outside the `MinHeap` class. `.add()` on the other hand is a basic min-heap function so should be made `public`.

```java
import java.util.ArrayList;

public class MinHeap {
    public ArrayList<Integer> heap;
    public int size;

    public MinHeap() {
        // body of constructor
    }

    public void add(int value) {
        heap.add(value);
        size++;
        bubbleUp();
    }

    private void bubbleUp() {
        // body of bubbleUp() method
    }
}

public class TrackAges {
    public static void main(String[] args) {
        MinHeap ages = new MinHeap();
        // Can call public MinHeap add() method here
        ages.add(42);
        ages.add(15);
        ages.add(27);
        // Can’t call private MinHeap bubbleUp() method here
        // Don’t need to because add() calls bubbleUp()!
    }
}
```

### Static

`static` is a keyword that can be added after the access modifier of a method or variable. It indicates that the declared entity is the same across all instances of that class and that it can be accessed even before an object of that class is created. `static` methods and variables are initialized only once upon execution and are shared by all instances of the class. You may have noticed that the `.main()` method of a class is always declared as `static`; this is because this method is the starting point of the program. The compiler needs to be able to call the `.main()` method before the creation of an instance of that class, so it’s declared `static`. An example using a `static` variable can be found in the **Instance Variables** section of this article.

### Method Overriding and Method Overloading

**Method overriding** is a topic that comes up a few times in this path. It is a feature in Java that allows a subclass to have a method with the same name and parameters as one declared in its parent class. This is handy because it allows a subclass to implement a specific behavior for that method. The version of the method used is determined by the object that is used to call it. For more detailed information regarding classes and subclasses, check out our lesson on [Inheritance and Polymorphism](https://www.codecademy.com/courses/learn-java/lessons/java-inheritance-and-polymorphism/exercises/introducing-inheritance) in Java. An implementation of method overriding can be found in exercise six of this lesson.

**Method overloading** is similar to overriding in that it involves methods with the same name. However with overloading, a single Java class can have multiple methods with the same name if they have **different** parameter lists. Overloaded methods are distinguished by their number and type of parameters.

**Constructor overloading** is a type of method overloading in which there are multiple constructors in a class. This gives the option to instantiate an object with different sets of arguments. You will see this in action in our [Learn Queues: Java](https://www.codecademy.com/paths/pass-the-technical-interview-with-java/tracks/linear-data-structures-java/modules/queues-java/lessons/queues-java/exercises/welcome-to-queues-in-java) data structure lesson in this path. In the second exercise of this lesson, you will implement two versions of a queue: one with a maximum size as a constructor parameter and one without. A keyword `this()` is used in constructor overloading; the next section of this article will provide a comprehensive description of its application with overloading.

### Instance Variables

As discussed in our [Learn Java](https://www.codecademy.com/learn/learn-java) course, _instance variables_, also called _instance fields_, are data associated with a class object. They make up the state that each instance will possess. If we want each instance of a `Car` class object to have a color and speed associated with it, we can define instance variables `color` of type `String` and `speed` of type `int` within the class. These variables are available for assignment within the class constructor. Here we’ll define them as `public`.

```java
public class Car {
    public String color;
    public int speed;

    public Car(String carColor, int carSpeed) {
        // Instantiate instance variables in constructor
        color = carColor;
        speed = carSpeed;
    }

    public static void main(String[] args) {
        Car carObject = new Car("red", 50);
    }
}
```

`this` is used within any class method or constructor to reference the **current** object. You can reference any instance variable of a class, from within the class, using `this`. It cannot be used in a `static` context. Using `this` easily clarifies which variables are being referenced. Typically, this is how a constructor is created:

```java
public class Car {
    public String color;
    public int speed;

    public Car(String color, int speed) {
        // Use keyword 'this' to distinguish between parameter and instance variables
        this.color = color;
        this.speed = speed;
    }
}
```

We assign the constructor arguments `color` and `speed` to the class instance variables `color` and `speed` which are referenced using `this.color` and `this.speed`. Distinguishing local variables (arguments or variables declared in a method) from instance variables is very important.

Here are two other frequent uses of `this`:

1. Call a current class method with `this.`

```java
public class Car {
    public String color;
    public int speed;

    public Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
        // Use keyword 'this' to call the class method 'race()'
        this.race(speed);
    }

    public void race(int speed) {
        System.out.println("Raced at " + speed + " mph");
    }
}
```

1. Call a current class constructor using `this()` (constructor overloading)

```java
public class Car {
    public String color;
    public int speed;
    public static String defaultColor = "black";
    public static int defaultSpeed = 30;

    public Car() {
        this(defaultColor, defaultSpeed);
    }

    public Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }
}
```

`this()` must be the first line in the constructor since it is creating the class instance. The variables `defaultColor` and `defaultSpeed` are declared `static` because we want them to have the same values across all instances of the `Car` class. This allows us to reference them in our call to the second constructor using `this()`. These `static` variables belong to the `Car` class, not its instances.

You will see `this()` used with a `static` variable in our [Learn Queues: Java](https://www.codecademy.com/paths/pass-the-technical-interview-with-java/tracks/linear-data-structures-java/modules/queues-java/lessons/queues-java/exercises/welcome-to-queues-in-java) lesson. You can also send `this` in as an argument to a class method or return `this`, the current class instance, in a method. These are [less common uses](https://www.javatpoint.com/this-keyword) of `this`. When you start using `this`, you may run into a message that says “`this` cannot be referenced from a static context”. This likely means you tried to use `this` in your `.main()` method or another `static` method. As with variables, a `static` method belongs to the class, not its instances. Therefore it can only access `static` variables and call `static` methods. However, if an instance is created within a `static` method, that instance’s non-static variables and methods can be called using `theInstanceName.variable` or `theInstanceName.method()`.

```java
public class Car {
    public String color;
    public int speed;
    public static String defaultColor = "black";
    public static int defaultSpeed = 30;

    public Car() {
        this(defaultColor, defaultSpeed);
    }

    public Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }
    
    public static void main(String[] args) {
        Car carObject = new Car();
        String staticColor = defaultColor; // static variable directly accessible from static context
        String instanceColor = carObject.color; // non-static variable accessible using instance, carObject
    }
}
```

`this` is a very handy tool used in Java to simplify and disambiguate code. Although this is the case, there are [different preferences](https://softwareengineering.stackexchange.com/questions/113430/what-is-the-accepted-style-for-using-the-this-keyword-in-java) for the contexts in which to use it.