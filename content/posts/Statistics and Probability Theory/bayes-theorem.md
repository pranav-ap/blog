---
title: "Bayes Theorem"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/bayes-theorem/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Bayes theorem** lets us update our beliefs based on new evidence.

We know that the probability of $B$ given $A$ is,

$$
P(B \mid A) = \frac {P(A \cap B)} {P(A)}
$$

The probability of $A$ given $B$ is,

$$
P(A \mid B) = \frac {P(B \cap A)} {P(B)}
$$

Due to symmetry of joint probabilities, $P(A \cap B) = P(B \cap A)$, we can expand and get,

$$
\begin{aligned}
P(B \mid A) \space P(A) &= P(A \mid B) \space P(B) \\\\
P(A \mid B) &= \frac { P(B \mid A) \space P(A) }{P(B)}
\end{aligned}
$$

where $A$ and $B$ are events, and $P(B) \ne 0$

Note that $P(B)$ can be represented in terms of the quantities appearing in the numerator, using the total probability theorem.

So Bayes theorem is defined as,

$$
P (A \mid B) = \frac { P(A) \space P(B \mid A) } { \sum_i P(A_i) \space P(B \mid A_i) }
$$

- $P(A)$ is called the **prior probability** of $A$. This is the probability of $A$ before we consider the evidence.
- $P (A \mid B)$ is called the **posterior**. This is the updated probability of $A$.
- $P (B \mid A)$ is called the **likelihood**. This is the probability of observing the new evidence, given our initial hypothesis.
- $P(B)$ is the probability of observing the evidence $B$.

Let $A$ be an event where you have malaria, and $B$ an event where you have high fever as a symptom.

$P(A)$ is the probability of any person in the population having malaria. $P(B)$ is the probability of any person in the population getting high fever.

$P (A \mid B)$ is the probability of you having malaria given that you have a fever. $P (B \mid A)$ is the probability that you will have high fever, in case you have malaria.

# References

- [Conditional probability explained visually (Bayes' Theorem)](https://www.youtube.com/watch?v=Zxm4Xxvzohk)
- [Bayes theorem](https://www.youtube.com/watch?v=OqmJhPQYRc8)
