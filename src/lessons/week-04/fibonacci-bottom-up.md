# Fibonacci Bottom-Up Dynamic Programming

In the previous lesson, we explored memoization, a top-down approach to dynamic programming. We learned how memoization optimizes recursive algorithms by caching results and reusing solutions to overlapping subproblems. Now, let's delve into another approach: *bottom-up* dynamic programming.

Unlike memoization, which starts with the original problem and recursively breaks it down into smaller subproblems, bottom-up dynamic programming works *iteratively* from the bottom (i.e., the base cases) up to the original problem.

## Bottom-up approach

When devising a bottom-up solution, we can use the following steps:

1. **Initialization:** Solve the base cases of the problem and store their solutions.

2. **Iterative Solution:** Iteratively solve increasingly larger subproblems, building up the solutions based on previously computed ones.

3. **Optimal Solution:** By the end of the iteration, we have computed the solution to the original problem.

Bottom-up dynamic programming is particularly useful when it's easy to determine the order in which subproblems should be solved and when all subproblems need to be solved.

## Applying bottom-up to Fibonacci

Let's see how bottom-up dynamic programming can be applied to the problem of computing the $$n$$th Fibonacci number. Instead of recursively solving smaller subproblems, we'll iteratively compute Fibonacci numbers starting from the base cases.

With the steps above in mind, we'll proceed as follows:

1. Initialize a list to store the first two Fibonacci numbers: `fib[0] = 0` and `fib[1] = 1`.
2. Iterate from `2` to `n`, computing each Fibonacci number as the sum of the two preceding ones: `fib[i] = fib[i - 1] + fib[i - 2]`.
3. The value of `fib[n]` represents the $$n$$th Fibonacci number.

```python
def fibonacci_bottom_up(n):
    fib = [0, 1] # the first two Fibonacci numbers
    for i in range(2, n + 1):
        next_number = fib[i - 1] + fib[i - 2]
        fib.append(next_number)
    return fib[n]
```

<aside>
<b>Check your understanding</b>
<p>What's the running time of the <code>fibonacci_bottom_up()</code> function above? Also, what's the space complexity?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> There's a single <code>for</code> loop that runs up to <code>n</code>, and the code inside the loop completes in constant time. Therefore, the running time is <code>O(n)</code>. Since we use a list to store all <code>n</code> Fibonacci numbers, the space complexity is also <code>O(n)</code>.</p>
</details>
</aside>

<aside>
<b>Check your understanding</b>
<p>Notice in the implementation of <code>fibonacci_bottom_up()</code> that we don't really <i>need</i> a list of length <code>n</code> -- at any point in time, we only care about the previous two Fibonacci numbers because we need them to compute the next Fibonacci number. Can you rewrite the function to improve the space complexity?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> We can accomplish this by only using two variables instead of a list. These variables represent the previous two Fibonacci numbers:</p>
<pre><code class="language-python">def fibonacci_bottom_up(n):
    if n <= 1:
        return n
    prev = 0
    curr = 1
    for _ in range(2, n + 1):
        temp = prev + curr
        prev = curr
        curr = temp
    return curr
</code></pre>
<p>Note that we need a variable <code>temp</code> in order to correctly advance the values (unless you use multiple assignment). Since we use only a constant number of variables, the space complexity is now <code>O(1)</code>.
</details>
</aside>

## Choosing top-down vs. bottom-up

Now that we know there are two different approaches to dynamic programming, you might be wondering which one you should choose when faced with a relevant problem.

In general, the two approaches are interchangeable, but here are some specific advantages of each:

* **Top-down (memoization)**: Intuitive and easy to implement, especially when translating an existing recursive solution to a memoized solution. Efficiently handles problems with a large state space by storing computed results in a cache. Preferred when the problem naturally lends itself to recursion and when only a subset of the state space needs to be explored.

* **Bottom-up**: Typically more efficient in terms of space complexity, especially for problems with a straightforward order of computation. Avoids the overhead of function calls and recursion. Preferred when all subproblems need to be solved and when the order of computation is well-defined.

Next, let's take a look at one more dynamic programming problems: computing the longest common subsequence.
