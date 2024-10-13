# Dynamic Programming

In the previous lesson, we explored the rod cutting problem and implemented a solution using a recursive strategy. However, we observed that the recursive approach led to a call tree with $$2^n$$ nodes, which translates to an exponential time complexity, making it impractical for large rod lengths.

Let's take another look at that call tree:

<center>
<img
  src="/images/week-04/dsa2-week4-rod-call-tree.png"
  alt="the call tree for calculating the maximum revenue for a rod of length 4. branches in a tree-like structure to recursively compute the maximum revenue for a rod of length 3, a rod of length 2, a rod of length 1, etc."
  style="width:650px;" />
</center>

Notice that when computing `max_revenue(4)`, we recompute the same values over and over again. We make a call to compute `max_revenue(2)` twice, `max_revenue(1)` four times, and `max_revenue(0)` eight times!

To overcome the inefficiency of the recursive approach, we can use a technique that *saves* previously computed results and reuses them when needed. This technique, called *dynamic programming*, allows us to avoid redundant computations and significantly improve the efficiency of our solution.

## Version with dynamic programming

Here's how we can modify our previous recursive solution to incorporate dynamic programming. We're going to ues a dictionary, `saved`, that maps rod lengths to the maximum revenue possible with that length:

```python
def max_revenue(length, prices, saved):
    # If we've calculated the max revenue for this length before, use it.
    if length in saved:
        return saved[length]

    if length <= 0:
        return 0

    # Start max_val at a value that will be overwritten by any number.
    max_val = float('-inf')

    # Consider every possible combination to cut a rod of length n:
    for i in range(1, length + 1):
        revenue = prices[i] + max_revenue(length - i, prices, saved)
        if revenue > max_val:
            max_val = revenue

    # Save this computation.
    saved[length] = max_val

    return max_val

# Example prices table
prices = {
    1: 1,
    2: 5,
    3: 8,
    4: 9,
    5: 10,
    6: 17,
    7: 17,
    8: 20
}

rod_length = 4
saved = {}
max_revenue = max_revenue_saved(rod_length, prices, saved)
print("Maximum revenue:", max_revenue)
```

## Time Complexity Analysis

With this approach, the time complexity significantly improves to $$O(n^2)$$, where $$n$$ is the length of the rod. This happens because for every cut size, we need to consider the cut sizes of all smaller subproblems. The improvement is achieved by avoiding redundant computations and reusing previously computed results.

However, it's worth noting that the space complexity of the solution increases, due to the storage of intermediate results in the `saved` dictionary. The space complexity becomes $$O(n)$$ as well. This is a classic example of a space-time tradeoff -- we're saving time by storing the intermediate results.

Check out the video below to see another explanation of how dynamic programming can be applied to the rod cutting problem:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/re9rF9SqRFc?si=x946qLsWkJS5Mvcm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Dynamic programming properties

Dynamic programming is a powerful technique used to solve problems by breaking them down into smaller subproblems and solving each subproblem only once. There are two key properties that are necessary for dynamic programming to be applicable, which are:

1. **Optimal Substructure**: The solution to a larger problem can be constructed from the solutions to its smaller subproblems.

2. **Overlapping Subproblems**: The same subproblems are encountered multiple times during the computation.

The rod cutting problem exhibits both optimal substructure and overlapping subproblems. The optimal way to cut a rod of length $$n$$ can be obtained by considering the optimal ways to cut its smaller subrods, and we encounter the same subrod lengths multiple times during the computation. Therefore, dynamic programming is well-suited for solving the rod cutting problem efficiently.

<aside>
<b>Check your understanding</b>
<p>We just discussed the two properties needed for dynamic programming to be applicable. Now, think back to the merge sort algorithm, in which we repeatedly divide a list into smaller and smaller sublists, and then merge sorted sublists together into larger, sorted lists.</p>
<p>Dynamic programming is not applicable to merge sort. Why not?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Merge sort involves combining the solutions to non-overlapping problems, i.e., sublists that are disjoint from each other. You can't reuse the computation of merging two sorted sublists. Therefore, if you tried to apply dynamic programming, there would be no computations to save.</p>
</details>
</aside>
