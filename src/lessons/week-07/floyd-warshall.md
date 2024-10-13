# Floyd-Warshall Algorithm

Let's explore another fundamental algorithm in the realm of graph theory: the Floyd-Warshall algorithm. While Dijkstra's algorithm and the Bellman-Ford algorithm focus on finding shortest paths from a *single* source vertex to all other vertices, the Floyd-Warshall algorithm takes a different approach, aiming to find the shortest paths between *all* pairs of vertices in a weighted graph.

## Algorithm

Watch the following video to learn about the Floyd-Warshall algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/4NQ3HnhyNfQ?si=tfYdhS92g9UH2ltD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

Summary:

* The algorithm uses a dynamic programming approach, keeping track of a table of shortest path distances between each pair of vertices, `dp`
* The algorithm performs $$|V|$$ iterations
* At each iteration $$k$$, the algorithm considers all pairs of vertices $$i$$ and $$j$$, and updates the table `dp[i][j]` if there exists a shorter path from $$i$$ to $$j$$ through vertex $$k$$
* At the end of the algorithm, the `dp` table contains all shortest path distances between every pair of vertices

## Time analysis

To find all possible $$|V|^2$$ shortest paths between all vertices $$i$$ and $$j$$, the algorithm does $$O(|V|)$$ amount of work for each shortest path, leaving an overall running time of $$O(|V|^3)$$. It's also worth noting that the algorithm requires $$O(|V|^2)$$ extra space to keep track of all of the distances for every pair of vertices.

## Summary

Watch the following video for a summary of the Floyd-Warshall algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/4OQeCuLYj-4?si=wPOQejRlxHFBbiwl" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
