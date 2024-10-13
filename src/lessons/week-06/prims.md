# Prim's Algorithm

There are multiple different ways of finding the minimum spanning tree of a graph. For example, a naive algorithm would just enumerate every possible spanning tree that can be formed from the graph, and would keep the one with the lowest total weight. However, in the worst case, for a connected graph there are $$O(n^n)$$ possible spanning trees, and so this is not a practical algorithm.

One popular alternative for efficiently computing the MST of a graph is *Prim's algorithm.*. Let's see how it works.

## Algorithm

The algorithm is as follows:

* Begin with the following two subsets:
    * $$A$$ = any one of the vertices
    * $$B$$ = all of the other vertices
* Repeatedly do the following:
    * Select the lowest-cost edge $$(v_a, v_b)$$ connecting a vertex in $$A$$ to a vertex in $$B$$
    * Add $$(v_a, v_b)$$ to the spanning tree
    * Move vertex $$v_b$$ from set $$B$$ to set $$A$$
*  Continue until set $$A$$ contains all of the vertices.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/jsmMtJpPnhU?si=R8t8yc5PmULhCLuf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Efficiency

Let's think about the efficiency of Prim's algorithm, both for an adjacency matrix and an adjacency list.

When using an adjacency matrix representation, Prim's algorithm has a time complexity of $$O(|V|^2)$$, where $$V$$ represents the vertices in the graph. This is because in each iteration of the algorithm, it scans through the entire adjacency matrix to find the minimum-weight edge connecting a vertex from the MST to a vertex outside the MST. Since there are $$|V|$$ vertices and for each vertex, we might have to consider all other vertices to find the minimum edge weight, the time complexity becomes $$O(|V|^2)$$.

For an adjacency list, in the worst case, you need to scan through all $$|E|$$ edges for every one of the $$|V|$$ nodes. Therefore, the running time is $$O(|V|*|E|)$.

## Example

Recall our city graph from the previous lessons:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities.png"
  alt="Some cities represented as a graph, where the vertices are cities and the edges are the distances of the roads that connect them."
  style="width:675px;" />
</center>

<aside>
<b>Check your understanding</b>
<p>Run Prim's algorithm on the graph above, starting with Lagos as the node in the first set.
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Starting with the set A being <code>{ Lagos },</code>, we have a choice between Ibadan and Benin City. Ibadan is closer, so we add the edge <code>(Lagos, Ibadan)</code> to the MST, and also add Ibadan to the set of cities already considered.</p>
<p>The next smallest edge between <code>{ Lagos, Ibadan }</code> and any other city is the length 400 edge between Lagos and Benin City, so we add that.</p>
<p>Next, the smallest edge between the elements in the set and the elements outside of the set is the edge between Benin City and Port Harcourt, so that gets added. The next smallest edge would be the edge between Port Harcourt and Aba, and so that would be added as well.</p>
<p>At this stage, the list of vertexes already considered is <code>{ Lagos, Ibadan, Benin City, Port Harcourt, Aba }</code>. The next smallest edge is the one connecting Aba to Onitsha, so we add it, along with the following: (Onitsha, Abuja); (Abuja, Kaduna); (Kaduna, Kano).</p>
</details>
</aside>

## Summary

Watch the video below to see a summary of Prim's algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/cplfcGZmX7I?si=RbdQ8lHD_w87xyQ-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
