#cpp #syntax

The size of an array in C++ is fixed, meaning you **cannot** **add** or **remove** elements after it is created
# Vectors

C++ provides **vectors**, which are resizable

The size of a vector is dynamic, meaning it can grow and shrink as needed

Vectors are found in the `<vector>` library, and they come with many useful functions to add, remove and modify elements:

```c++
// A vector with 3 elements  
vector<string> cars = {"Volvo", "BMW", "Ford"};  
  
// Adding another element to the vector  
cars.push_back("Tesla");
```

# Get the Size of an Array

To get the size of an array, you can use the `sizeof()` operator:

```c++
int myNumbers[5] = {10, 20, 30, 40, 50};  
cout << **sizeof(myNumbers)**;
//output: 20
```

Why did the result show `20` instead of `5`, when the array contains 5 elements?

It is because the `sizeof()` operator returns the size of a type in **bytes**

**To find out how many elements an array has**, you have to divide the size of the array by the size of the first element in the array

```c++
int myNumbers[5] = {10, 20, 30, 40, 50};  
int getArrayLength = sizeof(myNumbers) / sizeof(myNumbers[0]);  
cout << getArrayLength;
```

## Loop Through an Array with `sizeof()`

```c++
int myNumbers[5] = {10, 20, 30, 40, 50};  
for (int i = 0; i < sizeof(myNumbers) / sizeof(myNumbers[0]); i++) {  
  cout << myNumbers[i] << "\n";  
}
```