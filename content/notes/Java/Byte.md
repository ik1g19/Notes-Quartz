#java

---

`byte` is an 8-bit signed integer, meaning it uses 1 byte (8 bits) of memory

Since it is an 8-bit signed integer, its range is from **-128 to 127**

Operations on `byte` variables might be slightly slower than `int` because the byte-sized values may be converted to `int` in some arithmetic operations (since arithmetic in Java usually happens using `int` by default