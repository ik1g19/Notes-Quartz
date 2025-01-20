#design-patterns 

Allows the construction of a product in a step-by-step manner, where the construction process can change based on the type of product being built 🔗[GfG](https://www.geeksforgeeks.org/builder-design-pattern/)

# Components

- Product - Object the builder pattern is responsible for creating
- Builder - Interface or abstract class that declares the construction steps for building a complex object
- Concrete Builder - Implement the builder interface
- Director - Manages the construction process of the complex object
- Client - Code that initiates the construction of the complex object

# Example Implementation

![[Images/UML-Class-Diagram-for-Builder-Design-Pattern.webp]] ^builder-imp

```c++
#include <iostream>
#include <string>

using namespace std;

// Product
class Computer {
public:
    void setCPU(const std::string& cpu) {
        cpu_ = cpu;
    }

    void setRAM(const std::string& ram) {
        ram_ = ram;
    }

    void setStorage(const std::string& storage) {
        storage_ = storage;
    }

    void displayInfo() const {
        std::cout << "Computer Configuration:"
                  << "\nCPU: " << cpu_
                  << "\nRAM: " << ram_
                  << "\nStorage: " << storage_ << "\n\n";
    }

private:
    string cpu_;
    string ram_;
    string storage_;
};

// Builder interface
class Builder {
public:
    virtual void buildCPU() = 0;
    virtual void buildRAM() = 0;
    virtual void buildStorage() = 0;
    virtual Computer getResult() = 0;
};

// ConcreteBuilder
class GamingComputerBuilder : public Builder {
private:
    Computer computer_;

public:
    void buildCPU() override {
        computer_.setCPU("Gaming CPU");
    }

    void buildRAM() override {
        computer_.setRAM("16GB DDR4");
    }

    void buildStorage() override {
        computer_.setStorage("1TB SSD");
    }

    Computer getResult() override {
        return computer_;
    }
};

// Director
class ComputerDirector {
public:
    void construct(Builder& builder) {
        builder.buildCPU();
        builder.buildRAM();
        builder.buildStorage();
    }
};

// Client
int main() {
    GamingComputerBuilder gamingBuilder;
    ComputerDirector director;

    director.construct(gamingBuilder);
    Computer gamingComputer = gamingBuilder.getResult();

    gamingComputer.displayInfo();

    return 0;
}
```

# Usage

The Builder Pattern is used when you need to create complex objects with a large number of optional components or configurations