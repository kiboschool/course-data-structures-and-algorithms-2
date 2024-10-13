# Practice

Here is a selection of practice problems from LeetCode involving heaps.

* [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array)
    * Note that for this problem, you will need to use a max-at-top heap.
* [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency)
* [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists)
    * Note that for this problem, you will need to use a min-at-top heap.

In these problems, you might find it helpful to use either the `heapq` module, or the following `Heap` class:

```python
    class Heap:
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

You can copy and paste this `Heap` class directly into your code as an inner, nested class. You can then use it like:

```python
h = Solution.Heap([])
h.insert(50)
h.insert(20)
h.insert(75)
print(h.remove())
```
