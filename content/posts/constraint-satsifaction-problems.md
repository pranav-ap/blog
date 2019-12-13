---
title: "Constraint Satisfaction Problems"
date: "2019-11-16"
template: "post"
draft: false
slug: "/posts/constraint-satisfaction-problems/"
category: "Artificial Intelligence"
tags:
  - ""
description: ""
---

**Constraint satisfaction problems** (CSP) are defined as a set of variables whose values must satisfy a number of constraints.

In many cases, framing a problem as a CSP rather than a search problem, can make it faster and easier to solve.

# Components of a CSP

A CSP consists of multiple **variables** $X$ for which we need to find allowable values. This set of allowable values is called a **domain**. A domain can be finite or infinite, discrete or continuous.

A set of **constraints** $C$ can be placed on these variables. Constraints are an arithmetic or logical relationship involving one or more variables.

**Unary constraints** involve only one variable. **Binary constraints** involve two variables... You get the point.

We also have **global constraints**, which specify a relationship between a non-fixed number of variables. They don't necessarily need to involve all the variables.

# Solving a CSP

A state of a CSP at a given point in time is defined by an **assignment** of values to some or all of its variables. An assignment that does not violate any constraints is said to be **consistent**, otherwise it is **inconsistent**.

If every variable is given a value, the assignment is **complete**, otherwise it is **partial**.

A **solution** for a CSP is found if an assignment is both consistent and complete. To solve a CSP, we interleave between the typical *search* and a form of inference called *constraint propagation*. When and how we perform each action depends on the algorithm used.

## Search

**Search** is used to explore new values for variables and tests whether an assignment forms a solution.

Each node of the search tree or graph represents a partial or complete assignment. We choose a variable from a leaf node and assign it a legal value from its domain. Then we move onto another variable. We backtrack if this assignment is inconsistent.

<figure style="width: 500px">
	<img src="/media/artificial intelligence/csp-search-tree.png" alt="CSP Search Tree">
	<figcaption>CSP Search Tree for variables A, B and C</figcaption>
</figure>

This is where we notice the advantage of a *factored representation* over an atomic representation. We can determine whether a state (or assignment) is a goal state (or solution) or not, before reaching the leaves of the tree. ie. just by looking at a partial assignment.

Large areas of the search-space can thus be eliminated by identifying variable-value combinations that violate constraints. The factored representation, can also tell us *why* a certain assignment is not a solution by looking at the variables that violate the constraints.

## Constraint propagation

**Constraint propagation** is the use of constraints to reduce the number of legal values for a variable and its neighboring variables.

Consider the constraints $A \gt 2$ and $B = A^2$, where the domain of variable $A$ is:

$$
A = \{ 2, 3, 4 \}
$$

The domain of variable $B$ is:

$$
B = \{ 4, 9, 16 \}
$$

We reduce its domain of $A$ to $\{ 3, 4 \}$ due to its unary constraint. But this domain reduction has made $B\text{'s}$ domain inconsistent.

So, now we have to update $B\text{'s}$ domain to maintain consistency. This is why it is called propagation. Propagation reduces the domain size of the variables, thus making search operation faster.

In case a domain becomes empty, then it means that the combination of assignments that lead to this state does not yield a solution.

Sometimes, simply using constraint propagation can provide a solution, otherwise search has to be intertwined.

# Types of Consistency

Different algorithms try to maintain a certain level of consistency as it searches for a solution. The various types of consistencies are:

- Node consistency
- Arc consistency
- Path consistency
- K-consistency

## Node consistency

A node is *node-consistent*, if all values in its domain satisfy the variable's unary constraints. All nodes of any CSP can be made node-consistent.

Consider the constraint $X \ne 5$, where the domain of $X$ is:

$$
X = \{ 0, 1, 2, 3, 4, 5 \}
$$

To make $X$ node-consistent, we reduce its domain to $\{ 0, 1, 2, 3, 4 \}$.

## Arc consistency

A variable is *arc-consistent* if every value in its domain satisfies the variable's binary constraints. A network is arc-consistent if *every* variable is arc-consistent with every other variable.

Consider the constraint $Y = X^2$, where the domains of both $X$ and $Y$ are:

$$
X = \{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 \}

\\

Y = \{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 \}
$$

To make $X$ arc-consistent with respect to $Y$, we reduce its domain to $\{ 0, 1, 2, 3 \}$. To make $Y$ arc-consistent with respect to variable $X$, we reduce its domain to $\{ 0, 1, 4, 9 \}$.

The *AC-3 algorithm*, described later, can be used to make a CSP network arc-consistent.

Note that it is possible to convert all constraints starting from ternary constraints into binary constraints. This can be done using the *dual graph transformation*. So, most algorithms are designed to work only for binary constraints.

## Path consistency

Path consistency is stronger than arc consistency, because it has three variables within its scope. The variables $X$ and $Y$ are path consistent with respect to $Z$, if for every legal assignment to $X$ and $Y$, there is a legal assignment to $Z$.

## K-consistency

Stronger forms of consistency are defined with the notion of k-consistency. A CSP is k-consistent if, for any set of $k - 1$ variables with any assignment, a consistent value can always be assigned to any $k^\text{th}$ variable.

# The AC-3 Algorithm : Making it Arc Consistent

AC-3 maintains a set of all arcs in the csp network. An arc is represented by $(X, Y)$, where $X$ and $Y$ are the two nodes at the ends.

An arbitrary arc $(X, Y)$ is *popped out* from this set, and variable $X$ is made arc-consistent with respect to variable $Y$.

If this leaves the domain of $X$ unchanged, then the algorithm moves onto another arc in the set.

If domain reduction does occur, then we add all arcs $(K, X)$, where $K$ is a neighbor of $X$. This is done to check whether any domain reductions are required for $K$, now that domain reduction has occurred in $X$.

If any domain becomes empty, then the CSP is unsolvable and we return failure.

```python
def AC_3 ():
  while queue is not empty:
    (X, Y) <- pop_arc(queue)

    if revise (X, Y):
      if len(domain of X) == 0
        return false

      for K in neighbors of X :
        add (K, X) to queue

  return true

# returns true if domain was revised
def revise (X, Y):
  revised <- false

  for value in domain_of_X:
    if no value in Y consistent when X = value
      delete value from domain_of_X
      revised <- true

  return revised
```

# Backtracking search

**Backtracking search** is a depth first search algorithm that chooses values for one unassigned variable at a time and backtracks when a variable has no legal values left.

## Variable ordering : Choosing next variable

Consider a CSP with three variables, $A$, $B$ and $C$. Let their domains be as follows:

$$
A = \{ 1, 2, 3 \} \\
B = \{ 1, 2, 3 \} \\
C = \{ 1 \} \\
$$

The only constraint is:

$$
A \ne B \ne C
$$

<figure style="width: 700px">
	<img src="/media/artificial intelligence/variable-ordering.png" alt="Variable Ordering for CSP Search Tree">
	<figcaption>Variable Ordering for CSP Search Tree</figcaption>
</figure>

Using a search tree, you can try to various assignments to reach a solution. First, we assign a value to $A$. But we can this does not lead to a solution. We backtrack and choose $C$ and assign a value for it. This does lead to a solution at *Node 3*.

Clearly, it was unfruitful to go down the first path. If we had chosen $C$ first we could have reached the solution faster.

**Variable ordering** is an attempt to reach a solution faster by the use of heuristics instead of randomly choosing the next variable.

Choosing a variable based on the fewest remaining legal values is called the **minimum-remaining values heuristic**. By choosing the most constrained variable we will reach a failure point faster, thus pruning the search tree.

If a variable has no legal values left, this will be selected and immediately we find out that going down this path is useless and so can we backtrack.

The **degree heuristic** on the other hand, chooses the variable that is involved in the largest number of constraints with other unassigned variables. It is less powerful than the MRV heuristic but is useful as a tie breaker because it considers the future choices.

## Value ordering : Choosing next value

Once the variable is selected, we have to choose a value for it from its domain. Just as for variables, choosing a bad value will increase search time.

The **least constraining value heuristic** chooses a value that rules out the fewest choices for unassigned variables. This is done to improve the flexibility for subsequent assignments.

Note that, value ordering is irrelevant if you want to find all the solutions.

# Choice of inference

Every time we make an assignment, we have an opportunity to infer domain reductions on neighboring variables.

The simplest form of inference is **forward checking**. Whenever a variable is assigned, it establishes arc consistency between it and its *unassigned* neighbors. This domain reduction for the unassigned variables increases search speed.

The disadvantage is that forward checking only detects inconsistencies in the immediate neighbors. To detect all of them, we use the **Maintaining arc consistency (MAC) algorithm**.

In MAC, we first assign a value to a variable $X$. Then we call the AC-3 algorithm, but instead of an initial queue of *all* arcs in the network, MAC starts off with arcs $(Y, X)$ where $Y$ is an *unassigned neighbor* of the $X$.

From here, AC-3 algorithm does the constraint propagation in the usual way. In case of failure, the MAC algorithm backtracks and tries again.

# Local Search

Backtracking is not the only way to solve a CSP. Local search, turns out to be very effective.

**Local search** initializes all variables with a value from their domain disregarding whether or not they are consistent. This state inevitably violates a whole bunch of constraints. The goal of local search is eliminate these violations.

Local search then changes the values of each of the variables, one variable at a time chosen randomly.

*How do we decide which value to assign for a variable?* We use one that results in the minimum number of conflicts overall. This is called the **min-conflicts heuristic**.

This is repeated until we find a solution or for a fixed number of steps.

```python
def min_conflicts ():
  current <- initial complete assignment of CSP

  for 0 to max_steps
    if current is a solution
      return current

    var <- randomly chosen variable from CSP
    value <- a value for var that minimizes conflicts
    set var = value

  return failure
```

Local search is very useful in scheduling problems. Bad weather can render a flight schedule unusable. The best revision/solution is one with the least major changes. This can be accomplished with a local search algorithm starting from the current schedule.

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
- [6.034 Recitation 4: Constraint Satisfaction Problems](https://www.youtube.com/watch?v=dXTNQmqFo1k)