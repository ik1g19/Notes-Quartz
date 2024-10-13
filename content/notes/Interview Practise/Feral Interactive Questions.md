#java #interview-questions 

---
# Multiple Choice Assessment

## Optional

![[Images/2024-09-25 15_36_27-Feral Interactive __ Careers — Mozilla Firefox.png]]

![[notes/Java/Optional#^optional]]

- `new Aux()` will call the default constructor of `Aux`, which doesn't initialize `s`, so `s` remains `null`.
- `getAopt()` checks if `s == null`. Since `s` is `null`, it will return `Optional.empty()`.
- Calling `.get()` on an `Optional.empty()` will throw a `NoSuchElementException` because `Optional.empty()` contains no value.

### Correct Answer:

The last option is correct:

- **"The optional is empty, calling .get() on it causes a runtime error"**

# Online Assessment

## Question

```java
/**
	 * Perform a "rotation" of the integers inside data, modifying its contents.
	 * "Rotation" means to shift the integers left or right, and those which drop off the
	 * end of the array are added to the vacated positions at the other end.
	 *
	 * Examples with the starting array {0, 1, 2, 3, 4, 5, 6}
	 * e.g. rotate(1, true)   ->  {6, 0, 1, 2, 3, 4, 5}
	 * e.g. rotate(2, true)   ->  {5, 6, 0, 1, 2, 3, 4}
	 * e.g. rotate(3, false)  ->  {3, 4, 5, 6, 0, 1, 2}
	 *
	 * @param n The number of positions to rotate the dataArray by
	 * @param rotateRight If true, rotate elements to the right, otherwise, rotate
	 * them to the left
	 */
	public static void rotate(int[] data, int n, boolean rotateRight) {
    }
```

## My Solution

```java
public static void rotate(int[] data, int n, boolean rotateRight) {
		int size = data.length;

		//rotating by a negative position
		if (n < 0) {n = Math.abs(n); rotateRight = !rotateRight;}

		//rotating further than the size of the arr
		if (n > size) {n%=size;}

        if (rotateRight) {
            int[] temp = new int[size];

			//store last n elements
            for (int i = 0; i < n; i++) {
                temp[i] = data[size-n+i];
            }

			//store remaining elements
            for (int i = n; i<size; i++) {
                temp[i] = data[i-n];
            }

			//copy temp arr back
            for (int i = 0; i < size; i++) {
                data[i] = temp[i];
            }
        }
		else {
			int[] temp = new int[size];

			//store size-n elements
			for (int i = 0; i < size-n; i++) {
				temp[i] = data[i+n];
			}

			//store remaining elements
			for (int i = size-n; i<size; i++) {
				temp[i] = data[i-(size-n)];
			}

			//copy temp arr back
			for (int i = 0; i < size; i++) {
				data[i] = temp[i];
			}
		}
    }
```

This is garbage and awful

At the very least it could have been done with `System.arraycopy` to maintain clarity

```java
public static void rotate(int[] data, int n, boolean rotateRight) {
		int size = data.length;

		//rotating by a negative position
		if (n < 0) {n = Math.abs(n); rotateRight = !rotateRight;}

		//rotating further than the size of the arr
		if (n > size) {n%=size;}

        if (rotateRight) {
            int[] temp = new int[size];

			//store last n elements
            System.arraycopy(data, size - n, temp, 0, n);

			//store remaining elements
            System.arraycopy(data, 0, temp, n, size - n);

			//copy temp arr back
            System.arraycopy(temp, 0, data, 0, size);
        }
		else {
			int[] temp = new int[size];

			//store size-n elements
            System.arraycopy(data, n, temp, 0, size - n);

			//store remaining elements
            System.arraycopy(data, 0, temp, size - n, size - (size - n));

			//copy temp arr back
            System.arraycopy(temp, 0, data, 0, size);
		}
    }
```

## Not Stupid Solution

```java
public static void rotate(int[] data, int n, boolean rotateRight) {
		int[] newArray = new int[data.length];

		n = rotateRight ? n : -n;

		for(int x = 0; x <= data.length-1; x++){
			int i = (x+n) % data.length;
			newArray[ (i < 0) ? i+data.length : i ] = data[x];
		}

		//copy temp arr back
        System.arraycopy(newArray, 0, data, 0, data.length);
    }
```

This works by walking the array and inserting elements into their rotated positions in the temporary array

The rotated position of an element is calculated through `(x+n) % data.length`

If we are rotating left then `n` will be negative

This means `(x+n) % data.length` will evaluate to `-1`

Which is why we have the extra condition before indexing `newArray[ (i < 0) ? i+data.length : i ] `