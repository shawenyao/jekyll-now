---
layout: post
title: Three Random Variables
tag:
  - maths
comments: true
---
How can everything be negatively correlated?

Three random variables have the same pairwise correlation. What's the possible range of the correlation?

Two solutions are presented in this post. Note that the lack of reference is by no means indicative of the idea's originality.

## Problem Formulation
Random variable $x$, $y$ and $z$ have the same pairwise correlation $\rho$. What's the upper and lower bound of $\rho$?

## Solution 1: the Algebraic Approach
$$
M = \begin{bmatrix} 1 & \rho & \rho \\ \rho & 1 & \rho \\ \rho & \rho & 1 \end{bmatrix}
$$

[](https://en.wikipedia.org/wiki/Covariance_matrix), being a covariance/correlation matrix is equivalent to being symmetric and positive semi-definite. Additionaly, being positive semi-definite property is equivalent to all leading principal minors being positive.

## Solution 2: the Graphical Approach
Three random variables can be viewed as three vectors in a N dimensional space, and rho is the cosine of the angle between them. They can be pointing to the same direction where the correlation is maximized - cosine(0)=1, or pointing to three directions as far away as possible in the case of a equilateral triangle - cosine(120)=-0.5
This can be extended to the 4-random-variable case easily, where the equilateral triangle becomes a regular tetrahedron.
