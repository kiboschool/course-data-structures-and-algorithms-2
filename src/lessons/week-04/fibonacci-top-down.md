# Fibonacci Top-Down Dynamic Programming

Let's now take a look at another problem where dynamic programming can be used: the Fibonacci sequence.

We discussed the Fibonacci sequence in the previous data structures course. We defined it to be a series where each number is the sum of the two preceding numbers, starting from $$0$$ and $$1$$. The sequence therefore starts like this:

$$0, 1, 1, 2, 3, 5, 8, 13, 21, ...$$

And continues infinitely. You can define the Fibonacci sequence recursively as:

- Base cases:
  - $$\text{fib}(0) = 0$$
  - $$\text{fib}(1) = 1$$
- Recursive definition:
  - $$\text{fib}(n) = \text{fib}(n-1) + \text{fib}(n-2)$$, for $$n > 1$$

Let's now take a look back the recursive Python solution that we previously came up with to compute the $$n$$th Fibonacci number.

## Naive Fibonacci implementation

We've seen before that we can translate the recursive definition of the Fibonacci sequence above into some Python code as follows:

```python
def fibonacci(n):
    if n == 0:
        return 0
    if n == 1:
        return 1

    return fibonacci(n - 1) + fibonacci(n - 2)
```

This implementation is $$O(2^n)$$, since it requires an exponential number of function calls to compute. The analysis for why this is true is actually very similar to the analysis we did for the rod cutting problem. We end up recomputing the same value over and over again!

## Suitability for dynamic programming

The calculation of the $$n$$th Fibonacci number exhibits the two characteristics that make it suitable for dynamic programming: optimal substructure and overlapping subproblems.

Remember that *optimal substructure* means that an optimal solution to a problem can be constructed from optimal solutions to its subproblems. In the case of the Fibonacci sequence, the optimal substructure property holds because the value of the $$n$$th Fibonacci number depends on the values of the $$(n-1)$$th and $$(n-2)$$th Fibonacci numbers.

It also exhibits the characteristic of *overlapping subproblems*, since there are some subproblems that are reused multiple times. For example, when computing `fibonacci(5)`, we need `fibonacci(4)` and `fibonacci(3)`, both of which require `fibonacci(2)`.

## Applying dynamic programming

Let's now try applying dynamic programming to the Fibonacci problem.

Start with the naive implementation of `fibonacci()` below, and add dynamic programming using a dictionary of pre-computed values. This dictionary, called `saved`, has been added as an optional parameter, so its initial value is the empty dictionary.

Add to the dictionary as necessary, and each time the function is called, first consult the dictionary to check whether the solution to that subproblem has already been computed.

<iframe src="https://trinket.io/embed/python/24d0060652" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

When you think you've got it, check out the solution below:

<details>
<summary>
<i>Click to reveal the solution.</i>
</summary>
<pre><code class="language-python">def fibonacci(n, saved={}):
    if n in saved:
        return saved[n]
    if n == 0:
        return 0
    if n == 1:
        return 1

    saved[n] = fibonacci(n - 1) + fibonacci(n - 2)
    return saved[n]
</code></pre>
</details>

## Memoization

This technique of storing the already computed solutions in temporary data structure is known as *memoization* (note: not the same as *memorization*!). Memoization is a technique used to improve the performance of recursive algorithms by storing the results of expensive function calls and returning the cached result when the same inputs occur again. Essentially, memoization ensures that each subproblem is solved only once, eliminating redundant computations.

Using memoization is known as a *top-down* approach to dynamic programming, since we start with the original problem (the "top"), recursively break it down into smaller subproblems, solve these subproblems one by one until we reach the base cases (the "bottom") and memoize the results, and finally combine the solutions of the subproblems to obtain the solution to the original problem.

Check out the video below to learn more about dynamic programming and memoization:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/P8Xa2BitN3I?si=bLKYK5gKCdh0wm_M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

Aside from top-down dynamic programming, there's another approach known as *bottom-up*. Let's take a look at that next.
