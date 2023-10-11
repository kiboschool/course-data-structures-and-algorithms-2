# Hash Functions

At the end of last week, we discussed the characteristics of various implementations of data dictionaries. The most efficient variant we have seen so far is balanced binary search trees, which guarantee `O(logn)` lookup and insertion performance. But can we do better?

In this lesson, we will begin our discussion of hash tables and hash functions, which will ultimately lead us to a data dictionary that can achieve `O(1)` performance. Before we get there, however, let's take a look at a simpler example of a constant-time data dictionary: using keys to index an array directly.

## Directly indexed array

Say we are trying to insert some (key, value) pairs into an initially empty array of length `n`. If we know that each key is in the range [0, `n` - 1], then we can simply use the key as the index into the array!

For example, say that our (key, value) pairs represent football players. Each key is a player's jersey number, and each value is the player's name. If we can assume that jersey numbers are in the range 0-99, then we can easily insert all of the players into an array of length 100:

<!-- insert picture here -->

To lookup the name of a player, we can use their jersey number to index the array and find the name in `O(1)` time:

<!-- insert picture here -->

However, most real-world problems do not behave this way. In many problems, we don't know the likely *key space*, or range of potential keys, ahead of time. Even if we knew the range of keys, we have to make our array large enough to fit the maximum value in the range. In other words, if the maximum possible key value was 1,000,000, we would need to make our array large enough to hold 1,000,000 items, even if we were only expecting 1,000 items in total.

<aside>
<b>Check your understanding</b>
<p>What other issues can you think of regarding trying to use keys directly as indexes into an array? Hint: we've only considered an example where keys are integers.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Keys can be any data type, not just integers. If the keys were strings, floating point numbers, dates, etc., they could not be used to index an array, and therefore this approach would not work.</p>
</details>
</aside>

Because of these issues related to the data types and ranges of values of keys, directly using keys to index an array won't work in the general case. However, we can achieve a similar result using hash functions.

## Hash functions

*Hash functions* provide us with the ability to map keys of any data type to array indices. Watch the video below to learn about how hash functions work:

> Insert video here.

To summarize:

* A hash function `h(x)` maps a key `x` to a *hash code* or *hash value), which is an integer
* Ideally, hash functions map keys to integers uniformly at random
* A key can be mapped to an array position using the expression `h(x) % n`, where `n` is the size of the array
* An array that uses hash functions to manage (key, value) pairs is a *hash table*
* Since a hash function may map two different keys to the same table position, we need a way to deal with collisions

<aside>
<b>Check your understanding</b>
<p>Say that we have a hash function <code>h(x)</code> which operates on string keys, and just returns the index related to the first character of <code>x</code>, i.e., 0 for 'a', 1 for 'b', etc. If we have an initially empty hash table of length 7, what would the table look like after inserting the following keys: bat, dog, giraffe?
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b></p>
</details>
</aside>

## A sample hash function (optional)

You may be wondering how a hash function could possibly take, for example, a string key and map it to a number effectively. There are a lot of possible ways to do this; the following video describes just one approach.

<!-- https://www.youtube.com/watch?v=WyFwieF1NN4 -->
