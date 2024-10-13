# Concepts

#java #dynamic-programming #algorithm #codecademy

---

# Introduction to Dynamic Programming

Learn how to use dynamic programming to solve complex recursive problems.

## What is Dynamic Programming?

_Dynamic Programming_ is a programming technique used to solve recursive problems more efficiently. Specifically, it adds time efficiency, and it does so by taking advantage of data structures to store reusable solutions to intermediate steps, thus saving redundant computations. It’s a way of solving problems with recursive relationships by solving smaller problems and building up to the solution to the original problem.

Let’s take a look at a simple algorithm that can get computationally complex very quickly, and then let’s use dynamic programming to increase its efficiency.

## Fibonacci

The Fibonacci series is a classic mathematical series in which each number is equal to the sum of the two numbers before it, always starting with 0 and 1:

```
0, 1, 1, 2, 3, 5, 8, 13, 21, etc.
```

The 0th Fibonacci number is always `0` and first Fibonacci number is always `1`. So the second Fibonacci number is `0` + `1` = `1`, third Fibonacci number is `1` + `1` = `2`, and so on. You could calculate the `n`th number iteratively this way, but you could also calculate it recursively:

```pseudo
fib(n)
  if n is 0 or 1
    return n
  else
    return fib(n - 1) + fib(n - 2)
```

This technique breaks up calculating the `n`th number into many smaller problems, calculating each step as the sum of calculating the previous two numbers.

Although this technique will certainly work to find the correct number, as `n` grows, the number of recursive calls grows very quickly. Let’s visualize all the function calls if we were to calculate the fourth Fibonacci number:

```pseudo
fib(4) -> fib(3) + fib(2)
  fib(3) -> fib(2) + fib(1)
    fib(2) -> fib(1) + fib(0)
  fib(2) -> fib(1) + fib(0)
```

As you can see`fib(2)` is called twice, `fib(1)` is called three times. If `n` were larger than `4`, you’d see these numbers of calls get high very quickly. For instance, to calculate the 10th number, we’d make 34 calls to `fib(2)` and 177 total function calls! Why do we need to call the same function multiple times with the same input?

We don’t! We can use a dynamic programming technique called _memoization_ to cut down greatly on the number of function calls necessary to calculate the correct number.

## Memoization

_Memoization_ is a specialized form of caching used to store the result of a function call. The next time that function is called, if the result of that function call is already stored somewhere, we’ll retrieve that instead of running the function itself again. Memoization can result in much faster overall execution times (although it can increase memory requirements as function results are stored in memory).

Memoization is a great technique to use alongside recursion. The memo can even be saved between function calls if it’s being used for common calculations in a program.

### Memoizing Fibonacci

In the previous example, many function calls to `fib()` were redundant. Let’s memoize it in order to speed up execution.

To begin, we’ll use a Java `HashMap` to store the memoized values. Each key will represent `n` (starting from `0`), and the corresponding value will be the result of that Fibonacci number. Then, whenever we need to calculate a number, if it’s already been calculated, we can retrieve the value from the map in `O(1)` time.

In pseudocode, our approach to memoization will look something like this:

```pseudo
Create a memo map

fibMemo(n, map)
  if n is 0 or 1
    return n
  if n key exists in map
    return map.get(n)
  else
    calculate current fibonacci number through a recursive call
    store value in map
    return value
```

## My Java Implementation

```java
import java.util.HashMap;
import java.util.Map;

public class fibMemo {
    public static void main(String[] args) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        System.out.println(fibMemo(10, map));

        map = new HashMap<Integer, Integer>();
        System.out.println(fibMemo(20, map));
    }

    public static int fibMemo(int n, Map<Integer, Integer> map) {
        if (n == 1 | n == 0) {return n;}

        if (map.containsKey(n)) {return map.get(n);}

        else {
            int fibValue = fibMemo(n-1,map) + fibMemo(n-2,map);
            map.put(n, fibValue);
            return fibValue;
        }
    }
}

```

## Conclusion

Dynamic programming and memoization are great techniques breaking up complex recursive problems into smaller chunks. They are especially useful when tackling problems that involve combinations. For example, if I asked you to calculate the total number of ways to get four dice rolls to sum to `13`, you could imagine breaking that into multiple parts. You could split `13` into `6` and `7` and then find all the combinations of two rolls that would match each one of these. As you went down each path, you’d probably start seeing a lot of similar calculations, and memoization would help you reduce the number of overall function calls by storing intermediate values.

Some other common problems that can be solved using dynamic programming are the knapsack problem, the rod cutting problem, and the word break problem.