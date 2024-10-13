# Open Addressing II

The final probing technique for resolving collisions that we'll consider is double hashing, which actually uses two different hash functions.

## Double hashing

In double hashing, we use *two* hash functions instead of one. When there is a collision when using our first hash function, `h1(x)`, we'll add in increasingly larger factors of our second function, `h2(x)`. The probe sequence is as follows:

<pre><code>h1(x), h1(x) + 1*h2(x), h1(x) + 2*h2(x), h1(x) + 3*h2(x), ...</code></pre>

Because we are repeatedly adding in multiples of `h2(x)`, we must pick an `h2` that can never output 0 -- otherwise, the probe sequence would not change.

Watch the video below to see how double hashing uses two different hash functions to find an empty space in the table:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/7dxyWLwnges"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

With double hashing, we get the best of both worlds: a probing scheme that spreads the keys throughout the table like quadratic probing does, and is also guaranteed to find an open position (if one exists, and the table size is a prime number) like linear probing does.

<aside>
<b>Check your understanding</b>
<p>Consider the following open addressing hash table:</p>
<table>
  <tr>
    <td><code>'anaconda'</code></td>
  </tr>
  <tr>
    <td><code>'bat'</code></td>
  </tr>
  <tr>
    <td><code>'bison'</code></td>
  </tr>
  <tr>
    <td>&nbsp;</td>
  </tr>
  <tr>
    <td><code>'elephant'</code></td>
  </tr>
</table>
<p>Assume that the hash function <code>h(x) = index related to the first character of x</code>.</p>
<ol>
  <li>What would the sequence of probed positions be when trying to look up <code>'bear'</code> using linear probing?</li>
  <li>What would the sequence of probed positions be when trying to look up <code>'elephant'</code> using quadratic probing?</li>
  <li>What would the sequence of probed positions be when trying to look up <code>'ant'</code> using double hashing with <code>h2(x) = length of x</code>?</li>
</ol>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b></p>
<ol>
  <li><code>h('bear') = 1</code>, which is occupied but not the key we're looking for, so we try <code>h('bear') + 1 = 2</code> which is also occupied but not the key we're looking for. We then find an empty position at <code>h('bear') + 2 = 3</code>, so we then know that <code>'bear'</code> is not in the table.</li>
  <li></li>
  <li><code>h('elephant') = 4</code>, which is occupied with the value we're looking for, so the lookup is complete. For the record, if it had been occupied with a different value, we would have resumed the search at <code>h('elephant') + 1<sup>2</sup> = 5 % 5 = 0</code>, which would also have been occupied with something other than the key we're looking for, so we would have needed to continue searching.
  <li><code>h('ant') = 0</code>, which is occupied but not the key we're looking for, so we try <code>h('ant') + 1*h2('ant') = 0 + 3 = 3</code> which is empty. Therefore, we know that <code>'ant'</code> is not in the table.
</ol>
</details>
</aside>

## Analysis of open addressing

In many cases, looking up a key in an open addressing hash table is `O(1)`, especially if there are no collisions. However, when there are collisions, we need to utilize one of the probing algorithms, which can inflate the time complexity.

### Worst case analysis

In the worst case, the table is full and the key we are looking for (or inserting) is not yet in the hash table. In that case, the probing algorithms will lead us to probe all $$m$$ slots in the table to ensure that the key is not present, which is `O(m)`. This is because in the worst case, we hash a key to a slot in the hash table, but as we probe through the table, we continue to find full slots until we have checked every slot.

### Average case analysis

In the average case, when hashing a key to a slot in the table, we might encounter some small number of collisions during the probing algorithm. However, as long as the load factor is not too high (say, $$\alpha < 1/2$$), we will be able to find the key (or be sure it's not present) within a constant number of probes. Therefore, similar to separate chaining, under decent conditions (a good hash function and a table that's not too full), we can expect performance that approaches `O(1)`.
