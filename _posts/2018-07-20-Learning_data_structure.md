# Learn Data Structures by Practicing Part I
The structure of this article is derived from [here](https://en.wikipedia.org/w/index.php?oldid=850927589). However the organization of this wikipedia article is a mess. It need to be updated urgently in order not to mislead the newbies. 

## Data types
### Primitive types
Objectives: Knowing how the data are stored, exploiting intrinsic features of it and avoid making mistakes. 
* You should be able to declare, assign, read or print variables of these types. 
* You should be able to apply possible operators to variables of these types and predict the results. 
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
* Given a string of a heximal number(might not be an integer), print it in decimal form.
* Write a programm of encryption and decryption of Caesar ciphering.
* Name algorithms of string searching and compare their advantages and disadvantages. 
* Implement a expression evaluator supporting decimal numbers(with or without seperator), $+$ and $-$. 

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
* Use pointers or references to implement linked lists. 
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
  * Clear a given stack. 
* Use pointers or references to implement stacks. Including the operations above. 
* Given a sequence of push operations and a sequence of pop operations, tell whether it can be valid.
* Based on the expression evaluator above, add $\times$ and $\div$ support. 
* Based on the expression evaluator above, add brackets support. 

---
### Queue

*[[Bit array]]
*[[Circular buffer]]
*[[Lookup table]]
*[[Sparse matrix]]

*[[Skip list]]
{{main|Tree (data structure)}}

=== Binary trees ===
*[[AA tree]]
*[[AVL tree]]
*[[Binary search tree]]
*[[Binary tree]]
*[[Cartesian tree]]
*[[Left-child right-sibling binary tree]]
*[[Order statistic tree]]
*[[Pagoda (data structure)|Pagoda]]
*[[Randomized binary search tree]]
*[[Red–black tree]]
*[[Rope (computer science)|Rope]]
*[[Scapegoat tree]]
*[[Self-balancing binary search tree]]
*[[Splay tree]]
*[[T-tree]]
*[[Tango tree]]
*[[Threaded binary tree]]
*[[Top tree]]
*[[Treap]]
*[[WAVL tree]]
*[[Weight-balanced tree]]

=== B-trees ===
*[[B-tree]]
*[[B+ tree]]
*[[B*-tree]]
*[[B sharp tree]]
*[[Dancing tree]]
*[[2-3 tree]]
*[[2-3-4 tree]]
*[[Queap]]
*[[Fusion tree]]
*[[Bx-tree Moving Object Index|Bx-tree]]
*[[AList]]

=== Heaps ===
*[[Heap (data structure)|Heap]]
*[[Binary heap]]
*[[B-heap]]
*[[Weak heap]]
*[[Binomial heap]]
*[[Fibonacci heap]]
*[[AF-heap]]
*[[Smoothsort|Leonardo Heap]]
*[[2-3 heap]]
*[[Soft heap]]
*[[Pairing heap]]
*[[Leftist tree|Leftist heap]]
*[[Treap]]
*[[Beap]]
*[[Skew heap]]
*[[Ternary heap]]
*[[D-ary heap]]
*[[Brodal queue]]

=== Trees ===
In these data structures each tree node compares a bit slice of key values.
*[[Trie]]
*[[Radix tree]]
*[[Suffix tree]]
*[[Suffix array]]
*[[Compressed suffix array]]
*[[FM-index]]
*[[Generalised suffix tree]]
*[[B-trie]]
*[[Judy array]]
*[[X-fast trie]]
*[[Y-fast trie]]
*[[Merkle tree]]
*[[Ctrie]]

=== Multiway trees ===
*[[Ternary tree]]
*[[K-ary tree]]
*[[And–or tree]]
*[[(a,b)-tree]]
*[[Link/cut tree]]
*[[SPQR-tree]]
*[[Spaghetti stack]]
*[[Disjoint-set data structure]]
*[[Fusion tree]]
*[[Enfilade (Xanadu)|Enfilade]]
*[[Exponential tree]]
*[[Fenwick tree]]
*[[Van Emde Boas tree]]
*[[Rose tree]]

=== Space-partitioning trees ===
These are data structures used for [[space partitioning]] or [[binary space partitioning]].
*[[Segment tree]]
*[[Interval tree]]
*[[Range tree]]
*[[Bin (computational geometry)|Bin]]
*[[K-d tree]]
*[[Implicit k-d tree]]
*[[Min/max kd-tree|Min/max k-d tree]]
*[[Relaxed k-d tree]]
*[[Adaptive k-d tree]]
*[[Quadtree]]
*[[Octree]]
*[[Linear octree]]
*[[Z-order (curve)|Z-order]]
*[[UB-tree]]
*[[R-tree]]
*[[R+ tree]]
*[[R* tree]]
*[[Hilbert R-tree]]
*[[X-tree]]
*[[Metric tree]]
*[[Cover tree]]
*[[M-tree]]
*[[VP-tree]]
*[[BK-tree]]
*[[Bounding interval hierarchy]]
*[[Bounding volume hierarchy]]
*[[BSP tree]]
*[[Rapidly exploring random tree]]

=== Application-specific trees ===
*[[Abstract syntax tree]]
*[[Parse tree]]
*[[Decision tree]]
*[[Alternating decision tree]]
*[[minmax|Minimax tree]]
*[[Expectiminimax tree]]
*[[Finger tree]]
*[[Expression tree]]
*[[Log-structured merge-tree]]
*[[Lexicographic Search Tree]]

== Hashes ==
*[[Bloom filter]]
*[[Count-Min sketch]]
*[[Distributed hash table]]
*[[Double hashing]]
*[[Dynamic perfect hashing|Dynamic perfect hash table]]
*[[Hash array mapped trie]]
*[[Hash list]]
*[[Hash table]]
*[[Hash tree (disambiguation)|Hash tree]]
*[[Hash trie]]
*[[Koorde]]
*[[Prefix hash tree]]
*[[Rolling hash]]
*[[MinHash]]
*[[Quotient filter]]
*[[Ctrie]]

== Graphs ==
*[[Graph (data structure)|Graph]]
*[[Adjacency list]]
*[[Adjacency matrix]]
*[[Graph-structured stack]]
*[[Scene graph]]
*[[Binary decision diagram]]
*[[Zero-suppressed decision diagram]]
*[[And-inverter graph]]
*[[Directed graph]]
*[[Directed acyclic graph]]
*[[Propositional directed acyclic graph]]
*[[Multigraph]]
*[[Hypergraph]]

== Other ==
*[[Lightmap]]
*[[Winged edge]]
*[[Quad-edge]]
*[[Routing table]]
*[[Symbol table]]
