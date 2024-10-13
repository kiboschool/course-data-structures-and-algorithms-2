# Heapsort

Back in our previous data structures course, we talked about various sorting algorithms, including selection sort, insertion sort, mergesort, and radix sort. Here's a summary of the efficiencies of those algorithms:

| Algorithm      | Best case                     | Worst case                    | Space             |
|----------------|-------------------------------|-------------------------------|-------------------|
| Selection sort | <code>O(n<sup>2</sup>)</code> | <code>O(n<sup>2</sup>)</code> | <code>O(1)</code> |
| Insertion sort | <code>O(n)</code>             | <code>O(n<sup>2</sup>)</code> | <code>O(1)</code> |
| Mergesort      | <code>O(nlogn)</code>         | <code>O(nlogn</code>          | <code>O(n)</code> |
| Radix sort     | <code>O(m*n)</code>           | <code>O(m*n)</code>           | <code>O(n)</code> |

We were able to define fairly efficient algorithms in mergesort and radix sort, but both of those algorithms require `O(n)` extra space to work. Can we do better?

## Improving selection sort

Recall *selection sort*. It repeatedly finds the next smallest element in a list, and swaps it into place. It isn't a particularly efficient algorithm though, since for each of `O(n)` elements, it performs an `O(n)` pass over the list to find the next smallest element, leading to a running time of <code>O(n<sup>2</sup>)</code>.

However, we now have a data structure that allows us to efficiently find the next smallest (or largest) item: a heap! Indeed, we will use a heap to implement *heapsort*, which will repeatedly find the next largest item in a list and swap it into its final sorted position.

## Algorithm

Say that we start with an arbitrary list of numbers. We can use heapsort to sort the list with the following high-level algorithm:

1. Turn the list into a heap.
2. Remove the maximum item from the heap and place it at the end of the list. This element is now in its final sorted position. Re-heapify the heap.
3. Repeatedly remove the maximum item from the heap and place it in its final sorted position until all elements have been removed.

Watch the following video to see how heapsort works:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/5DWpYccmrl4"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

## Practice

Consider the following list:

```
[20, 18, 32, 3, 11, 7, 17]
```

Sort the list using heapsort. Show the evolution of the list as it changes in memory.

## Pseudocode for heapsort

Here is some pseudocode for the operation of heapsort. It's actually close to working Python code, but it won't quite work with the implementation of the `Heap` class that we made, since `remove()` actually pops the element from the list (as opposed to just placing it at the end and keeping it there).

```python
def heapsort(lst):
    # Create a new heap from the given list.
    heap = Heap(lst)

    end_unsorted = len(lst) - 1
    while end_unsorted > 0:
        # Get the largest remaining element and put it
        # at the end of the unsorted portion of the array.
        largest_remaining = heap.remove()
        lst[end_unsorted] = largest_remaining
        end_unsorted -= 1
```

A fun challenge could be to make this version of `heapsort()` work with the `Heap` class that we have given you, which would involve keeping the list the same length even as elements are removed.

## Other resources

Here are some other resources for heapsort that you might find helpful:

<iframe width="560" height="315" src="https://www.youtube.com/embed/LbB357_RwlY?si=b7p03u5etpRBX1Ra" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<p></p>
<iframe width="560" height="315" src="https://www.youtube.com/embed/2DmK_H7IdTo?si=hsolS8GCsr72Nmm6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
