#cpp #syntax

`cin` is a predefined variable that reads data from the keyboard with the extraction operator (`>>`)

In the following example, the user can input a number, which is stored in the variable `x`. Then we print the value of `x`:

```c++
int x;   
cout << "Type a number: "; // Type a number and press enter  
cin >> x; // Get user input from the keyboard  
cout << "Your number is: " << x; // Display the input value
```

Both `cin` and `cout` belongs to the `<iostream>` library, which is short for standard input / output streams