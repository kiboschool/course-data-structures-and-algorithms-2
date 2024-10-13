# Longest Common Subsequence

Another classic dynamic programming problem is finding the *longest common subsequence* between two strings. A subsequence of characters doesn't necessarily have to be in consecutive positions -- that would be substrings. For example, given these two strings:

$$S_1 = AABCDD$$
<br>
$$S_2 = ABBBD$$

Then the longest common substring between $$S_1$$ and $$S_2$$ is just $$AB$$, but the longest common *subsequence* between them is $$ABD$$, since that sequence of characters appears in both strings.

## Applications

## Naive Approach

Like most dynamic programming problems, it's helpful to think of a naive, recursive, and expensive solution first, and then improve on the solution once we have an initial understanding.

### Reasoning

Let's take a look at an example instance of the problem: let's try to compute the longest common subsequence between $$AABCDD$$ and $$ABBBD)$$.

First, we notice that both strings start with $$A$$. Since the two strings match in this position, that $$A$$ *must* be a part of the LCS. Therefore, we can say that $$LCS(AABCDD, ABBBD) = A + LCS(ABCDD, BBBD)$$ -- breaking the problem down into a subproblem by removing the initial $$A$$ from both strings. Note that this means the problem exhibits the optimal subproblem property!

What about when the first characters of the strings don't match? For example, let's take a look at that next subproblem: $$LCS(ABCDD, BBBD)$$. Since $$A$$ and $$B$$ don't match, we have two options for the next subproblem to consider:

1. Take the first character off of $$S_1$$ and see what the LCS is: $$LCS(BCDD, BBBD)$$
2. Take the first character off of $$S_2$$ and see what the LCS is: $$LCS(ABCDD, BBD)$$.

Once we've figured out both options, $$LCS(ABCDD, BBBD)$$ is equal to whichever is longer.

### Python Implementation

Here's a Python program that implements the naive, recursive approach:

```python
def lcs(s1, s2):
    if len(s1) == 0 or len(s2) == 0:
        # At least one of the strings is empty, so there's no
        # characters in the longest common subsequence.
        return ''
    if s1[0] == s2[0]:
        return s1[0] + lcs(s1[1:], s2[1:])
    else:
        # Pick whichever subproblem ultimately leads to a
        # longer LCS.
        r1 = lcs(s1, s2[1:])
        r2 = lcs(s1[1:], s2))
        if len(r1) > len(r2):
            return r1
        else:
            return r2
```

### Efficiency

This algorithm is quite inefficient, since it has to be called for all possible substrings of both `s1` and `s2`. Additionally, many of these function calls are redundant. For example:

```
lcs('cba', 'dea') calls lcs('cba', 'ea') and lcs('ba', 'dea')
    lcs('cba, 'ea') calls lcs('cba', 'a') and lcs('ba', ea')
        ...
    lcs('ba', 'dea') calls lcs('ba', 'ea') and lcs('a', 'dea')
        ...
```

As you can see, `lcs('ba', 'ea')` is called multiple times, in different parts of the call tree. This means that the LCS problem also exhibits overlapping subproblems -- another characteristic of dynamic programming problems.

Since it reconsiders all possible combinations of strings, the efficiency is $$O(2^n * 2^m)$$, where $$n$$ is the length of $$S_1$$ and $$m$$ is the length of $$S_2$$.

## Bottom-Up Approach

Above, we noticed that this problem exhibits both required characteristics for a dynamic programming solution. Let's see first how this can be achieved in a bottom-up approach:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Ua0GhsJSlWM?si=NUNSTqryBgLRI1Bw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize, the video above uses a bottom-up (tabulation) approach, where they solve the smallest subproblems first, and then use the solutions to those subproblems to build up a solution to the overall problem. As is illustrated by the usage of the 2D table, both the time and space complexity for this approach are $$O(mn)$$.

## Memoized Approach

We could also solve the LCS problem using top-down dynamic programming with memoization. This would require making $$O(mn)$$ recursive calls as well, since we need to consider all $$n$$ possible substrings for $$S_1$$ against all $$m$$ possible substrings of $$S_2$$. However, we never need to recompute the values after they are found the first time, since they can be stored in a table.
