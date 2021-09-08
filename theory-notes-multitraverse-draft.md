**[Note: This is a draft of a section of `rough-notes.txt` that is currently, and might always be, unsuitable for inclusion in that document. Right now, I think it confuses more than it illuminates, and combines many of the disadvantages of both insufficient and excessive detail. To improve it will require research, and perhaps a rewrite so that it no longer uses C++ as its example language. The technique described here *might* occcasionally be reasonable to do in C++, but I no longer think it&rsquo;s reasonable to *explain* it using C++.]**

### Multiple such traverals (concurrent or interleaved) could share data.

To illustrate the point about building the corresponding tree that has only parent pointers during depth-first traversal, it is useful to consider a situation where more than one path, and possibly even the whole upside-down tree, would need to exist in memory at a time.

In C++, [`std::set`](https://en.cppreference.com/w/cpp/container/set), [`std::multiset`](https://en.cppreference.com/w/cpp/container/multiset), [`std::map`](https://en.cppreference.com/w/cpp/container/map), and [`std::multimap`](https://en.cppreference.com/w/cpp/container/multimap) are typically implemented as [red-black trees](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree) *with parent pointers*. Thus they require only constant auxiliary space for traversal.

But consider how you might implement a cheaply copyable [BidirectionalIterator](https://en.cppreference.com/w/cpp/named_req/BidirectionalIterator) to perform depth-first traversal of a binary tree whose nodes are *not* equipped with parent pointers.

If the iterators needed to be fast to increment (and decrement) and dereference and if they did not need to be cheaply copyable, then each could contain its own full return path, stored in an [`std::stack`](https://en.cppreference.com/w/cpp/container/stack) of tree nodes.

If, instead of a [`std::stack`](https://en.cppreference.com/w/cpp/container/stack), a custom immutable singly linked list were used, then the lists used by iterators derived from one another (as with manual copying, passing by value, and calls to [`std::next`](https://en.cppreference.com/w/cpp/iterator/next) and [`std::prev`](https://en.cppreference.com/w/cpp/iterator/prev)) could be implemented in such a way as to share suffixes automatically.

The iterator object itself could wrap a [`std::shared_ptr`](https://en.cppreference.com/w/cpp/memory/shared_ptr) to a node in a singly linked list. This list node would contain its own `std::shared_ptr` to node after it in the last as well as a reference or raw pointer to the tree node. The list would function as a stack representing the path from the current tree node to the root of the tree. When the iterator would retreat, it would use only the suffix of the linked list that already exists. When it would advance, it would create new linked list nodes, but it would attach them to that suffix and still save some space. Where `p` were such a tree iterator, `std::next(p, k)` would use at most O(k) time and O(k) space, achieving the goal of the iterator being cheaply copyable.

Nodes in the linked list that are unreachable would have their reference count drop to zero and are deterministically destructed by their `shared_ptr` control block. Separate traversals down the tree would produce duplicate prefixes in the list. This could probably be avoided, but with more overhead.

In C++, this may be mostly useful as a conceptual illustration. If you&rsquo;re using C++, you likely care about the speed you would lose by having a `shared_ptr` take a lock every time an iterator is incremented, decremented, or copied. For most cases, this would use more space than the minimal approach of maintaining separate contiguous stacks for each iterator (and possibly using copy-on-write to make pass-by-value acceptably fast). Memory allocations incur bookkeepting, of which there is significantly more with `shared_ptr`, which must allocate memory for its control block. If more aggressive deduplication were attempted using `weak_ptr`, the control blocks would last even longer.

However, in a language that already has garbage collection, the cost of which must usually be paid anyway (modulo any application-specific tuning), this may be a reasonable approach.

*[Look into: Which functional programming languages&rsquo; standard libraries perform tree traversal in a manner similar to this?]*
