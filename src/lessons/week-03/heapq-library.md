# heapq Library

So far, we've built our own `Heap` class to illustrate the basic algorithms behind heaps. However, there are heap libraries available for you to use in Python as well.

One option is the `heapq` module, which provides functionality for a min-at-top heap. In this lesson, we'll cover the three main functions of `heapq`: `heappush()`, `heappop()`, and `heapify()`.

## heappush()

The `heappush()` function adds an element to the heap while maintaining the heap invariant. For example:

```python
import heapq

heap = []
heapq.heappush(heap, 4)
heapq.heappush(heap, 1)
heapq.heappush(heap, 7)
print(heap)  # Output: [1, 4, 7]
```

Notice that the "heap" is just a list, but the `heapq` library manages the list to enforce heap properties. After adding the three elements to the list, the list is `[1, 4, 7]`, representing a complete tree where `1` is the root node and `4` and `7` are its left and right children, respectively.

<aside>
<b>Check your understanding</b>
<p>The <code>heapq</code> library implements a min-at-top heap. How could you use <code>heapq</code> if you needed a max-at-top heap?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> To use <code>heapq</code> as a max-at-top heap, you can negate the priorities as you insert them. For example, instead of priorities 4, 1, and 7 as shown above, you would insert priorities -4, -1, and -7. Then, the -7 would be at the top of the heap, which represents the item with the maximum priority.</p>
</details>
</aside>

Note that you can also use this library to insert tuples, where the first element of the tuple is the priority, and the second element is some associated data:

```python
import heapq

heap = []
heapq.heappush(heap, (4, 'hello'))
heapq.heappush(heap, (1, 'world'))
heapq.heappush(heap, (7, 'foo'))
print(heap)  # Output: [(1, 'world'), (4, 'hello'), (7, 'foo')]
```

## heappop()

The `heappop()` function removes and returns the smallest element from the heap. After removal, it rearranges the remaining elements to maintain the heap structure.

```python
import heapq

# Construct a heap.
heap = []
heapq.heappush(heap, (4, 'hello'))
heapq.heappush(heap, (1, 'world'))
heapq.heappush(heap, (7, 'foo'))

print(heapq.heappop(heap))  # Output: (1, 'world')
print(heap)  # Output: [(4, 'hello'), (7, 'foo')]
```

When `heappop()` is called, the minimum element from the heap is removed, and the rest of the heap is maintained.

## heapify()

The `heapify()` function transforms an arbitrary list into a heap. For example:

```python
import heapq

heap = [(7, 'foo'), (1, 'world'), (4, 'hello')]
heapq.heapify(heap)
print(heap)  # Output: [(1, 'world'), (4, 'hello'), (7, 'foo')]
```

The `heapify()` function uses the same heap construction algorithm that we studied, which builds a heap in linear time.

## Example Problem

Now, let's apply what we've learned to solve a problem. Suppose we have a list of integers and we want to find the `k` smallest elements. We can use a heap to efficiently find these elements.

```python
import heapq

def k_smallest_elements(nums, k):
    smallest = []
    heapq.heapify(nums)
    for i in range(k):
        smallest.append(heapq.heappop(nums))
    return smallest

# Example usage:
nums = [5, 8, 2, 10, 3, 6]
k = 3
print(k_smallest_elements(nums, k))  # Output: [2, 3, 5]
```

The function heapifies the input list, and then calls `heappop()` `k` times to find the `k` smallest elements as it adds them to a list.
