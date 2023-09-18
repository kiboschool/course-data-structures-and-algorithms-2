# Recursion

Many problems in computer science can be solved by repeatedly breaking down a problem into a slightly smaller problem, since once you know the solution to the smaller problem, it's easier to solve the original problem.

In the previous course, we learned about how to use *recursion* to solve such problems. We saw that recursion is a natural and elegant way to write algorithms that operate on data structures such as arrays, linked lists, and trees.

Watch the video below to remind yourself about how to think recursively and write a recursive function:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/9bsK03SlmNM"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

## Recursion on data structures

Let's now take a look at the `length()` function, which uses recursion to find the length of a linked list:

```python
class LinkedList:
    class Node:
        def __init__(self, val, next):
            self.val = val
            self.next = next

    def __length(self, head):
        if head is None:
            return None

        length_of_rest = self.length(head.next)
        return length_of_rest + 1

    def length(self):
        return self.__length(self.head)
```

This is the style in which we had been writing recursive functions. Notice a few things in particular:

* We have a recursive helper method, which uses a parameter `head` to track where we currently are in the list.
* We have a base case to check whether `head` is `None`; if it is, we have reached the end of the list.
* We make a recursive call, passing in `head.next` to advance to the next node in the list. We store the return value in a variable `length_of_rest`.
* Once we know the length of the rest of the list we simply need to add one and return the result.

<aside>
<b>Check your understanding</b>
<p>Consider the following function, which replaces every occurrence of the value <code>old</code> with the value <code>new</code> in the linked list pointed to by <code>head</code>:</p>
<pre><code class="language-python">def replace(head, old, new):
    trav = head
    while trav is not None:
        if trav.val == old:
            trav.val = new<br>
        trav = trav.next</code></pre>
<p>1. Write a recursive version of this function.</p>
<p>2. What is the running time of your function?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Here is a recursive version of the function:</p>
<pre><code class="language-python">def replace(head, old, new):
    if head is None:
        return<br>
    if head.val == old:
        head.val = new<br>
    replace(head.next, old, new)
</pre></code>
<p>Notice that there isn't any work to be done after the recursive call returns.</p>
<p>The running time of this algorithm is <code>O(n)</code>, since it makes <code>n + 1</code> function calls for a linked list of length <code>n</code>, and each function call performs a constant amount of operations.</p>
</details>
</aside>
