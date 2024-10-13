# Heap Construction

Say that we have a list of numbers that we want to convert into a heap:

```
[15, 23, 39, 14, 8, 45, 18, 27]
```

To build a heap, we could take this list of random numbers and insert them, one at a time, into an initially empty heap. We know from the previous lesson that each insertion takes time `O(logn)`, and if there are `n` elements, then in the worst case this process takes time `n elements * O(logn) per insertion = O(nlogn)`.

However, this algorithm is not optimal. We can actually do better than `O(nlogn)`!

## Linear-time heap construction

An alternative method to building a heap is to start with all of the elements we want to insert in a complete tree. For example, we would represent the above list as the following complete tree:

<center>
<img
  src="/images/week-03/dsa2-week3-buildheap.png"
  alt="A complete tree with the following list added in level order: [15, 23, 39, 14, 8, 45, 18, 27]."
  style="width:425px;" />
</center>

Then, we use the following algorithm:

- Find the parent of the last child node.
- Sift down the parent as much as needed to obey the heap property. Remember that if both children are greater than the parent, the parent should be swapped with the greater of the two.
- Proceed to the rest of the nodes in the same level, from right to left. Sift them down as needed.
- Proceed to the next level up in the complete tree, moving from right to left and sifting them down as needed.
- Continue through the rest of the remaining levels.

Watch the following video to see an example of this algorithm:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/SSRu6kjdiuU"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

<aside>
<b>Check your understanding</b>
<p>Consider the following list representation of a complete tree:</p>
<center>
<img
  src="/images/week-03/dsa2-week3-example-array.png"
  alt="An example array that can be interpreted as a complete tree."
  style="width:400px;" />
</center>
<p>Build a heap from this list using the algorithm above.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Interpreting the list as a complete tree, we get the following representation:</p>
<img
  src="/images/week-03/dsa2-week3-buildheapexample.png"
  alt="The complete tree version of the list [26, 12, 32, 24, 18, 28, 47, 10, 9]."
  style="width:275px;" />
<p>The parent of the last leaf node is the 24, which is greater than both of its children so it doesn't need to be sifted. We next consider the 32. The 47 is greater than 32, so the 32 must be sifted down. We next consider the 12. The 24 is greater than 12, so the 12 must be sifted down. However, the 12 is greater than both of its children (the 10 and the 9), so it can stay where it is. Finally, we consider the 26, which is less than both of its children. The largest child is the 47, so we swap the 26 and the 47. We then sift the 26 down further, swapping the 26 and the 32. When finished, the heap looks like this:</p>
<img
  src="/images/week-03/dsa2-week3-buildheapexample-done.png"
  alt="The heap after the heap construction algorithm as described above."
  style="width:275px;" />
</details>
</aside>

This algorithm actually works in `O(n)` time! But how?

## Explanation of efficiency

Let's make an informal argument for why this heap construction method only takes linear time.

### Half the nodes are leaf nodes

First, let's think about how many nodes there are in each level of a complete tree:

| Level          | Number of nodes                  |
|----------------|----------------------------------|
| <code>0</code> | <code>1</code>                   |
| <code>1</code> | <code>2</code>                   |
| <code>2</code> | <code>4</code>                   |
| <code>3</code> | <code>8</code>                   |
| ...            | ...                              |
| <code>h</code> | <code>2<sup>h</sup></code>       |

Also, a complete tree of height `h` has <code>2<sup>(h + 1)</sup> - 1</code> nodes total. For example, a tree of height 2 (which has three levels) has 7 nodes total: 1 in the first level, 2 in the second level, and 4 in the third level.

Therefore, it stands to reason that out of the <code>2<sup>(h + 1)</sup> - 1</code> total nodes in a tree, <code>2<sup>h</sup></code> of them are in the last level (leaf nodes). For example, in a tree of height 4, there are 31 total nodes and 16 of them are leaf nodes!

This means that in a complete tree, roughly half of the nodes are leaf nodes. This is important because in the heap construction algorithm, we skip all of the leaf nodes -- we don't need to consider them for sifting down. We start with the parent of the last leaf node.

## Most nodes are not sifted far

We showed above that approximately half (`~n/2`) of the nodes don't need to be sifted at all because they're leaf nodes. Proceeding with that logic, there are `~n/4` parents of leaf nodes, and although they have to be considered for sifting, they are only sifted at most one level (down into a leaf node).

In fact, the further you work your way up in the tree, there are fewer and fewer nodes that need to be sifted throughout the height of the tree. The root node is the only node that needs to potentially be sifted throughout the full height `h` of the tree!

In other words, the time that you spend sifting a few elements throughout the height of tree is offset by the many nodes that are sifted only a small number of levels or are not sifted at all. Although we won't get into the mathematical argument for this, it turns out that by this argument, the running time of heap construction is `O(n)`!

## Code for heap construction

Up to this point, we have been using a definition of the `Heap` class that has a fairly simple constructor:

```python
class Heap:
    def __init__():
        self.contents = []
        self.num_items = 0
```

However, we could also use a version of the constructor that accepts a list `contents` as a parameter, and builds a heap based on that list. For example:

```python
    def __init__(self, contents):
        self.contents = contents
        self.num_items = 0
        self.__make_heap()

    def __make_heap(self):
        if len(self.contents) == 0:
            return
        last = len(self.contents) - 1
        parent_of_last = (last - 1) // 2
        for i in range(parent_of_last, -1, -1):
            self.__sift_down(i)
```

The `__make_heap()` method implements the algorithm described above for starting with the parent of the last leaf node, and repeatedly sifting down each element as needed in order to construct a heap.

In case it's helpful, here's an entire implementation of the `Heap` class for your reference:

```python
class Heap:
    def __init__(self, contents):
        self.contents = contents
        self.num_items = len(contents)
        self.__make_heap()

    def __make_heap(self):
        if len(self.contents) == 0:
            return
        last = len(self.contents) - 1
        parent_of_last = (last - 1) // 2
        for i in range(parent_of_last, -1, -1):
            self.__sift_down(i)

    def insert(self, item):
        self.contents.append(item)
        self.__sift_up(self.num_items)
        self.num_items += 1

    def remove(self):
        if self.num_items == 0:
            return None

        to_remove = self.contents[0]
        self.contents[0] = self.contents[self.num_items - 1]
        self.contents.pop()
        self.num_items -= 1
        if self.num_items > 0:
            self.__sift_down(0)
        return to_remove

    def is_empty(self):
        return self.num_items == 0

     # to_string - create a string representation of the heap of the form
     # { ( root ) ( items in level 1 ) ( items in level 2 ) ... }
    def to_string(self):
        string = '{ '

        start = 0
        level_size = 1
        while start < self.num_items:
            # print all of the items at the current level of the tree
            string += '( '
            i = start
            while i < start + level_size and i < self.num_items:
                string += (self.contents[i] + ' ')
                i += 1
            string += ') '

            # move down to the next level
            start += level_size
            level_size *= 2

        string += '}'
        return str

    def __sift_down(self, i):
        # Store a reference to the element being sifted.
        to_sift = self.contents[i]

        # Find where the sifted element belongs.
        parent = i
        child = 2 * parent + 1
        while child < self.num_items:
            # If the right child is bigger, compare with it.
            if child < self.num_items - 1 and self.contents[child] < self.contents[child + 1]:
                child = child + 1

            # Check if we're done.
            if to_sift >= self.contents[child]:
                break

            # If not, move child up and move down one level in the tree.
            self.contents[parent] = self.contents[child]
            parent = child
            child = 2 * parent + 1

        self.contents[parent] = to_sift

    def __sift_up(self, i):
        # Store a reference to the element being sifted.
        to_sift = self.contents[i]

        # Find where the sifted element belongs.
        child = i
        while child > 0:
            parent = (child - 1) // 2

            # Check if we're done.
            if to_sift <= self.contents[parent]:
                break

            # If not, move parent down and move up one level in the tree.
            self.contents[child] = self.contents[parent]
            child = parent

        self.contents[child] = to_sift
```
