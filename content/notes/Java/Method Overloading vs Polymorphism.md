#java

---
# Method Overloading

Method Overloading is a feature that allows a class to have multiple methods with the same name but different parameter lists (number, types, or order of parameters). It is a form of **static polymorphism**, meaning that the method that will be called is determined at **compile time**.

Key Points:
- Occurs within the same class.
- Methods share the same name but differ in the type or number of parameters.
- The return type may or may not differ, but overloading does not depend on the return type.
- It allows code to be more readable and organized.

Example:
```java
class Calculator {
    // Method to add two integers
    int add(int a, int b) {
        return a + b;
    }

    // Overloaded method to add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }

    // Overloaded method to add two doubles
    double add(double a, double b) {
        return a + b;
    }
}
```

In the example, the `add()` method is overloaded with different parameters (different number and type).

---

# Polymorphism

Polymorphism is a more general OOP concept that allows objects of different classes to be treated as objects of a common superclass. It means "many forms" and comes in two types:

- **Compile-time (Static) Polymorphism**: This is essentially **method overloading** and operator overloading.
- **Run-time (Dynamic) Polymorphism**: This is achieved through **method overriding**, where a subclass provides a specific implementation of a method that is already defined in its superclass. The method to be called is determined at **runtime** based on the actual object (not the reference type).

Key Points:
- It allows for a unified interface for different underlying forms (objects).
- In **dynamic polymorphism**, the decision of which method to call happens at runtime.
- Polymorphism is achieved using **inheritance** and **interfaces**.

Example of Dynamic Polymorphism (Method Overriding):
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class TestPolymorphism {
    public static void main(String[] args) {
        Animal a1 = new Dog();  // Upcasting
        Animal a2 = new Cat();
        
        a1.sound();  // Outputs: Dog barks (decided at runtime)
        a2.sound();  // Outputs: Cat meows (decided at runtime)
    }
}
```

In this example, both `Dog` and `Cat` override the `sound()` method of the `Animal` class. The actual method to be called is determined by the type of object (`Dog` or `Cat`) at runtime, even though the reference type is `Animal`.

---

### Summary of Differences

| **Aspect**                | **Method Overloading**                   | **Polymorphism**                                |
|---------------------------|------------------------------------------|------------------------------------------------|
| **Definition**             | Multiple methods with the same name but different parameters in a class. | Ability to treat objects of different types through a common interface (typically through inheritance). |
| **Type**                   | Compile-time (static) polymorphism.      | Can be both compile-time (method overloading) and runtime (method overriding) polymorphism. |
| **When is it determined?** | At compile time.                         | In dynamic polymorphism, it is determined at runtime. |
| **Relation between methods** | Same method name with different parameters. | Methods are typically overridden (not overloaded) in dynamic polymorphism. |
| **Inheritance Required?**  | No.                                      | Yes, for dynamic polymorphism. |
| **Example**                | Overloading `add(int, int)` and `add(double, double)`. | Overriding the `sound()` method in a `Dog` and `Cat` class that inherit from `Animal`. |

In short, **method overloading** is a form of **polymorphism** (specifically static polymorphism), but **polymorphism** covers more than just overloading—it also includes method overriding, which is dynamic and allows for more flexible behaviour in object-oriented systems