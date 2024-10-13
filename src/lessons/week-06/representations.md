# Representations

Now that we understand the definition of graphs, we can turn our attention to thinking about how to represent them in computers.

Think back to our time designing data structures such as stacks, queues, and heaps. In those cases, we had choices to make about how to represent them in memory. In particular, we were able to choose between array-based data structures and linked data structures. For example, in a previous course we saw how to represent stacks and queues with both arrays and linked lists, and in this course saw that we could greatly simplify the representation of a heap (a complete tree) by using an array.

For graphs, there are typically three ways that they can be represented in a program's memory:

1. Edge list
2. Adjacency matrix
3. Adjacency list

Let's now talk about each of these representations.

## Edge list

Watch the following video to see how to represent a graph using a vertex list and edge list:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZdY1Fp9dKzs?si=-yCosVfmVayKZquy" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize:

* Graphs can be represented as separate lists: one for the vertices $$V$$, and one for the edges $$E$$
* Algorithms like finding all vertices that are adjacent to a given vertex, or checking whether two vertices are adjacent, require time $$O(|E|)$$, which in the worst case can be $$O(|V|^2)$$, which is not very time efficient

## Adjacency matrix

Another option is to represent the graph using an adjancency matrix:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/9C2cpQZVRBA?si=wI9MGI3v-WHSkOvY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

To summarize:

* Graphs can be represented using a list of vertices and a two-dimensional matrix that represents the edges between those vertices
* When represented this way, finding the adjacent vertices of a given vertex only requires $$O(|V|)$$ time, and checking whether two vertices are adjacent is even better: $$O(1)$$ time!
* The main disadvantage is that we now require $$O(|V|^2)$$ space to store the edge representation

Let's take a closer look at our cities graph from the previous lesson. If we chose to store it as an adjacency matrix, here's what it would look like:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities-matrix.png"
  alt="Representing the cities graph using an adjacency matrix."
  style="width:650px;" />
</center>

## Adjacency list

The final representation of graphs we will consider is that of an adjacency list:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/k1wraWzqtvQ?si=AS0Z7Fu8hTK9KVRg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
To summarize:

* For every vertex, we can keep track of the vertices with which it is neighbors using an adjacency list
* This makes (1) finding the adjacent vertices of a given vertex and (2) checking whether two vertices are adjacent run in time $$O(|V|)$$, but typically performs much better than the edge list representation, since we don't need to consider unrelated vertices

Bringing back our cities example, here is our final representation using an adjacency list. Note that two of the vertices and the edge connecting them are highlighted in the diagram:

<center>
<img
  src="/images/week-06/dsa2-week6-graph-cities-list.png"
  alt="Representing the cities graph using an adjacency list."
  style="width:650px;" />
</center>
