# Heap Removal

The `remove()` operation of a heap is extremely important -- usually, the reason why we keep the items in a heap is so that we can efficiently remove them when ready.

The removal algorithm is quite similar to the insertion algorithm, in the sense that we will need to do some sifting to keep the heap in order. However, this time we'll be sifting down instead of sifting up.

## Algorithm

Watch the video below to see how to remove the maximum item from a heap:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/SLJVhd3eToQ"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize, when removing the maximum item from the heap, we can:

1. Make a copy of the largest item
2. Move the last item in the heap to the root
3. "Sift down" the new root item until it is >= its children (or it's a leaf)
    * Note: when a parent is less than *both* of its children, we need to swap the parent with the *greater* of the two children.
4. Return the largest item

<aside>
<b>Check your understanding</b>
<p>Consider the following heap:</p>
<center>
<img
  src="/images/week-03/dsa2-week3-heap-removal.png"
  alt="A heap with 35 at the root and 25 and 23 as its left and right children. The left and right children of the 25 are 11 and 14, and the left and right children of the 23 are 3 and 19."
  style="width:300px;" />
</center>
<p>What would the heap look like after removing the maximum item?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The 35 would be copied and saved, and the 19 (the last item in the heap) would be moved to the root. When sifting down, the 19 would swap with the 25 (since the 25 is greater than the 23). It would then not need to swap with the 11 or the 14 since it is greater than both of those values. The final list representation of the heap would be <code>[25, 19, 23, 11, 14, 3]</code>.
</details>
</aside>

## Efficiency

Rather than discuss the efficiency explicitly, let's put your analytical skills to the test:

<aside>
<b>Check your understanding</b>
<p>Think about the analysis we did in calculating the worst-case efficiency for heap insertion. Using those same ideas, what is the big-O efficiency for removing an item from a heap?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The process of sifting down the last item makes this algorithm <code>O(logn)</code>, since in the worst case it must sift the new root down the height of the tree (heap), which is <code>O(logn)</code> levels.</p>
</details>
</aside>
