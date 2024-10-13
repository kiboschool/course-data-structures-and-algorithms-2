# Hash Tables

In the previous lesson, we saw that there were multiple issues with trying to index a table directly using keys, including the fact that keys can be any value (including strings!).

To solve this, *hash tables* provide us with the ability to map a key of any data type to an array index. Watch the two videos below to learn about how hash functions work:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/rBRPwzY76WM"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>
<p></p>
<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/LeNQqDJ6exA"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

* A hash function `h(x)` maps a key `x` to a *hash value*, which is an integer.
* A key can be mapped to an array position using the expression `h(x) % n`, where `n` is the size of the array.
* An array that uses hash functions to manage (key, value) pairs is a *hash table*.
* Ideally, hash functions map keys to integers uniformly at random.
* Typically, performing a key lookup in a hash table is a constant time (`O(1)`) operation.
* Since a hash function may map two different keys to the same table position, we need a way to deal with collisions.

<aside>
<b>Check your understanding</b>
<p>Say that we have a hash function <code>h(x)</code> which operates on string keys, and just returns the index related to the first character of <code>x</code>, i.e., 0 for 'a', 1 for 'b', etc. If we have an initially empty hash table of length 7, what would the table look like after inserting the following keys: <code>'bat'</code>, <code>'dog'</code>, <code>'zebra'</code>?
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Hashing <code>'bat'</code> will give us <code>h('bat') = 1 % 7 = 1</code>, which can fit in index 1 since it is currently unoccupied:</p>
<p><code>    [ , 'bat', , , , , , ]</code></p>
<p>Hashing <code>'dog'</code> yields <code>h('dog') = 3 % 7 = 3</code>, which we can put into index 3:</p>
<p><code>    [ , 'bat', , 'dog', , , , ]</code></p>
<p>And finally, we have <code>h('zebra') = 25 % 7 = 4</code>:<p>
<p><code>    [ , 'bat', , 'dog', 'zebra', , , ]</code></p>
</details>
</aside>

<aside>
<b>Check your understanding</b>
<p>Again consider the hash function <code>h(x)</code> that just returns the index related to the first character of <code>x</code>, i.e., 0 for 'a', 1 for 'b', etc. Is this a good hash function in terms of uniform mapping of keys?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> No, this would not be a good hash function for strings, since it only has 26 possible hash values -- one for each letter of the alphabet. Imagine a situation where we want to store millions of strings in a table. Each of the strings we want to store would be hashed to one of the first 26 slots of the table, instead of evenly spreading the strings over the millions of available positions.
</details>
</aside>
