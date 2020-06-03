---
title: "Trigonometry"
date: "2020-06-3"
template: "post"
draft: false
slug: "/posts/trigonometry"
category: "Geometry"
tags:
- ""
description: ""
---

**Trigonometry** is the geometric study of triangles. It finds relationships between the length of the sides and the angles between them.

The right-angled triangle is most commonly used here. The hypotenuse the longest side and is opposite to the right angle. The opposite lies opposite to the angle $\theta$ and the adjacent side lies adjacent to $\theta$.

<figure style="width: 900px">
	<img src="/media/geometry/adjacent-opposite-hypotenuse.svg" alt="The sides of a right-angled triangle">
	<figcaption>The sides of a right-angled triangle</figcaption>
</figure>

## Trigonometric ratios

Trigonometric ratios define a relationship between an angle and two other sides. The six trig ratios are as follows.

$$
\begin{aligned}
   \text{sin} \space \theta &= \frac {\text{opposite}} {\text{hypotenuse}} \\\\
   \text{cos} \space \theta &= \frac {\text{adjacent}} {\text{hypotenuse}} \\\\
   \text{tan} \space \theta &= \frac {\text{opposite}} {\text{adjacent}} \\\\
\end{aligned}
$$

$$
\begin{aligned}
   \text{csc} \space \theta &= \frac {1} {\text{sin} \space \theta} \\\\
   \text{sec} \space \theta &= \frac {1} {\text{cos} \space \theta} \\\\
   \text{cot} \space \theta &= \frac {1} {\text{tan} \space \theta} \\\\
\end{aligned}
$$

## Unit circle

The unit circle is circle with radius of $1$ unit.

<figure style="width: 1000px">
	<img src="/media/geometry/unit circle.png" alt="Unit circle">
	<figcaption>Unit circle</figcaption>
</figure>

$$
\begin{aligned}
   \text{sin} \space \theta &= \frac {\text{height along y-axis}} {\text{hypotenuse}} \\\\
   \text{cos} \space \theta &= \frac {\text{length along x-axis}} {\text{hypotenuse}}
\end{aligned}
$$

The hypotenuse is $1$ as it is a unit circle. By simplifying, we get

$$
\begin{aligned}
   \text{sin} \space \theta &= \text{height along y-axis} \\
   \text{cos} \space \theta &= \text{length along x-axis}
\end{aligned}
$$

The coordinates at the circumference indicate the sine and cosine for some angle $\theta$.

<figure style="width: 550px">
	<img src="/media/geometry/unit circle angles.png" alt="Unit circle angles">
	<figcaption>Unit circle angles</figcaption>
</figure>

[How to remember the unit circle?](https://www.youtube.com/watch?v=c819bGfH8FA)

## Periodicity

A function $f(x)$ is *periodic* if there is a positive number $p$ such that,

$$
f(x + p) = f(x)
$$

for every value of $x$. The smallest possible value for $p$ is called the **period** of $f$.

Both tangent and cotangent have a period of $\pi$. The others have a period of $2 \pi$.

<figure style="width: 650px">
	<img src="/media/geometry/trig period.png" alt="Periodicity">
	<figcaption>Periodicity</figcaption>
</figure>

## Even and Odd Functions

Functions that are symmetric along the y-axis are called **even** functions.

$$
f(-x) = f(x)
$$

<figure style="width: 650px">
   <img src="/media/geometry/even function.svg" alt="Even Function">
   <figcaption>Even Function</figcaption>
</figure>

Functions that are symmetric along the x-axis are called **odd** functions.

$$
f(-x) = -f(x)
$$

<figure style="width: 650px">
   <img src="/media/geometry/odd function.svg" alt="Odd Function">
   <figcaption>Odd Function</figcaption>
</figure>

Cosine and secant are *even* functions, while the others are *odd*.

$$
\begin{aligned}
   \text{sin} \space ( -\theta ) &= - \text{sin} \space ( \theta ) \\
   \text{cos} \space ( -\theta ) &= \text{cos} \space ( \theta )
\end{aligned}
$$

They are called **negative angle identities**.

Now, we can calculate for tangent,

$$
\begin{aligned}
   \text{tan} \space ( -\theta ) &= \frac{\text{sin} \space ( -\theta )} {\text{cos} \space ( -\theta )}
                                 = \frac{- \text{sin} \space ( \theta )} {\text{cos} \space ( \theta )} \\\\
                                 &= - \text{tan} \space ( \theta )
\end{aligned}
$$

## Trigonometric Identities

Trigonometric identities are equations that are true for all right-angled triangles. Some important kinds of identities include:

1. Trigonometric ratios
1. Negative angle identities
1. Pythagorean identities
1. Sum and Difference Identities
1. Double Angle Identities
1. Half Angle Identities
1. Law of sines
1. Law of cosines

### Pythagorean identities

Start with the pythagorean theorem,

$$
\tag{1} \text{hyp}^2 = \text{opp}^2 + \text{adj}^2
$$

Divide $(1)$ by $\text{hyp}^2$,

$$
1 = \Big ( \frac{opp}{hyp} \Big ) ^2 + \Big ( \frac{adj}{hyp} \Big ) ^2
$$

$$
\tag{2} 1 = \text{sin}^2 (\theta) + \text{cos}^2 (\theta)
$$

Divide $(2)$ by $\text{sin}^2 (\theta)$,

$$
\tag{3} \text{csc}^2 (\theta) = 1 + \text{cot}^2 (\theta)
$$

Divide $(2)$ by $\text{cos}^2 (\theta)$,

$$
\tag{4} \text{sec}^2 (\theta) = \text{tan}^2 (\theta) + 1
$$

### Sum and Difference Identities

$$
\tag{5} \text{sin} \space ( A + B ) =
      \text{sin} \space A \space \text{cos} \space B +
      \text{cos} \space A \space \text{sin} \space B
$$

$$
\tag{6} \text{cos} \space ( A + B ) =
      \text{cos} \space A \space \text{cos} \space B -
      \text{sin} \space A \space \text{sin} \space B
$$

Let's calculate $\text{tan} \space ( A + B )$,

$$
\begin{aligned}
   \text{tan} \space ( A + B ) &= \frac {\text{sin} \space ( A + B )} {\text{cos} \space ( A + B )}
   \\\\
   \text{tan} \space ( A + B ) &= \frac
      {\text{sin} \space A \space \text{cos} \space B + \text{cos} \space A \space \text{sin} \space B}
      {\text{cos} \space A \space \text{cos} \space B - \text{sin} \space A \space \text{sin} \space B}
\end{aligned}
$$

Divide numerator and denominator by $\text{cos} \space A \space \text{cos} \space B$,

$$
\tag{7} \text{tan} \space ( A + B ) = \frac
      {\text{tan} \space A + \text{tan} \space B}
      {1 - \text{tan} \space A \space \text{tan} \space B}
$$

The difference identities can be derived by replacing $B$ with $-B$, and using the negative angle identities.

$$
\tag{8} \text{sin} \space ( A - B ) =
      \text{sin} \space A \space \text{cos} \space B -
      \text{cos} \space A \space \text{sin} \space B
$$

$$
\tag{9} \text{cos} \space ( A - B ) =
      \text{cos} \space A \space \text{cos} \space B +
      \text{sin} \space A \space \text{sin} \space B
$$

$$
\tag{10} \text{tan} \space ( A - B ) = \frac
      {\text{tan} \space A - \text{tan} \space B}
      {1 + \text{tan} \space A \space \text{tan} \space B}
$$

### Double Angle Identities

The double angle identities can be derived from sum identities. Just replace $B$ with $A$.

$$
\begin{aligned}
   \text{sin} \space ( A + A ) &=
         \text{sin} \space A \space \text{cos} \space A +
         \text{cos} \space A \space \text{sin} \space A \\

   \tag{11} \text{sin} \space 2A &= 2 \space \text{sin} \space A \space \text{cos} \space A
\end{aligned}
$$

$$
\begin{aligned}
   \text{cos} \space ( A + A ) &=
         \text{cos} \space A \space \text{cos} \space A -
         \text{sin} \space A \space \text{sin} \space A \\

   \tag{12} \text{cos} \space 2A &= \text{cos}^2 \space A - \text{sin}^2 \space A
\end{aligned}
$$

$$
\begin{aligned}
   \text{tan} \space ( A + A ) &= \frac
      {\text{tan} \space A + \text{tan} \space A}
      {1 - \text{tan} \space A \space \text{tan} \space A} \\

   \tag{13} \text{tan} \space 2A &= \frac {2 \space \text{tan} \space A} {1 - \text{tan}^2 \space A}
\end{aligned}
$$

### Half Angle Identities

Consider $(2)$ and $(12)$,

$$
\text{sin}^2 (\theta) + \text{cos}^2 (\theta) = 1
$$

$$
\text{cos} \space 2A = \text{cos}^2 \space A - \text{sin}^2 \space A
$$

Add them to get,

$$
\begin{aligned}
   2 \space \text{cos}^2 \space A &= 1 + \text{cos} ( 2A ) \\
   \tag{14} \text{cos}^2 \space A &= \frac {1 + \text{cos} ( 2A )} {2}
\end{aligned}
$$

Subtract them to get,

$$
\begin{aligned}
   2 \space \text{sin}^2 \space A &= 1 - \text{cos} ( 2A ) \\
   \tag{15} \text{sin}^2 \space A &= \frac {1 - \text{cos} ( 2A )} {2}
\end{aligned}
$$

### Law of sines

### Law of cosines
