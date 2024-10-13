#cpp #syntax

```c++
#include <iostream>
using namespace std;

int main() {
  cout << "Hello World!";
  return 0;
} 
```

`#include <iostream>` is a **header file library** that lets us work with input and output objects, such as `cout` (used in line 5). Header files add functionality to C++ programs

`using namespace std` means that we can use names for objects and variables from the standard library without having to write `std` all the time
- `std::cout << "Hello World!";`

`cout`  is an **object** used together with the _insertion operator_ (`<<`) to output/print text. In our example, it will output "Hello World!"

To insert a new line in your output, you can use the `\n` character:

```c++
#include <iostream>  
using namespace std;  
  
int main() {  
  cout << "Hello World! **\n**";  
  cout << "I am learning C++";  
  return 0;  
}
```

You can also use another `<<` operator and place the `\n` character after the text, like this:

```c++
#include <iostream>  
using namespace std;  
  
int main() {  
  cout << "Hello World!" **<< "\n";**  
  cout << "I am learning C++";  
  return 0;  
}
```