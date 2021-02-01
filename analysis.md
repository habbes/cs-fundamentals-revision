# Big O Notation and Algorithm Analysis

The Big-O Notation is used to measure the rate of growth of an algorithm as a function of its input, describing its complexity in terms of times of space.

The **time complexity** tells us how the number of operations performed by the algorithm grows as the input size grows.

The **space complexity** tells us how much the memory allocated by the algorithm grows as the input size grows.

The Big-O notation doesn't exactly tell us how fast an algorithm runs or how much space it consumes, **it gives us an indication of how well the algorithm will scale as the size of the input grows**. The exact time an algorithm takes depends on factors like hardware, interpreter or compiler used, etc. but the order of growth is independent of these factors and allows us to analyze algorithms without independent of languages, hardware, etc.

In most cases, we care mostly about optimizing for time more than space. Since it's usually cheaper to get more memory, it's more common to make trade-offs that improve speed at the expense of memory. However, you should always be clear about which trade-offs you're making when making such decisions. If you're in a scenario where keeping memory usage to a minimum is of upmost importance, then this assumption might not hold and you should make trade-offs accordingly.

## Primitive operations
Primitive operations are basic computations like computing an addition, multiplication, assigning a value to a variable, calling a method, returning from a method, etc. You can assume that these operations take constant-time regardless of the input size.
Analyzing the time complexity of an algorithm usually consists of identifying and counting the number of primitive operations and how the number increases based on input.

When analyzing space complexity, we should consider which operations allocate memory. Function arguments and local variables allocate memory on the stack. Calling a function also allocates memory since the called function's data will be pushed to the call stack (This is important to be aware of when analyzing the space complexity of recursive functions). Most of these create constant memory. Creating an array allocates memory in proportion to the size of the array. Analyzing space complexity is usually more challenging as variables may have different scopes and life times.

## Common orders of growths
Here's a list of the most common orders of growth from best to worst:

O    | Complexity
-----|-----------
O(1) | constant
O(log n) | logarithmic
O(n)  | linear
O(n * log n) | log linear
O(n^2)  | quadratic
O(n^3)  | cubic
O(2^n)  | exponential
O(n!)   | factorial


In general, you can expect an O(1) algorithm to perform faster than a O(n) one, but
this is not always the case in practice. E.g. doing a linear search in a small
array can turn out to be faster than looking up an element in hash table. But for
sufficiently large arrays, the hash table will be faster. Remember we're talking
about order of growth or scalability, not exact speed for all possible scenarios. And usually we care about the average scenario or the worse scenario than the best scenario.

In the following segments we'll try to build some intuition in understanding and detecting the common order-of-growths

### Understanding O(1)

In terms of time complexity, this usually means the algorithm executes a fixed or constant amount of operations regardless of the input size. Executing a constant number of primitive operations is O(1). Executing a loop with a fixed number of iterations is also O(1).

In terms of space complexity, this means the algorithm a constant amount of extra space regardless of the input size. Most primitive data types like ints, bytes, chars have a fixed size (fixed number of bits) regardless of their value they hold (e.g. a 32-bit integer takes up the same amount of space whether it stores the value 0 or 1000000). Create fixed number of variables of such data types has O(1) space complexity. Data structures like strings or arrays which contain multiple elements occupy space depending on the number of items they hold. If your algorithm allocates an array or string whose size is fixed regardless of the input size, then this is also O(1). When you call a function, space is automatically allocated for it on the process's call stack (the stack frame contains local variables and other data). When the function returns, that stack frame is automatically de-allocated from the call stack. So if you're calling a function inside of a loop with n iterations, that will still cause O(1) space because in each iteration the function will be pushed, then popped from the stack. So the stack doesn't keep growing. But if it's a recursive function that calls itself before it returns, then the stack will keep grown and this would not be O(1).

### Understanding O(log n)

A logarithmic functions grows very slowly in time when the input size grows.

