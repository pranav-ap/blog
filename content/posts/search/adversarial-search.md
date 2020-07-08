---
title: "Adversarial Search in Perfect Information Games"
date: "2019-12-7"
template: "post"
draft: false
slug: "/posts/adversarial-search/"
category: "Search"
tags:
  - ""
description: ""
---

In competitive environments, agents have conflicting goals and this gives rise to **adversarial search problems** or **games**. A game is defined as a search problem with the following elements:

- Initial game state
- Transition model
- Terminal test
- Utility function

The **transition model** maps a state and an action to the next state. The **terminal test** tests whether the game has come to an end. Such a state is called a **terminal state**.

A **utility function** returns a numeric value representing the favorability of a given state for a player or team.

The **initial game state** is the root node of the game tree. The first player makes his move here. This node gives rise to branches representing the moves available to him. Continuing branching will eventually reach all possible states of the game.

# Constructing a Contingent strategy

A **contingent strategy** is takes the opponents moves into account and provides an optimal response to them. If two $X$'s are placed in a row, then the optimal strategy is to block it with an $O$.

The strategy is represented as **game tree**. A node in a game tree holds three pieces of data:

- State
- Current player
- Utility vector

The **state** is some configuration of the game. For example, the position of chess pieces on the board. The **utility vector** is a list of values, each representing the utility of the state from each players viewpoint.

A node has one incoming link and multiple outgoing links. The **incoming link** is the action performed on previous state to reach current state. The **outgoing links** represent the actions available to current player.

# Finding the Optimal Move : Minimax Algorithm

<figure style="width: 700px">
	<img src="/media/search/game-tree.png" alt="Game Tree">
	<figcaption>Game Tree</figcaption>
</figure>

The optimal action for a player $P$ at a state $S$ is given by the **minimax algorithm**.

It is a simple recursive algorithm that proceeds all the way down to the leaves, assigns utility to these terminal states which are then pulled up through the tree as the recursion unwinds.

The utility vector for a non-terminal state $X$ is the utility vector of a child node with the highest value for the $X$'s current player.

Let's find the best move for Player $A$ at the root. Minimax algorithm first assigns utility vector for the red node's children, then backs up to the red node itself. Here, $B$ plays, so it chooses node with $\langle 3, 7, 2 \rangle$.

Recursion goes through blue node's children, assigns utility vectors and backtracks to the blue node. The $\langle 5, 6, 3 \rangle$ vector is pulled up to the blue node. Similarly, for green node is assigned $\langle 2, 3, 1 \rangle$.

All of the root node's children have a utility vector now, so it chooses the best one from Player $A$'s viewpoint. $5$ is a better utility than $3$, so root pulls up $\langle 5, 6, 3 \rangle$.

# Disregard the Unnecessary : Alpha-beta Pruning

The problem with minimax search is that it is inefficient when the number of game states it has to examine is exponential. The **alpha-beta pruning algorithm** helps you prune away branches that cannot possibly influence the optimal decision for the current player.

<figure style="width: 700px">
	<img src="/media/search/alpha-beta.png" alt="Alpha-beta Pruning">
	<figcaption>Alpha-beta Pruning</figcaption>
</figure>

For simplicity, let's consider a *two-person* game tree. The utility vector can be replaced by a single value (representing Player $A$'s utility) because a winning state for Player $A$ is a losing state for Player $B$.

Let's find the best move for Player $A$ at the root. Minimax algorithm first assigns utility for the red node's children, then backs up to the red node itself. Here, B plays, so it wants the smallest possible utility value. It first pulls $3$. Then compares it with $12$ and keeps $3$. Compares $3$ with $8$ and still keeps $3$.

Recursion goes through blue node's children, assigns utility and backtracks to the blue node. It first pulls $2$. We have an opportunity for pruning, and this is why. Consider two things:

- Since it is Player $B$'s turn to play, it will either just keep $2$ or choose a smaller utility value.
- Player $A$ at the root wants the highest utility.

Currently Player $A$ has two options: red's $3$ and blue's $\le 2$. You can now see that whatever utility the other two children of blue have, they will not affect root's choice. It *will* choose $3$, among these two options. But we still have to consider the green node. Maybe there is $\ge 3$ utility there.

Recursion goes through green node's children, assigns utility and backtracks to the blue node. It first pulls $14$. Then compares it with $5$, sees that $5$ is better and keeps $5$. Compares $5$ with $2$ and keeps $2$.

*Will the root pull up green node's utility?* No, because it already found a larger utility in red node. In this example, we only pruned away two leaves, but it is easy to see how whole branches can be pruned away, saving us much compute and time.

# Real time decisions

Minimax generates the entire game tree. Alpha-beta pruning eliminates large parts of it. Yet, it still has to reach the leaves to make a good decision, which makes in impractical for real-time decisions.

Time can be saved by cutting off search earlier. So instead of trying to use a utility function on a leaf, we use an **evaluation heuristic** on a non-terminal state.

The evaluation function quickly returns an estimate of the utility at a given position. Needless to say, an inaccurate evaluation function will guide an agent into terrible situations.

Lets say a state $P$ has a utility of $45$ and $Q$ has a utility of $20$. An evaluator does not need to return the exact utility, but does have to say that $P$ is more favorable than $Q$; ie. value of $P$ must be greater than $Q$. For example, in Chess, checkmating the opponent must be given a larger value than losing a Queen.

*Where do we cut-off the search?* A simple method is to use a fixed depth limit at which we perform an evaluation of state.

But what if at a single level deeper, the situation is completely different and you are in a losing position. The evaluator will not have access to this information and thus return an inaccurate utility. Obviously, a more sophisticated cut-off test is needed.

# Handling random elements : Stochastic Games

The methods discussed above do not take random elements into account. What if the game random elements like dice. These games are called **stochastic games**.

To handle randomness, we include chance nodes in the game tree. A **chance node** branches to multiple nodes, each representing the state the game might end up in. The branches also have a probability of occurrence associated with them.

The uncertainty makes in impossible for us to use *actual* utility as we did previously. We need to use the **expected utility**, which takes into account both the favorability of a state and its likelihood of occurrence.

Minimax algorithm can be used here as usual, with the modified formula for finding utility of a chance node. The utility of a chance node is the sum of utilities of the its successor nodes each weighted by their probabilities.

Look at the blue chance node of the two-player stochastic game tree. It has a value of $3.2$, which is found using $(0.9 * 3) + (0.1 * 5)$.

<figure style="width: 700px">
	<img src="/media/search/stochastic-game.png" alt="Stochastic Game">
	<figcaption>Stochastic Game</figcaption>
</figure>

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
- [Figures from AIMA](http://aima.cs.berkeley.edu/figures.html)
