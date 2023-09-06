# Data Structures

As we continue our study of data structures and algorithms, let's first think back to some of the concepts we learned in the previous course.

Before continuing our study of data structures and algorithms, let's first think back to what we have previously learned. In the previous data structures course, we learned about a few different *linear* data structures, including arrays, linked lists, stacks, and queues.

We think of arrays and linked lists as *building block* data structures; we often use them to implement other data structures with some kind of abstraction, such as stacks and queues.

How we choose to implement data structures, including deciding between using an array or a linked list, depends on what properties we are looking for and what efficiency is required. Check out the video below to remind yourself about these data structures:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/o6VuST08S60?si=0nwfp2MlJjPQDA2o"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

* Big-O notation provides us with a language to analyze the efficiency of algorithms, both in terms of time and space. Big-O classes include `O(1)` (constant), `O(logn)`, `O(n)`, <code>O(n<sup>2</sup>)</code>, and <code>O(c<sup>n</sup>)</code> (in order from fastest to slowest).
* An array is a fixed-size collection of items that provides random access to its elements.
* A linked list is an extensible collection of items that does not provide random access to its elements.
* A queue is a data structure with a *first-in, first-out* (FIFO) abstraction.
* A stack is a data structure with a *last-in, first-out* (LIFO) abstraction.

## Data structures in Python

As we learn about these data structures, we implement them in Python or use existing Python constructs.

### Array

Python doesn't have a built-in array data type. However, it does have a *list* data type, which we use to simulate an array. Under the hood, Python lists are actually implemented as arrays.

### Linked list

When we need to use a linked list, we create a special `Node` class that contains at least a piece of data and a reference to the next node in the list. We then create instances of the `Node` list and connect them to form a linked list.

### Queue

Python provides a `deque` object from its `collections` library that we can use as a queue data structure. A `deque` (pronounced "deck", stands for *double-ended queue*) provides with `O(1)` enqueue and dequeue operations by using the `append()` and `popleft()` methods, respectively:

<iframe src="https://trinket.io/embed/python3/e130167ca4" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Stack

The easiest way to simulate a stack in Python is to use a list. To push items onto the stack, we can use the `append()` method, and the pop items from the top of the stack we can use the (you guessed it) `pop()` method:

<iframe src="https://trinket.io/embed/python3/63a0468993" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
