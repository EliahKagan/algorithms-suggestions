<!-- SPDX-License-Identifier: CC0-1.0 -->

# Suggested Exercises

Define and write tests for (warmup):

- a function to print a vector, of anything printable, on a line.
- a function to sort a vector of int (can use `std::sort`).
- a function to sort a vector of int, but puts all odds before all evens.
- a function to find the index of an element in a vector if present.
- *\[optional\]* a function to sort a vector using insertion sort.
- *\[optional\]* a function to sort a vector using recursive mergesort.
- *\[optional\]* a function to sort a vector using iterative mergesort.
- *\[optional\]* (benchmark all 3, and `std::sort`, with `std::chrono` facilities.)

---

Define and write tests for (object pool):

- a class template providing an expanding (but not contracting) object pool.

---

Define and write tests for (singly linked lists - creation and traversal):

- a singly linked list node type.
- a function to construct a singly linked list from a vector.
- a function to determine the size of a singly linked list.
- a function to construct a vector from a singly linked list.
- a function to find a value, if present, in a singly linked list.
- *\[optional\]* a function to remove the node with the smallest element.
- *\[optional\]* a function that tells if a list is sorted.
- *\[optional\]* a function to break a list into two halves as close as possible to the middle.
- *\[optional\]* a function to concatenate two lists.
- *\[optional\]* a function to build `vector<Lnode<T>*>`<sup>1</sup>, `std::sort` it by element values, and relink.

<sub><sup>**1**</sup> With whatever the singly list node type was called, in place of `Lnode`.</sub>

---

Define and write tests for (singly linked lists - other common operations):

- a function to compare singly linked lists for sequence equality.
- a function to copy a singly linked list.
- a function to reverse a singly linked list by rearranging its nodes.
- a function to split a list into two lists based on matching a predicate.
- a function to merge two sorted linked lists in sorted order.
- *\[optional\]* a function to sort a singly linked list with insertion sort.
- *\[optional\]* a function to sort a singly linked list with recursive mergesort.
- *\[optional\]* a function to sort a singly linked list with iterative mergesort.
- *\[optional\]* (these sorting functions should use no more than *O(log n)* auxiliary space.)
- *\[optional\]* (benchmark all 3, and `std::sort`+relinking, with `std::chrono` facilities.)

---

Define and write tests for (singly linked lists - topology and cycle detection):

- a function that checks if a singly linked list has a cycle.
- a function that checks if two singly linked lists share any nodes.
- (both hash-based and constant auxiliary space implementations.)

---

Define and write tests for (binary trees - creation and traversal):

- a binary tree node type (without parent pointers).
- a helper function object to make trees like `f(4, f(3, {}, {}), f(5, {}, {}))`.
- a function to determine the size of a binary tree.
- a function to construct a vector from a binary tree, in any order.
- a function to find a value&rsquo;s node, if present, in a binary tree.
- preorder, inorder, and postorder traversal *(a)* to print and *(b)* applying a function object.
- iterative preorder traversal and level-order traversal.
- iterative inorder and postorder traversal.
- a function to determine the height of a binary tree by iterative DFS.
- iteratively implemented recursive preorder, inorder, and postorder algorithms.
- *\[optional\]* a function to compute the sum all of elements in a tree.
- *\[optional\]* a function to find the maximum of that sum over all subtrees *O(n)* - values can be negative.
- *\[optional\]* right-to-left preorder, inorder, and postorder traversals.
- *\[optional\]* vertical order traversal (following *L* left pointers and *R* right pointers puts you in column *R - L*).

---

Define and write tests for (binary trees - other common or interesting operations):

- a function to find the lowest common ancestor of two nodes, given their values.
- a function to pretty-print a tree.
- a function to check if trees&rsquo; topology and corresponding data are the same.
- a function to copy a tree.
- a function to check if a tree is mirror-symmetric.
- a function to turn a tree into its mirror image by rearranging its nodes.
- *\[optional\]* a function to count the leaves (nodes with no children) of a tree.
- *\[optional\]* a function to tell if a binary tree is a BST (binary search tree).
- *\[optional\]* a function to find the lowest common ancestor of two nodes in a BST.
- *\[optional\]* a function to rearrange a binary tree&rsquo;s nodes into a BST with the same topology.
- *\[optional\]* a function to find the difference in heights between a node&rsquo;s subtrees.
- *\[optional\]* a function to find that difference for all nodes of a tree, in *O(n)* time.
- *\[optional\]* a function to build a tree of unique elements in *O(n)* time, given its preorder and inorder sequences.
- *\[optional\]* functions to serialize/deserialize a tree of (possibly nonunique) ints to/from a file.
- *\[optional\]* a function to emit dot code for a tree so https://en.wikipedia.org/wiki/Graphviz can display it.
- (both recursive and iterative implementations of each of these functions.)

---

Define and write tests for (binary trees - topology/cycle detection/other):

- a function that detects violations of the tree&rsquo;s topological invariant.
    * this will check if there is a cycle or a (nonempty) shared subtree
- a function that detects only violations preventing normal traversal.
    * this will check just for cycles, but NOT for shared subtrees
- *\[optional\]* a function that searches in one tree for a copy of another.
- *\[optional\]* a function to copy a tree, with all duplicate subtrees shared in the copy.
- (both recursive and iterative implementations of each of these functions.)

---

Write functions/types to (undirected graphs - representation and connectivity):

- given (undirected, unweighted) edges, build an adjacency list.
- given edges, report if there is a (undirected) cycle.
- given edges and *{u, v}* queries, report if vertices *u* and *v* are connected.
- given edges, report the number and size of components.
- given edges, report if the graph is bipartite.
- construct minimum spanning tree/forest via Kruskal&rsquo;s algorithm.
- *\[optional\]* construct a spanning tree that minimizes the product of edge weights.
- (use BFS, iterative and recursive DFS, and union-find, wherever applicable.)
