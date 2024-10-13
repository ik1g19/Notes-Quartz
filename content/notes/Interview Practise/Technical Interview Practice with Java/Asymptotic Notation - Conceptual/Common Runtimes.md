#o-notation  #codecademy

Before we delve into the multiple runtime cases, let’s see the different common runtimes a program could have. Below is a list of common runtimes that run from fastest to slowest.

- **Θ(1)**. This is _constant_ runtime. This is the runtime when a program will always do the same thing regardless of the input. For instance, a program that only prints “hello, world” runs in `Θ(1)` because the program will always just print “hello, world”.
- **Θ(log N)**. This is _logarithmic_ runtime. You will see this runtime in search algorithms.
- **Θ(N)**. This is _linear_ runtime. You will often see this when you have to iterate through an entire dataset.
- **Θ(N*logN)**. You will see this runtime in sorting algorithms.
- **Θ(N2)**. This is an example of a _polynomial_ runtime. When **N** is raised to the **2nd** power, it’s known as a _quadratic_ runtime. You will see this runtime when you have to search through a two-dimensional dataset (like a matrix) or nested loops.
- **Θ(2N)**. This is _exponential_ runtime. You will often see this runtime in recursive algorithms (Don’t worry if you don’t know what that is yet!).
- **Θ(N!)**. This is _factorial_ runtime. You will often see this runtime when you have to generate all of the different permutations of something. For instance, a program that generates all the different ways to order the letters “abcd” would run in this runtime.

![[Pasted image 20240412020721.png]]