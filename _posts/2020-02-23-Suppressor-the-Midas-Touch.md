---
layout: post
title: Suppressor&#58 the Midas Touch
tag:
  - maths
  - R
draft: false
comments: true
---
Can adding additional explanatory variable make previously-insiginificant ones significant?

You are conducting regression analysis with lots of variables. You find one of them has a huge p-value. Shall we drop it?

Not so fast. In this post, I show that there is a certain category of explanatory variables (formally known as [*suppressor*](https://en.wikipedia.org/wiki/Mediation_(statistics)#Other_third_variables)), the inclusion of which will increase the explanatory power of exisiting variables, so much so that insignificant ones might end up being significant.

## Problem Formulation
Find $x_1$, $x_2$ and $y$ such that $x_1$ is insiginificant according specification:

$$ y = \alpha + \beta_1 x_1 + \epsilon $$

but siginificant in specification:

$$ y = \alpha ^ \prime + \beta_1 ^ \prime x_1 + \beta_{ 2 } ^ \prime x_2 + \epsilon ^ \prime $$

By definition, $x_2$ is the suppressor we are looking for.

## A Stylized Example
One possible solution would be:

```r
n <- 100
x1 <- rnorm(n, 0, 0.01) # random varaible drawn from normal distribution
x2 <- runif(n, 0, 10) # random variable drawn from uniform distribution
epsilon <- rnorm(n, 0, 0.001)
y <- 3 + 1 * x1 + 1 * x2 + epsilon
```

Not surprisingly, $x_1$ by itself has negligible explanatory power:

| y ~ x1 | Estimate | Std. Error | t value | p-value |
| :---:  | :---:    | :---:      | :---:   | :---:   |
| (Intercept) | 8.0420 | 0.2835 | 28.368 | <2e-16 |
| x1 | 32.3034 | 30.2206 | 1.069 | 0.288 |

However, things change dramatically once we bring $x_2$ into the equation:

| y ~ x1 + x2 | Estimate | Std. Error | t value | p-value |
| :---:       | :---:    | :---:      | :---:   | :---:   |
| (Intercept) | 3.000e+00 |  2.018e-04 | 14866.98 | <2e-16 |
| x1 | 9.867e-01 | 1.052e-02 | 93.81 | <2e-16 |
| x2 | 1.000e+00 | 3.497e-05 | 28599.16 | <2e-16 |

## Discussion
The real reason behind the weird case is the fact $x_2$ completely outshines $x_1$ in terms of the ability to explain the variation in $y$. $x_1$'s usefullness is simply overwhelmed by the huge error term in the absence of $x_2$.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/suppressor/plot1.svg" />
</div>

On the contrary, after controlling for $x_2$ (which already does an excellent job in explaining $y$), the small but non-zero remainder of $y$ is almost entirely driven by $x_1$. 

<div align="center">
  <img src="https://shawenyao.github.io/R/output/suppressor/plot2.svg" />
</div>


## Implications
The existence of suprressor calls for caution when we delete explanatory variables soley based on their insiginificance, although it can also be argued that missing such an important regessor in the first place ($x_2$ in this case) is the greater sin.
