# Direct-Address Tables

At the end of last week, we discussed the characteristics of various implementations of data dictionaries. The most efficient variant we have seen so far is balanced binary search trees, which guarantee `O(logn)` lookup and insertion performance. But can we do better?

Ultimately, we will see that *hash tables* allow us to achieve even better performance than balanced BSTs. However, before we talk about hash tables, we need to discuss *direct-address tables*.

## Direct-address tables

Say we are trying to insert some (key, value) pairs into an initially empty array of length `n`. If we know that each key is in the range [0, `n` - 1], then we can simply use the key as the index into the array!

For example, say that our (key, value) pairs represent football players. Each key is a player's jersey number, and each value is the player's name. If we can assume that jersey numbers are in the range 0-99, then we can easily insert all of the players into an array of length 100:

<center>
<img
  src="/images/week-02/dsa2-week2-jerseynumber.png"
  alt="An array of length 100 that holds only three entries: 'Rashidi Yekini' at index 9, 'Jay Jay Okocha' at index 10, and 'John Obi Mikel' at index 21. The remaining indices are empty."
  style="width:500px;" />
</center>

To lookup the name of a player, we can use their jersey number to index the array and find the name in `O(1)` time.

However, there are a few issues with this approach to storing (key, value) pairs:

* In many cases, we don't know the *key space*, or range of potential keys, ahead of time. For example, the key could be any number, not just a number in the range 0-99.
* Even if we knew the range of the keys, we have to make our array large enough to fit the maximum value in the range. In other words, if the maximum possible key value was 1,000,000, we would need to make our array large enough to hold 1,000,000 items, even if we were only expecting 1,000 items in total.

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

Because of these issues related to the data types and ranges of values of keys, directly using keys to index an array won't work in the general case. However, we can achieve a similar result using *hash functions*.
