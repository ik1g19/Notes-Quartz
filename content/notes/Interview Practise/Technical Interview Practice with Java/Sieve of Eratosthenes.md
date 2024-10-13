# Concepts

#java #algorithm #codecademy

---

The sieve provides a set of steps for finding all prime numbers up to a given limit. In this article, we’ll cover implementing the Sieve of Eratosthenes in Java. As a reminder, a prime number is a positive number with no divisors but `1` and itself. `2`, `3`, `11`, and `443` are all prime numbers.

## Sieve Implementation

The sieve works by first assuming that all numbers from

$$\{2,…,n\}$$

are prime, and then successively marking them as NOT prime.

The algorithm works as follows:

1. Create a list of all integers from 2 to n.
2. Start with the smallest number in the list (2, the smallest prime number).
3. Mark all multiples of that number up to n as not prime.
4. Move to the next non-marked number and repeat this process until the entire list has been covered.

When the steps are complete, all remaining non-marked numbers are prime.

### Example

If we wanted to find all prime numbers less than or equal to 10, we would:

1. Start with a list where all are assumed to be prime:

$$2\;3\;4\;5\;6\;7\;8\;9\;10$$

1. Starting with `2`, mark all multiple up to `10` as NOT prime:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;9\;\cancel{10}$$

1. Move to the next non-marked number, `3`, and mark its multiples as NOT prime (`6`) is already marked:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;\cancel{9}\;\cancel{10}$$

1. Continue marking, starting with every non-marked number (in this case, all multiples of `5` are already marked, and `7`‘s first multiple is out of range). This means that we have now found all primes up to `10`:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;\cancel{9}\;\cancel{10}$$


## Implementation Steps in Java

There are many possible ways of implementing this algorithm in Java. We’ll outline a basic approach here and then walk through it step-by-step.

1. Create an array of all integers from `2` to `n`
2. Set all elements of the array to `true`
3. Starting with `2`, iterate through the array. If the current element is `true`, it is still considered prime. Since we know that all multiples of that number are NOT prime, iterate through all multiples of that number up to `n` and set them equal to `false`
4. Change the current element to the next non-`false` index.
5. Return the corresponding number value for any element still marked as prime (value of `true`).

### Optimizations

There are several small optimizations that can be made to the basic implementation of the sieve to remove duplicate checks for prime-ness.

#### End Boundary

In our basic implementation, the outer loop iterated from `2` to `n`. Because the inner loop marks multiples of a base value, we only need to check individual numbers lower than the square root of `n`. Consider the example of a limit of `10`:

1. First, all multiples of `2` are marked:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;9\;\cancel{10}$$

1. Then, all multiples of `3` are marked:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;\cancel{9}\;\cancel{10}$$

1. `4` is greater than the square root of `10` (approximately `3.16`), so we can break. If you look at the previous step, all non-prime numbers have indeed already been marked.

#### First Multiple

In our basic implementation, the inner loop started checking multiples at 2 times the current number. We can skip a few checks starting the checks at current2.

Consider the example of a limit of `10` again:

1. First, all multiples of `2` are marked:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;9\;\cancel{10}$$

1. Then, all multiples of `3` are marked, but we can skip `6` (`3 * 2`) because it’s already been marked. Instead we start at 32, `9`:

$$2\;3\;\cancel{4}\;5\;\cancel{6}\;7\;\cancel{8}\;\cancel{9}\;\cancel{10}$$

1. We’ve now completed the check with one less comparison.

#### Pre-mark All Even Numbers

This optimization comes in when building the initial array. There’s no need to ever check even numbers after `2`, since they will never be prime, so they can all be marked as non-prime initially.

---

These optimizations may seem small when dealing with a limit of `10`, but they can significantly speed up the algorithm with larger limits.

## Complexity

The complexity of the Sieve of Eratosthenes with optimizations is

$$O(nlog⁡(log⁡n))$$

There are two operations to take into account: the creation of the array and the incrementing and multiple-marking loops.

Creation happens in `O(n)` time, since it creates an element for each number from 2 to `n`.

Multiple marking happens in `O(n log log n)` time. The reasons for this come down to some complex math, but briefly:

The number of times you mark a non-prime number is

$$\frac{n}{2}+\frac{n}{3}+...\frac{n}{\sqrt{n}}$$

It begins with `n / 2` because initially all multiples of `2` are marked as non-prime (this will happen 50 times with a limit of 100, as each even number is marked). This process continues up until the square root of `n`. Through some [fancy mathematical proofs](https://en.wikipedia.org/wiki/Divergence_of_the_sum_of_the_reciprocals_of_the_primes), this works out to an overall time complexity of

$$O(nlog⁡(log⁡n))$$

since this is larger than the `O(n)` array-creation time.

## Conclusion

The Sieve of Eratosthenes is a millennia-old algorithm, so there are some more improvements and more advanced methods for finding primes invented since its discovery, but it’s still a great way to generate lists of prime numbers. Included below is our sieve code including optimizations:

```java
import java.util.*;

public class SieveOfEratosthenes {
    void sieveOfEratosthenes(int limit) {
        boolean[] output = new boolean[limit + 1];
        for (int x = 0; x <= limit; x++) {
            output[x] = true;
        }
        output[0] = false;
        output[1] = false;

        for (int i = 2; i <= Math.pow(limit, 0.5); i++) {
            if (output[i] == true) {
                for (int j = (int) Math.pow(i, 2); j <= limit; j = j + i) {
                    output[j] = false;
                }
            }
        }

        List<Integer> result = new ArrayList<Integer>();

        for (int i = 0; i < output.length; i++) {
            if (output[i] == true) {
                result.add(i);
            }
        }

        System.out.println(Arrays.toString(result.toArray()));
    }

    public static void main(String[] args) {
        int n = 7;
        SieveOfEratosthenes g = new SieveOfEratosthenes();
        g.sieveOfEratosthenes(n);
    }
}

```