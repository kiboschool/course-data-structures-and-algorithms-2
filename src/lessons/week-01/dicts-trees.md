# Dictionaries and trees

At the very end of the previous course, we left off by describing the concept of *data dictionaries* -- data structures that are purpose-built for storing and looking-up data. There are many different kinds of data dictionaries, and many forms of search algorithms, including linear search, binary search, and binary search trees.

## Linear search

Perhaps the simplest way of implementing a data dictionary would be to store all of our data in an array, and iterate over that array when searching for an item. However, if we don't know anything about the position of a desired item, then we have no choice except to look at all items, which makes linear search an `O(n)` algorithm.

## Binary search

However, we can search much faster if we keep the items of the array in sorted order. If the items are ordered, then we can use binary search to more quickly "jump" to positions in the array. This significantly cuts down on the number of items we need to inspect when searching, which makes binary search an `O(logn)` algorithm.

However, keeping the items of the array in sorted order comes at a cost. When we need to insert a new item, we need to move all elements that come after the newly-inserted item. This takes `O(n)` time, which is not ideal.

<aside>
<b>Check your understanding</b>
<p>We've said previously that a benefit of linked lists is that you can insert an item in <code>O(1)</code> time once you've found the desired position in the list -- there is no shifting required, as in arrays. Does this mean that it's worth it to keep a linked list in sorted order to use binary search?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> No. Although it's a constant time operation to insert an item once the proper position is found, <i>finding</i> the proper position is more expensive in a linked list, since you don't have random access to the elements of the list. In fact, binary search is a poor choice of algorithm for searching in a list, since it requires <code>O(nlogn)</code> time!
</details>
</aside>

## Binary search trees

In order to achieve `O(logn)` lookup time in addition to `O(logn)` insertion time, we can use binary search trees. By using a linked data structure that branches at each junction, we can more quickly perform insertions while still getting the benefits of binary search.

With *balanced* binary search trees, we can additionally guarantee logarithmic time lookup and insertion algorithms. Otherwise, "standard" BSTs can become unbalanced in some cases, leading to linear time complexities.

## What's next?

With linear search, binary search, and binary search trees, our current understanding of the different implementations of data dictionaries at the moment is summarized by this table:

| data structure                                 | searching for an item                                 | inserting an item                                     |
|------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| a list implemented using an array              | `O(logn)` using binary search                           | `O(n)`                                                  |
| a list implemented using a linked list         | `O(n)` using linear search                              | `O(n)`                                                  |
| binary search tree                             | `O(logn)` in best and average cases; `O(n)` in worst case | `O(logn)` in best and average cases; `O(n)` in worst case |
| balanced binary search trees (e.g., 2-3 trees) | `O(logn)` in all cases                                  | `O(logn)` in all cases                                  |

Logarithmic algorithms are quite fast for data dictionaries, and are certainly a significant improvement over linear algorithms. However, we can actually do even *better* with the help of *hash tables*. Believe it or not, we will actually be able to implement search and insertion in `O(1)` time! This will be the topic of our next week of study.
