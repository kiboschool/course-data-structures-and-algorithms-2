# Rabin-Karp Algorithm

Believe it or not, we can actually improve even further on the string matching problem than the KMP algorithm. In the *Rabin-Karp* algorithm, we can search for a string $$M$$ in $$S$$ again in $$O(n + m)$$ time, but by using only $$O(1)$$ space.

## Algorithm

Watch the following video to see how the Rabin-Karp algorithm works:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/qQ8vS2btsxI?si=tqJxSAL7vfyINCQF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize:

* The algorithm uses hashing to convert the pattern and substrings of the text into numerical values. This allows for quick comparisons between the pattern and text substrings based on their hash values.
* The algorithm employs a rolling hash function to efficiently compute the hash value of the next substring in constant time by updating the hash value of the current substring. This avoids recomputing the hash from scratch for each substring.
* If the hash values of the pattern and a text substring match, a direct comparison is performed to confirm the match. This step ensures that false positives (hash collisions) are correctly identified and handled.
* The main drawback of the Rabin-Karp algorithm is the possibility of hash collisions, where different substrings have the same hash value. This requires additional verification steps, potentially affecting performance. Additionally, the algorithm's average-case time complexity is $$O(n + m)$$, but its worst-case time complexity can degrade to $$O(n * m)$$ if many hash collisions occur.

## Summary

Here's another video that summarizes the Rabin-Karp technique:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/rii2QSpTqOY?si=ofFR25-aZAaHL8y2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
