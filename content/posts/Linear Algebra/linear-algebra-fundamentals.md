---
title: "The Fundamentals of Linear Algebra"
date: "2019-09-26"
template: "post"
draft: false
slug: "/posts/linear-algebra-fundamentals/"
category: "Linear Algebra"
tags:
- ""
description: ""
---

**Linear Algebra** is a branch of mathematics that is essential to understand learning algorithms and to describe rotations and translations in animations.

# Table of Contents

- Basics

   - Scalars, Vectors and Matrices
   - Operations on Vectors
   - Operations on Matrices
   - Special Matrices
   - Norms

- Vector Space

   - Vector Space and its properties
   - Linear Combination and Span
   - Linear Independence
   - Basis of a Vector Space
   - Change of Basis using the Gram-Schmidt Process
   - Null Space
   - Row and Column Spaces

- System of Linear Equations

   - Elementary Matrices and Row Echelon Form
   - Solving a System using Gaussian Elimination
   - Linear Transformations
   - Determinant

- Inverse of a Matrix

   - Existence of an Inverse
   - Finding the Inverse using Gauss-Jordan Elimination

- Decomposition

   - Eigen Decomposition
   - LU Decomposition
   - Singular Value Decomposition

# Scalars, Vectors and Matrices

A **scalar** is just any real number. It is denoted by a lowercase alphabet.

A **vector** is an ordered list of numbers and functions. The numbers and functions are called **components** of the vector. It is denoted by a bold lowercase alphabet.

A vector in the form of a column is called a **column vector**, and a vector in the form of a row is called a **row vector**.

$$
\begin{bmatrix}
   a \\
   b
\end{bmatrix}

\qquad

\begin{bmatrix}
   a & b
\end{bmatrix}
$$

The $i^\text{ th}$ element of a vector $\bold{v}$ can be referenced by using a subscript, $\bold{v}_\text{i}$.

A vector can be visualized as a *point in space*, where its components represent the coordinates along different axis.

A **matrix** is a rectangular array of numbers or functions enclosed in brackets. The numbers and functions are called **elements** of the matrix. It is denoted by an uppercase alphabet.

$$
A = \begin{bmatrix}
   a & b \\
   c & d
\end{bmatrix}
$$

$$
B = \begin{bmatrix}
   a & sin(x) & 4 \\
   cos(y) & d & sin(z)
\end{bmatrix}
$$

The **dimension** of a matrix is denoted as *m x n*, where *m* is the number of rows and *n* is the number of columns. You can now see that vectors are a type of matrix where either *m* or *n* is $1$.

The element at the $i^\text{ th}$ row and $j^\text{ th}$ column of a matrix $A$ can be referenced by using a subscript, $A_\text{ i j}$.

$$
A = \begin{bmatrix}
   a & b & c\\
   d & e & f \\
   g & h & i
\end{bmatrix}
$$

# Operations on Vectors

A vector can be seen as an arrow in space, where its components are the coordinates along the different axes. For example, consider the following two-dimensional vector $\bold{v}$.

<figure style="width: 390px">
	<img src="/media/linear algebra/vector.png" alt="Vector">
	<figcaption>The Vector <b>v</b></figcaption>
</figure>

Numerically, it is represented as $
\begin{bmatrix}
   2 \\ 1
\end{bmatrix}
$. The first number tells you how far away from the origin you have to move along the $x$-axis and the second number tells you how far away you have to move along the $y$-axis.

The geometric interpretation of vectors will help us better understand vector operations.

## Addition

Assume that two vectors $\bold{v}$ and $\bold{w}$ have magnitudes $5$ and $7$ respectively. The **addition** of these two vectors can be seen as a tourist following directions. First you walk $5$ steps in the direction of $\bold{v}$. Then, you walk $7$ steps in the direction of the $\bold{w}$.

<figure style="width: 900px">
	<img src="/media/linear algebra/vector addition.png" alt="Vector Addition">
	<figcaption>Vector Addition</figcaption>
</figure>

Note that the same destination point can be reached if you first go in the $\bold{w}$ direction and then the $\bold{v}$. This is the commutative property of vector addition.

Only two vectors with the same dimensions can be added together. The sum is obtained by adding the corresponding elements of both the vectors.

$$
\begin{bmatrix}
	2 \\
	4
\end{bmatrix}

+

\begin{bmatrix}
	0 \\
	7
\end{bmatrix}

=

\begin{bmatrix}
	2 \\
	11
\end{bmatrix}
$$

Addition holds the following properties:

$$
\begin{matrix}
   \bold{a} + \bold{b} = \bold{b} + \bold{a}             				   & \text{Commutative Law} \\\\
   \bold{a} + (\bold{b} + \bold{c}) = (\bold{a} + \bold{b}) + \bold{c}     & \text{Associative Law} \\\\
   \bold{a} + 0 = \bold{a}                    							   & \text{Identity Law}
\end{matrix}
$$

Here, $0$ is a vector where all the elements are $0$, also known as a zero vector.

## Subtraction

**Subtraction** too can be visualized similarly. The tourist just has to move in the opposite direction of $\bold{w}$.

<figure style="width: 900px">
	<img src="/media/linear algebra/vector subtraction.png" alt="Vector Subtraction">
	<figcaption>Vector Subtraction</figcaption>
</figure>

Only two vectors with the same dimensions can be subtracted. The difference is obtained by subtracting the corresponding elements of both the vectors.

$$
\begin{bmatrix}
   1 & 2 \\
   3 & 4
\end{bmatrix}

-

\begin{bmatrix}
   1 & 0 \\
   3 & 7
\end{bmatrix}

=

\begin{bmatrix}
   0 & 2 \\
   0 & -3
\end{bmatrix}
$$

Subtraction holds the following properties:

$$
\begin{matrix}
   \bold{a} - \bold{b} = \bold{b} - \bold{a}                				 & \text{Commutative Law} \\\\
   \bold{a} - (\bold{b} - \bold{c}) = (\bold{a} - \bold{b}) - \bold{c}       & \text{Associative Law} \\\\
   \bold{a} - 0 = \bold{a}                     								 & \text{Identity Law}
\end{matrix}
$$

## Scalar Multiplication

Vectors can be stretched and squished by any factor. This is called **scalar multiplication**. If we want to double the length of a vector, we multiply all its elements by $2$.

<figure style="width: 900px">
	<img src="/media/linear algebra/vector scaling.png" alt="Scalar Multiplication">
	<figcaption>Scalar Multiplication</figcaption>
</figure>

If we want to change the direction of a vector, we multiply it by $-1$.

<figure style="width: 900px">
	<img src="/media/linear algebra/vector direction changing.png" alt="Scalar Multiplication - Reverse Direction">
	<figcaption>Scalar Multiplication - Reverse Direction</figcaption>
</figure>

The product of a vector $\bold{a}$ and a scalar $c$ is written as $c \bold{a}$. The result is obtained by multiplying each element in the matrix by $c$.

$$
5

\cdot

\begin{bmatrix}
   1 \\
   3
\end{bmatrix}

=

\begin{bmatrix}
   5 \\
   15
\end{bmatrix}
$$

Scalar Multiplication holds the following properties :

$$
\begin{matrix}
   c ( \bold{a} + \bold{b}) = c \bold{a} + c \bold{b}        & \text{Distributive Law} \\\\
   ( c + k ) \bold{a} = c \bold{a} + k \bold{a}      	     & \text{Distributive Law} \\\\
   c (k \bold{a}) = (ck) \bold{a}            					     & \text{Associative Law} \\\\
   1 \bold{a} = \bold{a}              				         & \text{Identity Law}
\end{matrix}
$$

## Element-wise product

This is a simple form of vector multiplication where we multiply the corresponding elements of two input vectors with the same dimension. It is denoted by the symbol $\odot$.

$$
\begin{bmatrix}
   4 \\
   2
\end{bmatrix}

\odot

\begin{bmatrix}
   1 \\
   3
\end{bmatrix}

=

\begin{bmatrix}
   4 \\
   6
\end{bmatrix}
$$

## Projection

Let's project a vector onto another vector. In the following figure $a$, $\bold{v}$ and $\bold{w}$ have an angle $\theta$ between them.

<figure style="width: 900px">
	<img src="/media/linear algebra/projection.png" alt="Projection">
	<figcaption>Projection</figcaption>
</figure>

The **projection vector** of $\bold{v}$ onto $\bold{w}$ is like a shadow of $\bold{v}$ falling on $\bold{w}$. The length of the shadow will differ based on the angle $\theta$, but intuitively we can tell that the direction of the projection is always in the same direction as $\bold{w}$.

The **length** of a projection is given by simple trigonometry,

$$
cos(\theta) = \frac{\text{Length of projection}}{\mid \bold{v} \mid}
$$

where, $\mid \bold{v} \mid$ is the magnitude of $\bold{v}$.

The projection vector is,

$$
\bold{p} = \frac {\bold{w}} {\mid \bold{w} \mid} \mid \bold{v} \mid cos(\theta)
$$

## Dot Product

The **dot product** of two vectors $\bold{v}$ and $\bold{w}$ is related to this idea of geometric projection. Assume that both $\bold{v}$ and $\bold{w}$ are unit vectors :

- If $\theta$ is $90$, there will not be any projection of $\bold{v}$ onto $\bold{w}$, so the dot product is $0$. See figure $c$.
- If $\theta$ is $180$, the projection of $\bold{v}$ onto $\bold{w}$ will be in the opposite direction of $\bold {w}$, so the dot product is $-1$. See figure $d$.
- If $\theta$ is $0$, the projection of $\bold{v}$ onto $\bold{w}$ will be in the same direction of $\bold{w}$, so the dot product is $1$. See figure $b$.

This operation takes two vectors of the same dimension and returns a scalar. Hence, it is also known as **scalar product**. Dot product between $\bold{x}$ and $\bold{y}$ is denoted by a central dot $\bold{x} \cdot \bold{y}$.

Geometrically, dot product is defined as,

<figure style="width: 390px">
	<img src="/media/linear algebra/dot product.gif" alt="Finding Dot product">
	<figcaption>Finding Dot product between <b>a</b> and <b>b</b></figcaption>
</figure>

$$
\bold{x} \cdot \bold{y} = \mid \bold{x} \mid \mid \bold{y} \mid \text{cos} \space (\theta)
$$

To multiply two vectors it makes sense to multiply their lengths together but only when they point in the same direction. So we make one point in the same direction as the other by using its projection.

Algebraically, dot product is defined as,

<figure style="width: 390px">
	<img src="/media/linear algebra/dot product 2.gif" alt="Finding Dot product">
	<figcaption>Finding Dot product between <b>a</b> and <b>b</b></figcaption>
</figure>

$$
\bold{x} \cdot \bold{y} = \bold{x}^T \bold{y} = \bold{y}^T \bold{x}
$$

## Cross Product

The **cross product** is another way to multiply two vectors. This operation results in another vector that is orthogonal to both the input vectors. It is also known as **vector product**.

<figure style="width: 390px">
	<img src="/media/linear algebra/cross product.gif" alt="Vector">
	<figcaption>The Vector <b>v</b></figcaption>
</figure>

The length of the resulting vector equals the area of the parallelogram formed by the two input vectors. It reaches maximum length when the input vectors are at right angles. The length is zero when input vectors point in the same or opposite direction.

<figure style="width: 390px">
	<img src="/media/linear algebra/cross product area.svg" alt="Area of the parallelogram">
	<figcaption>Area of the parallelogram</figcaption>
</figure>

It is defined by the formula :

$$
a \times b = \pm \mid a \mid \mid b \mid sin(\theta) \space n
$$

where $\theta$ is the angle between $a$ and $b$, and $n$ is a unit vector perpendicular to $a$ and $b$. The direction of $n$ is determined by the right hand rule.

<figure style="width: 390px">
	<img src="/media/linear algebra/rhs cross.jpg" alt="Right hand rule">
	<figcaption>Right hand rule</figcaption>
</figure>


# Operations on Matrices

## Equality

Two matrices $A$ and $B$ are equal if and only if they have the same dimensions and the corresponding elements are equal.

$$
\begin{bmatrix}
   1 & 2 \\
   3 & 4
\end{bmatrix}

\not =

\begin{bmatrix}
   1 & 10 \\
   23 & 4
\end{bmatrix}
$$

## Transposition

A **transpose** of a matrix $A$ is another matrix obtained by interchanging its rows to columns and its columns to rows. The resulting matrix is denoted by $A^T$.

So, if the dimension of $A$ is *m x n*, the dimension of $A^T$ is *n x m*.

$$
\begin{bmatrix}
   1 & 2 & 5 \\
   3 & 4 & 8
\end{bmatrix} ^ T

=

\begin{bmatrix}
   1 & 3 \\
   2 & 4 \\
   5 & 8
\end{bmatrix}
$$

Performing this operation on a row vector will change it into a column vector, and vice versa.

$$
\begin{bmatrix}
   1 & 2 & 5
\end{bmatrix} ^ T

=

\begin{bmatrix}
   1 \\
   2 \\
   5
\end{bmatrix}
$$

$$
\begin{bmatrix}
   6 \\
   1 \\
   9
\end{bmatrix} ^ T

=

\begin{bmatrix}
   6 & 1 & 9
\end{bmatrix}
$$

Transposition abides by the following rules:

$$
\begin{matrix}
   (A^T)^T = A \\\\

   (A + B)^T = A^T + B^T \\\\

   (cA)^T = cA^T \\\\

   (AB)^T = B^T A^T
\end{matrix}
$$

## Addition

Only two matrices with the same dimensions can be added together. The sum is obtained by adding the corresponding elements of both the matrices.

$$
\begin{bmatrix}
   1 & 2 \\
   3 & 4
\end{bmatrix}

+

\begin{bmatrix}
   1 & 0 \\
   3 & 7
\end{bmatrix}

=

\begin{bmatrix}
   2 & 2 \\
   6 & 11
\end{bmatrix}
$$

Addition holds the following properties:

$$
\begin{matrix}
   A + B = B + A                 & \text{Commutative Law} \\\\
   A + (B + C) = (A + B) + C     & \text{Associative Law} \\\\
   A + 0 = A                     & \text{Identity Law}
\end{matrix}
$$

Here, $0$ is a matrix or vector where all the elements are $0$, also known as zero matrix or zero vector.

## Subtraction

Only two matrices with the same dimensions can be subtracted. The difference is obtained by subtracting the corresponding elements of both the matrices.

$$
\begin{bmatrix}
   1 & 2 \\
   3 & 4
\end{bmatrix}

-

\begin{bmatrix}
   1 & 0 \\
   3 & 7
\end{bmatrix}

=

\begin{bmatrix}
   0 & 2 \\
   0 & -3
\end{bmatrix}
$$

Subtraction holds the following properties:

$$
\begin{matrix}
   A - B = B - A                 & \text{Commutative Law} \\\\
   A - (B - C) = (A - B) - C     & \text{Associative Law} \\\\
   A - 0 = A                     & \text{Identity Law}
\end{matrix}
$$

## Scalar Multiplication

The product of a matrix $A$ and a scalar $c$ is written as $cA$. The result is obtained by multiplying each element in the matrix by $c$.

$$
5

\cdot

\begin{bmatrix}
   1 & 0 \\
   3 & 7
\end{bmatrix}

=

\begin{bmatrix}
   5 & 0 \\
   15 & 35
\end{bmatrix}
$$

Scalar Multiplication holds the following properties :

$$
\begin{matrix}
   c ( A + B ) = cA + cB         & \text{Distributive Law} \\\\
   ( c + k ) A = cA + kA         & \text{Distributive Law} \\\\
   c (kA) = (ck) A               & \text{Associative Law} \\\\
   1 A = A                       & \text{Identity Law}
\end{matrix}
$$

## Matrix Multiplication

The product of two matrices $A$ and $B$ is another matrix $C$. $A$, $B$ can be multiplied only if the number of columns in $A$ equals the number of rows in $B$.

This operation is defined by,

$$
C_\text{i, j} = \sum_k A_\text{i, k} B_\text{k, j}
$$

$$
\begin{bmatrix}
   1 & 2 \\
   3 & 4
\end{bmatrix}

\begin{bmatrix}
   1 & 0 \\
   3 & 7
\end{bmatrix}

=

\begin{bmatrix}
   1 \times 1 + 2 \times 3 & 1 \times 0 + 2 \times 7 \\
   3 \times 1 + 4 \times 3 & 3 \times 0 + 4 \times 7
\end{bmatrix}

=

\begin{bmatrix}
   7 & 14 \\
   15 & 28
\end{bmatrix}
$$

Matrix Multiplication holds the following properties :

$$
\begin{matrix}
   C (A + B) = CA + CB        & \text{Distributive Law} \\\\
   (A + B) C = AC + BC        & \text{Distributive Law} \\\\
   A (BC) = (AB) C            & \text{Associative Law} \\\\
   (kA) B = k (AB) = A (kB)   & \text{Associative Law}
\end{matrix}
$$

It is important to note that matrix multiplication is not commutative.

$$
AB \not = BA
$$

# Special Matrices

Certain types of matrices occur frequently in linear algebra. We will look at some important ones here.

## Square Matrix

If a matrix has an equal number of rows and columns, it is called a **square matrix**. In a square matrix, the diagonal containing the entries $a, b, c$ is called the **main diagonal**. The diagonal containing $c, e, g$ is called the **secondary diagonal**.

## Symmetric and Skew-Symmetric Matrices

**Symmetric Matrices** are square matrices whose transpose equals matrix itself.

$$
A^T = A
$$

**Skew-Symmetric Matrices** are square matrices whose transpose equals *minus* the matrix.

$$
A^T = -A
$$

## Triangular Matrices

**Upper triangular matrices** are square matrices that can have non-zero elements only on and above the main diagonal. All elements below the main diagonal must be $0$.

$$
\begin{bmatrix}
   1 & 2 & 5 \\
   0 & 0 & 8 \\
   0 & 0 & 8
\end{bmatrix}
$$

**Lower triangular matrices** are square matrices that can have non-zero elements only on and below the main diagonal. All elements above the main diagonal must be $0$.

$$
\begin{bmatrix}
   1 & 0 & 0 \\
   6 & 22 & 0 \\
   9 & 3 & 0
\end{bmatrix}
$$


## Orthogonal Matrix

Two vectors $\bold{x}$ and $\bold{y}$ are said to be orthogonal to each other if

$$
\bold{x}^T \bold{y} = 0
$$

Orthogonal unit vectors are called **orthonormal** vectors.

An **orthogonal matrix** is a square matrix whose rows and columns are orthogonal vectors. An **orthonormal matrix** is a square matrix whose rows and columns are orthonormal vectors.

## Diagonal Matrices

**Diagonal matrices** are square matrices where all entries outside the main diagonal are $0$. The diagonal elements can be zero or non-zero.

$$
\begin{bmatrix}
   1 & 0 & 0 \\
   0 & 22 & 0 \\
   0 & 0 & 55
\end{bmatrix}
$$

If all diagonal elements of a diagonal matrix are equal, say $c$, we call this a **scalar matrix**, $S$. This is because the multiplication of any square matrix $A$ with $S$ has the same effect as multiplying each element of $A$ by $c$.

$$
AS = SA = cA
$$

$$
\begin{bmatrix}
   4 & 0 & 0 \\
   0 & 4 & 0 \\
   0 & 0 & 4
\end{bmatrix}
$$

In the above example, the matrix A will be scaled by a factor of $4$.

Another special case is when $c = 1$, this is called an **identity matrix**, and is denoted by $I$. This is a scalar matrix that scales $A$ by $1$; meaning it does not do anything.

$$
AI = IA = A
$$

$$
\begin{bmatrix}
   1 & 0 & 0 \\
   0 & 1 & 0 \\
   0 & 0 & 1
\end{bmatrix}
$$

Diagonal matrices allow for fast computation of determinants, powers and inverses.

- The determinant is the product of its diagonal values.
- A diagonal matrix $D$ raised to the power $k$ is given by each diagonal entry raised to the power $k$.
- The inverse $D^{-1}$ is the reciprocal of all diagonal elements in $D$.

# Norms

We measure the *size* or *magnitude* of a vector using a function called a **norm**. Norms are functions that map vectors to non-negative values. Intuitively, they measure the distance of the vector from the origin.

The general formula for norm is :

$$
\parallel x \parallel_p = \Bigg( \sum_i \mid x_i \mid^p \Bigg)^{\frac {1}{p}}
$$

for $p \in \R$ and $p \ge 1$.

Not any function can be used as a norm. A norm needs to hold the following properties :

- $f(x) = 0 \implies x = 0$. A zero vector must be assigned zero norm.
- $f(x + y) \le f(x) + f(y)$ (the triangle inequality)
- For any $c \in \R$, $f(cx) = \mid c \mid f(x)$. The norm of a vector scaled by $c$ must also be scaled by $c$.

There are many types of norms, each useful in different situations.

## $L^1$ Norm

$$
\parallel x \parallel_1 \space = \space \sum_i \mid x_i \mid
$$

$L^1$ norm is the sum of all components of the vector. It is also called the **Manhattan distance**.

## $L^2$ Norm

$$
\parallel x \parallel_2 \space = \space \Bigg( \sum_i \mid x_i \mid^2 \Bigg)^{\frac {1}{2}}
$$

The $L^2$ norm is the sum of the squares of the components, which is the Euclidean distance between $\bold{x}$ and the origin (a *zero vector*). It is also called **Euclidean norm**, and its the most commonly used norm.

It is also be calculated as $x^T x$.

## Max Norm

The **max norm** of a vector is the absolute value of the component with largest magnitude. It is also known as the $L^\infin$ norm.

$$
\parallel x \parallel_\infin \space = \space \text{max}_i \mid x_i \mid
$$

# Vector Space and its properties

A **vector space** $V$ is a set of vectors upon which we have defined two operations: *scalar multiplication* and *vector addition*. For a set of vectors to be a vector space it must also hold the following properties:

## Closure

- *Additive closure* - If $\bold{u}, \bold{v} \in V$, then $\bold{u} + \bold{v} \in V$
- *Scalar closure* - If $c \in \R$ and $\bold{u} \in V$, then $ c \bold{u} \in V$

## Commutativity

If $\bold{u}, \bold{v} \in V$, then $\bold{u} + \bold{v} = \bold{v} + \bold{u}$

## Associativity

- *Additive associativity* - If $\bold{u}, \bold{v}, \bold{w} \in V$, then $(\bold{u} + \bold{v}) + \bold{w} = \bold{u} + (\bold{v} + \bold{w})$
- *Scalar multiplication associativity* - If $c \in \R$ and $\bold{u}, \bold{v} \in V$, then $\bold{u} (c \bold{v}) = (\bold{u} c) \bold{v}$

## Distributivity

- *Distributivity across vector addition* - If $c \in \R$ and $\bold{u}, \bold{v} \in V$, then $c (\bold{u} + \bold{v}) = c\bold{u} + c\bold{v}$
- *Distributivity across scalar addition* - If $c, d \in \R$ and $\bold{u} \in V$, then $(c + d) \bold{u} = c \bold{u} + d \bold{u}$

## Identity

- *Zero vector* - There is a vector $0$, such that $\bold{u} + 0 \in V$ for all $u \in V$
- *One vector* - There is a vector $1$, such that $1 \bold{u} \in V$ for all $u \in V$

## Inverse

If $\bold{u} \in V$, then there exists a vector $-\bold{u}$, such that $\bold{u} + (-\bold{u}) = 0$.

This is called an *additive* inverse. Note that *multiplicative* inverse is not a property of $V$. This is because only scalar multiplication is defined for vector spaces.


# Linear Combination and Span

Consider a set of vectors $\{ \bold{v^{(1)}}, \bold{v^{(2)}}, ... , \bold{v^{(n)}} \}$ with the same dimension. We define an operation called a **linear combination** where we scale each vector and add all the resulting vectors together. This gives us another vector $\bold{p}$ with the same dimension as the input vectors.

$$
\bold{p} = \sum_i c_i \bold{v^{(i)}}
$$

The components of $\bold{p}$ define a point in space. So, by using different scales $c_i$ we can reach many other points.

<figure style="width: 540px">
	<img src="/media/linear algebra/span.gif" alt="Span">
	<figcaption>Span</figcaption>
</figure>

The set of all possible points reached by *atleast* one linear combination of coefficients (*scales*) is called the **span** of the vectors $\{ \bold{v^{(1)}}, \bold{v^{(2)}}, ... , \bold{v^{(n)}} \}$.

**Example**

Consider the set $\{ \begin{bmatrix}
	1 \\
	0
\end{bmatrix}, \begin{bmatrix}
	0 \\
	1
\end{bmatrix} \}$. In linear combination they can reach any point $\begin{bmatrix}
	a \\
    b
\end{bmatrix}$ in $2D$ space as shown below.

$$
\begin{bmatrix}
	a \\
	b
\end{bmatrix}

=
a \begin{bmatrix}
	1 \\
	0
\end{bmatrix}

+

b \begin{bmatrix}
	0 \\
	1
\end{bmatrix}
$$

Formally, they are said to *span* the vector space $\R^2$.

There can be many sets of vectors that can span the same vector space. For example, the set $\{ \begin{bmatrix}
	1 \\
	1
\end{bmatrix}, \begin{bmatrix}
	0 \\
	1
\end{bmatrix} \}$ can span $\R^2$ with the coefficients $a$ and $b-a$.

$$
a \begin{bmatrix}
	1 \\
	1
\end{bmatrix}

+

(b - a) \begin{bmatrix}
	0 \\
	1
\end{bmatrix}

=

a \begin{bmatrix}
	1 \\
	1
\end{bmatrix}

+

b \begin{bmatrix}
	0 \\
	1
\end{bmatrix}

-

a \begin{bmatrix}
	0 \\
	1
\end{bmatrix}

=

\begin{bmatrix}
	a \\
	b
\end{bmatrix}
$$

# Linear Independence

Consider three vectors $\bold{v^{(1)}}, \bold{v^{(2)}}$ and $\bold{v^{(3)}}$. The vector $\bold{v^{(3)}}$ is said to be linearly independent *wrt* $\bold{v^{(1)}}$ and $\bold{v^{(2)}}$ if it cannot be written as a linear combination of $\bold{v^{(1)}}$ and $\bold{v^{(2)}}$.

$$
\bold{v^{(3)}} \not = a \bold{v^{(1)}} + b \bold{v^{(2)}}
$$

To prove that a set of vectors $\bold{v^{(1)}}, \bold{v^{(2)}}$ and $\bold{v^{(3)}}$ are independent, check if their linear combination is $0$ only if all the coefficients are set to $0$.

$$
a \bold{v^{(1)}} + b \bold{v^{(2)}} + c \bold{v^{(3)}} = 0
$$

Some interesting points to note are:

- A vector set with a zero vector is linearly dependent
- A vector set with only one vector is linearly independent as long as it is not a zero vector.
- If the vector set is already linearly independent, then removing a vector does not affect independence.

[Example](https://youtu.be/yLi8RxqfowA)

# Basis of a Vector Space

A **basis** is a set of $n$ linearly independent vectors the span an $n$-dimensional space. Every point in this $n$-dimensional space can be reached using the basis.

A vector space $V$ can have many number of different bases, but each basis always contains the same number of vectors. The number of basis vectors in a single basis is called the **dimension** of $V$.

<figure style="width: 500px">
	<img src="/media/linear algebra/change of basis.png" alt="Change of Basis">
	<figcaption>Change of Basis</figcaption>
</figure>

The above diagram shows two sets of basis vectors $U$ and $V$ with two dimensions. We can reach any point in the vector space using either of the basis.

It is often useful to be able to change the representation of a vector from one basis to another. This operation is called the **change of basis**.

<figure style="width: 500px">
	<img src="/media/linear algebra/change of basis 2.png" alt="Change of Basis">
	<figcaption>Change of Basis</figcaption>
</figure>

# Gram-Schmidt Process

Sometimes, life is easier if we use an orthonormal basis for a vector space. An **orthonormal basis** consists of vectors with unit norm that are orthogonal to each other.

The **Gram–Schmidt process** takes in a basis $V$ and generates an orthonormal basis $U$ for the same vector space.

<figure style="width: 390px">
	<img src="/media/linear algebra/gram schmidt process.gif" alt="Gram-Schmidt Process">
	<figcaption>Gram-Schmidt Process</figcaption>
</figure>

Consider a basis $V$ with three vectors $\{ v^{(1)}, v^{(2)}, v^{(3)}, v^{(4)}, v^{(5)} \}$. We will incrementally build an orthonormal basis $U$, by iterating through this $V$.

### Finding $u^{(1)}$

First we pick $v^{(1)}$ and make it a unit vector $u^{(1)}$.

$$
u^{(1)} = \frac {v^{(1)}} {\parallel v^{(1)} \parallel}
$$

### Finding $u^{(2)}$

Next we pick $v^{(2)}$. If $v^{(2)}$ has a non-zero projection on $u^{(1)}$, then it is not orthogonal to $u^{(1)}$.

<figure style="width: 390px">
	<img src="/media/linear algebra/gram schmidt projection.svg" alt="Removing the Projection">
	<figcaption>Removing the Projection</figcaption>
</figure>

Note that $v^{(2)}$ can be written as a sum of its $x$ and $y$ components,

$$
v^{(2)} = ({v^{(2)}} \cdot {u^{(1)}})  \space  u^{(1)} + u^{(2)\prime}
$$

By rewriting, we get

$$
u^{(2)\prime} = {v^{(2)}} - ({v^{(2)}} \cdot {u^{(1)}}) \space u^{(1)}
$$

$u^{(2)\prime}$ is divided by its length to get the orthonormal vector $u^{(2)}$.

$$
u^{(2)} = \frac {u^{(2)\prime}} {\parallel u^{(2)\prime} \parallel}
$$

### Finding $u^{(3)}$

The goal is to generate $u^{(3)}$ such that it is orthogonal to *both* $u^{(1)}$ and $u^{(2)}$. Note that $v^{(2)}$ can be written as a sum of its $x$ and $y$ components,

$$
v^{(3)} = \text{projection}_{u^{(1)} u^{(2)} \text{plane}} + u^{(3)\prime}
$$

Expand and rewrite,

$$
\begin{aligned}
   u^{(3)\prime} &=
      v^{(3)} - \Big ( (v^{(3)} \cdot u^{(1)}) \space u^{(1)} + (v^{(3)} \cdot u^{(2)}) \space u^{(2)} \Big )

   \\\\

   u^{(3)\prime} &=
      v^{(3)} - (v^{(3)} \cdot u^{(1)}) \space u^{(1)} - (v^{(3)} \cdot u^{(2)}) \space u^{(2)}

   \\\\

   u^{(3)} &= \frac {u^{(3)\prime}} {\parallel u^{(3)\prime} \parallel}
\end{aligned}
$$

Continue this process until the span of the original vectors $V$ has been reached by $U$.

# Null Space

A null space of a matrix $A$ is a set of vectors that satisfy the homogenous system $A \bold{v} = 0$. It is also called a kernel.

To find the null space, use Gaussian elimination to solve for all possible $\bold{v}$.

[Finding the Null Space Example](https://youtu.be/xRJCdbFY17k)

# Row Space

The **row space** of a matrix $A$ is the span of the rows of $A$, where each row is treated as a basis vector.

<figure style="width: 900px">
	<img src="/media/linear algebra/row vectors.png" alt="Row Vectors">
	<figcaption>Row Vectors</figcaption>
</figure>

Any vector $\bold{v}$ from the span can be reached as a linear combination,

$$
\begin{aligned}
   \bold{v} &= A \bold{x}

   \\\\

   \bold{v} &=
      \begin{bmatrix}
         1 & 8 & 13 & 12\\\\
         14 & 11 & 2 & 7 \\\\
         4 & 5 & 16 & 9 \\\\
         15 & 10 & 3 & 6
      \end{bmatrix}

      \begin{bmatrix}
         a \\\\
         b \\\\
         c \\\\
         d
      \end{bmatrix}

\end{aligned}
$$

# Column Space

The **column space** of a matrix $A$ is the span of the columns of $A$, where each column is treated as a basis vector.

<figure style="width: 900px">
	<img src="/media/linear algebra/column vectors.png" alt="Column Vectors">
	<figcaption>Column Vectors</figcaption>
</figure>

Any vector $\bold{v}$ from the span can be reached as a linear combination,

$$
\begin{aligned}
   \bold{v} &= A \bold{x}

   \\\\

   \bold{v} &=
      a 	\begin{bmatrix}
         1 \\\\
         14 \\\\
         4 \\\\
         15
      \end{bmatrix}

      +

      b 	\begin{bmatrix}
         8 \\\\
         11 \\\\
         5 \\\\
         10
      \end{bmatrix}

      +

      c 	\begin{bmatrix}
         13 \\\\
         2 \\\\
         16 \\\\
         3
      \end{bmatrix}

      +

      d 	\begin{bmatrix}
         12 \\\\
         7 \\\\
         9 \\\\
         6
      \end{bmatrix}

\end{aligned}
$$

[Example](https://youtu.be/A27d9YKFcDE?list=PLkZjai-2Jcxlg-Z1roB0pUwFU-P58tvOx)

# Elementary Matrices and Row Echelon Form

An **elementary matrix** is a square matrix obtained from an identity matrix by performing an elementary row or column operations.

The **row operations for matrices** are as follows:

- *Interchange two rows of the matrix* - It corresponds to the interchange of two equations.
- *Multiplying a row by a nonzero constant* $c$ - It corresponds to multiplying both sides of an equation by the same constant $c$.
- *Adding a constant multiple of one row to another row* - It corresponds to adding two equations together, after multiplying both sides of one of the equations by a constant $c$.

Column operations are similar to this, but unlike row operations they alter the underlying equations into having different solutions.

Row operations are used to convert matrices to the row echelon form. This is called **Gaussian elimination**. A matrix is in **row echelon form** if it satisfies the following conditions:

- Any rows with all zero elements are below rows having non-zero elements
- The leftmost nonzero entry in a row is further to the right than the leftmost nonzero entry of the previous row

For example, triangular matrices are in the row echelon form. Two linear systems are said to be **row equivalent** if one can be obtained from the other using a finitely many row operations. Row equivalent linear systems share the same solution set.

Row echelon forms are useful in solving a system of linear equations, calculating the inverse of a matrix and its rank and nullity.

The **reduced row echelon form** is a more stricter version of the row echelon form.

- It is in row echelon form
- The leading entry in each non-zero row is $1$
- Any column with a leading entry $1$ has zeros in all its other entries

When you use Gaussian elimination to get a *reduced* row echelon form, it is called the **Gauss-Jordan elimination**.

[Reduced Row Echelon Form Example](https://youtu.be/1rBU0yIyQQ8)

# System of Linear Equations

A system of $m$ linear equations with $n$ unknowns is a set of equations in the form of:

$$
a_\text{11} x_1 + \cdots + a_\text{1n} x_n = b_1    \\
a_\text{21} x_1 + \cdots + a_\text{2n} x_n = b_2    \\

\vdots   \\

a_\text{m1} x_1 + \cdots + a_\text{mn} x_n = b_m
$$

It is also known as a **linear system**. The system is called *linear* because each variable $x_i$ only appears in the first power.

If all the $b_i$ are $0$, the system is called a **homogeneous system**. If atleast one $b_i$ is non-zero, the system is called a **non-homogeneous system**.

A **solution** to a system of equations is a set of numbers assigned to the variables $x_1, x_2, \dots, x_n$ that satisfies all the $m$ equations. These numbers are presented as components of a vector called a **solution vector**. For a homogeneous system, there is atleast one solution, which is a zero vector, also called a **trivial solution**.

From the definition of matrix multiplication, we can see that these $m$ equations may be written as a single vector equation.

$$
A \bold{x} = \bold{b}
$$

where $A$ is called the **coefficient matrix** with size *m x n*. $\bold{x}$ is a column vector with $n$ components and $\bold{b}$ is a column vector with $m$ components.

$$
\underbrace{\begin{bmatrix}
   a_\text{11} \qquad a_\text{12} \qquad \cdots \qquad a_\text{1n}   \\
   a_\text{21} \qquad a_\text{22} \qquad \cdots \qquad a_\text{2n}   \\

   \vdots            \\

   a_\text{m1} \qquad a_\text{m1} \qquad \cdots \qquad a_\text{mn}
\end{bmatrix}}_A

\space

\underbrace{\begin{bmatrix}
   x_1 \\
   x_2 \\
   \vdots \\
   x_n
\end{bmatrix}}_\bold{x}

=

\underbrace{\begin{bmatrix}
   b_1 \\
   b_2 \\
   \vdots \\
   b_m
\end{bmatrix}}_\bold{b}
$$

We can be even more terse by using an **augmented matrix** $\widetilde{A}$.

$$
\widetilde{A} = \begin{bmatrix}
   a_\text{11} \qquad a_\text{12} \qquad \cdots \qquad a_\text{1n} \qquad b_1   \\
   a_\text{21} \qquad a_\text{22} \qquad \cdots \qquad a_\text{2n} \qquad b_2   \\

   \vdots            \\

   a_\text{m1} \qquad a_\text{m1} \qquad \cdots \qquad a_\text{mn} \qquad b_m
\end{bmatrix}
$$

The augmented matrix characterizes the system completely because it contains all the numbers appearing in the system.

# Existence and Uniqueness of Solutions

Consider a system of two linear equations with two unknowns,

$$
a_\text{11} x_1 + a_\text{12} x_2 = b_1 \\\\
a_\text{21} x_1 + a_\text{22} x_2 = b_2
$$

If we interpret $x_1$ and $x_2$ as coordinates on an $xy$ axis, then each of these equations represent a straight line, and $\begin{bmatrix}
   p & q
\end{bmatrix}^T$ will be a solution if it is a point that coincides with both the lines.

- If the lines *intersect*, there is one unique solution.
- If the lines *coincide*, there are infinitely many solutions.
- If the lines are *parallel*, there are no solutions.

This geometric visualization can be extended to solving a system with three equations with three unknowns.

A system is called **over determined** if it has more equations than unknowns. It is called **determined** if *m = n*. It is called **under determined** if it has fewer equations than unknowns.

# Solving a System using Gaussian Elimination

**Gaussian Elimination** is a method to convert any linear system into the *row echelon form*, while keeping the solution unchanged. It works with augmented matrices. A system of linear equations is said to be in row echelon form if its augmented matrix is in row echelon form.

Once the system is in row echelon form, we can use *back substitution* to find the unknowns.

[Example 1](https://youtu.be/2j5Ic2V7wq4)
[Example 2](https://youtu.be/RgnWMBpQPXk)

If the linear system has **no solutions**, then Gauss elimination will show this by producing a contradiction in the resulting row echelon form.

The following result of a gauss elimination is inconsistent, due to the presence of the contradiction, $0 = 12$.

$$
\widetilde{A} = \begin{bmatrix}
   3 & 2 & 1 & 3   \\\\
   0 & -\frac{1}{3} & \frac{1}{3} & -2   \\\\
   0 & 0 & 0 & 12
\end{bmatrix}
$$

A system with a contradiction is called **inconsistent** and it does not have any solutions. Otherwise, a system is **consistent** and has at least one solution.

If the system is consistent and under determined, we assign some variables arbitrary values and express the other variables in terms of these arbitrarily assigned unknowns. Due to the arbitrary assignments, the system has **infinitely many solutions**.

A system has a **unique solution** if it is consistent and determined.

# Linear Transformations

A **transformation** is a function that takes a point from $n$-dimensional space and moves it to another location. We can imagine every point from this $n$-dimensional space getting transformed this way, thus space itself is being reshaped.

In some cases, the input vector space, can get squished into a smaller dimension. This means it is possible to take $3D$ space and reshape it into a $2D$ plane.

A transformation is said to be **linear** if the origin stays at the same location, and the grid lines remain evenly spaced and parallel to each other.

What are the new coordinates of a point $V$, after a linear transformation? It turns out that we only need to record where the basis vectors land after the transformation. The *transformed* $V$ is the same linear combination of the *transformed* basis vectors.

**Example**

In the input vector space, the vector $\bold{v}$, $\begin{bmatrix}
   -1 \\
   2
\end{bmatrix}$, is represented as:

$$
-1

\begin{bmatrix}
   1 \\
   0
\end{bmatrix}

+

2

\begin{bmatrix}
   0 \\
   1
\end{bmatrix}

=

\begin{bmatrix}
   -1 \\
   2
\end{bmatrix}
$$

The *transformed* vector $\bold{p}$ is obtained by the same linear combination of the *transformed* basis vectors.

$$
-1

\begin{bmatrix}
   3 \\
   1
\end{bmatrix}

+

2

\begin{bmatrix}
   1 \\
   2
\end{bmatrix}

=

\begin{bmatrix}
   5 \\
   2
\end{bmatrix}
$$

It turns out that this can be expressed using matrix multiplication. The columns of the matrix $L$ known as the **transformation matrix**, are the new positions of the basis vectors.

$$
\underbrace{\begin{bmatrix}
   3 & 1 \\
   1 & 2
\end{bmatrix}}_L

\underbrace{\begin{bmatrix}
   -1 \\
   2
\end{bmatrix}}_\bold{v}

=

\underbrace{\begin{bmatrix}
   5 \\
   2
\end{bmatrix}}_\bold{p}
$$

<figure style="width: 500px">
	<img src="/media/linear algebra/linear transformation matrix.gif" alt="Linear Transformation Matrix">
	<figcaption>Linear Transformation Matrix</figcaption>
</figure>

Some types of transformations include scaling, rotation and sheer. A **composition** is a series of transformations.

For example, a rotation followed by a sheer.

$$
\underbrace{\begin{bmatrix}
   1 & 1 \\
   0 & 1
\end{bmatrix}}_\text{Shear}

\underbrace{\begin{bmatrix}
   0 & -1 \\
   1 & 0
\end{bmatrix}}_\text{Rotation}

\underbrace{\begin{bmatrix}
   x \\
   y
\end{bmatrix}}_\bold{v}

=

\underbrace{\begin{bmatrix}
   1 & -1 \\
   1 & 0
\end{bmatrix}}_\text{Compostion}

\underbrace{\begin{bmatrix}
   x \\
   y
\end{bmatrix}}_\bold{v}
$$

# Determinant

The **determinant** of a transformation measures the factor by which the transformation expands or contracts space.

<figure style="width: 500px">
	<img src="/media/linear algebra/determinant.gif" alt="Determinant">
	<figcaption>Determinant</figcaption>
</figure>

If the determinant is $0$, then the vector space has been squashed to a smaller dimension. Atleast one dimension has been squashed completely.

If the determinant is $1$, then the transformation preserves the number of dimensions of the vector space. A negative value means that the transformation has flipped space over.

The determinant of transformation $L$ is denoted by $det(L)$. In case of two dimensions, calculating the determinant is quiet simple.

$$
det \Bigg( \begin{bmatrix}
   a & b \\
   c & d
\end{bmatrix} \Bigg) = ad - bc
$$

<figure style="width: 500px">
	<img src="/media/linear algebra/calculating determinant.png" alt="Calculating Determinant">
	<figcaption>Calculating Determinant</figcaption>
</figure>

We calculate the area using basic geometric formulas. Read [this](https://www.mathsisfun.com/algebra/matrix-determinant.html) for learning how to calculate the determinant for higher dimensions.

# Inverse of a Matrix

The inverse of a matrix $L$, is a transformation that plays out in the opposite direction of $L$. It is denoted as $L^\text{-1}$.

If $L$ is a rotation of $45$ degrees, then $L^\text{-1}$ is a rotation of $-45$ degrees. If we execute both one after the other, the vector space remains the same. So, the composition of any matrix and its inverse does nothing.

$$
L L^\text{-1} = L L^\text{-1} = I
$$

A matrix with an inverse is called a **non singular matrix** or **invertible matrix**, else it is called a **singular matrix**. Not every matrix has an inverse; but if it does have an inverse, it is always unique.

# Existence of an Inverse

Not all matrices have inverses. Only matrices that satisfy the following conditions are invertible:

- It must be a square matrix $n \times n$.
- The determinant of the matrix must not be zero.
- The *rank* of the matrix must be $n$.

If the determinant becomes $0$, we know that some dimensions of space have been lost. There is no way to regain them by using another transformation.

**Rank** is defined as the maximum number of linearly independent row or column vectors in the matrix. It is equal to the number of non-zero rows in its row echelon matrix.

When all of the vectors in a matrix are linearly independent, the matrix is said to be **full rank**.

# Finding the Inverse using Gauss-Jordan Elimination

**Gauss-Jordan Elimination** can be used to find the inverse of a matrix. Given a matrix $A$, we create a corresponding identity matrix with the same dimensions,

$$
A  = \begin{bmatrix}
	-1 & 1 & 2 \\
	3 & -1 & 2 \\
   -1 & 3 & 4
\end{bmatrix}
$$

$$
[ A \thickspace \mid \thickspace I ]

=

\Bigg \lbrack
\begin{array}{ccc|ccc}
	-1 & 1 & 2 & 1 & 0 & 0 \\
	3 & -1 & 1 & 0 & 1 & 0 \\
   -1 & 3 & 4 & 0 & 0 & 1
\end{array}
\Bigg \rbrack
$$

We perform row operations on the $A$ to convert it to an identity matrix. We perform the same set of row operations to the corresponding identity matrix. This will result in a matrix $A^\text{-1}$ in place of the identity matrix.

Once we get a identity matrix on the left hand side, we can stop.

$$
\Bigg \lbrack
\begin{array}{ccc|ccc}
	1 & 0 & 0 & -0.7 & 0.2 & 0.3 \\
	0 & 1 & 0 & -1.3 & -0.2 & 0.7 \\
   0 & 0 & 1 & 0.8 & 0.2 & -0.2
\end{array}
\Bigg \rbrack
$$

The $RHS$ is the inverse of A.

$$
A^\text{-1}

=

\begin{bmatrix}
	-0.7 & 0.2 & 0.3 \\
	-1.3 & -0.2 & 0.7 \\
   0.8 & 0.2 & -0.2
\end{bmatrix}
$$

# Eigenvectors and Eigenvalues

An **eigenvector** is a non-zero vector such that multiplication by matrix $A$ alters only the scale of $\bold{v}$. The direction of the vector remains the same.

$$
A\bold{v} = \lambda \bold{v}
$$

The scalar $\lambda$ is a real number called the **eigenvalue** or **characteristic value**, and is associated with the **eigenvector** $\bold{v}$.

<figure style="width: 500px">
	<img src="/media/linear algebra/eigenvectors.gif" alt="Eigenvectors">
	<figcaption>Eigenvectors</figcaption>
</figure>

If $\bold{v}$ is an eigenvector of $A$, then so is *every* scaled vector $c\bold{v}$. For this reason, we usually only deal with unit eigenvectors.

## Finding Eigenvalues and Eigenvectors

You have a matrix $A$,

$$
A = \begin{bmatrix}
	-5 & 2\\
	2 & -2
\end{bmatrix}
$$

We write it in terms of the vector equation,

$$
A\bold{v} = \lambda \bold{v}
$$

$$
\begin{bmatrix}
	-5 & 2\\
	2 & -2
\end{bmatrix}

\begin{bmatrix}
	x_1 \\
	x_2
\end{bmatrix}

=

\lambda

\begin{bmatrix}
	x_1 \\
	x_2
\end{bmatrix}
$$

We multiply by $I$ on both sides.

$$
A \bold{v} I = \lambda \bold{v} I
$$

By simplification, we get,

$$
A \bold{v} - \lambda \bold{v} I = 0
$$

$$
A \bold{v} - \lambda \bold{v} I = 0
$$

$$
\tag{1} (A - \lambda I ) \bold{v} = 0
$$

Equation $(1)$ holds true only if the determinant of the matrix $A$ is $0$.

$$
\mid A - \lambda I \mid = 0
$$

$$
\Bigg |

\begin{bmatrix}
	-5 & 2\\
	2 & -2
\end{bmatrix}

-

\lambda

\begin{bmatrix}
	1 & 0 \\
	0 & 1
\end{bmatrix}

\Bigg |

= 0
$$

$$
\Bigg |

\begin{bmatrix}
	-5 & 2\\
	2 & -2
\end{bmatrix}

-

\begin{bmatrix}
	\lambda & 0 \\
	0 & \lambda
\end{bmatrix}

\Bigg |

= 0
$$

$$
\begin{vmatrix}
	-5 - \lambda & 2\\
	2 & -2 - \lambda
\end{vmatrix}

= 0
$$

$$
D(\lambda) = \lambda^2 + 7\lambda + 6 = 0
$$

Equation $D(\lambda)$ is called the **characteristic equation** of $A$. The solutions to this equation are the eigenvalues of matrix $A$. The solutions are $\lambda_1 = -1$ and $\lambda_2 = -6$.

To find the eigenvectors, we plugin each of the eigenvalues in place of $\lambda$ in the characteristic matrix and solve for $\bold{v}$ using Gauss Elimination.

[Another Example](https://youtu.be/IdsV0RaC9jM)

# Eigen Decomposition

Just like integers can be decomposed into prime factors, square matrices can be decomposed into a set of eigenvectors and eigenvalues. Doing so can help us understand certain properties of the matrix.

Consider a matrix $A$ that has $n$ linearly independent eigenvectors $\{ \bold{v}^\text{(1)}, \bold{v}^\text{(2)}, \cdots, \bold{v}^\text{(n)} \}$ with corresponding eigenvalues $\{ \lambda_1, \lambda_2, \cdots, \lambda_n \}$.

We can form a matrix $V$ with one eigenvector per column, $V = [ \bold{v}^\text{(1)}, \bold{v}^\text{(2)}, \cdots, \bold{v}^\text{(n)} ]$. Likewise we form a vector $\lambda$ with all the eigenvalues, $\lambda = [ \lambda_1, \lambda_2, \cdots, \lambda_n ]$.

The **eigen decomposition** of $A$ is given by,

$$
A = V diag(\lambda) V^{-1}
$$

- The first step is to find the eigen values. Then place them in any order as the diagonal elements of a diagonal matrix, denoted as $diag(\lambda)$.
- Find the eigen vectors for these eigen values. Place them in any order as columns of matrix $V$.
- Calculate the inverse of $V$.

This is also called the **diagonalization** of matrix $A$.

[Diagonalization Example](https://youtu.be/Sf91gDhVZWU)

# LU Decomposition

The **Lower-Upper decomposition** factors a square matrix $A$ as a product of a lower and an upper triangular matrix.

$$
A = L \space U
$$

Here is an example. Consider a matrix $A$,

$$
A
=
\begin{bmatrix}
   1 & 2 & 4 \\
   3 & 8 & 14 \\
   2 & 6 & 13
\end{bmatrix}
$$

It turns out we only need to consider a lower triangular matrix filled with $1$'s in the diagonal.

$$
L
=
\begin{bmatrix}
   1 & 0 & 0 \\
   L_{21} & 1 & 0 \\
   L_{31} & L_{32} & 1
\end{bmatrix}
$$

$U$ can be written as follows,

$$
U
=
\begin{bmatrix}
   U_{11} & U_{12} & U_{13} \\
   0 & U_{22} & U_{23} \\
   0 & 0 & U_{33}
\end{bmatrix}
$$

The decomposition can be written as,

$$
\begin{bmatrix}
   1 & 2 & 4 \\
   3 & 8 & 14 \\
   2 & 6 & 13
\end{bmatrix}

=

\begin{bmatrix}
   U_{11}        & U_{12}                        & U_{13} \\
   L_{21} U_{11} & U_{21} U_{12} + U_{22}        & U_{21} U_{13} + U_{23} \\
   L_{31} U_{11} & U_{31} U_{12} + U_{32} U_{22} & U_{31} U_{13} + U_{32} U_{23} + U_{33}
\end{bmatrix}
$$

We know the values of $U_{11}$, $U_{12}$ and $U_{13}$, so we use back substitution to find the values of $U_{ij}$ and $L_{ij}$.

Now we can express the decomposition $A = L \space U$ using these values.

## Row swapping

A matrix is LU decomposable only if all its leading sub-matrices have non-zero determinants. If this is not the case, we need to re-order the rows of $A$ to make it so.

$$
P \space A = L \space U
$$

[Example](https://youtu.be/-eA2D_rIcNA)

# Singular Value Decomposition

**Singular value decomposition** provides another way to factorize a matrix into **singular vectors** and **singular values**.

**SVD** works for all matrices, unlike eigen decomposition which only works for square matrices.

SVD is written as a product of three matrices:

$$
A = UDV^T
$$

Both $U$ and $V$ are square orthogonal matrices. The matrix $D$ is a rectangular diagonal matrix. The elements along $D$ are called the **singular values**. The columns of $U$ are called **left-singular vectors** and the columns of $V$ are called **right-singular vectors**.

# References

- [StackExchange : Basis](https://math.stackexchange.com/questions/2781728/intuition-for-a-basis-in-vector-spaces?rq=1)
- [StackExchange : Basis vs Span](https://math.stackexchange.com/questions/1298492/understanding-the-difference-between-span-and-basis)
- [A First Course in Linear Algebra](http://linear.ups.edu/html/section-VS.html)
- [Gram–Schmidt Process MIT](https://www.youtube.com/watch?v=TRktLuAktBQ&)
- [Row Echelon Form](https://stattrek.com/statistics/dictionary.aspx?definition=reduced_row_echelon_form)
- [Row Echelon Form vs Upper Triangular Matrix](https://math.stackexchange.com/questions/1720647/is-there-no-difference-between-upper-triangular-matrix-and-echelon-matrixrow-ec)
- [Matrix Rank](https://stattrek.com/matrix-algebra/matrix-rank.aspx)
