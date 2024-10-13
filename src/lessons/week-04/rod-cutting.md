# Rod Cutting Problem

The *rod cutting problem* is a classic optimization problem in computer science and mathematics. It involves cutting a rod of a certain length into smaller pieces to maximize the total revenue obtained from selling those pieces. This problem has various practical applications, such as in manufacturing, resource allocation, and finance.

Let's take a closer look at this problem to motivate our study of dynamic programming.

## Problem Setup

In the rod cutting problem, we are given:

- A rod of length $$n$$ cm
- A table of prices $$p_i$$ for rod pieces of length $$i$$, where $$i$$ ranges from 1 to $$n$$

The goal is to determine the optimal way to cut the rod to maximize revenue. Each cut of the rod is free. Note that if the price $$p_n$$ of a rod of length $$n$$ is large enough, the optimal solution might be to not cut the rod at all.

## Example

Let's consider the following table of prices for rod pieces of different lengths:

| Length          | Price     |
|-----------------|-----------|
| 1               | 1         |
| 2               | 5         |
| 3               | 8         |
| 4               | 9         |
| 5               | 10        |
| 6               | 17        |
| 7               | 17        |
| 8               | 20        |

Say that we have a rod of length $$n = 4$$. The following image shows all of the possible ways that we could cut a rod of this length:

<center>
<img
  src="/images/week-04/dsa2-week4-rod-cutting.png"
  alt="All of the eight possible ways of cutting a rod of length 4 units, along with the revenue generated for each."
  style="width:675px;" />
</center>

The optimal solution with this price table is to cut the rod into two rods of length 2 cm, since that leads to a revenue of 10.

Next, let's think about how to write a program that solves this problem.

## Solution Approach: Recursive Strategy

One approach to solve the rod cutting problem is through a recursive strategy. We start by considering all possible ways to cut the rod into smaller pieces and calculate the revenue for each combination. We then choose the combination that yields the maximum revenue.

### Python Implementation

```python
def max_revenue(length, prices):
    if length <= 0:
        return 0

    # Start max_val at a value that will be overwritten by any number.
    max_val = float('-inf')

    # Consider every possible combination to cut a rod of length n:
    for i in range(1, length + 1):
        revenue = prices[i] + max_revenue(length - i, prices)
        if revenue > max_val:
            max_val = revenue

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
max_revenue = max_revenue(rod_length, prices)
print("Maximum revenue:", max_revenue)
```

This implementation defines a function `max_revenue(length, prices)` that takes the length of the rod and a dictionary of prices as input and returns the maximum revenue that can be obtained by cutting the rod. It recursively considers all possible ways to cut the rod and calculates the revenue for each combination, then returns the maximum revenue among them.

For example, say that we want to know the maximum revenue that we can generate with a rod of length `4`. This is represented by `max_revenue(4)` (ignoring the `prices` parameter for simplicity). In the stack frame for `max_revenue(4)`, we find the maximum among the following:

```
price(1) + max_revenue(3)
price(2) + max_revenue(2)
price(3) + max_revenue(1)
price(4) + max_revenue(0)
```

We apply the function recursively, and in the end return the maximum.

### Time Complexity Analysis

The time complexity of this recursive approach is *exponential*, specifically $$O(2^n)$$, where $$n$$ is the length of the rod.

This exponential time complexity arises because the function explores all possible combinations of cuts, leading to a function call tree with $$2^n$$ nodes. Each node in the call tree represents a subproblem, and as the rod length increases, the number of subproblems grows exponentially.

For example, let's consider the call tree for a rod of length 4 cm:

<center>
<img
  src="/images/week-04/dsa2-week4-rod-call-tree.png"
  alt="The call tree for calculating the maximum revenue for a rod of length 4. Branches in a tree-like structure to recursively compute the maximum revenue for a rod of length 3, a rod of length 2, a rod of length 1, etc."
  style="width:650px;" />
</center>

In this call tree:

- At each level, the function makes a decision to cut the rod at a particular length, starting from the maximum length and recursively exploring all possible cuts.
- The tree branches out exponentially as the function explores all possible combinations of cuts.

As we can see, the call tree grows exponentially with the length of the rod.

| Rod length      | Number of calls   |
|-----------------|-------------------|
| 0               | 1                 |
| 1               | 2                 |
| 2               | 4                 |
| 3               | 8                 |
| 4               | 16                |
| ...             | ...               |
| n               | 2^n               |

For a rod of length $$n$$, the number of nodes in the call tree is exactly $$2^n$$. This exponential growth in the number of function calls leads to the overall time complexity of $$O(2^n)$$, which is an extremely expensive algorithm!

Next, let's look at a new technique to reduce the complexity of this algorithm: dynamic programming!
