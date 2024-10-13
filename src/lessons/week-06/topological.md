# Topological Sort

Another interesting algorithm that comes up in many applications is *topological sort*. Topological sort is an algorithm that works specifically on directed acyclic graphs (DAGs), and orders the vertices such that if there is directed edge from $$a$$ to $$b$$, then $$a$$ comes before $$b$$ in the output of the sort.

## DAGs

*Directed acyclic graphs* (DAGs) are a fundamental data structure, often used to represent relationships between objects. As the name suggests, DAGs consist of nodes connected by directed edges, and since they are *acyclic*, they must not contain any cycles.

The importance of DAGs lies in their applicability to a wide range of problems in various fields. In computer science, DAGs are commonly used in algorithms for tasks such as scheduling and dependency resolution. For example, in software development, DAGs can represent the dependencies between different modules or components of a program, allowing for efficient compilation or build processes.

Beyond computer science, DAGs find applications in domains including biology, finance, and logistics. In finance, they can represent financial transactions and dependencies between assets in a portfolio. In logistics, DAGs can help optimize supply chain management by representing the flow of goods between different locations. Overall, DAGs serve as powerful tools for representing and analyzing complex relationships and dependencies in various domains.

<aside>
<b>Check your understanding</b>
<p>How could a DAG be used to represent prerequisites in a university?</p>
<details>
<summary>
<i>Click to reveal the answer.</i>
</summary>
<p><b>Answer.</b> Prerequisites for classes would be very natural to represent using a DAG, since by their nature, they are directed (you have to take one class before another), and they are acyclic (you don't have classes that are requisites of each other). Therefore, a DAG nicely models the concept of prerequisites.
</details>
</aside>

## Algorithm

Watch the video below to see how topological sort works:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/guJkbg-gnLM?si=Xbs4eT2yme5q9Ynt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
