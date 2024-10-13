#cpp #syntax

Structures are a way to group several related variables into one place. Each variable in the structure is known as a **member** of the structure

Unlike an array, a structure can contain many different data types

# Create a Structure

To create a structure, use the `struct` keyword and declare each of its members inside curly braces.

After the declaration, specify the name of the structure variable (**myStructure** in the example below):

```c++
struct {             // Structure declaration  
  int myNum;         // Member (int variable)  
  string myString;   // Member (string variable)  
} myStructure;       // Structure variable
```

# Access Structure Members

To access members of a structure, use the dot syntax (`.`):

```c++
// Create a structure variable called myStructure  
struct {  
  int myNum;  
  string myString;  
} myStructure;  
  
// Assign values to members of myStructure  
myStructure.myNum = 1;  
myStructure.myString = "Hello World!";  
  
// Print members of myStructure  
cout << myStructure.myNum << "\n";  
cout << myStructure.myString << "\n";
```

# One Structure in Multiple Variables

You can use a comma (`,`) to instantiate a struct multiple times:

```c++
struct {  
  int myNum;  
  string myString;  
} myStruct1, myStruct2, myStruct3;
// Multiple structure variables separated with commas
```

```c++
struct {  
  string brand;  
  string model;  
  int year;  
} myCar1, myCar2; // We can add variables by separating them with a comma here  
  
// Put data into the first structure  
myCar1.brand = "BMW";  
myCar1.model = "X5";  
myCar1.year = 1999;  
  
// Put data into the second structure  
myCar2.brand = "Ford";  
myCar2.model = "Mustang";  
myCar2.year = 1969;  
  
// Print the structure members  
cout << myCar1.brand << " " << myCar1.model << " " << myCar1.year << "\n";  
cout << myCar2.brand << " " << myCar2.model << " " << myCar2.year << "\n";
```