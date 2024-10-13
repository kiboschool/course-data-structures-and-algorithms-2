# Linear Programming

*Linear programming* (LP) is a mathematical method used for optimizing a linear objective function, subject to a set of linear inequality or equality constraints.

The primary goal of linear programming is to find the best possible outcome, such as maximum profit or lowest cost, in a mathematical model whose requirements are represented by linear relationships. Linear programming is widely used in various fields, including economics, business, engineering, and military applications, for solving problems related to resource allocation, production planning, transportation, and scheduling.

## Formulating LP problems

To formulate a linear programming problem, you need to define three main components:

1. the objective function
2. the decision variables
3. the constraints

The objective function is a linear equation that represents the goal of the optimization, such as maximizing revenue or minimizing costs. The decision variables are the unknowns that you are solving for, and they represent the quantities you want to determine. The constraints are linear inequalities or equalities that represent the limitations or requirements of the problem.

For example, consider a company that produces two products, $$A$$ and $$B$$. The company wants to maximize its profit, where the profit from product $$A$$ is $5 per unit and from product $$B$$ is $4 per unit.

The production of these products is subject to resource constraints: each unit of product $$A$$ requires 2 hours of labor and 1 unit of material, while each unit of product $$B$$ requires 1 hour of labor and 2 units of material. The company has a total of 100 hours of labor and 80 units of material available. The linear programming model for this problem would be:

Objective function: Maximize profit = $$5A + 4B$$

Constraints:

* $$2A + B \leq 100$$ (labor constraint)
* $$A + 2B \leq 80$$ (material constraint)
* $$A, B \geq 0$$ (non-negativity constraint)

## Simplex algorithm

Linear programming problems can be solved using various methods, the most common of which is the *simplex algorithm*.

To see an overview of linear programming and the simplex algorithm, watch the following video:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/E72DWgKP_1Y?si=NSU3ekHIiT4GN7El" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>
