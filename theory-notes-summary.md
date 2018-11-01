1. Call stacks are often special cases of singly linked lists.
2. Immutable singly linked lists provide space-saving "copyable" stack data structures.
3. Reverse traversal of a singly linked list using recursion or a stack data structure is effectively building the list (or part of it) in reverse. Taken together, these are like a (transient) doubly linked list.
4. Overlapping stacks implemented as immutable singly linked lists, considered together, form an "upside down" tree: they are a tree with *only* parent pointers (no child pointers).
5. Depth-first traversal of a *binary* tree *with* parent pointers needs just O(1) auxiliary space to remember where we were.
6. Depth-first traversal of a binary tree *without* parent pointers needs O(h) auxiliary space to remember where to retreat to. This *stack* represents (part of) the corresponding tree that has *only* parent pointers. Taken together, these are like a (transient) binary tree with parent pointers.
