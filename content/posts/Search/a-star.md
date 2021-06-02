---
title: "Understanding A* Search"
date: "2021-6-1"
template: "post"
draft: false
slug: "/posts/a-star/"
category: "Search"
tags:
  - ""
description: ""
---

Consider a graph with no step costs. Let the start node be $S$ and goal state be $X$. And as always, the frontier queue starts off with just the start node $S$.

<figure style="width: 700px">
	<img src="/media/search/no-cost-graph.svg" alt="A Simple Graph">
	<figcaption>A Simple Graph</figcaption>
</figure>

If you use _breadth-first search_ to find $X$, you will always get the shallowest node on the search tree with the state $X$.

[Provide example]

**But what happens when you introduce step costs into the graph?** BFS will not be optimal. This is because a shallow node can still have a higher _path cost_ than a deep node.

[Provide example]

We need an algorithm that considers the step costs. This is where uniform-cost search comes in.

**Uniform-cost search** maintains its frontier in a priority queue ordered by the function $g$. The function $g(n)$ is the path cost from $S$ to the current node $n$.

[Provide example]

The algorithm pops out the first element $n$ in the queue, which is the node with the lowest path cost $g(n)$. If $n$ is the goal state, search is done. If not, then its successors are pushed into the priority queue.

Uniform-cost search does not care about the number of nodes on a path, only the total path cost. This is why it pushes the new successors into the priority queue, instead of performing a goal test immediately. If a successor $m$ has the lowest path cost $g(m)$, then it will be the first element of the priority queue and will be chosen in the next round.

The uniform-cost search algorithm is a form of uninformed search, since it does not use any problem-specific knowledge. On the other hand, the **Greedy best-first search** algorithm is a form of informed search and uses problem-specific heuristics to find the goal state. A heuristic is a non-negative, problem-specific function with one constraint : if $n$ is a goal state, then $h(n) = 0$.

[Provide example]

The node to be expanded next is chosen based on a **evaluation function** $f(n)$. It calculates an estimate of the actual cost of the path to the goal state. The node with the lowest cost estimate will be expanded first.

Greedy best-first search evaluates nodes by just using the heuristic $h(n)$,

$$
f(n) = h(n)
$$

For example, lets say you need to find a route from New York to Chicago. You could use the straight line distance heuristic in the scenario.

[Provide example]

**A\* Search**

The evaluation function for the A\* algorithm is written as,

$$
f(n) = g(n) + h(n)
$$

where, $g(n)$ is the actual path cost from the start node $S$ to the current node $n$, and $h(n)$ is the heuristic function that estimates the lowest path cost from current node $n$ to the goal state $X$.

# References

- [Artificial Intelligence : A Modern Approach](http://aima.cs.berkeley.edu/)
- [StackExchange : How does an admissible heuristic ensure an optimal solution?](https://cs.stackexchange.com/questions/16065/how-does-an-admissible-heuristic-ensure-an-optimal-solution)
- [Artificial Intelligence : Foundations of Computational Agents, Chapter 3](https://artint.info/2e/html/ArtInt2e.Ch3.S6.SS1.html)
