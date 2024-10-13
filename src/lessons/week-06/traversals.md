# Traversals

In a previous course, we saw that we can traverse trees in a variety of ways, including *depth-first* traversals (including pre-order, post-order, and in-order traversals), and *breadth-first* traversals (which is the same as a level-order traversal).

With graphs, we need similar traversal algorithms. Given a starting point, we need to define ways of traversing the graph to visit all of the nodes -- at least, the ones reachable from the starting point.

<aside>
<b>Check your understanding</b>
<p>Given a vertex to start from, how is it possible that there are other vertices that are not reachable from the starting node? Think of what conditions could make this possible.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> In a graph that is not connected, when you start from a given vertex, you won't be able to reach other islands of vertices since there are no edges that lead there. Also, in directed graphs, there may be edges present between all of the vertices, but they may not be directed in a way that's needed to be able to reach each other.</p>
</details>
</aside>

Let's talk about the two main traversal techniques: depth-first and breadth-first traversals.

## Depth-first traversal

Watch the following video to see how a depth-first traversal works on graphs, and to see what kinds of algorithms you can write with a depth-first traversal:

<iframe width="560" height="315" src="https://www.youtube.com/embed/7fujbpJ0LB4?si=9Zm0r9vjAUSJuRh2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

To summarize:

* A depth-first traversal proceeds as far as possible along a given path before backing up
* A DF traversal is most naturally implemented recursively
* Since graphs can have cycles (unlike trees), we need to mark nodes as "visited" in order to know when the recursion down a particular path should stop

<aside>
<b>Check your understanding</b>
<p>What would happen in the depth-first traversal algorithm if nodes are not marked as visited?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Marking nodes as visited is the way in which we decide when the recursive calls down a particular path should stop. Without it, a DF traversal could continually follow cycles in the graph, leading to infinite recursion.</p>
</details>
</aside>

<aside>
<b>Check your understanding</b>
<p>Consider the following graph:</p>
<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities.png"
  alt="Some cities represented as a graph, where the vertices are cities and the edges are the distances of the roads that connect them."
  style="width:475px;" />
</center>
<p>If a DF traversal was run on this graph starting from Lagos, what would be the order in which cities are visited? Assume that if there are multiple options for the next neighbor (city) to visit, the <i>nearest</i> neighbor is chosen.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> The DF traversal starts from Lagos and marks it as visited. It then goes to Ibadan (since it is the closest neighbor to Lagos) and marks it as visited. From Ibadan, the only unvisited neighbor is Abuja, so we visit Abuja. From Abuja, the closest neighbor is Kaduna, so we mark it as visited and then also visit Kano, since it is the only unvisited neighbor of Kaduna.<p>
<p>At Kano, we have no unvisited neighbord, so we backtrack to Kaduna. At Kaduna, we also have no unvisited neighbors, so we backtrack to Abuja. At Abuja, we the next closest unvisited neighbor is Onitsha, so we visit it and then visit Aba. From Aba, we visit Port Harcourt. At Port Harcourt, the only unvisited neighbor is Benin City. Once we visit Benin City, it has no unvisited neighbors, so we return back to Port Harcourt.</p>
<p>We then similarly return back through Aba, Onitsha, Abuja, and Ibadan. Back at Lagos, there are also no remaining unvisited neighbors, so the DF traversal is complete.</p>
<p>The final order is therefore: Lagos, Ibadan, Abuja, Kaduna, Kano, Onitsha, Aba, Port Harcourt, Benin City.
</details>
</aside>

For your reference, here's some pseudocode for a depth-first traveral (assuming an adjacency list graph):

```python
def df_trav(v, parent):
    # Visit v.
    print(v.id)

    # Mark this vertex as visited.
    v.done = True

    # Mark this vertex's parent in the DF traversal
    v.parent = parent

    # Iterate over the vertex's adjacency list.
    e = v.edges
    while e is not None:
        w = e.end # Consider a neighbor w
        if not w.done:
            df_trav(w, v)
        e = e.next
```

## Breadth-first traversal

Watch the following video to see how a breadth-first traversal works on graphs, and to see what kinds of algorithms you can write with a breadth-first traverasl:

<iframe width="560" height="315" src="https://www.youtube.com/embed/oDqjPvD54Ss?si=7jbtaEMZMcrBlztm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

To summarize:

* A breadth-first traversal uses the following algorithm:
    1. visit a vertex
    2. visit all of its neighbors
    3. visit all unvisited vertices 2 edges away
    4. visit all unvisited vertices 3 edges away, etc
* In order to visit one level at a time, the BF traversal algorithm uses an auxiliary queue
* Nodes still need to be marked as visited during the algorithm, since nodes can be seen in multiple "levels" of the traversal (since there can be cycles)

<aside>
<b>Check your understanding</b>
<p>Consider the following graph:</p>
<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities.png"
  alt="Some cities represented as a graph, where the vertices are cities and the edges are the distances of the roads that connect them."
  style="width:475px;" />
</center>
<p>If a BF traversal was run on this graph starting from Lagos, what would be the order in which cities are visited? Assume that at each city, the unvisited neighboring cities are added to the queue in order by smallest distance first.</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> We start from Lagos and Ibadan and Benin City to the queue (in that order). We dequeue Ibadan and visit it. There, the only unvisited neighbor is Abuja, so we enqueue that. The next city dequeued is Benin City, so we visit it and add Port Harcourt to the queue. So far, we've visited all of the cities a distance of 0 or 1 edges away from Lagos.</p>
<p>The next city in the queue is Abuja. We visit it and Kaduna and Onitsha to the queue (in that order). We next dequeue Port Harcourt, and add Aba to the queue. The queue is therefore: Kaduna, Onitsha, Aba at this stage, and at this point, we have visited all cities a distance of 2 or fewer away from lagos.</p>
<p>We dequeue Kaduna and visit it, and add Kano to the queue. We next dequeue Onitsha, but it has no unvisited neighbors. We then dequeue Aba, but it also has no unvisited neighbors. We have now visited all neighbors a distance of less than or equal to three edges away from Lagos.</p>
<p>The only remaining item in the queue is Kano, so we dequeue it and since the queue is empty, the BF traversal is done. The final order is therefore: Lagos, Ibadan, Benin City, Abuja, Port Harcourt, Kaduna, Onitsha, Aba, Kano.</p>
</details>
</aside>

For your reference, here's some pseudocode to implement the BF traversal (assuming an adjacency list implementation):

```python
def bf_trav(origin):
    origin.encountered = true
    origin.parent = null

    q = Queue()
    q.insert(origin)
    while len(q) > 0:
        # Get next vertex in the traversal.
        v = q.remove()

        # Visit v.
        print(v.id)

        # Add v's unencountered neighbors to the queue.
        e = v.edges
        while e is not None:
            w = e.end
            if not w.encountered:
                w.encoutered = True
                w.parent = v
                q.insert(w)
            e = e.next
```
