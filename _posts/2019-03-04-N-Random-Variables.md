---
layout: post
title: N Random Variables
tag:
  - maths
comments: true
draft: false
---
Three Random Variables Part II.

In [Part I](/Three-Random-Variables/), I presented the algebraic solution to the problem of what the possible range of correlation is given all three random variables have the same pairwise correlation. Things get a little more interesting when there are more of them, but the idea still holds. 

## Problem Formulation
$N$ random variables $x_1$, $x_2$, ..., $x_N$ have the same pairwise correlation $\rho$. Find the upper and lower bound of such $\rho$.

## Solution
The correlation matrix of $x_1$, $x_2$, ..., $x_N$ can be written as:

$$
P = {\begin{bmatrix} 
1      & \rho   & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & 1      & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & \rho   & 1      & \cdots & \rho   & \rho   & \rho   \\
\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
\rho   & \rho   & \rho   & \cdots & 1      & \rho   & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & 1      & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & \rho   & 1      \\
\end{bmatrix}}_{N \times N}
$$

Generally, $P$'s leading principal minor of order $i$ has the form of:

$$
M_{i} = {\begin{vmatrix} 
1      & \rho   & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & 1      & \rho   & \cdots & \rho   & \rho   & \rho   \\
\rho   & \rho   & 1      & \cdots & \rho   & \rho   & \rho   \\
\vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
\rho   & \rho   & \rho   & \cdots & 1      & \rho   & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & 1      & \rho   \\
\rho   & \rho   & \rho   & \cdots & \rho   & \rho   & 1      \\
\end{vmatrix}}_{i \times i} \\
$$

If $\rho = 1$, we have:

$$
M_{i} = 0
$$

If $\rho \neq 1$, we can find the equivalent upper-triangle of $M_{i}$ by performing two [elementary row operations](https://en.wikipedia.org/wiki/Gaussian_elimination#Computing_determinants):
* substract the last row from every other row;
* add every other row multiplied by $\rho / (\rho - 1)$ to the last row.

$$
\begin{align}
M_{i} &= {\begin{vmatrix} 
1 - \rho & 0        & 0        & \cdots & 0        & 0        & \rho -1 \\
0        & 1 - \rho & \rho     & \cdots & \rho     & \rho     & \rho -1 \\
0        & 0        & 1 - \rho & \cdots & \rho     & \rho     & \rho -1 \\
\vdots   & \vdots   & \vdots   & \ddots & \vdots   & \vdots   & \vdots  \\
0        & 0        & 0        & \cdots & 1 - \rho & 0        & \rho -1 \\
0        & 0        & 0        & \cdots & 0        & 1 - \rho & \rho -1 \\
\rho     & \rho     & \rho     & \cdots & \rho     & \rho     & 1       \\
\end{vmatrix}}_{i \times i} \\
\\
&= {\begin{vmatrix} 
1 - \rho & 0        & 0        & \cdots & 0        & 0        & \rho -1          \\
0        & 1 - \rho & \rho     & \cdots & \rho     & \rho     & \rho -1          \\
0        & 0        & 1 - \rho & \cdots & \rho     & \rho     & \rho -1          \\
\vdots   & \vdots   & \vdots   & \ddots & \vdots   & \vdots   & \vdots           \\
0        & 0        & 0        & \cdots & 1 - \rho & 0        & \rho -1          \\
0        & 0        & 0        & \cdots & 0        & 1 - \rho & \rho -1          \\
0        & 0        & 0        & \cdots & 0        & 0        & (i - 1) \rho + 1 \\
\end{vmatrix}}_{i \times i} \\
\\
&= (1 - \rho) ^ {i - 1} [(i - 1)  \rho + 1]
\end{align}
$$

which also happens to be $0$ when $\rho = 1$.

From [Part I](/Three-Random-Variables/), we know that all leading principal minors of $P$ need to be non-negative. Solving the system of inequalities:

$$
\begin{cases}
(1 - \rho) ^ {1 - 1} [(1 - 1) \rho + 1] \geq 0 \\ 
(1 - \rho) ^ {2 - 1} [(2 - 1) \rho + 1] \geq 0 \\
\quad \vdots \\
(1 - \rho) ^ {i - 1} [(i - 1) \rho + 1] \geq 0 \\
\quad \vdots \\
(1 - \rho) ^ {N - 1} [(N - 1) \rho + 1] \geq 0 \\
\end{cases}
$$

will give us the permissible range of $\rho$:

$$
-\frac{1}{N - 1} \leq \rho \leq 1
$$

## Implications
The general form of lower bound suggests that it is _always_ possible for every pair of random variables to have negative correlation, regardless of how many of them there are.

Back to the graphical analogy, every vector will be pushed towards being perpendicular to each other in the limit.
