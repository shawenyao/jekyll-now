---
layout: post
title: Three Random Variables
tag:
  - maths
comments: true
---
How can everything be negatively correlated?

Three random variables have the same pairwise correlation. What's the possible range of the correlation?

Two solutions are presented in this post. Note that the lack of reference is by no means indicative of the idea's originality. In fact, I owe it to many of my friends and professors.

## Problem Formulation
Random variable $x$, $y$ and $z$ have the same pairwise correlation $\rho$. What's the upper and lower bound of $\rho$?

## Solution 1: the Algebraic Approach
The correlation matrix of random variables $x$, $y$ and $z$ can be written as:

$$
M = \begin{bmatrix} 1 & \rho & \rho \\ \rho & 1 & \rho \\ \rho & \rho & 1 \end{bmatrix}
$$

From [covariance matrix's properties](https://en.wikipedia.org/wiki/Covariance_matrix#Which_matrices_are_covariance_matrices?), we know that being a covariance matrix is equivalent to being symmetric and positive semi-definite. Additionaly, from [matrix definitiveness' properties](https://en.wikipedia.org/wiki/Definiteness_of_a_matrix#Characterizations), it can be proven that being positive semi-definite is equivalent to all leading principal minors being positive.

In the case of a $3 \times 3$ correlation matrix, the three leading principal minors are:

$$
1st leading principal minor = 1 \\
2nd leading principal minor = 1- { \rho } ^ 2 \\
3nd leading principal minor = \\
$$

## Solution 2: the Graphical Approach
Three random variables can be viewed as three vectors in a N dimensional space, and rho is the cosine of the angle between them. They can be pointing to the same direction where the correlation is maximized - cosine(0)=1, or pointing to three directions as far away as possible in the case of a equilateral triangle - cosine(120)=-0.5
This can be extended to the 4-random-variable case easily, where the equilateral triangle becomes a regular tetrahedron.
