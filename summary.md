# Data Structures and Algos

## Common order of growths in Big-O analysis:

O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n) < O(n!)

## Primitive data types

- `int`, `char`, `boolean`, `long`, `double`, `float`, etc.

There's a class associated with each primitive type.
It's useful when you have generic containers for
primitive types, e.g. `ArrayList<Integer>`

These classes also have helper methods and properties e.g.

```java
Integer.MAX_INT; // largest value that can fit in an int var
Integer.MIN_INT;
Integer.parseInt("10"); // returns the integer value 10
Integer.toString(10); // returns the string "10"
```

```java
Character.isLetter('c'); // whether the character is a letter

// characters are actually numbers, e.g.

'A' == 65
'B' == 66
//...
'a' == 97
'z' == 122

int ans = 'C' - 'A'; // result is 2
```


## Arrays

Contiguous sequence of elements of the same type
- fixed size (cannot be resized)

```java
int[] nums = new int[10]; // array of ten ints
int[] otherNums = { 1, 2, 3 }; // array with initializer
nums[0] = 10; // setting values of an array by index
int second = nums[1]; // getting value by index
// iterating over an array
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}

for (int num : nums) {
    System.out.println(num);
}
```

## 2D Arrays

Think of it as a grid or matrix;

```java
int[][] matrix = new int[5][10]; // matrix with 5 rows and 10 columns
int[][] grid = {
    {0, 1, 0},
    {0, 0, 0},
    {1, 0, 0}
}; // grid with 3 rows and 3 columns

grid[0][2] = 3; // setting the item at the 1st row and 2 col to 3

// iterating over an array, matrix addition
int[][] A = new int[3][3];
int[][] B = new int[3][3];

int[][] C = new int[3][3];

// let's assume A and B have been populated with values
// now let's computer matrix addition where C = A + B
// i.e. 
// C[0][0] = A[0][0] + B[0][0]
// C[0][1] = A[0][1] + B[0][1]
// ...
// C[i][j] = A[i][j] + B[i][j]

for (int i = 0; i < A.length; i++) {
    for (int j = 0; j < A[0].length; j++) {
        C[i][j] = A[i][j] + B[i][j];
    }
}
```

## Strings

A string is a sequence of characters.
Strings are immutable, i.e. cannot be modified,
operations on strings create new strings
instead of modifying the original string.

```java
String greeting = "Hello";
String target = "World";
// String concatenation
// phrase is a new string in memory
// greeting and target remain unchanged
String phrase = greeting + " " + target; // Hello World

// You can concatenate strings with other data types,
// they'll be converted to strings automatically using
// the type's respective toString() method
int count = 20;
String s = "There are " + count + " items in this bag;
```

```java

// strings are objects stored on the heap
// when comparing strings for equality,
// their references will be compared, not their values
String a = "Hello";
// you can create a string from an array of characters
String b = new String(new char[] { 'H', 'e', 'l', 'l', 'o' });
// The == operator compares the references/addresses
// of the string in memory
a == b; //returns false

// The equals() method compares their values
a.equals(b); // returns true

```

```java
String phrase = "Hello World";
// getting a character at an index
phrase.charAt(2); // returns 'l'

// this creates 2 new strings, the original string phrase
// remains unchanged
// note that the split() method has to traverse the entire
// string, i.e. O(n)
String[] parts = phrase.split(" ");// returns { "Hello", "World"}

// join an collection of strings into a single string
// String.join is a static method called on the String class directly
String.join(",", parts); // returns "Hello,World"

// get a substring of the string from the given range
// the substring starts from the first index to the
// item before the end index (i.e. characters 1, 2, 3, 4)
phrase.substring(1, 5); // returns "ello"
// returns a substring starting at the specified index to the end
phrase.substring(6); // returns "World"

// returns a the index of the first occurrence
// of a string in another string
phrase.indexOf("World"); //returns 6
// returns -1 if the index doesn't exist
phrase.indexOf("world"); // returns -1, world != World

phrase.replace("World", "Earth"); // -> Hello Earth

// iterating over a string
for (int i = 0; i < phrase.length(); i++) {
    System.out.println(phrase.chartAt(i));
}

```

### StringBuilder

Used to create a string efficiently when you want to combine many strings or character together.

```java
String phrase = "Hello";
phrase += " World."; // "Hello World."
phrase += " It is";  // "Hello World. It is"
phrase += " a ";     // "Hello World. It is a ";
phrase += "good day"; // "Hello World. It is a good day";

// With string build
StringBuilder builder = new StringBuilder();
builder.append("Hello");
builder.append(" World.");
builder.append(" It is");
builder.append(" a ");
builder.append(" good day");
String newPhrase = builder.toString(); // Hello World. It is a good day";



StringBuilder newBuilder = new StringBuilder();
newBuilder.append("word");
newBuilder.reverse();
String reversed = newBuilder.toString(); // "drow"
```

### ArrayList

It's a dynamic array. Allows fast access by index.

Internally, it's based on a normal array. 
But when it gets full, a new array of double the size is created
and items are copied over to the new array.
So it gives the illusion of an array that grows as needed, not
fixed size.

```java

List<int> nums = new ArrayList<int>();
// adding to the end of the list is O(1)
nums.add(10);
nums.add(20);
// getting an item by index is O(1)
nums.get(0); // -> returns 10
// modifying an item by index is O(1)
nums.set(1, 15); // sets second item to 15
// list is now [10, 15]

// Insert in the middle of a list is O(n)
// cause you to shift everything after it
nums.insert(0, 25); // insert 25 at the beginning
// list is now [25, 10, 15]

// O(n) to remove an item from the middle
nums.remove(1);
// list is now [25, 15]

// Iterating of a list
for(int i = 0; i < nums.size(); i++) {
    System.out.println(nums.get(i));
}

for(int num : nums) {
    System.out.println(num);
}
```

### LinkedList

The `LinkedList` class implements a double-ended queue `Deque`,
which is basically a linked-list with `head`, a `tail` and each
node has both a `next` reference as well as a `prev` reference.

```java
List<int> nums = new LinkedList<int>();
// adding to the end of the list is O(1)
// (for a doubly-linked list, since we maintain a reference
// to the tail
nums.add(10);
nums.add(20);
// getting an item by index is O(n) cause
// you have traverse the list (either from the head or tail,
// depending on which is closer)
nums.get(1); // -> returns 20
// modifying an item by index is O(n)
nums.set(1, 15); // sets second item to 15
// list is now [10, 15]

// Insert in the middle of a list is O(n)
// cause you to shift everything after it
nums.insert(1, 25); // insert 25 at the beginning
// list is now [10, 25, 15]

// Insert at the beginning is O(1)
nums.insert(0, 5);
// list is now [5, 10, 25, 15]

// O(n) to remove an item from the middle
// removal from the beginning is O(1)
// in doubly-linked list, removing from the end is also O(1)
nums.remove(1);
// list is now [25, 15]

nums.isEmpty(); // check it's empty

// Iterating of a list
for(int num : nums) {
    System.out.println(num);
}
```

### Stacks and Queues

```java
// You can use a doubly-LinkedList to implement both a stack
// or a queue, because it provides efficient O(1) insertion
// and removal both at the end and the beginning

Queue<int> queue = new LinkedList<int>();
queue.add(10);
queue.add(20);
queue.peek(); // returns 10
queue.remove(); // removes 10

LinkedList stack = new LinkedList<int>();
stack.push(10);
stack.push(20);
stack.peekLast(); //returns 20
stack.pop(); // removes 20

// There's also a Stack class in java
Stack<int> stack2 = new Stack<int>();
stack.push(10);
stack.push(20);
stack.peek(); //returns 20
stack.pop(); // removes 20
```

### HashMap

```java
// Stores key-value pairs. Allows you to efficiently O(1)
// insert, access, update, delete items by key
// All keys are unique, inserting a key already exists
// will replace the value of the existing key
// Entries are not ordered, and not sorted

Map<String, Integer> map = new HashMap<>();
map.put("One", 1);
map.put("Two", 2);
map.get("One"); // -> 1
map.put("Two", 3); // replaces the value of "Two"
map.remove("Two");

map.containsKey("One"); // true


// iterating over a map
for(Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " " + entry.getValue());
}

/*
A hashmap contains a bunch of arrays called buckets
where data stored. Ideally, all buckets should
have the same number of elements, and they
shouldn't grow passed a certain capacity.

Since a bucket has a fixed capacity, finding something
in the bucket is O(1)

Assume we have hashmap with 4 buckets, each with ideal capacity 2

Assume you have entry ("One", 1), ("Two", 2), ("Three", 3)
"One".hashCode() -> 10, 10 % 4 -> 2 ("One" goes in bucket 2)
"Two".hashCode() -> 16, 16 % 4 -> 0 ("Two" goes in bucket 0)
"Three".hashCode() -> 32, 32 % 4 -> 0 ("Three" goes in bucket  0)
"Four".hashCode() -> 7, 7 % 4 -> 3 ("Four" goes in bucket 3)

[
    0 -> [Entry("Two", 2), Entry("Three", 3)]
    1 -> []
    2 -> [Entry("One", 1)]
    3 -> [Entry("Four", 4)]
]

When the hashmap fills up, i.e. we have 8 entries,
we just add more buckets 

After we add buckets, we have to move items depending
on where their hashcodes land them in the new map
"Four".hashCode() -> 7, 7 % 8 -> 7 ("Four" moves to bucket 7)

[
    0 -> [Entry("Two", 2), Entry("Three", 3)]
    1 -> []
    2 -> [Entry("One", 1)]
    3 -> []
    4 -> []
    5 -> []
    6 -> []
    7 -> [Entry("Four", 4)]
]


*/

```

### HashSet

Stores unique items. Works like a hash map, but without the values.

```java
Set<String> set = new HashSet<>();
set.add("One");
set.add("Two");
set.add("Two"); // adding something that already exists does nothing
// { "One", "Two" }
set.remove("Two");

set.contains("One"); // true


// iterating over a map
for(String item : set) {
    System.out.println(item);
}
```

### Sorting

- Merge sort: Recursively splits a list in halves, then starts merging 2 halves at a time into a sorted list.
  - Time complexity: **O(nlogn)**
  - Space complexity: **O(n)**
  - Can be also be applied to linked lists since it doesn't need to swap elements at random indexes
  - It **stable** meaning 2 items with the same ordering value will end up in their original in the original list
- Quick sort: Picks a pivot element, moves items smaller than the pivot to the left, and items greater than the pivot to the right, then recursively calls quick sort to the left and right sub lists.
  - Time complexity: **O(nlogn)**
  - Space complexity: **O(logn)**
  - Can be also be applied to linked lists since it doesn't need to swap elements at random indexes
  - It **unstable** meaning 2 items with the same ordering value might not end up in their original in the original list

- Insertion Sort: For each element[i] in the array, swap the element[i] with element[i - 1] so long as element[i] < element[i - 1]
  - Time complexity: **O(n^2)**
  - Space complexity: **O(1)**
  - **Stable**


```java

// sorting array
int[] nums = { 1, 5, 0, 3, 2};
// sorts the array in-place using a built-in efficient O(nlogn)
// algorithm
Arrays.sort(nums);

// sorting a collection like ArrayList
List<int> list = new ArrayList<>();
Collections.sort(list);
```

### Swapping to variables

```java
int a = 7;
int b = 10;

// swapping
int temp = a;
a = b;
b = temp;
```

### Binary search / Bisection search

- Get the item in the middle, compare it to the search term, if it's search term is smaller, then run binary search recursively on the left sublist, if it's greater, run binary search on the right sublist, if equals, return the middle index

- Time complexity: **O(logn)**
- Space complexity: **O(1)** if iterative, **O(logn)** if recursive

```java

// return the index of the target if it exists in the array
int binarySearch(int[] items, int target, int start, int end) {
    if (start == end) {
        return -1;
    }
    if (end - start == 1) {
        if (items[start] == target) {
            return start;
        }

        return -1;
    }

    int middle = (start + end) / 2;
    if (items[middle] == target) {
        return middle;
    }

    if (target > items[middle]) {
        return binarySearch(middle + 1, end);
    }

    // target < items[middle]
    return return binarySearch(start, middle);
}

```

```java
// built-in binary
int[] items = { 0, 1, 2, 5, 6 };

int index = Arrays.binarySearch(items, 0, items.length, 1);
// index -> 1

// if item not in array, it returns
// -(insertion point) - 1
Arrays.binarySearch(items, 0, items.length, 3);
// returns -> -4
// so if you want to find where 3 should have been placed
// if it were in the array, you'll do -(-4) - 1 = 4 - 1 = 3

```

## Trees

A tree has root and children, the children are also sub trees.
Nodes also have values.

A leaf is child node which doesn't have children.

### Binary Tree

A tree where each node has at most 2 children.

The **height** of a tree is the distance between the root node
and the deepest leaf node. The depth of a node is distance between
the root node and a specified node.

You can also think of the height as the number of levels of levels in the tree.

A **balanced** tree is a tree where each branch has roughly the same number of nodes. i.e. you don't have some branches that are too deep while others are too shallow.

**When a tree is balanced**, the **height of the binary tree is O(logn)**


You can traverse a tree using Bread-first-search or Depth-first-search.

You can implement the traversal recursively or iteratively (using a stack for BFS or a queue for DFS). It's usually easier to use recursion when traversing a tree.

You have different DFS variants:
- pre-order traversal: visit parent node then traverse left then traverse right
- in-order traversal: traverse left, then visit parent, then traverse right
- post-order traversal: traverse left, traverse right, then visit parent

```java
class TreeNode {
    int value;
    TreeNode left;
    TreeNode right;

    public void dfsTraverse() {
        System.out.println(this.value);

        if (this.left != null) {
            dfsTraverse(this.left);
        }

        if (this.right != null) {
            dfsTraverse(this.right);
        }
    }
}

class Main {
    public static void dfsTraverse(TreeNode node) {
        if (node == null) {
            return;
        }

        // visiting the node
        System.out.println(node.value);

        // traverse the left
        dfsTraverse(node.left);
        // traverse the right
        dfsTraverse(node.right);
    }
}

```

### Binary Search Trees (BST)

A binary tree where everything on the left branch is smaller or equals than the node's value and everything on the right branch is greater then the node

So the BST is a sorted tree.

Searching BST requires traversing only a single path in the tree instead of visiting all the nodes in the tree.
- Time complexity is **O(h)**
If the tree is balanced, and h is O(logn), then **searching 
balanced BST is O(logn)**

```java

boolean searchTree(TreeNode node, int searchValue) {
    if (node == null) {
        return false;
    }

    if (node.value == searchValue) {
        return true;
    }

    if (node.left != null && searchValue < node.value) {
        boolean foundInLeft = searchTree(node.left, searchValue);
        if (foundInLeft) {
            return true;
        }
    }
    else if (node.right != null && searchValue > node.value) {
        boolean foundInRight = searchTree(node.left, searchValue);
        if (foundInRight) {
            return true;
        }
    }

    return false;
}

```

### Self-Balancing BST

Self-balancing BSTs automatically re-balance themselves while maintaining the BST property whenever you insert, update, or remove from a tree. Keeping it balanced means the height remains O(logn).

- Time complexity is **O(logn)** for insertion, removal and updates

Self-Balancing BSTs can be used to implement sorted maps, sorted sets or priority queues.

```java
TreeSet<int> set = new TreeSet<>();
set.add(2);
set.add(1);
set.add(3);
set.firstKey(); // -> 1
```

```java
PriorityQueue<int> queue = new PriorityQueue<>();

queue.add(2); // O(logn)
queue.add(1);
queue.add(4);
queue.peek(); // returns 1, O(1) because smallest item is always stored at root
queue.pop(); // removes 1, O(logn), removing an item requires
// rebalancing the tree which is O(logn)

```
