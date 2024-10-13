# Open Addressing I

Separate chaining is just one technique for resolving collisions in hash tables. The other main technique is known as *open addressing*.

In open addressing, the keys are stored directly in the entries of the hash table (not in buckets of linked lists). If a collision occurs when trying to insert a new key, a different, open entry in the table must be found instead. The process of finding an open entry is known as *probing*, and we'll consider three different techniques: linear probing, quadratic probing, and double hashing.

## Linear probing

In linear probing, whenever a collision occurs in the hash table, we look sequentially in the table for the next open entry, one index a time. In other words, as long as there are collisions, we continue to look for the next empty cell according to this sequence (wrapping around as needed):

<pre><code>h(x), h(x) + 1, h(x) + 2, h(x) + 3, ...</code></pre>

Watch the following video to see an example of linear probing:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/_UM12uI1nG8"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

If there is an open cell in the table (and if the table size is a prime number), linear probing will eventually find it. The disadvantage, however, is that linear probing doesn't tend to spread keys throughout the table very well. It can lead to clusters of occupied cells, which leads to longer subsequent probes when looking up values.

To try to correct this behavior, we can consider *quadratic probing*.

## Quadratic probing

Quadratic probing skips increasingly larger sequences of cells when looking for an open position. It uses the following sequence of probes (wrapping around as necessary):

<pre><code>h(x), h(x) + 1<sup>2</sup>, h(x) + 2<sup>2</sup>, h(x) + 3<sup>2</sup>, ...</code></pre>

Watch the following video to see an example of quadratic probing:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/RMf5QPmoTcA"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

The advantage of quadratic probing is that it spreads the keys of the table further apart, which creates smaller clusters of occupied cells compared to linear probing. However, the disadvantage is that quadratic probing is not necessarily guaranteed to find an open cell. Because the probe sequence increases quadratically, there is no mathematical guarantee that we will eventually land on an empty cell.

Therefore, we'll consider one more probing scheme in the next lesson: double hashing.
