# Data Structures and Algos

## Common order of growths in Big-O analysis:

From best to worst:

- O(1) -> Constant
- O(logn) -> Logarithmic
- O(n) -> Linear
- O(nlogn) -> Loglinear
- O(n^2) -> Quadratic
- O(n^3) -> Cubic
- O(2^n) -> Exponential
- O(n!) -> Factorial

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
  - It **unstable** meaning 2 items with the same ordering value might not end up in their original order in the original list

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

Self-Balancing BSTs can be used to implement sorted maps, sorted sets

```java
// A set where items are sorted
TreeSet<int> set = new TreeSet<>();
set.add(2); // O(logn)
set.add(1); // O(logn)
set.add(3); // O(logn)
set.contains(2); // -> true, O(logn)
set.firstKey(); // -> 1, O(logn)
```

### Min-heap

A balanced tree (not BST) where the each node is smaller than its children.
Therefore the smallest value is at the root. When you remove
the root, it restructures the tree such that the smallest item in the remaining nodes becomes the new root. This restructuring (heapify) is O(logn)

```java
// a priority queue is a queue where items are removed
// by order of priority rather than using a FIFO order
// The smaller the value, the higher the priority
// A priority queue is implemented as min-heap
// a type of balanced binary tree where the smallest item is always
// stored at the root (there's also a max-heap which stores the largest item at the root)
PriorityQueue<int> queue = new PriorityQueue<>();

queue.add(2); // O(logn)
queue.add(1);
queue.add(4);
queue.peek(); // returns 1, O(1) because smallest item is always stored at root
queue.pop(); // removes 1, O(logn), removing an item requires
// rebalancing the tree which is O(logn)

```

## Graphs

- A graph is a collection nodes and links between those nodes.
- The nodes that are directly linked to a given node, are called its neighbours.
- The links can represent any type of relationship (e.g. friends, synonyms, interest, manager)
- The links can be bidirectional (meaning if A is connected B, therefore B is connected A, e.g. a friend relationship) or can be unidirectional (A -> B does not mean B -> A. E.g. manager relationship)
- When the links have a direction, the graph is called a directed graph
- Links can also have weights, i.e. number which could represent the strength of the relationship, the distance between 2 cities, etc.
- Graphs can have cycles, A - B, B - C, C - A
- Graphs without cycles is called an acyclic graph
- A tree is a directed acyclic graph where one node serves as the root

- A graph can be represented with an **adjacency matrix**, a 2d array where M[i][j] == 1 if there's a connection between nodes i and j, otherwise M[i][j] = 0
- A more common way to represent a graph is using **adjacency lists**. Normally this hashmap where each node is a key in the map, and for key, the value is a list of all the nodes directly connected to it.
- You can traverse a graph using DFS or BFS

```java
// job:work job:occupation occupation:career ablaze:burning
HashMap<String, List<String>> graph = new HashMap<>();
graph.put("job", new ArrayList<>(String[] { "occupation", "work" }));
graph.put("work", new ArrayList<>(String[] { "job" }));
graph.put("occupation", new ArrayList<>(String[] { "job", "career" }));
graph.put("career", new ArrayList<>(String[] { "occupation" }));
graph.put("ablaze", new ArrayList<>(String[] { "burning" }));
graph.put("burning", new ArrayList<>(String[] { "ablaze" }));

void traverse(Map<String, List<String>> graph, String startNode) {
    // pick a starting node
    Queue<String> toVisit = new LinkedList<>();
    Set<String> visited = new HashSet<>();
    toVisit.push(startNode);
    
    while (!toVisit.isEmpty() {
        String current = toVisit.remove();
        if (visited.contains(current)) {
            continue;
        }
        System.out.println(current);
        List<String> neighbors = graph.get(current);
        visited.add(current);
        for (String neighbor : neighbors) {
            toVisit.add(neighbor);
        }
    }
    
}

boolean contains(Map<String, List<String>> graph, String startNode, String searchKey) {
    // pick a starting node
    Queue<String> toVisit = new LinkedList<>();
    Set<String> visited = new HashSet<>();
    toVisit.push(startNode);
    
    while (!toVisit.isEmpty() {
        String current = toVisit.remove();
        if (visited.contains(current)) {
            continue;
        }
        if (current == searchKey) {
            return true;
        }
        List<String> neighbors = graph.get(current);
        visited.add(current);
        for (String neighbor : neighbors) {
            toVisit.add(neighbor);
        }
    }

    return false;
}

```

### Dynamic programming

Fibonacci sequence: 0 1 1 2 3 5 8 13 21

```
fib(0) = 0
fib(1) = 1
fib(x) = fib(x - 1) + fib(x - 2)
```

```java

int fibonacci(int index) {
    if (index == 0) {
        return 0;
    }
    if (index == 1) {
        return 1;
    }

    return fibonacci(index - 1) + fibonacci(index - 2);
}

```

The naive recursive implementation is O(2^n)
```

                               fib(5)
        fib(4)                               fib(3)
    fib(3)    +     fib(2)                  fib(2) +   fib(1)
 fib(2) +  fib(1)  fib(1) + fib(0)        fib(1) + fib(0)
fib(1) + fib(0)
```


It calls computes the same value multiple times, e.g.
fib(3) is called 2 times
fib(2) is called 3 times

But the value of fib(3) never changes
We can save the values we've already computed, so that the next
we need it, we get it from the cache instead of computing again

This is called **memoization**

```java

int fibonacci(int index, Map<int, int> cache) {
    if (index <= 1) {
        return 1;
    }

    if (!cache.containsKey(index)) {
        int value = fibonacci(index - 1) + fibonacci(index - 2);
        cache.put(index, value);
    }

    return cache.get(index);
}

```

With memoization, this is O(n)
```

                               fib(5)
        fib(4)                               fib(3)from cache
    fib(3)*    +     fib(2)from cache       
 fib(2)* +  fib(1)            
fib(1) + fib(0)
```

But you can use a bottom-up loop instead of recursion:

```java

int fibonacciIterative(int index) {
    if (index <= 1) {
        return 1;
    }

    int x = 1; // previous-1 value
    int y = 1; // previous value
    newValue = 3;


    for (int i = 2; i <= index; i++) {
        int newValue = x + y;
        x = y;
        y = newValue;
    }

    return y;
}
```

# System Design

- Database: Stores data persistently in a way that can be queried. e.g. MySQL
- API Server: Server that receives and handles API requests from clients

- **Horizontal Scaling**: Increasing the capacity of your system by increasing number of nodes that perform a given task in order to handle more tasks/requests
- **Vertical Scaling**: Increasing the capacity of your system by adding resources to a single node, making it more powerful (e.e. increasing RAM, CPU cores, etc.)

- **Load Balancer**: (Reverse proxy) Receives requests from clients and distributed those requests across multiple servers. This allows traffic to be distributed across many servers instead of a single server bearing all the load. This allows your application to handle more concurrent users (e.g. multiple requests sent at the same time) as well improves reliability (e.g. if one server goes down, then other servers will continue to serve requests).
When you're scaling your API server horizontal, you should also use a load balancer.

- **Database replication**: Having multiple instances of database server in a cluster. The data in the database is replicated/copied on all the servers. Usually one of the servers acts the primary or master and the others are secondaries or slaves. Only the primary node accepts writes (i.e. insertions, deletions or updates). But other nodes can also serve reads.
Whenever the primary receives writes, the updates are sent to the secondaries to update their own copies. There's a delay in time within which the servers have different data i.e. inconsistency.

Replication allows multiple instances to serve reads from the database system, so this is a form of scaling. But replication also allows a secondary
to take over as primary if the original primary goes down. This improves reliability of your system (makes it more fault-tolerant).

If there's a network issue and the instances can't communicate, then you have to make a choice:
- Either you stop responding to all requests until the network issue is resolved. But in this case your system is **no longer available**
- Or you continue responding requests but since your nodes are not communicating, they can end up having different copies of data. This means your system is **inconsistent**

This notion is known as the **CAP** theorem: In a distributed, in the presence of a network **P**artition, you can either have **A**vailability or **C**onsistency, but not both.

- **Database sharding**: splitting the data and storing it on different databases. It useful when your data is too large to fit in a single database or when you want to distribute your geographically such that data is closer to the people who need them. This usually introduces more complexity, makes queries difficult, and some queries impossible. It's not recommended to do this unless you've exhausted what you can store in a single database.

- **Database indexing**: Index a field in table to make queries that use that field faster. If a query uses an indexed field the database will search index instead of doing a linear search in the table.
An index is a separate data structure on disk and is implemented using a **B-Tree** (type of balanced search tree). Searching through an index is O(logn), doing a table scan is O(n)

  - Trade offs: Indexes take up extra storage space. Also an index is updated each time a new value is inserted into the table, delete, or updated. An index makes queries much faster, but slightly slows down writes. So it's recommended to use indexes on fields that are queried frequently, but updated rarely.

- **Distributed Cache (Redis)**: A server that stores key-value data in memory and allows you to add, or access data by key. Thing of it as a server that works like a hashmap. It's usually faster than accessing data in a database (memory is much faster than disk), but has limited queries capabilities (i.e. you can only access data by key). Might be expense to have large caches cause RAM is more expensive than HDD. So caches are usually smaller than the original data source. So you need a way to evict data when the cache gets full (e.g. LRU eviction).

Because data is stored in memory, data will be lost when if the server crashes or power is lost.

If you're caching data that's in a database, you might have to deal with consistency issues, i.e. when data is updated in the database, it should also be updated in cache.

- **Message Queue/Message Broker (e.g. RabbitMQ)**: Provides message queues through which different nodes communicate with each other without talking to each other directly. Direct communication between a sender and a receiver is not always possible ideal because it requires the sender to know the IP of all receivers, to keep track of new receivers that want may want to receiver the message, to keep track of connections that break, etc. A message broker in an intermediary that decouples the sender (producer) and receiver (consumer). Sender sends message to queue, and all receivers on that queue receive the message.

Use cases: 
 - when one node wants to broadcast a notification to other nodes
 - when you have multiple workers and you want to distribute tasks equally across the worker, you could use worker queues where the message broker sends a task to one worker, then the next task to the other worker, etc.

 Other benefits:
 - message brokers can allow you to manage topics so that messages are only delivered to nodes which have subscribed to that topic (publish/subscribe or pub/sub)
 - message brokers can keep track of acknowledgements to know whether a task was complete or not before removing it from the queue, if the task failed or the worker handling it crashed, it an requeue the message and send it to a different worker
 - message brokers can ensure that a receiver is not receiving more messages than it can handler


 - **Background worker**: A node in your system which handles long-running tasks. You create background workers to avoid running long-running tasks in the same API server that's responding to user requests. User requests should be responded to quickly. So if the requests has requires a long-running job (e.g. processing an image, sending bulk emails), then the server creates a task and sends it to the worker queue. The message brokers sends it to a background worker and then background worker process the task. When it's complete it can broadcast a notification back to the server and the server can send a notification to the user using WebSockets, or send an email to the user, 

 - **Websockets**: WebSockets create persistent connections between server and client and allows bi-directional communication between the server and client. This means once the WebSocket connection is established, the server can send a message directly to the client even when the client has not sent a request. In normal HTTP, the client creates a connection to the server then sends a request, the server sends a response over the same connection, then the connection is closed. The server cannot send anything to the client without the client initiating a request.

 WebSockets are used in realtime applications (e.g. chat applications, realtime notifications, etc.)
