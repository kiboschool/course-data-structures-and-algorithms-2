# Priority Queues

Now that we've finished talking about data dictionaries in the form of search trees and hash tables, let's turn our attention to a new kind of ADT: the *priority queue*.

A priority queue is a data structure where each element has an associated *priority*. The priority of an element determines the order in which the element will be removed from the queue. In a *max* priority queue, the element with the maximum priority would be the first to be removed, the element with the next maximum priority would be removed second, etc. For example:

<center>
<img
  src="/images/week-03/dsa2-week3-priority-queue.png"
  alt="Three objects getting inserted into an initially empty priority queue: order #4300 (priority 20), order #4301 (priority 15), and order #4302 (priority 25). Once inserted, order #4302 is at the top of the priority queue, followed by order #4300, followed by order #4301."
  style="width:650px;" />
</center>

There is also a *min* priority queue variation, where the element with the minimum priority would be the first to be removed, etc.

Priority queues are useful for a number of applications, including:

* Scheduling a shared resource, such as the CPU: give some processes a higher priority so that they will be scheduled first
* Huffman encoding: at every step of forming the Huffman tree, you need to know the next two nodes with the highest frequencies; this could be implemented using a priority queue.
* Traffic prioritization: when network bandwidth is limited, packets are prioritized according to their priority, and higher priority packets are sent first

## Operations of a PQ

The priority queue ADT generally calls for the following operations:

* `insert(item, priority)`: insert an item with a given priority into the queue
* `remove()`: remove the maximum priority item from the queue
* `peek()`: return the maximum priority element (and/or the priority itself) without actually removing the element

Notice that these operations are very similar to the operations of the queue and stack ADTs that we learned about in a previous course. Indeed, a priority queue is a generalization of the concepts of queues and stacks -- it just makes the priority of each element explicit. In a stack, the priority of an element is related to how recently it was added -- more recently added items have higher priorities.

<aside>
<b>Check your understanding</b>
<p>Say that we implemented a queue using a priority queue. How would you define the priority of each item?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> In a queue, the items that are inserted <i>first</i> have the highest priorities, and the priority decreases with every successive item that is inserted. So the priority of the first element would be some maximum value, and then you could monotonically decrease the priority with every successive item inserted into the priority queue.</p>
</details>
</aside>

## Implementing a PQ

There are various ways that we could implement the PQ ADT using the data structures we have at our disposal. Here are some options:

### Unsorted array or linked list

With an unsorted array or linked list, every time the `insert()` operation is called, we could just append the new item onto the end of the data structure. Generally speaking, this should take only `O(1)` time, although in the case of an array we might need to occasionally resize the array.

However, when we go to `remove()` the element with the maximum priority, we would need to do an `O(n)` pass over the array or linked list to (a) find the element and (b) remove it, closing any gaps in the elements by shifting as needed. Even though insertion is very efficient, removal is quite inefficient.

### Sorted array or linked list

Perhaps if we maintain a sorted list, then we could do better! If we kept an array or linked list sorted by the priorities, then we could always know that the maximum priority is always at the beginning of the list (or end of the list, depending on how you want to implement it). We could therefore easily implement the `remove()` operation in `O(1)` time.

<aside>
<b>Check your understanding</b>
<p>What would be the big-O running time of <code>insert()</code> for a sorted array or linked list?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> When performing an insertion, it would take <code>O(n)</code> to maintain the array or linked list in sorted order. A linked list would require an <code>O(n)</code> pass, starting from the beginning of the list. Maintaining sortedness in an array also takes time <code>O(n)</code>, since although you could use binary search to quickly find the location (by priority) of the new element, it would still take <code>O(n)</code> time to move all of other items over by one position to make room.</p>
</details>
</aside>

Linear data structures seem to always require `O(n)` time, one way or another. Could we do better with a binary search tree?

### Balanced BST

If we use a balanced BST, with priorities as the keys and items as the values, then we could implement the priority queue in logarithmic time: it takes time `O(logn)` to insert a new (priority, item) pair. Removal also takes `O(logn)` time, since although we could always maintain a reference to the maximum priority in the tree for quick access, the operation of removing requires re-balancing the tree, which takes time `O(logn)`. While this is better in some ways than the `O(n)` time required by the linear data structures, it's still not ideal.

Instead, what we need is a new abstraction: a heap.
