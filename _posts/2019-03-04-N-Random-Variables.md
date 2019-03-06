---
layout: post
title: N Random Variables
tag:
  - maths
comments: true
---
Three Random Variables Part II.

In [Part I](/Three-Random-Variables/), I presented the algebraic solution to the problem of what the possible range of correlation is given all three random variables have the same pairwise correlation. Things get a little more interesting when there are more of them, but the question still holds. 

## Problem Formulation
$N$ random variables $x$, $y$ and $z$ have the same pairwise correlation $\rho$. Find the upper and lower bound of such $\rho$.

## Solution
The solution to the $N$ random variable is in spirit the same as the algebraic solution in the 3-variable case. Instead of solving the system of 3 inequalities, we do it for $N$ of them. Note that only the inequality of the highest order is the binding constraint.

$$
M = {
\begin{bmatrix} 
1      & \rho   & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & 1      & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & \rho   & 1      & \cdots & \rho   & \rho   & \rho   \\
\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
\rho   & \rho   & \rho   & \cdots & 1      & \rho   & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & 1      & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & \rho   & 1      \\
\end{bmatrix}}_{N \times N}
$$

## Proof by Induction

$$
m_N = (1 - \rho) ^ {N - 1} [(N - 1) \rho + 1]
$$

**Base Case**: Showing the equation holds when $N = 1$ is trivial, as

$$
m_1 = 1
$$

**Inductive Step**: Suppose the equation holds for some value of $N \geq 1$, we have:

$$
m_{N + 1} = 
$$


