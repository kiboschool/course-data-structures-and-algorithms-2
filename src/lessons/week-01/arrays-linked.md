# Arrays vs. Linked Lists

A classic tradeoff in computer science is whether to implement your data structure using an array or a linked data structure. Let's remind ourselves of some of the space and time tradeoffs between the two, since we will continue to use them in building new data structures in the coming weeks.

Watch the following video to remind yourself of the similarities and differences between arrays and linked lists:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/lC-yYCOnN8Q?si=fLrt41hHzxqXSbie"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

### Arrays

* Allow random (`O(1)`) access to elements, which makes them amenable to techniques like binary search (since it requires jumping to specific points in the array)
* Need to be stored in contiguous memory, so they are typically not resizable
* If you need to add more items to the array than its capacity would allow, you would need to create a new, larger array and copy all of the elements over (`O(n)`)

### Linked lists

* Linked lists don't allow random access to elements; to find an item in the list, you generally must start at the head of the list and traverse as far as needed (`O(n)`)
* Doesn't need to be stored in contiguous memory. Instead, individual nodes can be stored anywhere on the memory heap, with pointers connecting nodes. Therefore, linked lists are not fixed-length
* Adding to the head or tail of the list is generally `O(1)`

<aside>
<b>Check your understanding</b>
<p>You are tasked with building a linear data structure (i.e., either an array or linked list) that is always kept in sorted order. Additionally, you are told that there could be frequent additions to the middle of the list. Which would be the more efficient data structure for the task -- an array or a linked list?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Neither would be more especially more efficient than the other. With an array, you could quickly find the location where a new item was to be added using binary search (<code>O(logn)</code>), but it would take <code>O(n)</code> time to perform the insertion due to the need to shift items. With a linked list, it would take <code>O(n)</code> time to reach the middle of the list, but then only <code>O(1)</code> time to perform the insertion. Therefore, both would generally require <code>O(n)</code> insertion algorithms.</p>
</details>
</aside>
