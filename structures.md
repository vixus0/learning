Data Structures
===

Dynamic set operations
---

Structures will usually only implement a subset of these for a certain
application.

  * Search (S,k): searches S for value k
  * Insert (S,x): adds element x to the set S
  * Delete (S,x): removes element x from S
  * Min (S): returns the smallest value in ordered set S
  * Max (S): returns the largest …
  * Succ (S,x): returns next largest element to x from ordered set S
  * Pred (S,x): returns next smaller …

Array
---

Linear collection of data, usually stored congruently in memory. Worst storage
complexity O(n). Access by index is O(1), but search/insertion/deletion is O(n)
because array elements need to be iterated through/resized+moved.

Stack
---

LIFO structure. Insertion and deletion are O(1) because we always do so at the
top of the stack. Direct access and search are O(n) because we would need to
iterate backwards from the top of the stack to access elements in order.

*Implementation* An array with a pointer to the top of the stack. Pushing
increments the pointer and sets the value there. Popping returns the value 
pointed at and decrements the pointer.

Queue
---

FIFO structure. Insertion is O(1) since it's always at the tail of the queue and
deletion is O(1) because it's always done at the head. Access and searching are
O(n) because we'd have to iterate from the head/tail to get what we want.

*Implementation* Array with two pointers to head and tail. Enqueuing increments
the tail and sets the value, dequeueing returns the value at head and decrements
the head. The pointers wrap around when the end of the array is reached. If
    
    head = tail + 1

then the queue is full. If

    head = tail

the queue is empty.

Linked lists
---

Collection of objects that contain pointers to the previous (doubly-linked) and
next (singly- and doubly-linked) element of the list. The list also has a
pointer to the head element.

Sorted lists mean the elements are ordered by their keys. If the list is
circular, the tail's next element is the head and the head's previous element
is the tail.

(For unsorted list) search and access are O(n) since the entire 
list may have to be traversed to locate a specific element. Insertion is O(1) 
since we can just put the new element at the head or tail of the list. Deletion
is O(1) if we have a pointer to the element we want to delete. We can use a
dummy object (sentinel) between the actual head and tail of the list to remove
the need for a pointer to the head and to simplify deletions and insertions.
Sentinels increase required memory so shouldn't be used for numerous small
lists.

*Implementation* For languages that have objects and pointers, these are easy to 
implement. However, when we don't have pointers or objects, we need to use
something like multiple arrays, one for each attribute of the objects, or a
single array with the key, prev and next attributes being stored consecutively.

Rooted Trees
---

Trees can be represented much in the same way as linked list except instead of
pointers to the previous/next element, we have pointers to the children and
parent of each element.

Can represent a tree with arbitrary numbers of children in O(n) space by giving
each element two pointers: one to the leftmost child and one to its sibling on
the right. So if a node has no children, `left-child = null` and if a node is the
rightmost child `right-sibling = null`. The node will also have a pointer to its
parent.
