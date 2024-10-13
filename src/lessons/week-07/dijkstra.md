# Dijkstra's Algorithm

Let's now turn to a new problem that graphs can help us solve: the *shortest path* problem. It's often useful to know the shortest path from one vertex to another – i.e., the one with the minimal total cost. This can help in applications such as routing traffic in the Internet.

For an unweighted graph, we can simply do the following:

1. Start a breadth-first traversal from the origin, $$v$$
2. Stop the traversal when you reach the other vertex, $$w$$
3. The path from $$v$$ to $$w$$ in the resulting (possibly partial) spanning tree is a shortest path

A breadth-first traversal works for an unweighted graph because the shortest path is simply the one with the fewest edges, and a breadth-first traversal visits cities in order according to the number of edges they are from the origin.

<aside>
<b>Check your understanding</b>
<p>Why might this approach not work for a <i>weighted</i> graph?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> It won't necessarily work in a weighted graph because it's possible to connect two vertices via one, very costly edge (they are neighbors), but there may also be a path of multiple low-cost edges that end up being cheaper.</p>
</details>
</aside>

For weighted graphs, there are multiple algorithms that find the shortest paths. One very famous example is Dijkstra's algorithm.

## Dijkstra's algorithm

Dijkstra's algorithm allows us to find the shortest path from a vertex $$v$$ (the *origin*) to all other vertices that can be reached from $$v$$.

The basic idea is to maintain estimates of the shortest paths from the origin to every vertex (along with their costs), and gradually refine these estimates as we traverse the graph

Watch the video below to see how Dijkstra's algorithm works:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/bZkzH5x0SKU?si=JQvjASo2v199X24P" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Implementation

We can now add Dijkstra's algorithm to our `graph.py` file:

```python
    def dijkstra(self, origin_id):
        self.reinit_vertices()
        origin = self.get_vertex(origin_id)
        if origin is None:
            raise ValueError(f"No such vertex: {origin_id}")
        origin.cost = 0

        while True:
            w = None
            v = self.vertices
            while v:
                if not v.done and (w is None or v.cost < w.cost):
                    w = v
                v = v.next

            if w is None or w.cost == float('inf'):
                return

            print(f"\tfinalizing {w.id} (cost = {w.cost}" +
                  (f", parent = {w.parent.id})" if w.parent else ")"))
            print(f"\t\tpath = {w.path_string()}")
            w.done = True

            edge = w.edges
            while edge:
                x = edge.end
                if not x.done:
                    cost_via_w = w.cost + edge.cost
                    if cost_via_w < x.cost:
                        x.cost = cost_via_w
                        x.parent = w
                edge = edge.next
```

Try adding this code to your `graph.py` file and running it with an example graph.

## Example

Recall the graph that we've been using that represents some cities and roads in a map (note: some of the edge weights have been slightly changed from previous versions so that the output of the algorithm is more interesting):

<img
  src="/images/week-07/dsa2-week7-graph-cities.png"
  alt="Some cities represented as a graph, where the vertices are cities and the edges are the distances of the roads that connect them."
  style="width:675px;" />

<aside>
<b>Check your understanding</b>
<p>Run Dijkstra's algorithm on the above graph starting from Abuja. Your answer should be a table where each row contains the name of a city and the shortest path distance from Abuja to that city according to the graph.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Here's the algorithm, step-by-step, from Abuja:
<h2>Iteration 0 (Initial State)</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
  </tr>
</table>
We finalize Abuja (distance 0) and see if we can improve estimates of its neighbors:
<h2>Iteration 1</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
</table>
We finalize Kaduna (distance 310) and see if we can improve estimates of its neighbors:
<h2>Iteration 2</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
</table>
We finalize Onitsha (distance 430) and see if we can improve estimates of its neighbors:
<h2>Iteration 3</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
  </tr>
</table>
We finalize Kano (distance 530) and see if we can improve estimates of its neighbors (it has no unfinalized neighbors, so we can't improve at all):
<h2>Iteration 4</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
    <th>Iteration 4</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
    <td>690</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
    <td>620</td>
  </tr>
</table>
We finalize Ibadan (distance 600) and see if we can improve estimates of its neighbors:
<h2>Iteration 5</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
    <th>Iteration 4</th>
    <th>Iteration 5</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>740</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
    <td>690</td>
    <td>690</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
  </tr>
</table>
We finalize Aba (distance 620) and see if we can improve estimates of its neighbors:
<h2>Iteration 6</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
    <th>Iteration 4</th>
    <th>Iteration 5</th>
    <th>Iteration 6</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>740</td>
    <td>740</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
    <td>690</td>
    <td>690</td>
    <td>680</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
  </tr>
</table>
We finalize Port Harcourt (distance 680) and see if we can improve estimates of its neighbors:
<h2>Iteration 7</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
    <th>Iteration 4</th>
    <th>Iteration 5</th>
    <th>Iteration 6</th>
    <th>Iteration 7</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>980</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>740</td>
    <td>740</td>
    <td>740</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
    <td>690</td>
    <td>690</td>
    <td>680</td>
    <td>680</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
  </tr>
</table>
We finalize Lagos (distance 740) and see if we can improve estimates of its neighbors (but we can't, since the route to Benin City through Lagos is longer than the route through Port Harcourt):
<h2>Iteration 8</h2>
<table>
  <tr>
    <th>City</th>
    <th>Iteration 0</th>
    <th>Iteration 1</th>
    <th>Iteration 2</th>
    <th>Iteration 3</th>
    <th>Iteration 4</th>
    <th>Iteration 5</th>
    <th>Iteration 6</th>
    <th>Iteration 7</th>
    <th>Iteration 8</th>
  </tr>
  <tr>
    <td>Abuja</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Kaduna</td>
    <td>∞</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
    <td>310</td>
  </tr>
  <tr>
    <td>Kano</td>
    <td>∞</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
    <td>530</td>
  </tr>
  <tr>
    <td>Ibadan</td>
    <td>∞</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
    <td>600</td>
  </tr>
  <tr>
    <td>BeninCity</td>
    <td>∞</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>1000</td>
    <td>980</td>
    <td>980</td>
  </tr>
  <tr>
    <td>Lagos</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>740</td>
    <td>740</td>
    <td>740</td>
    <td>740</td>
  </tr>
  <tr>
    <td>PortHarcourt</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>690</td>
    <td>690</td>
    <td>690</td>
    <td>680</td>
    <td>680</td>
    <td>680</td>
  </tr>
  <tr>
    <td>Onitsha</td>
    <td>∞</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
    <td>430</td>
  </tr>
  <tr>
    <td>Aba</td>
    <td>∞</td>
    <td>∞</td>
    <td>∞</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
    <td>620</td>
  </tr>
</table>
We can then finalize the estimate to Benin City (distance 980) as it is the last unfinalized vertex.
</details>
</aside>

## Time analysis

The time complexity of Dijkstra's algorithm depends in part on what technique is used to select the vertex with the next-smallest estimate in order to finalize it. For example, for every iteration of the algorithm, we could scan over the entire list of vertices, but a faster way would be to store the vertices in a min-at-top priority queue, where the priority is the vertex's current shortest path estimate. This way, we could repeatedly remove the next-smallest estimate vertex and finalize it.

When using a priority queue, each operation to the extract the minimum takes $$O(log|V|)$$ time, and there are $$|V|$$ such operations. Over the course of the algorithm, vertexes are decreased according to the $$|E|$$ edges, and each decrease operation requires $$O(log|V|)$$ time, since you must search through the heap for the vertex whose estimate you want to decrease. Therefore, the running time is $$O(|E|*log|V| + |V|*log|V|) = O((|E| + |V|)log|V|)$$. In most cases, $$|E| > |V|$$, so often the running time is written as $$O(|E|log|V|)$$.

## Summary

Watch the following video to see a quick summary of Dijkstra's algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/_lHSawdgXpI?si=qqIUz0FRWrK-FUmW" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
