---
layout: post
title: Three Random Variables
tag:
  - maths
comments: true
---
How can everything be negatively correlated?

Three random variables have the same pairwise correlation. What's the possible range of such correlation? Intuitively, 1 needs to be there, so is 0. -1 seems to be a stretch, but what about -0.9? -0.5? or -0.001? If one is negatively correlated with the rest two, is it necessary for the other two to exihibit positive correlation?

Two solutions are presented in this post. Note that the absence of reference is by no means indicative of the idea's originality. In fact, I owe it to many of my friends and professors.

## Problem Formulation
Random variable $x$, $y$ and $z$ have the same pairwise correlation $\rho$. What's the upper and lower bound of $\rho$?

## Solution 1: the Algebraic Approach
The correlation matrix of random variables $x$, $y$ and $z$ can be written as:

$$
M = \begin{bmatrix} 
1 & \rho & \rho \\
\rho & 1 & \rho \\
\rho & \rho & 1
\end{bmatrix}
$$

From [covariance matrix's properties](https://en.wikipedia.org/wiki/Covariance_matrix#Which_matrices_are_covariance_matrices?), we know that being a covariance matrix is equivalent to being symmetric and positive semi-definite. Additionaly, from [matrix definitiveness' properties](https://en.wikipedia.org/wiki/Definiteness_of_a_matrix#Characterizations), it can be proven that being positive semi-definite is equivalent to all leading principal minors being positive.

In the case of a $3 \times 3$ correlation matrix, the three leading principal minors are:

$$
m_1 = 1 \\
m_2 = 1- { \rho } ^ 2 \\
m_3 = 2 {\rho} ^ 3 - 3 {\rho} ^ 2 + 1 = (\rho - 1) ^ 2 (2 \rho + 1)
$$

Solving the system of inequalities:

$$
\begin{cases}
1 \geq 0 \\ 
1- { \rho } ^ 2 \geq 0 \\
(\rho - 1) ^ 2 (2 \rho + 1) \geq 0 \\
\end{cases}
$$

will give us the possible range of $\rho$:

$$
-0.5 \leq \rho \leq 1
$$

## Solution 2: the Graphical Approach
Let three new random variables $X$, $Y$ and $Z$ be the demeaned versions of $x$, $y$ and $z$:

$$
X = x - \bar{x} \\
Y = y - \bar{y} \\
Z = z - \bar{z}
$$

Substracting a constant has no impact on the correlation, so $\rho$ is still the pairwise correlation of $X$, $Y$ and $Z$.

$$
\rho = \frac{ \sum_{i = 1}^N X_i \times Y_i }{ \sqrt{ \sum_{i = 1}^N X_i } \sqrt{ \sum_{i = 1}^N Y_i } }
$$

Thas implies that if we think of the $X$, $Y$ and $Z$ as three vectors $\vec{X}$, $\vec{Y}$ and $\vec{Z}$ in an N dimensional space, $\rho$ is numerically equal to the cosine similarity between any two of them. The three vectors can be pointing to the same direction where the correlation is maximized

where $\rho = \cos(0^\text{o}) = 1$,

or pointing to three directions as far away as possible in the case of a equilateral triangle

where $\rho = \cos(120^\text{o}) = -0.5$.

## Final Thoughts
Both approaches can be easily extended to the 4-random-variable case. In the algebraic solution, all it takes is to include the constraint of the 4th leading minor in the system of inequalities; in the graphical one, the equilateral triangle becomes a regular tetrahedron. For 5 random variables and beyond, the former seems to be the superior solution due to my inability of further visualization, but feel free to leave a comment if you believe otherwise.

