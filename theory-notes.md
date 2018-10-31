### Call stacks are often special cases of singly-linked lists.

Each stack frame holds:

- a return address, the **link**, *and*
- local (automatic) variables, the **data**.

The list is build from tail to head as functions are called, and correspondingly dismantled from head to tail as they return.

### Immutable singly linked lists work as space-saving "copyable" stack data structures.

To push, make a new list with the old list as its tail. To pop, advance to the tail. Each case requires only constant time and space, and can be done independently and concurrently without any corruption of state.

### A doubly linked list can be traversed in either direction without extra space.

The only auxiliary space required to traverse a double linked list in reverse is the the space needed to hold a pointer to the current node in the list--just like if one traverses it forward. The back pointers are topologically indistinguishable from the forward pointers.

If one traverses forward some number of links in a doubly linked list, it's *not* necessary (and would typically be useless) to use recursion or a stack data structure to remember where to get back to. Just keep track of how far you went, and follow the back pointers that number of times.

### Reverse traversal of a singly-linked list using recursion or a stack data structure is effectively building the list (or part of it) in reverse.

One way to traverse a singly-linked list in reverse is to recurse to node where you wish to start, and then visit the precending nodes in "postorder," i.e., while retreating.

With recursion in most languages, this is only safe if the porton of the list being used is short; otherwise it may overflow the call stack. But using a stack data structure instead of the call stack lifts this restriction.

If that stack data structure is itself a singly-linked list, then the portion of the list being traversed backwards is built up as a singly linked list. This is what the common iterative algorithm to reverse a singly linked list does.

Whenever one uses recursion or a stack data structure to visit nodes in a singly linked list in reverse, one is effectively building a reversed copy of that section of the list (without its stored data).

These data, taken together with the original list, are like a (transient) doubly-linked list.

### Overlapping stacks, implemented as immutable singly-linked lists, form an "upside-down" tree.

These are singly-linked lists that share suffixes. Considered together, they consistute a tree with *only* parent pointers (and no child pointers).

### Depth-first traversal of a *binary* tree whose nodes contain parent pointers requires only constant auxiliary space.

In addition to the space to remember what node we are currently on, we must remember where we just were so we know whether to traverse right or to retreat, but this is still O(1) extra space.

Rather than needing recursion or a stack data structure to keep track of the path we took so we can retreat, we just follow the parent pointers.

(In an n-ary tree with parent pointers, we *could* similarly keep track of where we were and traverse it in constant auxiliary space. However, unless each node's children are stored in a data structure that accepts any node and maps it in constant time to its successor sibling, we would pay for this with extra time. If nodes could have many children, the worst-case time complexity would even be quadratic in the size of the tree itself.)

### Depth-first traversal of a binary tree *without* parent pointers requires O(h) auxiliary space.

Without parent pointers, we must keep track of where to retreat to. This is naturally expressed with recursion or a stack data structure and requires auxiliary space proportional to the height of the tree.

This *stack* represents a portion of the corresponding "upside down" tree that has *only* parent pointers. Taken together with the tree being traversed, these are like a (transient) binary tree with parent pointers.
