# Learn Data Structures by Practicing Part I
The structure of this article is derived from [here](https://en.wikipedia.org/w/index.php?oldid=850927589). However the organization of this wikipedia article is a mess. It need to be updated urgently in order not to mislead the newbies. 

> "Algorithm is to construct a proper structure, and insert data. "
> ---kulasama

## Data types
### Primitive types
Objectives: Knowing how the datum is stored, exploiting intrinsic features of it and avoid making mistakes. 
* You should be able to declare, assign, read or print variables of these types. 
* You should be able to apply all possible operators to variables of these types and predict the results. 
* You should be able to predict the results of conversions between these types.
* You should know the limits of these types and should be able to predict the results of exceeding them. 
#### Boolean
#### Character
#### Floating point
* Including single precision floats, double precision (IEEE 754) floats, etc. 
#### Fixed-point numbers
* Integer, including signed and unsigned integer
* Reference, pointer, or handle
#### Enumerated types

---
Literatures
* _Hacker's Delight_, Henry S. Warren, Jr.

Excercises
* Given two 32-bit signed integers $a$ and $b$, print how many bits changes when turning $a$ to $b$.
  * Hint: Hamming weight of $a\underline\vee b$
* Given a number of height in inches and a number of height in centimeters, tell whether they equal each other. 
* Explain ASCII code $0$, $9$, $10$, $13$, and declare variables of them in charactor literals.
* How to print an emoji? 
* Given $n$ integers, each of them appears twice except for one, which appears exactly once. Find that single one.
  * Advanced: Given $n$ integers, each of them appears three times except for one, which appears exactly once. Find that single one.

**Only premitive types are allowed in these excersices. **

---

### Composite types or non-primitive type
Objectives: Getting familiar with how multiple data are organized basically. 
#### Array
#### Record, tuple, or structure
#### String
#### Union
#### Tagged union, variant, variant record, discriminated union, or disjoint union

---

Excercises
* Given a string of a heximal number (might not be an integer), print it in decimal form.
* Write a programm of encryption and decryption of Caesar ciphering.
* Name algorithms of string searching and compare their advantages and disadvantages. 
* Implement a expression evaluator supporting decimal numbers (with or without seperator), $+$ and $-$.
* Store sparse matrices with various methods and compare where they should be applied. (Note that some of them depends pointers or references)
  * Dictionary of keys
  * List of lists
  * Coordinate list
  * Compressed sparse row
  * Compressed sparese column
  * Diagnal
  * ELLPACK
  * Hybrid (ELLPACK + Coordinates)
  * Orthogonal linked list
* Implement a hash table. 
  * How do you hash the keys and how do you handle the conflictions? 

---

## Basic data structures
Objective: Understanding the principles of basic data structures, and knowing when to use them. 
### Linked list
* Singly linked list
* Doubly linked list
* XOR linked list

---
Excercises
* Use arrays to implement linked lists. 
  * Append a node into a given list.
  * Insert a node after a given node. 
  * Remove a node from a given stack.
  * Empty a list. 
* Use pointers or references to implement linked lists.
* Implement undo/redo functionality(or back/forward navigation in explorer). 
* Revert a given linked list(unless otherwise specified, linked lists refer to sigly linked list of number)
* Find $n$'th node from the end of a given linked list. 
* Find the middle node of a given linked list. 
* Sort a given linked list.
  * If you get stucked on this problem, you may also try the following problems first. 
  * Find and delete a specified node in a given linked list.
  * Swap two nodes on a given linked list.
  * Implement **bubble sort** on linked lists. 
  * Given an ordered linked list, insert a new number without destroying its order. 
  * Implement **insertion sort** on linked lists. 
  * Given a linked list, divide them into two even halves.
  * Given two ordered linked lists, merge them into one ordered linked list. 
  * Implement **merge sort** on linked lists. 
  * Given a linked list, divide them into two halves(might not be even) and meanwhile let each number in the first half be greater than all numbers in the second half.
  * Implement **quick sort** on linked lists.
* Given a linked list(assume it is), tell whether there is a loop and find the entry of it.
* Given two linked list, tell whether and where they intersect each other. What if there can be loops?

---

### Stack

---
Excercises
* Use array to implement stacks. 
  * Push a node into a given stack.
  * Pop a node from a given stack.
  * Peak the top node of a given stack.
  * Empty a given stack. 
* Use pointers or references to implement stacks. Including the operations above. 
* Given a sequence of push operations and a sequence of pop operations, tell whether it can be valid.
* Implement a queue supporting `push()`. `pop()` and `getMin()`. 
* Without recursion, use backtracking to solve [n queens problem](https://en.wikipedia.org/wiki/N_queens_problem). 
* Based on the expression evaluator above, add $\times$ and $\div$ support. 
* Based on the expression evaluator above, add brackets support. 
---
### Queue

---
Excercises
* Use arrays to implement queue. 
  * Enqueue a node into a given queue.
  * Dequeue a node from a given queue.
  * Empty a queue. 
* Use pointers or references to implement linked lists.
* Given a sequence of enqueue operations and a sequence of dequeue operations, tell whether it can be valid.
* Implement a queue supporting `enqueue()`. `dequeue()` and `getMin()`. 
  * Hint: You may first think of implementing a queue with stacks. 
* Implement a circular buffer. // *TODO: Better problem needed*
* Implement a message queue. // *TODO: Better problem needed*

---

### Tree

---
Excercises
* Explain binary tree, full binary tree, complete binary tree.
* Given the root node of a tree, print its pre-order traversal, in-order traversal, post-order traversal and level-order traversal. 
  * Same problem, without recursion. 
* Given the post-order traversal and in-order traversal of a tree, print its pre-order traversal.
* Given a tree with a in-order traversal of which the data are in increasing order, i.e. BST, insert a new node while keeping this property.
  * Implement a sorting algorithm with it (tree sort). 
* Given $n$, how many structurally unique BST's (binary search trees) that store values $1\ldots n$? 
  * Hint: Catalan Number. 
* Analyze the complexity of BST, tell in which situation it behaves bad. 
* Implement a binary heap.
  * Consider a complete binary tree. Can it be properly stored in an array? How to get parent / child node of a given node?
  * If every node of this tree either has no parent (it is the root! ) or the datum of its parent is larger than its, it is called a heap. Can you insert a new node, and keep its properties (complete binary tree, parent datum larger than children datum)?
  * If the root node is removed, can you transform the rest nodes into a heap? 
  * Implement a sorting algorithm with it (heap sort). 
* Given a tree (no root node specified), print its diameter.
  * The diameter of a tree ($T=\left(V, E\right)$) is defined as $max_{u,v\in V}\delta\left(u, v\right)$, which means, the length of longest path among all shortest paths between all vertices. 
* Given a set of strings, find them in a text.
  * Hint: Aho-Corasick algorithm
* Construct Huffman tree with a given set of nodes and their weights. 

---

### Graph

---
* Store a graph with:
  * Adjacency matrix
  * Adjacency list
* Explain the possible meaning of powers of adjacency matrices.
* Calculate shortest paths from a source node $s$ to a target node $t$ in a given graph.
  * Hint: DFS, BFS, Bidirectional BFS, Dijkstra, Bellman-ford, etc.
  * Compare their complexity and tell what kind of graphs fit them best. 
* Calculate shortest paths from a source node $s$ to every other node in a given graph.
* Calculate shortest paths from every node to every other node in a given graph.
  * Floyd-Warshall
* Generate minimum spanning tree of a given graph.
  * Prim, Krustal, etc.

---
