# Stable Marriage Problem

The *stable marriage problem (SMP)* is a classic problem in the field of combinatorial optimization and computer science, which seeks to find a stable matching between two sets of elements given a set of preferences.

The problem is widely used in matching markets, such as assigning medical residents to hospitals, students to schools, and even in some organ donation programs where donors and recipients are paired. Its importance and utility in economics, game theory, and real-world applications have made it a fundamental problem in algorithm design and analysis, showcasing the intersection of theoretical computer science and practical optimization problems.

The most common scenario involves two equally sized sets of individuals, typically referred to as men and women, each of whom ranks all members of the opposite set based on their preference for marriage partners. The goal is to pair each man with a woman in such a way that no pair of individuals would both prefer each other over their current partners. This condition ensures that no "blocking pairs" exist, which would make the matching unstable.

## Bipartite graphs

In the context of the stable marriage problem, bipartite graphs provide a useful way to visualize and understand the matching process. For the SMP, the two disjoint sets in the bipartite graph represent the two groups to be matched, typically men and women. Each vertex in one set (men) is connected to vertices in the other set (women) based on the potential for marriage. An edge between a man and a woman signifies that they are potential partners.

## Gale-Shapley algorithm

The Gale-Shapley algorithm, also known as the deferred acceptance algorithm, is a solution to the stable marriage problem that ensures a stable matching between two equally sized sets of participants.

The algorithm proceeds in rounds, with each man proposing to his most-preferred woman who has not yet rejected him. Each woman then reviews her current set of proposals, including any existing tentative engagements, and tentatively accepts the proposal from the man she prefers the most while rejecting the others. Rejected men then move on to propose to their next choice. This process repeats until no man has a new woman to propose to, at which point all tentative engagements become final.

Watch the following videos to learn more about the stable marriage problem and Gale-Shapley algorithm:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Qcv1IqHWAzg?si=jV4nFkEBZ4TzrPBa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
<p></p>
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/RE5PmdGNgj0?si=RrEnWcZMyr9UZ-8y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
