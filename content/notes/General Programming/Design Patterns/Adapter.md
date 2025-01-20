#design-patterns 

An adapter pattern converts the interface of a class to another interface so it can work with other classes

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=56&selection=6,0,8,23&color=yellow|Software Modelling and Design Notes, p.56]]%%

Mostly used to allow two incompatible classes to work together

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=56&selection=12,21,12,83&color=yellow|Software Modelling and Design Notes, p.56]]%%

The adapters can also be used as a “wrapper”, which is a class where you put the original object in and the wrapper allows it to act like another interface

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=56&selection=42,0,44,74&color=yellow|Software Modelling and Design Notes, p.56]]%%

# UML

![[Images/Software Modelling and Design Notes.png]] ^adapter-example

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=56&rect=163,81,431,215&color=yellow|Software Modelling and Design Notes, p.56]]%%

# Components

- Target Interface - Interface expected by the client, represents the set of operations that the client code can use
- Adaptee - Existing class or system with an incompatible interface ^adaptee
- Adapter - Class that implements the target interface and internally uses an instance of the adaptee to make it compatible with the target interface
- Client - Code that uses the target interface to interact with objects

# Implementation Types

## Class Adapter (*Inheritance*)

Adapter class inherits from both the target interface and the adaptee

Useful in multiple inheritance languages like C++, less so Java and C#

## Object Adapter (*Composition*)

Adapter holds an instance of the adaptee and implements the target interface

Allows a single adapter to work with multiple adaptees and does not require the complexities of inheritance

## Two-way Adapter

Adapter can function as both a target and an adaptee, depending on which interface is being invoked

## Interface Adapter

Used when only a few methods from an interface are necessary

# Example

![[Images/Class-Diagram-of-Adapter-Design-Pattern_.webp]]

- Step 1: The client initiates a request by calling a method on the adapter via the target interface.
- Step 2: The adapter maps or transforms the client’s request into a format that the adaptee can understand using the adaptee’s interface.
- Step 3: The adaptee does the actual job based on the translated request from the adapter.
- Step 4: The client receives the results of the call, remaining unaware of the adapter’s presence or the specific details of the adaptee.

```c++
// Adapter Design Pattern Example Code

#include <iostream>

// Target Interface
class Printer {
	public:
	    virtual void print() = 0;
};

// Adaptee
class LegacyPrinter {
	public:
	    void printDocument() {
		    //Step 3
	        std::cout << "Legacy Printer is printing a document." 
	        << std::endl;
	    }
};

// Adapter
class PrinterAdapter : public Printer {
	private:
	    LegacyPrinter legacyPrinter;
	
	public:
	    void print() override {
		    //Step 2
	        legacyPrinter.printDocument();
	    }
};

// Client Code
void clientCode(Printer& printer) {
	//Step 1
    printer.print();
    //Step 4
}

int main() {
    // Using the Adapter
    PrinterAdapter adapter;
    clientCode(adapter);

    return 0;
}
```