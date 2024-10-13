# Traveling Salesman Problem

To begin this week's material, let's tackle a very famous problem in computer science: the *traveling salesman problem* (TSP).

Here's one way of thinking about the TSP: Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city?

## Definition

The input to the traveling salesman problem is:

* A set of $$n$$ cities.
* A distance matrix (or a set of distances in some format) where each entry specifies the distance between two cities.

The objective is to find the shortest possible route that visits each city once and returns to the starting city.

Watch the following video to see an overview of the TSP:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/1pmBjIZ20pE?si=Xfh1lk8KS6UChwhi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

## Brute force algorithm

One way of solving the TSP is to use a *brute force* approach -- generating all possible permutations of the cities to find the shortest possible route that visits each city exactly once and returns to the starting city.

Here’s a detailed description of this approach:

1. Generate all possible permutations of the cities. For $$n$$ cities, there are $$n!$$ ($$n$$ factorial) possible permutations. However, since the route is a cycle (i.e., starting and ending at the same city), we can fix one city as the starting point and only consider permutations of the remaining $$n−1$$ cities. This reduces the number of permutations to $$(n-1)!$$.

2. For each permutation (route), calculate the total distance by summing the distances between consecutive cities in the permutation and adding the distance from the last city back to the starting city.

3. Compare the total distances of all permutations and keep track of the permutation with the shortest distance.

### Complexity

The brute force approach has a time complexity of $$O(n!)$$, where $$n$$ is the number of cities. This factorial growth makes the brute force approach impractical for large $$n$$. The space complexity is $$O(n)$$, for storing the current permutation and other necessary variables.

Due to its factorial time complexity, the brute force approach is only feasible for small instances of the TSP (usually up to about 10-12 cities). For larger instances, the computation time becomes prohibitively large, necessitating the use of more sophisticated algorithms.

## Held-Karp algorithm

One such algorithm is the *Held-Karp* algorithm. Proposed by Michael Held and Richard M. Karp in 1962, this algorithm is a cornerstone method in computer science, and significantly reduces the computational complexity of solving the TSP compared to brute-force methods. It leverages the principle of dynamic programming to break down the problem into smaller subproblems, which are solved once and stored for future use, thus avoiding redundant calculations.

The algorithm works by iteratively building up the solution using subsets of the cities. It starts with the smallest possible subsets and progressively adds more cities, calculating the minimum cost to reach each subset's final city from the starting point. For each subset of cities, it records the shortest path that ends at each specific city within the subset. This process continues until it encompasses all cities, ultimately determining the shortest path for the complete set.

Watch the following algorithm to learn about the Held-Karp algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/XaXsJJh-Q5Y?si=vQ632YavuuWdYDq_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>

### Complexity

Although the Held-Karp algorithm reduces the time complexity significantly from factorial to exponential (specifically, $$O(n^2*2^n)$$), it is still computationally intensive for very large numbers of cities. Despite this, it remains a critical theoretical approach and a benchmark for evaluating heuristic and approximation algorithms for the TSP.
