# Graph Implementation

Let's now look more closely at a Python implementation of a graph that we'll be using throughout this week. The implementation uses an adjacency list approach, where we have:

* A linked list of `Vertex` objects representing the vertices of the graph
* Each `Vertex` object contains a linked list of `Edge` objects, representing the edges that are connected to the given `Vertex`
* Each `Edge` object contains a reference to the two `Vertex` objects that it connects, along with a cost (weight)

Here's a visual representation of our forthcoming `Graph` class:

<img
  src="/images/week-07/dsa2-week7-graph.png"
  alt="The in-memory representation of a graph that uses a linked list (vertices) of linked lists (edges)."
  style="width:675px;" />

Try to match up the vertices and edges in the graph on the right with the in-memory representation on the left.

Here's the core definitions of the `Graph`, `Vertex`, and `Edge` objects:

```python
class Graph:
    def __init__(self):
        self.vertices = None    # linked list of vertices in the graph

    class Vertex:
        def __init__(self, id):
            self.id = id        # vertex ID
            self.edges = None   # linked list of edges for this vertex
            self.next = None    # next vertex in the linked list of vertices
        ...

    class Edge:
        def __init__(self, start, end, cost):
            self.start = start  # starting vertex of the edge
            self.end = end      # ending vertex of the edge
            self.cost = cost    # weight of the edge
            self.next = None    # next edge in the linked list of edges
        ...
```

<aside>
<b>Check your understanding</b>
<p>Why do both <code>Vertex</code> objects as well as <code>Edge</code> objects contain a <code>next</code> field?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> This <code>Graph</code> class represents the vertices as a linked list of <code>Vertex</code> objects, so each one needs a pointer to the next one in the list. Similarly, each vertex has a linked list of <code>Edge</code> objects, so each one needs a pointer to the next edge in the list.</p>
</details>
</aside>

Here's the full implementation: <code><a href="https://storage.googleapis.com/anchor-eu/csa003_apr_2024/src/images/week-07/graph.py">graph.py</a></code>

Here's a sample graph: <code><a href="https://storage.googleapis.com/anchor-eu/csa003_apr_2024/src/images/week-07/graph.txt">graph.txt</a></code>

When you run `graph.py`, you will be prompted to enter both (1) the name of the input file (`graph.txt` in this case) and (2) the starting point for the algorithms:

```
$ python graph.py
Graph info file: graph.txt
starting point: Lagos

depth-first traversal from Lagos:
...
```

Note that there are a methods provided in `graph.py`:

* `get_vertex()`, `add_vertex()`, and `add_edge()` for fetching and building the graph
* `init_from_file()`, which reads in a graph configuration from a file and creates a `Graph` object with the vertices and edges that are listed in the file (example file)
* Various graph algorithms: `breadth_first_trav()`, `depth_first_trav()`, and `prim()`
* Since the various graph algorithms may mark the graph (such as to mark vertices as encountered or done), there is a `reinit_vertices()` method that resets the state of each vertex so that the next algorithm can have a clean slate
