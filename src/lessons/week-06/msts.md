# Minimum Spanning Trees

In the previous lesson, we performed depth-first and breadth-first traversals of the city graph starting from Lagos. For each traversal, we were looking to find the order in which the cities were visited.

However, instead of the sequence of cities, we could have asked for a different output: the spanning tree produced by each traversal. A *spanning tree* is a subset of a connected graph that contains all of the vertices and a *subset* of the edges, which form a tree. For example, here is the spanning tree produced by the depth-first traversal:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities-dfs-st.png"
  alt="The spanning tree that results from the depth-first traversal starting from Lagos."
  style="width:475px;" />
</center>

Note that the spanning tree is formed by connecting each visited child node with its parent node, which is the node that caused the child to be visited via a recursive call.

And here is the spanning tree produced by the breadth-first traversal:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities-bfs-st.png"
  alt="The spanning tree that results from the breadth-first traversal starting from Lagos."
  style="width:475px;" />
</center>

Note that the spanning tree is formed by connecting each visited child node with its parent node, which is the node that added the child to the queue.

## Minimum spanning trees

Although both the DF traversal and BF traversal produce spanning trees, neither of the spanning trees produced by the algorithm in the example above are *minimum spanning trees*. A minimum spanning tree (MST) has the smallest total cost among all possible spanning trees.

For example, the spanning tree produced by the DF traversal has a total edge weight of 2250, while the BF traversal spanning tree is 2460. However, the MST has a total edge cost of 2050 (it doesn't use the edge between Ibadan and Abuja):

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities-mst.png"
  alt="The minimum spanning tree of the city graph."
  style="width:475px;" />
</center>

Note that if all edges have unique costs, there is only one MST. If some edges have the same cost, there may be more than one MST.

Computing an MST could be useful for various applications, including determining the shortest highway system for a set of cities, or calculating the smallest length of cable needed to connect a network of computers.

> **Note:**
>
> The MST does not necessarily include the minimal cost path between a pair of vertices. For example, the shortest path between Ibadan and Abuja is the edge that directly connects them, which is not included in the MST.

So how can we compute the MST of a graph? Let's next look at one option: Prim's algorithm.
