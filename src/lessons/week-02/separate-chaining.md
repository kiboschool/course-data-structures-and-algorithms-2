# Separate chaining

As we previously saw, a hash table can have a *collision* if two different keys have the same hash value. More formally, we say that two keys $x$ and $y$ collide if $h(x) = h(y)$ where $x \neq y$.

Therefore, we may sometimes run into a situation where we are trying to insert key $y$ into the table, but the key $x$ already occupies the bucket where $y$ belongs! One technique for resolving a collision is known as *separate chaining*.

## Buckets of linked lists

In a separate chaining hash table, the table is represented as an array of buckets, where each bucket contains a linked list of entries:

<center>
<img
  src="/images/week-02/dsa2-week2-separate-chaining.png"
  alt="An array where each element is a linked list. At index 0, there is a linked list of length 2 with the keys ant and alligator. At index 1, there is no linked list (it is empty). At index 2, there is a linked list of length 3 with the keys cat, cow, and camel. At index 3, there is a linked list of length 1 with the key dog. The rest of the table is implied, until index 25 where there is a linked list of length 1 with the key zebra."
  style="width:450px;" />
</center>

Now, two (or more) keys that have the same hash value are inserted into the corresponding bucket's linked list. For example, `cat`, `cow`, and `camel` are all hashed to the bucket at index 2 and are therefore stored in a linked list.

Note: from this point on, for simplicity our hash table diagrams will only show the keys that are used to organize the table. However, don't forget that typically, a hash table is used to store (key, value) pairs as a data dictionary.

## Building a hash table

Watch the following video to see how to build a separate chaining hash table from a list of keys:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/ekVVKv4rtr0"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

## Analyzing separate chaining

Previously, we saw that in many cases, looking up a key in a hash table is `O(1)`. However, collisions complicate the lookup operation. In separate chaining, when we hash a key to a bucket, we then need to walk down the linked list in that bucket to find the key (if it's present).

### Worst case analysis

In the worst case, all $n$ keys that are in the table have been hashed to the same bucket, creating a linked list in that bucket that is `n` nodes long. Looking up a key in this list would therefore take time `O(n)` in the worst case, since we would need to start at the beginning of this list and walk down it until we find the key we're looking for.

### Average case analysis

But what about the average case? Is it typically closer the best case `O(1)` performance, or closer to the worst case `O(n)` performance? To answer this question, we first need to define the *load factor* of a hash table.

The load factor ($\alpha$, "alpha") of a hash table is the main way to measure how full the hash table is. It is defined as the ratio of the number of entries in the table ($n$) to the overall number of buckets in the table ($m$):

$\alpha = n/m$

For example, the load factor of a hash table of length 100 with 50 items in it is $\alpha = 0.5$.

When looking up a key in a separate-chaining hash table, the average length of the linked lists is the load factor, since it represents $n$ elements spread out over $m$ slots. Therefore, you can think of the average case lookup performance in a separate chaining hash table as `O(n/m)`.

However, as long as the load factor is kept < 1 (i.e., the table is not too full), the time complexity is generally better than `O(logn)`, and approaches `O(1)`.

This is yet another classic time-space tradeoff in computer science. Larger hash tables take up more memory, but have a lower load factor, which means that the linked lists in buckets are shorter, which leads to faster lookup times. Smaller hash tables conserve space, but have longer linked lists and therfore longer lookup times.

<aside>
<b>Check your understanding</b>
<p>In a previous lesson, we learned that hash functions ideally map keys to indexes uniformly at random. The time complexity of hash tables is dependent on this property -- without it, the lookup operation could degrade to <code>O(n)</code>. Why?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> A poor hash function may map many keys to a small set of buckets, which will make the linked lists in this buckets quite long. In the extreme case, a hash function would map all keys to the exact same bucket, which would therefore have a linked list of length <code>n</code>, leading to a worst case lookup time of <code>O(n)</code>. To get <code>O(1)</code> performance, the hash function needs to uniformly spread the keys throughout the table.</p>
</details>
</aside>
