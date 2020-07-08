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

The right-angled triangle is most commonly used here. The hypotenuse the longest side and is opposite to the right angle. The opposite lies opposite to the angle $\theta$ and the remaining side is the adjacent.

<figure style="width: 900px">
	<img src="/media/geometry/adjacent-opposite-hypotenuse.svg" alt="The sides of a right-angled triangle">
	<figcaption>The sides of a right-angled triangle</figcaption>
</figure>

# Table of Contents

- Trigonometric ratios
- Unit circle
- Periodicity
- Even and Odd Functions
- Trigonometric Identities
   - Pythagorean Identities
   - Double Angle Identities
   - Half Angle Identities
   - Law of Sines
   - Law of Cosines

# Trigonometric ratios

Trigonometric ratios define a relationship between an angle and two other sides. The six trig ratios are as follows.

$$
\begin{aligned}
   \sin \space \theta &= \frac {\text{opposite}} {\text{hypotenuse}} \\\\
   \cos \space \theta &= \frac {\text{adjacent}} {\text{hypotenuse}} \\\\
   \tan \space \theta &= \frac {\text{opposite}} {\text{adjacent}} \\\\
\end{aligned}
$$

$$
\begin{aligned}
   \cosec \space \theta &= \frac {1} {\sin \space \theta} \\\\
   \sec \space \theta &= \frac {1} {\cos \space \theta} \\\\
   \cot \space \theta &= \frac {1} {\tan \space \theta} \\\\
\end{aligned}
$$

# Unit circle

The unit circle is circle with radius of $1$ unit.

<figure style="width: 1000px">
	<img src="/media/geometry/unit circle.png" alt="Unit circle">
	<figcaption>Unit circle</figcaption>
</figure>

$$
\begin{aligned}
   \sin \space \theta &= \frac {\text{height along y-axis}} {\text{hypotenuse}} \\\\
   \cos \space \theta &= \frac {\text{length along x-axis}} {\text{hypotenuse}}
\end{aligned}
$$

The hypotenuse is $1$ as it is a unit circle. By simplifying, we get

$$
\begin{aligned}
   \sin \space \theta &= \text{height along y-axis} \\
   \cos \space \theta &= \text{length along x-axis}
\end{aligned}
$$

The coordinates at the circumference indicate the sine and cosine for some angle $\theta$.

<figure style="width: 550px">
	<img src="/media/geometry/unit circle angles.png" alt="Unit circle angles">
	<figcaption>Unit circle angles</figcaption>
</figure>

[How to remember the unit circle?](https://www.youtube.com/watch?v=c819bGfH8FA)

# Periodicity

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

# Even and Odd Functions

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
   \sin \space ( -\theta ) &= - \sin \space ( \theta ) \\
   \cos \space ( -\theta ) &= \cos \space ( \theta )
\end{aligned}
$$

Now, we can calculate for tangent,

$$
\begin{aligned}
   \tan \space ( -\theta ) &= \frac{\sin \space ( -\theta )} {\cos \space ( -\theta )}
                                 = \frac{- \sin \space ( \theta )} {\cos \space ( \theta )} \\\\
                                 &= - \tan \space ( \theta )
\end{aligned}
$$

These are called **negative angle identities**.

# Trigonometric Identities

Trigonometric identities are equations that are true for all right-angled triangles. Some important kinds of identities include:

1. Trigonometric ratios
1. Negative angle Identities
1. Pythagorean Identities
1. Sum and Difference Identities
1. Double Angle Identities
1. Half Angle Identities
1. Law of sines
1. Law of cosines

## Pythagorean Identities

Start with the pythagorean theorem,

$$
\tag{1} \text{hyp}^2 = \text{opp}^2 + \text{adj}^2
$$

Divide $(1)$ by $\text{hyp}^2$,

$$
1 = \Big ( \frac{opp}{hyp} \Big ) ^2 + \Big ( \frac{adj}{hyp} \Big ) ^2
$$

$$
\tag{2} \boxed{1 = \sin^2 (\theta) + \cos^2 (\theta)}
$$

Divide $(2)$ by $\sin^2 (\theta)$,

$$
\tag{3} \boxed{\cosec^2 (\theta) = 1 + \text{cot}^2 (\theta)}
$$

Divide $(2)$ by $\cos^2 (\theta)$,

$$
\tag{4} \boxed{\sec^2 (\theta) = \tan^2 (\theta) + 1}
$$

## Sum and Difference Identities

$$
\tag{5} \boxed{\sin \space ( A + B ) =
      \sin \space A \space \cos \space B +
      \cos \space A \space \sin \space B}
$$

$$
\tag{6} \boxed{\cos \space ( A + B ) =
      \cos \space A \space \cos \space B -
      \sin \space A \space \sin \space B}
$$

Let's calculate $\tan \space ( A + B )$,

$$
\begin{aligned}
   \tan \space ( A + B ) &= \frac {\sin \space ( A + B )} {\cos \space ( A + B )}
   \\\\
   \tan \space ( A + B ) &= \frac
      {\sin \space A \space \cos \space B + \cos \space A \space \sin \space B}
      {\cos \space A \space \cos \space B - \sin \space A \space \sin \space B}
\end{aligned}
$$

Divide numerator and denominator by $\cos \space A \space \cos \space B$,

$$
\tag{7}  \boxed{\tan \space ( A + B ) = \frac
      {\tan \space A + \tan \space B}
      {1 - \tan \space A \space \tan \space B}}
$$

The difference identities can be derived by replacing $B$ with $-B$, and using the negative angle identities.

$$
\tag{8} \boxed{\sin \space ( A - B ) =
      \sin \space A \space \cos \space B -
      \cos \space A \space \sin \space B}
$$

$$
\tag{9} \boxed{\cos \space ( A - B ) =
      \cos \space A \space \cos \space B +
      \sin \space A \space \sin \space B}
$$

$$
\tag{10} \boxed{\tan \space ( A - B ) = \frac
      {\tan \space A - \tan \space B}
      {1 + \tan \space A \space \tan \space B}}
$$

## Double Angle Identities

The double angle identities can be derived from sum identities. Just replace $B$ with $A$.

$$
\begin{aligned}
   \sin \space ( A + A ) &=
         \sin \space A \space \cos \space A +
         \cos \space A \space \sin \space A \\

   \tag{11} \sin \space 2A &= 2 \space \sin \space A \space \cos \space A
\end{aligned}
$$

$$
\begin{aligned}
   \cos \space ( A + A ) &=
         \cos \space A \space \cos \space A -
         \sin \space A \space \sin \space A \\

   \tag{12} \cos \space 2A &= \cos^2 \space A - \sin^2 \space A
\end{aligned}
$$

$$
\begin{aligned}
   \tan \space ( A + A ) &= \frac
      {\tan \space A + \tan \space A}
      {1 - \tan \space A \space \tan \space A} \\

   \tag{13} \tan \space 2A &= \frac {2 \space \tan \space A} {1 - \tan^2 \space A}
\end{aligned}
$$

## Half Angle Identities

Consider $(2)$ and $(12)$,

$$
1 = \sin^2 (\theta) + \cos^2 (\theta)
$$

$$
\cos \space 2A = \cos^2 \space A - \sin^2 \space A
$$

Add them to get,

$$
\begin{aligned}
   2 \space \cos^2 \space A &= 1 + \cos ( 2A ) \\
   \tag{14} \cos^2 \space A &= \frac {1 + \cos ( 2A )} {2}
\end{aligned}
$$

Subtract them to get,

$$
\begin{aligned}
   2 \space \sin^2 \space A &= 1 - \cos ( 2A ) \\
   \tag{15} \sin^2 \space A &= \frac {1 - \cos ( 2A )} {2}
\end{aligned}
$$

## Law of Sines

<figure style="width: 650px">
   <img src="/media/geometry/triangle.png" alt="Triangle">
   <figcaption>Triangle</figcaption>
</figure>

The area of any arbitrary triangle is given by,

$$
\frac {1} {2} \space \text{base} \times \text{height}
$$

So, depending on the choice of base, we can write area of a triangle as,

$$
\frac {1} {2} \space b \space (c \space \sin \space A)
=
\frac {1} {2} \space c \space (a \space \sin \space B)
=
\frac {1} {2} \space a \space (b \space \sin \space C)
$$

Simplifying,

$$
b \space c \space \sin \space A
=
c \space a \space \sin \space B
=
a \space b \space \sin \space C
$$

Divide by $a \space b \space c$,

$$
\tag{16} \frac {\sin \space A} {a}
=
\frac {\sin \space B} {b}
=
\frac {\sin \space C} {c}
$$

## Law of Cosines

[Proof is here](https://www.mathopenref.com/lawofcosinesproof.html)

# Reference

- Thomas' Calculus
- [Wikipedia : List of trigonometric identities](https://en.wikipedia.org/wiki/List_of_trigonometric_identities)
- [Math is fun : Even and Odd Functions](https://www.mathsisfun.com/algebra/functions-odd-even.html)
