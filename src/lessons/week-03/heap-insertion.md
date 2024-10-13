# Heap Insertion

Let's talk about how to insert items into a heap. To do so, let's define a `Heap` class that we can add functionality to, and start it with a list of items and a counter for the current number of items:

```python
class Heap:
    def __init__():
        self.contents = []
        self.num_items = 0
```

Recall that since heaps are complete trees, they have a convenient representation as a list. Therefore, we'll avoid creating a linked data structure and instead implement the heap using a list.

## Algorithm

Watch the video below to see how to insert an item into a heap:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/ND3-Dnx_Rqc"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

* The new item initially gets put into the end of the list (a leaf node).
* The value in that leaf node is "sifted up" in the heap until it obeys the heap property.

<aside>
<b>Check your understanding</b>
<p>Consider the following heap:</p>
<center>
<img
  src="/images/week-03/dsa2-week3-heap-insertion.png"
  alt="A heap with 28 at the root and 16 and 20 as its left and right children. The left and right children of the 16 are 12 and 8, and the left child of the 20 is 5."
  style="width:250px;" />
</center>
<p>What would the heap look like after inserting 30?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The 30 would initially be inserted as the right child of 20 in a leaf node. It is then sifted up as far as needed: first, 30 is greater than its parent (20), so the 30 and 20 swap positions. Then, the 30 is still greater than its parent (28), so the 30 and 28 swap positions. Therefore, the 30 is sifted up all the way to the root node.</p>
</details>
</aside>

## Efficiency

When inserting an item into the heap, we first place the item in the last position in the list in constant time. However, we then need to run the `sift_up()` algorithm, which in the worst case pushes the item from a leaf node all the way up to the root.

Since the heap is a complete tree, we know that it is also balanced, and therefore we can say that in the worst case, an item is sifted up throughout the height of the tree, where `h = O(logn)`. Each of the swaps that occurs during the sift operation takes constant time.

Therefore, insertion in a heap is `O(logn)`.

Now that we know how to insert items into a heap, let's take a step back and look at the overall heap constructoin algorithm and its efficiency. The big-O notation for building a heap may surprise you!

<aside>
<b>Check your understanding</b>
<p>What's the big-O notation of insertion into a heap in the best case?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> In the best case, when we place the new item into a leaf node, it is already less than its parent, and therefore doesn't need to be sifted at all. In this case, insertion is <code>O(1)</code>.</p>
</details>
</aside>
