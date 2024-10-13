# Hash Deletion

In the past few lessons, we covered how to insert new items into separate chaining and open addressing hash tables. Let's also now take a look at how to *delete* an item from a hash table.

## Separate chaining

Deleting a key `x` is relatively simple in a separate chaining hash table. The algorithm is:

1. Compute `h(x)` to find the bucket where `x` belongs.
2. Use the linked list deletion algorithm to delete the node with key `x`.

## Open addressing

Deletion in an open addressing hash table is a little bit more challenging, since it can leave gaps in the table that interfere with the probing process. Watch the following video to see why deletion can create gaps, and how to fix it:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/COXaY-Uj9uc"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

* When deleting an item, assign a special "removed" value to that slot in the table.
    * For example, "empty" spaces may contain -1 and "removed" spaces may contain -2 as sentinel values
* When performing lookups, we need to skip past any removed slots and continue searching
* When performing insertions, we can insert into *either* empty or removed slots (whichever comes first), after checking to make sure the key to be inserted doesn't already exist

<aside>
<b>Check your understanding</b>
<p>Consider the following open addressing hash table with linear probing and removed spaces:</p>
<center>
<img
  src="/images/week-02/dsa2-week2-hash-deletion.png"
  alt="An example open addressing hash table with removed spaces: [aardvark, removed, cat, bear, empty, dog, removed]."
  style="width:275px;" />
</center>
<p>The hash function used is <code>h(x) = index of first character of x</code>, i.e., <code>'a' = 0</code>, <code>'b' = 1</code>, etc.</p>
<ol>
  <li>One of the keys has been incorrectly inserted. Which one?</li>
  <li>Where would the key <code>giraffe</code> be inserted?</li>
</ol>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b>
<ol>
  <li>The key <code>dog</code> must have been incorrectly inserted. It starts with <code>'d'</code>, so it should have been hashed to <code>3</code>. Even though another key occupies that space, with linear probing it should have been placed in index <code>4</code>.</li>
  <li><code>h(giraffe) = 6</code>, so we first check there. It's a removed cell, so we need to keep looking through the hash table to confirm <code>giraffe</code> isn't already present. We wrap around to the beginning of the table, and check indexes <code>0</code> (occupied), <code>1</code> (removed), <code>2</code> and <code>3</code> (both occupied), until we reach index <code>4</code>, which is empty. At this point, we can be assured that <code>giraffe</code> is not in the table, and so we insert it into index <code>6</code>, since that was the first removed position we encountered.</li>
</ol>
</details>
</aside>


