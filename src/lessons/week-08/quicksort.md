# Quicksort

In this course and the previous DSA course, we have seen many different sorting algorithms:

- Insertion sort
- Selection sort
- Radix sort
- Merge sort
- Heapsort

We have finally reached our last sorting algorithm: *quicksort*. Similar to merge sort, quicksort is a *divide-and-conquer* algorithm, since it repeatedly divides a list to break it down into smaller and smaller subproblems, and recursively sorts those subproblems.

Let's take a closer look at how quicksort works.

## Algorithm

Watch the following videos to learn about quicksort:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/COk73cpQbFQ?si=cGV7w7KtWw3V8lUB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize:

- Quicksort is a recursive, divide-and-conquer algorithm
- It repeatedly rearranges (*partition*) the elements so that we end up with two sublists that meet the following criterion: *each element in left array <= each element in right array*
- It applies quicksort recursively to the sublists, stopping when a sublist has a single element

## Choice of pivot

There are many possible ways of choosing the quicksort pivot, including:

* The first element or the last element
    * Risky, because it could lead to worst case behavior if the list is sorted or almost sorted
* The middle element of the list
* A randomly chosen element
* The median of three elements
    * For example, the median of the first, last, and middle elements

<aside>
<b>Check your understanding</b>
<p>Consider the following list: <code>[7, 39, 20, 11, 16, 5]</code>. Say that we choose the pivot to be the middle element (in this case, the 20). What would the list look like after partitioning around this pivot? What would be the next two sublists?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The partition algorithm proceeds by starting from the left and looking for elements >= 20. It therefore stops at the 39. It then starts from the right, looking for elements <= 20. It therefore stops at the 5, and swaps the 39 and the 5: <code>[7, 5, 20, 11, 16, 39]</code>. It then continues from the left, stopping at the 20 (since it is >= 20). Continuing from the right, it stops at 16, and swaps the 20 and 16: <code>[7, 5, 16, 11, 20, 39]</code>. Continuing from the left, it goes past the 11 and then stops again at the 20 (since it is >= 20). Continuing from the right, it stops at the 11 (since it is <= 20). Since the pointers coming from the two sides have crossed, no swap is needed, and the partition step ends with the list as <code>[7, 5, 16, 11, 20, 39]</code>.</p>
<p>At this point, the left sublist is <code>[7, 5, 16, 11]</code>, and the right subarray is <code>[20, 39]</code>.</p>
</details>
</aside>

## Application

Quicksort is widely recognized for its impact and extensive application in various fields due to its efficient average-case performance and in-place sorting capability. It is frequently used in systems where speed is crucial, such as in database management, search engines, and large-scale data processing.

Quicksort's ability to handle large datasets efficiently makes it a preferred choice in many real-time applications and performance-critical environments. The algorithm's in-place sorting feature minimizes memory usage, making it suitable for systems with limited resources. Additionally, Quicksort is often the default sorting algorithm in many programming language libraries, including C's standard library (`qsort`), Python's `Timsort` (which includes elements of quicksort), and Java's `Arrays.sort`. Its combination of simplicity, speed, and low memory overhead ensures that quicksort remains a foundational algorithm in computer science and software engineering.

## Summary

Here's a couple more good videos about quicksort, in case you need some more examples:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZHVk2blR45Q?si=iUPx2Rn6dDXZcCUZ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
<br>
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Hoixgm4-P4M?si=DgJYQYqEXKGg8RXu" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
