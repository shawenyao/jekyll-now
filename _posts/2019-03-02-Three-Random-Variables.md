---
layout: post
title: Three Random Variables
tag:
  - maths
comments: true
---
Can everything be negatively correlated?

Three random variables have the same pairwise correlation. What values can such correlation take? Obviously, 1 has to be there. So does 0. -1 seems a stretch, but what about -0.9, -0.5 or even -0.0001? The bigger question is, if one is negatively correlated with the rest two, is it necessary for the other two to have positive correlation?

The short answer is no. To see why, I present two solutions in this post. Note that the absence of references is by no means indicative of the idea's originality. In fact, I owe it to many of my friends and professors from the past.

## Problem Formulation
Three random variables $x$, $y$ and $z$ have the same pairwise correlation $\rho$. Find the upper and lower bound of such $\rho$.

## Solution 1: the Algebraic Approach
The correlation matrix of $x$, $y$ and $z$ can be written as:

$$
P = \begin{bmatrix} 
1 & \rho & \rho \\
\rho & 1 & \rho \\
\rho & \rho & 1
\end{bmatrix}
$$

From [covariance matrix's properties](https://en.wikipedia.org/wiki/Covariance_matrix#Which_matrices_are_covariance_matrices?), we know that being a covariance matrix is equivalent to being symmetric and positive semi-definite. Additionaly, from [matrix definitiveness' properties](https://en.wikipedia.org/wiki/Definiteness_of_a_matrix#Characterizations), it can be proven that being positive semi-definite is equivalent to all leading principal minors being non-negative. In the case of a $3 \times 3$ correlation matrix, the three leading principal minors are:

$$
M_1 = 1 \\
M_2 = 1- { \rho } ^ 2 \\
M_3 = 2 {\rho} ^ 3 - 3 {\rho} ^ 2 + 1 = (1 - \rho) ^ 2 (2 \rho + 1)
$$

Solving the system of inequalities:

$$
\begin{cases}
1 \geq 0 \\ 
1- { \rho } ^ 2 \geq 0 \\
(1 - \rho) ^ 2 (2 \rho + 1) \geq 0 \\
\end{cases}
$$

will give us the permissible range of $\rho$:

$$
-0.5 \leq \rho \leq 1
$$

## Solution 2: the Graphical Approach
Let three new random variables $X$, $Y$ and $Z$ be the demeaned version of $x$, $y$ and $z$:

$$
X = x - \bar{x} \\
Y = y - \bar{y} \\
Z = z - \bar{z}
$$

Correlation-wise, substracting a constant doesn't change anything. This suggests that if we think of $X$, $Y$ and $Z$ as three vectors $\vec{X}$, $\vec{Y}$ and $\vec{Z}$ in a $D$-dimensional space, $\rho$ is numerically equal to the [cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity) between any two of them:

$$
\begin{align}
\rho &= \frac{ \sum_{i = 1}^D X_i Y_i }{ \sqrt{ \sum_{i = 1}^D X_i^2 } \sqrt{ \sum_{i = 1}^D Y_i^2 } } \\
&= \frac{ \vec{X} \cdot \vec{Y} }{ \lVert \vec{X} \rVert \lVert \vec{Y} \rVert } \\
&= \frac{ \vec{X} \cdot \vec{Z} }{ \lVert \vec{X} \rVert \lVert \vec{Z} \rVert } \\
&= \frac{ \vec{Y} \cdot \vec{Z} }{ \lVert \vec{Y} \rVert \lVert \vec{Z} \rVert } \\
&= \cos{\theta}
\end{align}
$$

These vectors can point to the same direction to maximize cosine similarity:

<p align="center">
  <img src="https://shawenyao.github.io/R/output/three_random_variables/max_rho.svg" />
</p>

where $\rho = \cos(0^\text{o}) = 1$.

Or they can point to three different directions as far off as possible in the case of a equilateral triangle on the hyperplane:

<p align="center">
  <img src="https://shawenyao.github.io/R/output/three_random_variables/min_rho.svg" />
</p>

where $\rho = \cos(120^\text{o}) = -0.5$.

## Final Thoughts
Both methods can be easily extended to the 4-random-variable case. In the algebraic solution, all it takes is to include the constraint of the 4th-order leading minor in the system of inequalities; in the graphical one, the equilateral triangle becomes a regular tetrahedron.

For 5 random variables and beyond, the former seems to be the better approach due to my inability of further mental visualization, but feel free to leave a comment if you believe otherwise.
