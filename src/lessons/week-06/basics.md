# Basics

Let's now turn our attention to yet another fundamental data structure: *graphs*. Just like other data structures, such as arrays, linked lists, and trees, graphs are a building block on which we can build other abstractions to solve complex problems.

We have discussed graphs to some degree in previous courses, so let's begin with a review of graphs and the associated terminology. To begin with, here's an example of a graph:

<center>
<img
  src="/images/week-06/dsa2-week6-graph.png"
  alt="An example graph data structure."
  style="width:675px;" />
</center>

Each graph, including the one above, is defined in terms of a set of *vertices* $$V$$ (also known as *nodes) and a set of *edges* $$E$$. Each edge connects a pair of vertices.

Graphs therefore give us the ability to represent entities and the relationships between them. For example, social networks are most naturally represented as graphs.

<aside>
<b>Check your understanding</b>
<p>In a social network graph, what is represented by the vertices? What is represented by the edges?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> In a social network, the vertices are the people (members) of the social network. The edges between member represents that those people are linked in some way ("friends" or "following").</p>
</details>
</aside>

Here's another example: a graph that shows the connectedness of some cities:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities.png"
  alt="Some cities represented as a graph, where the vertices are cities and the edges are the distances of the roads that connect them."
  style="width:675px;" />
</center>

In this case, the vertices represent cities, and the edges represent the lengths of the roads between these cities. This is actually an example of a *weighted* graph, since there is a *cost* associated with each edge. Eventually, we'll be able to represent problems as graphs, and then ask questions like: what's the shortest route from Abuja to Port Harcourt?

Watch the following videos to learn about the basics of graphs:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/gXgEDyodOJU?si=rVi22ScLzlF_LZ0h" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<p></p>
<iframe width="560" height="315" src="https://www.youtube.com/embed/AfYqN3fGapc?si=UEseA4sXyFG0nyki" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Terminology

As you can see from the videos, there is a lot of terminology associated with graphs. Let's revisit some of the more important concepts below with examples:

### Adjacent

Two vertices are *adjacent* if they are connected by a single edge.

For example, in the graph below, nodes $$d$$ and $$f$$ are adjacent, but $$f$$ and $$j$$ are not adjacent.

<center>
<img
  src="/images/week-06/dsa2-week6-graph.png"
  alt="An example graph data structure."
  style="width:675px;" />
</center>

### Neighbors

The collection of vertices that are adjacent to a vertex $$v$$ are known as the *neighbors* of $$v$$. For example, the neighbors of $$d$$ are $$c$$, $$f$$, and $$e$$.

### Path

A *path* in a graph is a sequence of edges that connects two vertices. For example, here's a graph with a highlighted path:

<center>
<img
  src="/images/week-06/dsa2-week6-path.png"
  alt="A graph marked with a path that goes through a subset of the graph's vertices."
  style="width:675px;" />
</center>

### Connected

A graph is *connected* if there is a path between any two pairs of vertices. The graph above is connected, but the following six vertices (all part of the same graph) are not connected:

<center>
<img
  src="/images/week-06/dsa2-week6-connected.png"
  alt="A graph composed of two groups of vertices, with three vertices in each group."
  style="width:500px;" />
</center>

Sometimes, we call the different parts of an unconnected graph *islands*, as in, the above graph has two islands of vertices.

> **Note:**
> Depending on context, you might consider the above image to consist of two connected graphs *or* one unconnected graph.

### Complete

A graph is *complete* if there is an edge between every pair of vertices. Here's an example:

<center>
<img
  src="/images/week-06/dsa2-week6-complete.png"
  alt="A graph composed of five vertices, where each vertex is connected to every other vertex."
  style="width:500px;" />
</center>

### Directed

A *directed* graph has a direction associated with each edge, which is depicted using an arrow:

<center>
<img
  src="/images/week-06/dsa2-week6-directed.png"
  alt="A directed graph, with multiple vertices and directed arrows as edges between the vertices."
  style="width:500px;" />
</center>

Edges in a directed graph are often represented as ordered pairs of the form (start vertex, end vertex). For example, $$(a, b)$$ is an edge in the graph above, but $$(b, a)$$ is not.

Graphs which have no direction on edges are known as *undirected* graphs.

### Cycles

A *cycle* is a path that leaves a given vertex using one edge, and then later returns to that same vertex using a different edge. For example:

<center>
<img
  src="/images/week-06/dsa2-week6-cycle.png"
  alt="An undirected graph with multiple cycles between vertices."
  style="width:625px;" />
</center>

Now that we know a bit about graphs and the terminology used to describe them, we can turn our attention to ways to represent graphs in programs.
