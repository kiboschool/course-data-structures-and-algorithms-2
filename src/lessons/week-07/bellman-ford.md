# Bellman-Ford Algorithm

In addition to Dijkstra's algorithm, there is another common algorithm for solving the single-source shortest paths problem: the Bellman-Ford algorithm.

The Bellman-Ford algorithm is actually slower than Dijkstra's algorithm, but it has one notable advantage: it is capable of solving the shortest paths problem even for graphs that have some edges with *negative* weights.

## Negative edge weights

Negative edge weights are exactly what they sound like: weights assigned to edges in a graph that have a negative value. While they might seem counterintuitive at first, negative edge weights serve various purposes and can model a wide range of real-world scenarios. These scenarios include:

* Time savings: In certain scenarios, negative edge weights can represent time savings. For instance, if the edge weight between two cities represents travel time, a negative weight might indicate that taking a certain route reduces travel time, perhaps due to a shortcut or a faster mode of transportation.
* Financial transactions: In financial networks or economic models, negative edge weights can represent gains or profits. For instance, in a trade network, negative weights could signify profitable transactions or reduced costs associated with certain trade routes.
* Resource allocation: Negative edge weights can also model situations where resources are saved or conserved. For example, in a network representing resource allocation, a negative weight could denote a more efficient use of resources or a reduction in resource consumption along a particular path.

## Bellman-Ford algorithm

The algorithm itself is similar to Dijkstra's algorithm, in that it repeatedly *relaxes* edge estimates. The main difference, however, is that Bellman-Ford repeatedly relaxes *all* edges in the graph, whereas Dijkstra's algorithm relaxes the edges connected only to each vertex as each vertex is finalized.

Since the Bellman-Ford algorithm can work on graphs with negative weights, a possible output of the algorithm is that there *are no* shortest paths due to the existence of cycles in the graph with net negative cost. If such negative cycles exist, then the algorithm returns that fact. Otherwise, the algorithm returns the shortest paths from a given vertex.

In pseudocode, the algorithm works as follows:

1. Initialization: Set the distance from the source vertex to itself as 0, and all other distances as infinity.

2. Relaxation: Repeat the following relaxation step for $$|V| - 1$$ times:

    * For each edge $$(u, v)$$ in the graph, relax the edge by updating the distance to vertex $$v$$ if the distance to $$u$$ plus the weight of $$(u, v)$$ is less than the current distance estimate to $$v$$.

3. Detection of Negative Cycles: After the relaxation step, perform an additional iteration over all edges. If any distance is updated during this iteration, it indicates the presence of a negative cycle in the graph.

Watch the following video to learn about the Bellman-Ford algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/lyw4FaxrwHg?si=xxMkOLj1nKNwiRZD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Time analysis

We mentioned above that the Bellman-Ford algorithm is slower than Dijkstra's algorithm. That's because whereas Dijkstra's algorithm is $$O(|E|log|V|)$$, Bellman-Ford is $$O(|E||V|)$$. This is easily seen from the pseudocode of the algorithm: relax all $$|E|$$ edges repeatedly for $$O(|V|)$$ times.

## Summary

Watch the following short videos to summarize the concept of Bellman-Ford and see another example:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/9PHkk0UavIM?si=jFM3uC_rqUYYJ-jT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
<p></p>
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/obWXjtg0L64?si=LlUUkcqpkRWCgWwK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
