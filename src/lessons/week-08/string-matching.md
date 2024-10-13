# String Matching

We now leave quicksort to look at a familiar algorithm: string matching. In other words, given a string $$S$$, we want to find whether a string $$W$$ occurs within that string.

For example, if $$S$$ is `ABC ABCDAB ABCDABCDABDE` and $$W$$ is `ABCDABD`, then $$W$$ appears in $$S$$ (at position 15).

## Naive algorithm

At this point, you're likely familiar with the "naive" string matching algorithm, which checks every possible position in $$S$$ for $$W$$:

```python
def naive_string_match(s, w):
    n = len(s)
    m = len(w)

    # Loop through the text from the start to the point where the pattern can fit
    for i in range(n - m + 1):
        # Check for a match at this position
        match = True
        for j in range(m):
            if s[i + j] != w[j]:
                match = False
                break

        # If match is still True, we found a match
        if match:
	    return i

    return -1
```

The worst-case running time for this algorithm is $$O(n * m)$$, where $$n$$ is the length of the longer string $$S$$ and $$m$$ is the length of the smaller string $$W$$. This is because the algorithm compares each character of the pattern with the text for each possible starting position.

However, we can do better than this algorithm. One example is the Knuth-Morris-Pratt algorithm.

## Knuth-Morris-Pratt algorithm

The Knuth-Morris-Pratt (KMP) algorithm improves on naive string search using the following algorithm:

1. Preprocessing phase: The KMP algorithm preprocesses the pattern to create a partial match (or "failure") table, which takes $$O(m)$$ time.
2. Matching phase: The actual string matching is done in $$O(n)$$ time. The KMP algorithm avoids redundant comparisons by using the information from the partial match table, ensuring that each character in the text is compared at most once.

Watch the following video to see how the KMP algorithm works:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/5i7oKodCRJo?si=z3tbIF0xJ81yfu1W" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

As described above, this algorithm is significantly faster, and operates in $$O(n + m)$$ time. However, the space complexity of the algorithm increases to $$O(m)$$, which is more space than the naive algorithm.
