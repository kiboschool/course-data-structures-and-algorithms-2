# Heaps

A *heap* is a type of tree data structure that satisfies the *heap property*: every node's key is greater than or equal to the keys of its children.

<aside>
<b>Note</b>
<p>This the heap property defined for <i>max-at-top</i> heaps, which we will assume to be the case by default. For <i>min-at-top</i> heaps, every node's key is <i>less</i> than or equal to the keys of its children.</p>
</aside>

Here are some example heaps:

<center>
<img
  src="/images/week-03/dsa2-week3-heaps.png"
  alt="Three max-at-top heaps of various shapes."
  style="width:650px;" />
</center>

Note that with the heap property, it necessarily means that the maximum value in the heap is at the root of the tree. This makes it a very natural data structure to use when implementing a priority queue, since the highest priority element is readily available!

<aside>
<b>Check your understanding</b>
<p>In a max-at-top heap, where is the element with the <i>minimum</i> priority?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> It has to be in one of the leaf nodes. However, there's no guarantee about which leaf node it will be in.</p>
</details>
</aside>

The most common way of implementing a heap is by using a *complete binary tree*.

## Complete binary tree

A complete binary tree (note: not a binary *search* tree) is a binary tree of height *h* where:

* levels 0 through h - 1 are fully occupied
* in level h, there are no "gaps" to the left of any node

In essence, a complete tree is one where the tree is filled with nodes from top to bottom, left to right, and each node is full of nodes except for possibly the last layer. Here are some examples of complete trees:

<center>
<img
  src="/images/week-03/dsa2-week3-complete-trees.png"
  alt="Three complete trees of various shapes."
  style="width:650px;" />
</center>

And here are some examples of trees that are *not* complete (where the node that's missing to prevent it from being complete is highlighted):

<center>
<img
  src="/images/week-03/dsa2-week3-not-complete-trees.png"
  alt="Three trees of various shapes that are close to being complete trees, but are missing a node that prevents it from being complete."
  style="width:650px;" />
</center>

### Representing a complete binary tree

In our previous data structures course, we represented trees a linked data structure: every node in a tree had some data element, as well as pointers to its left child, right child, and parent. This works great in the general case for representing trees.

However, when using *complete* trees (as we are for heaps), we can actually have a simpler representation that just uses an array. This makes it a lot simpler to manage and manipulate the heap.

To represent a complete tree as an array, the trees's nodes are stored in the order given by a level-order traversal; top to bottom, left to right:

<center>
<img
  src="/images/week-03/dsa2-week3-heap-array.png"
  alt="A complete tree showing how it can be interpreted using an array. The root node shows a[0] and its left and right children show a[1] and a[2], respectively. The node with a[1] has a[3] and a[4] as its left and right child, etc."
  style="width:325px;" />
</center>

<center>
<img
  src="/images/week-03/dsa2-week3-heap-array-example.png"
  alt="Side-by-side comparison of a complete tree and its array representation."
  style="width:325px;" />
</center>

Once the tree is represented as an array (or in our case, a list in Python), you can use the following formulas to navigate the tree:

* The root node is in `lst[0]`
* Given the node in `lst[i]`:
    * its left child is in `lst[2*i + 1]`
    * its right child is in `lst[2*i + 2]`
    * its parent is in `lst[(i - 1)/2]` (using integer division)

For example, consider this complete tree:

<center>
<img
  src="/images/week-03/dsa2-week3-complete-tree-formula.png"
  alt="Another complete tree where each node is marked with the corresponding array indexes from the array representation."
  style="width:425px;" />
</center>

* the left child of the node in `lst[1]` is in `lst[2*1 + 1] = lst[3]`
* the left child of the node in `lst[2]` is in `lst[2*2 + 1] = lst[5]`
* the right child of the node in `lst[3]` is in `lst[2*3 + 2] = lst[8]`
* the parent of the node in `lst[4]` is in `lst[(4 - 1)/2] = lst[1]`

<aside>
<b>Check your understanding</b>
<p>Using the formulas above (not the picture), complete the statements:</p>
<ol>
  <li>the right child of the node in <code>lst[2]</code> is in ____</li>
  <li>the parent of the node in <code>lst[7]</code> is in ____</li>
</ol>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b></p>
<ol>
  <li>The right child is in <code>lst[2*2 + 2] = lst[6]</code>.</li>
  <li>The parent is in <code>lst[(7 - 1)/2] = lst[3]</code>.</li>
</ol>
</details>
</aside>

<aside>
<b>Check your understanding</b>
<p>Consider the following array representation of a complete tree:</p>
<center>
<img
  src="/images/week-03/dsa2-week3-example-array.png"
  alt="An example array that can be interpreted as a complete tree."
  style="width:400px;" />
</center>
<p>What is the left child of 24?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The left child of the 24 is the 10, since the 24 is in index 3, and therefore its left child is in <code>lst[2*3 + 1] = lst[7]</code>.</p>
</details>
</aside>

### Summary

To summarize, we are now looking to implement the priority queue ADT using a max-at-top heap. Most often, heaps are complete trees, which are implemented as arrays due to the simplicity of the representation.

Watch the following video to see a summary of heaps and complete trees:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/0wPlzMU-k00"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>
