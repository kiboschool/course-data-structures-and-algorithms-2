# Quicksort Analysis

We mentioned in the last lesson that quicksort is similar to merge sort, since they are both divide-and-conquer algorithms that improve on the running time of more primitive sorting algorithms (such as insertion sort or selection sort). However, whereas merge sort is $$O(nlogn)$$ in all cases, quicksort has sa more nuanced running time that depends on the contents of the list.

## Best case and worst case

Watch the following video to see the best case and worst case running time behavior of quicksort:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/-qOVVRIZzao?si=d-z6oTiErlWwuFSa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize:

* In the best case, each partition divides the remaining portion of the list approximately in half. In this caes, there are $$O(logn)$$ partitions -- when visualized as a call tree, the height of the tree is $$O(logn)$$. At each of the levels of that tree, $$O(n)$$ amount of operations are performed to do the partitioning. Therefore, the best case running time is $$O(nlogn)$$.
* In the worst case, each partition reduces the size of the list by one element, i.e., the pivot is chosen to be the smallest or largest element of each sublist. In this case, the call tree has a height of $$O(n)$$, with $$O(n)$$ operations performed at each level to perform the partition, leading to a running time of $$O(n^2)$$.
* Notice that the choice of partition can have a significant impact on the running time of the algorithm.

## Average case

In the average case of quicksort, there is a mixture of good and bad partitions. In practice, the running time in the average case is closer to $$O(nlogn)$$ than it is to O$$(n^2)$$. Watch the following video to see an empirical explanation of the average case:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/FzKn3BT_TmM?si=GP4jHd1prAdl2uYM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

