---
title: "Propositional Logic"
date: "2019-12-7"
template: "post"
draft: false
slug: "/posts/prop-logic/"
category: "Logic"
tags:
  - ""
description: ""
---

**Propositional logic** studies the ways statements interact with each other. It does not care about the *meaning* of the statements under consideration. In logic, the statement "If the moon is made of cheese then basketballs are round", is credible.

A **proposition** is simply a statement with a truth value. A proposition is set of proposition symbols connected by logical operators. Each symbol holds a truth value.

Proposition symbols are represented by capital letters, like $P$ and $Q$.

An **atomic sentence** consist of just a single proposition symbol and no logical operators. **Complex sentences** are constructed from simpler sentences using parenthesis and logical operators.

Operator precedence is as follows : $\neg, \space \wedge, \space \vee, \implies, \iff$.

<figure style="width: 700px">
	<img src="/media/logic/truth-table.png" alt="Truth Table">
	<figcaption>Truth Table</figcaption>
</figure>

# Knowledge base

The **knowledge base** is a set of sentences that assert facts about the world. Some of these sentences can be axioms, meaning they do not need to be derived from other sentences.

A knowledge base can capture both mutable and immutable aspects of the environment. Immutable aspects can include the rules of the environment, whereas mutable aspects can describe a particular instance of its variables.

The fact that there is mountain at some coordinate is a immutable aspect, whereas an opponent hiding somewhere in the mountain is an mutable fact.

## Model

A **model** is a description of an environment where we fix truth values to the proposition symbols in all relevant sentences.

Consider the knowledge base,

$$
P \iff Q \vee R \\\\
P \wedge Q
$$

One possible model for this KB is,

$$
\{ P : \text{false}, Q : \text{false}, R : \text{true} \}
$$

If a sentence $\alpha$ is true in a model $m$, we say that $m$ **satisfies** $\alpha$. The set of all models that satisfy $\alpha$ is denoted by $M(\alpha)$.

**Validity :** A sentence is valid if it is true in *all* models. For example, $A \vee \neg A$ is true in all models. Such sentences are called **tautologies**.

**Satisfiability :** A sentence is satisfiable if it is true in *some* model.

Validity and satisfiability are related. $\alpha$ is valid if and only if $\neg \alpha$ is unsatisfiable. On the other hand, $\alpha$ is satisfiable if and only if $\neg \alpha$ is not valid.

# Logical equivalency

Two sentences $\alpha$ and $\beta$ are logically equivalent if they are true in the same set of models, ie. they are logically equivalent if $M(\alpha) = M(\beta)$.

In the words of entailment, two sentences are equivalent if and only if $\alpha \models \beta$ and $\beta \models \alpha$.

Equivalence is denoted by $\alpha \equiv \beta$.

Some logical equivalencies are given below:

**Commutative law**

$$
\alpha \wedge \beta \equiv \beta \wedge \alpha \\
\alpha \vee \beta \equiv \beta \vee \alpha
$$

**Associative law**

$$
(\alpha \wedge \beta) \wedge \gamma \equiv \alpha \wedge (\beta \wedge \gamma) \\
(\alpha \vee \beta) \vee \gamma \equiv \alpha \vee (\beta \vee \gamma)
$$

**Distributive law**

$$
\alpha \wedge (\beta \vee \gamma) \equiv (\alpha \wedge \beta) \vee (\alpha \wedge \gamma) \\
\alpha \vee (\beta \wedge \gamma) \equiv (\alpha \vee \beta) \wedge (\alpha \vee \gamma)
$$

**DeMorgan's law**

$$
\neg (\alpha \wedge \beta) \equiv \neg \alpha \vee \neg \beta \\
\neg (\alpha \vee \beta) \equiv \neg \alpha \wedge \neg \beta
$$

**Contraposition**

$$
\alpha \implies \beta \equiv \neg \beta \implies \neg \alpha
$$

**Double negation elimination**

$$
\neg (\neg \alpha) \equiv \alpha
$$

**Implication elimination**

$$
\alpha \implies \beta \equiv \neg \alpha \wedge \beta
$$

**Biconditional elimination**

$$
\alpha \iff \beta \equiv (\alpha \implies \beta) \wedge (\beta \implies \alpha)
$$

# Entailment

Consider two sentences, $\alpha$ and $\beta$. $\alpha$ is true in $M(\alpha)$ and $\beta$ is true in $M(\beta)$. If $M(\alpha)$ is a subset of $M(\beta)$, then whenever $\alpha$ is true, we know $\beta$ is also true.

The sentence $\alpha$ is said to **entail** the sentence $\beta$. And $\beta$ is said to **logically follow** from $\alpha$. Entailment is denoted as $\alpha \models \beta$.

Note that $\alpha$ is the more stronger assertion because it rules of more possible worlds.

If you replace $\alpha$ with a conjugation of all the propositions in your KB, you can find the logical consequences $\beta$ of our known knowledge in the KB.

$$
KB \models \beta
$$

<figure style="width: 350px">
	<img src="/media/logic/entailment.png" alt="Entailment">
	<figcaption>Entailment</figcaption>
</figure>

## Inference

**Inference** is the act of checking for entailment between $\alpha$ and $\beta$.

An inference algorithm is **sound** if it only finds entailed sentences. An unsound inference algorithm just makes things up as it goes along.

The algorithm is **complete** if it can derive *any* sentence that is entailed.

Some methods of inference include:

- TT-Entails algorithm
- Proof By Resolution
- DPLL Algorithm

# Model Checking

**Model checking** is a method to check for entailment. In model checking, we enumerate all possible models and check whether $\beta$ is true in all models where $\alpha$ is true. If so, then $\alpha \models \beta$.

This model checking approach to inference is called by the **TT-Entails algorithm**, a truth table enumeration algorithm. It is both sound and complete.

First, it incrementally creates new models, assigning truth values one variable at a time. Once assignment is completed, it checks if a model satisfies both the knowledge base and the $\alpha$.

<figure style="width: 750px">
	<img src="/media/logic/tt-enumeration-algorithm.png" alt="TT-Entails algorithm">
	<figcaption>TT-Entails algorithm</figcaption>
</figure>

A truth table enumeration will produce an exponential number of models. In this a case, theorem proving can be more efficient because a proof can disregard irrelevant propositions.

# Theorem Proving

Theorem proving means applying rules of inference to the sentences in our knowledge base to construct a proof that the desired sentence is true.

Some rules that are used to derive a proof are:

**Modus Ponens**

$$
\frac{\alpha \implies \beta, \alpha}{\beta}
$$

**And Elimination**

$$
\frac{\alpha \wedge \beta}{\alpha}
$$

$$
\frac{\alpha \wedge \beta}{\beta}
$$

Logical equivalences can be also be used as inference rules.

## Proof by Contradiction

The basic idea behind this is to assume that the statement $\beta$ we want to prove is false, and then show that this assumption leads to nonsense.

We are then led to conclude that we were wrong to assume that $\beta$ was false, so $\beta$ must be true.

Lets say, $\alpha$ does entail $\beta$. In this case the sentence $\alpha \wedge \beta$ will be true. In order to prove this we will assume $\alpha \wedge \neg \beta$ is true, and try to find a contradiction.

$\alpha \wedge \neg \beta$ is said to be unsatisfiable, if we find a contradiction.

## Implementing theorem proving

How can a computer perform proof by contradiction? The answer is to define it as a search problem. Search algorithms like iterative deepening can be used to find the sequence of steps that constitute a proof.

It can be defined as follows:

- Initial state - initial knowledge base
- Actions - a set of logical equivalencies and inference rules that match the LHS of the current sentence
- Result - the result of the action on a sentence
- Goal - is the sentence we want to derive

## Proof by Resolution

One problem we face here is that the inference algorithm is not complete. This is because if a particular inference rule is not available, then the goal is unreachable.

But a single inference rule, named *resolution* when coupled with any complete search algorithm, it yields a complete inference algorithm.

A proof that uses resolution is called a **proof by resolution**. Such a proof works on *clauses*. A **clause** is a disjunction of literals like $x \vee y$.

The **resolution rule** takes two clauses and produces a new clause containing all literals of the two clauses except for *one* pair of complementary literals. The new clause is called a **resolvent**.

A resolution can be represented as:

$$
\frac { l_1 \vee l_2 \vee l_3, \qquad l_1' \vee m_2 \vee m_3 } { l_2 \vee l_3 \vee m_2 \vee m_3 }
$$

where $l_i$ and $l_i'$ are a pair of complementary literals.

## Conjunctive Normal Form

The resolution rule only applies to clauses, so all sentences in our KB needs to be expressed as clauses or a conjugation of clauses. This is known as the **conjunctive normal form (CNF)**.

Steps to *convert to CNF* are:

1. Eliminate $\iff$ using biconditional elimination
1. Eliminate $\implies$ using implication elimination
1. Move $\neg$ inwards, using double negation and DeMorgan's law
1. Ensure $\wedge$ operators are not nested inside $\vee$ operators using the distributive law

Check page $258$ AIMA for an example.

## PL-Resolution Algorithm

The **PL-Resolution algorithm** is used to show that $KB \models \alpha$, by assuming that $KB \wedge \neg \alpha$ and then try to find a contradiction.

The algorithm, first converts $KB \wedge \neg \alpha$ to CNF form. This gives us a set of clauses. Each pair of clauses with a pair of complementary literals are resolved to produce a resolvent. The resolvent is added to the set if it is not already present.

The process continues until one of two things happen:

- A resolvent is an empty clause - in which case $KB$ entails $\alpha$. An empty clause arises only from resolving two complementary unit clauses like $P$ and $\neg P$, which is a contradiction.
- No new clauses can be added - in which case KB does not entail $\alpha$; because a contradiction is not found.

<figure style="width: 600px">
	<img src="/media/logic/pl-resolution-algorithm.png" alt="PL Resolution Algorithm">
	<figcaption>PL Resolution Algorithm</figcaption>
</figure>

# DPLL Algorithm

The **DPLL algorithm** is a backtracking based search algorithm for deciding the satisfiability of a proposition; ie. for testing entailment.

It performs a depth first enumeration of all possible models, and is an improvement over the TT_Entails algorithm. DPLL works with CNF form.

## Early termination

The algorithm detects whether a truth value can be assigned to a sentence even with a partial model. Early termination avoids exploration of entire sub-trees.

- The clause $A \vee B \vee C$, is true if model is $\lbrace  A : true \rbrace$
- The sentence $(A \vee B \vee C) \wedge (B \vee X)$, is false if model is $\lbrace  B : false, X : false \rbrace$.

## Pure symbol heuristic

A **pure symbol** is a literal that always appears with the same sign in all clauses of a sentence.

In the sentence $(A \vee \neg B) \wedge (\neg B \vee \neg C) \wedge (C \vee D)$, the symbols $A$, $D$ are pure as they only appear as positive literals; and $B$ is pure as it only appears as a negative literal.

DPLL tries to assign truth values to $A$ and $B$ such that their respective clauses become true even with a partial model. The other symbols in the clauses can be ignored.

For the above given sentence, with a partial model $\lbrace A : true, B : false \rbrace$, only $(C \vee D)$ clause is left.

## Unit propagation

A **unit clause** is a clause which has exactly one literal which is still unassigned, and the other literals are all assigned false. We assign true to this lone literal to make the clause true.

Consider the KB,

$$
\neg C \vee B	\\\\
C \vee A
$$

Under the partial model $\lbrace B : true \rbrace$, $\neg B \vee C$ simplifies to unit clause $\neg C$. Now $C$ is assigned the value *false* to make its clause *true*.

Note that $C \vee A$ now becomes a unit clause $A$. Assigning one unit clause a value could create other unit clauses waiting for truth value assignments. This cascade of assignments is called **unit propagation**.

<figure style="width: 700px">
	<img src="/media/logic/dpll.png" alt="DPLL Algorithm">
	<figcaption>DPLL Algorithm</figcaption>
</figure>

# WalkSAT

**WalkSAT algorithm** is a local search approach for finding a model that satisfies all the clauses given to it.

The algorithm picks a random unsatisfied clause and picks a symbol in the clause to flip. The symbol is chosen using one of the following ways:

- **min-conflicts** - choose a symbol that when flipped minimizes number of unsatisfied clauses.
- **random-walk** - picks a symbol randomly. This helps it to get out of local minima.

We do this for a specified number of steps, or until it finds a model that satisfies every clause.

If a model is returned, then WalkSAT has indeed proved satisfiability of the set of clauses (sentence). Failure, on the other hand, can represent either of the following:

- The sentence is unsatisfiable
- The algorithm needs more time, ie. larger `max_flips` to find a model that satisfies the propositions

<figure style="width: 700px">
	<img src="/media/logic/walk-sat.png" alt="WalkSAT Algorithm">
	<figcaption>WalkSAT Algorithm</figcaption>
</figure>

Since WalkSAT cannot always detect unsatisfiability (required to detect entailment), it is most useful when we expect a solution to exists.

For example, an agent cannot reliably use WalkSAT to prove that a square is safe in the wumpus world. What it can do, is say "I thought for an hour and could not come up with a possible world in which the square isn't safe".

# Forward Chaining

The **Forward chaining algorithm** determines if a proposition symbol *q* is entailed by a knowledge base.

It begins from a known set of sentences, some of which are **facts** (single positive literals) and the rest are implications ($x \implies y$). If all the premises of an implication are known to be true, then its conclusion is added to the knowledge base as a fact.

Forward chaining is an application of modus ponens. This process continues until the query *q* is added to the KB or until no inferences can be made.

Forward chaining is an example of **data-driven reasoning**.

<figure style="width: 700px">
	<img src="/media/logic/forward-chaining.png" alt="Forward Chaining">
	<figcaption>Forward Chaining</figcaption>
</figure>

The **backward chaining algorithm** works backward from a query *q*. It finds an implication with *q* as a conclusion, then attempts to prove that all its premises are true. It is a form of **goal-directed reasoning**.

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
- [Wikipedia: Conjunctive normal form](https://en.wikipedia.org/wiki/Conjunctive_normal_form)
- [Figures from AIMA](http://aima.cs.berkeley.edu/figures.html)
