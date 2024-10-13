#cpp #syntax

# Creating Pointers

A **pointer**  is a variable that **stores the memory address as its value**

A pointer variable points to a data type (like `int` or `string`) of the same type, and is created with the `*` operator. The address of the variable you're working with is assigned to the pointer

```c++
string food = "Pizza";  // A food variable of type string  
string* ptr = &food;
// A pointer variable, with the name ptr, that stores the address of food  
  
// Output the value of food (Pizza)  
cout << food << "\n";  
  
// Output the memory address of food (0x6dfed4)  
cout << &food << "\n";  
  
// Output the memory address of food with the pointer (0x6dfed4)  
cout << ptr << "\n";
```

# Dereference

You can also use the pointer to get the value of the variable, by using the `*` operator (the **dereference** operator):

```c++
string food = "Pizza";  // Variable declaration  
string* ptr = &food;    // Pointer declaration  
  
// Reference: Output the memory address of food with the pointer (0x6dfed4)  
cout << ptr << "\n";  
  
// Dereference: Output the value of food with the pointer (Pizza)  
cout << *ptr << "\n";
```

