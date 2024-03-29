<!-- SPDX-License-Identifier: CC0-1.0 -->

# Theory Notes

### Call stacks are often implemented as special cases of singly-linked lists.

In such an implementation, each stack frame holds:

- a return address, the **link**, *and*
- local (automatic) variables, the **data**.

The list is built from tail to head as functions are called, and correspondingly dismantled from head to tail as they return.

### Immutable singly linked lists work as space-saving &rdquo;copyable&rdquo; stack data structures.

To push, make a &rdquo;new&rdquo; list with the old list as its tail, by creating a node that points to the old head node and updating your head pointer to point to it. To pop, advance your head pointer to the tail (i.e., by one node). Each case requires only *O(1)* (i.e., constant) time and space, and can be done independently and concurrently without any corruption of state. (You need separate head pointers, but not separate list nodes.)

### A doubly linked list can be traversed in either direction with only *O(1)* extra space.

The only auxiliary space required to traverse a doubly linked list in reverse is the space needed to hold a pointer to the current node in the list--just like traversing it forward. A doubly linked list&rsquo;s back pointers are topologically similar to its forward pointers. In many implementations, which ones are regarded to be which is merely a matter of convention.

If one traverses forward some number of links in a doubly linked list, it&rsquo;s *not* necessary (and would typically be useless) to use recursion or a stack data structure to remember where to get back to. Just keep track of how far you went, and follow the back pointers that number of times.

### Reverse traversal of a singly-linked list using recursion or a stack data structure is effectively building the list (or part of it) in reverse.

One way to traverse a singly-linked list in reverse is to recurse to the node where you wish to start, and then visit the preceding nodes in &rdquo;postorder,&rdquo; i.e., while retreating.

With recursion in most languages, this is only safe if the portion of the list being used is short; otherwise it may overflow the call stack. But using a stack data structure instead of the call stack lifts this restriction.

If that stack data structure is itself a singly linked list, then the portion of the list being traversed backwards is built up at the head to produce a reversed list corresponding to part or all of the original list. This is what the common iterative algorithm to reverse a singly linked list does.

Whenever one uses recursion or a stack data structure to visit nodes in a singly linked list in reverse, one is effectively building a reversed copy of that section of the list (without its stored data). These data, taken together with the original list, are like a (transient) doubly-linked list.

### Overlapping stacks, implemented as immutable singly-linked lists, form an &rdquo;upside-down&rdquo; tree.

These are singly-linked lists that share suffixes. Considered together, they constitute a tree with *only* parent pointers (and no child pointers).

### Depth-first traversal of a *binary* tree whose nodes contain parent pointers requires only constant auxiliary space.

In addition to the space to remember what node we are currently on, we must either remember where we just were so we know whether to traverse right or to retreat (or we can retreat and advance in a single step, which is equivalent). But this is still *O(1)* extra space.

Rather than needing recursion or a stack data structure to keep track of the path we took so we can retreat, we just follow the parent pointers.

(In an *n-ary* tree with parent pointers, we *could* similarly keep track of where we were and traverse it in constant auxiliary space. However, unless each node&rsquo;s children are stored in a data structure that accepts any node and maps it in constant time to its successor sibling, we would pay for this with extra time. If nodes could have many children, the worst-case time complexity would even be quadratic in the size of the tree itself.)

### Depth-first traversal of a binary tree *without* parent pointers requires *O(h)* auxiliary space.

Without parent pointers, we must keep track of where to retreat to. This is naturally expressed with recursion or a stack data structure and requires auxiliary space proportional to the height of the tree.

This *stack* represents a portion of the corresponding &rdquo;upside down&rdquo; tree that has *only* parent pointers. Taken together with the tree being traversed, these are like a (transient) binary tree with parent pointers.
