#cpp #syntax 

To use strings, you must include an additional header file in the source code, the `<string>` library:

```c++
// Include the string library  
#include <string>  
  
// Create a string variable  
string greeting = "Hello";
```

# String Concatenation

The `+` operator can be used between strings to add them together to make a new string

```c++
string firstName = "John ";  
string lastName = "Doe";  
string fullName = firstName + lastName;  
cout << fullName;
```

# Append

A string in C++ is actually an object, which contain functions that can perform certain operations on strings. For example, you can also concatenate strings with the `append()` function:

```c++
string firstName = "John ";  
string lastName = "Doe";  
string fullName = firstName.append(lastName);  
cout << fullName;
```

# Length

To get the length of a string, use the `length()` function:

```c++
string txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";  
cout << "The length of the txt string is: " << txt.length();
```

# Access Strings

You can access the characters in a string by referring to its index number inside square brackets `[]`

```c++
string myString = "Hello";  
cout << myString[0];  
// Outputs H
```

## Change String Characters

To change the value of a specific character in a string, refer to the index number, and use single quotes:

```c++
string myString = "Hello";  
myString[0] = 'J';  
cout << myString;  
// Outputs Jello instead of Hello
```

# User Input Strings

`cin` considers a space (whitespace, tabs, etc) as a terminating character, which means that it can only store a single word (even if you type many words):

```c++
string fullName;  
cout << "Type your full name: ";  
cin >> fullName;  
cout << "Your name is: " << fullName;  
  
// Type your full name: John Doe  
// Your name is: John
```

That's why, when working with strings, we often use the `getline()` function to read a line of text. It takes `cin` as the first parameter, and the string variable as second:

```c++
string fullName;  
cout << "Type your full name: ";  
getline(cin, fullName);  
cout << "Your name is: " << fullName;  
  
// Type your full name: John Doe  
// Your name is: John Doe
```

# C-Style Strings

C-style strings are created with the `char` type instead of `string`

The name comes from the C which does not have a `string` type for easily creating string variables. Instead, you must use the `char` type and create an array of characters

```c++
string greeting1 = "Hello";  // Regular String  
char greeting2[] = "Hello";  // C-Style String (an array of characters)
```

It is more convenient to work with the standard `string` type, rather than C-style strings

However, one reason some users continue to use C-style strings is that they have access to functions from the C standard library