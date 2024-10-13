# Efficiency and Big-O Notation

With every new data structure and algorithm that we have learned, we have also discussed the efficiency implications. We will continue to do so in this course, and will also learn new ways of evaluating the efficiency of algorithms in terms of time and space.

We have been using *big-O notation* to describe efficiency. To remind yourself of the basics of big-O notation, watch the video below:

<div
  style="position: relative; padding-bottom: 56.25%; height: 0;">
  <iframe
    src="https://www.youtube.com/embed/__vX2sjlpXU?si=3N_7qDTUEeD_v6xA"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

To summarize:

* Big-O notation is a measure of an algorithms efficiency
* It describes the efficiency as a function of the size of the input, `n`
* When given an expression that represents the number of operations of an algorithm, the corresponding big-O notation can be calculated by ignoring lower-order terms and constants
* Other heuristics can be used to derive big-O expressions, such as by analyzing loops
* It's important to remember that big-O notation is a simplified way of describing efficiency that focuses on the *worst-case* behavior of an algorithm; in practice, we care about all cases

<aside>
<b>Check your understanding</b>
<p>Say that there exists two algorithms, A and B, to solve a problem. Algorithm A is <code>O(n)</code>, and algorithm B is <code>O(n<sup>2</sup>)</code>. We know that algorithm A is considered a faster algorithm in general. However, for an input of size <code>n</code> = 1,000,000, does algorithm A necessarily take less time than algorithm B?
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> No. Remember that big-O notation describes an algorithm's <i>asymptotic</i> running time behavior, i.e., how long it will take to run as the input size grows to <i>infinity</i>. Big-O notation is helpful to describe general classes of efficiency, but for practical uses, constants and lower-order terms <i>do</i> make a difference.</p>
<p>For example, algorithm A may be <code>O(n)</code> but have high constant terms associated with it. Meanwhile, algorithm B may indeed be <code>O(n<sup>2</sup>)</code>, but have relatively lower constant terms, making it reasonably fast for some values of <code>n</code>, such as <code>n</code> = 1,000,000.</p>
</details>
</aside>

<aside>
<b>Check your understanding</b>
<p>Consider the following function:</p>
<pre><code class="language-python">def mystery(lst):
    for i in range(len(lst)):
        if lst[i] % 2 == 1: # i is odd
            lst[i] += 1<br>
    total = 0
    for i in range(len(lst)):
        for j in range(i):
            if lst[i] > lst[j]:
                total += 1
    return total</code></pre>
<p>What is the big-O running time of the function?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The first <code>for</code> loop has a running time of <code>O(n)</code>, since the loop bound is some function of the size of the list (<code>n</code>). The second loop is <code>O(n<sup>2</sup>)</code>, since the outer loop is <code>O(n)</code> and the inner loop is <code>O(n)</code> (since it depends on the outer loop variable <code>i</code>). Our expression for the big-O running time is therefore <code>O(n) + O(n)*O(n)</code>, which is <code>O(n<sup>2</sup>)</code>.</p>
</details>
</aside>
