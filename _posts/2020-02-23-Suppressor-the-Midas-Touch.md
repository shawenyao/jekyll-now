---
layout: post
title: Suppressor&#58 the Midas Touch
tag:
  - maths
  - R
draft: true
comments: true
---
Can adding additional explanatory variable make previously-insiginificant ones significant?

You are conducting regression analysis with lots of varibales. You find one of them has a huge p-value of. Can you drop it?

Not so fast. In this post, I show that there exisits a certain category of explanatory variable (formally known as [*suppressor*](https://en.wikipedia.org/wiki/Mediation_(statistics)#Other_third_variables)), the inclusion of which will increase the explanatory power of exisiting variables, so much so that insignificant ones might end up being significant.

## Problem Formulation
Find $x_1$, $x_2$ and $y$ such that $x_1$ is insiginificant according specification:

$$ y = \alpha + \beta_1 x_1 + \epsilon $$

but siginificant in specification:

$$ y = \alpha ^ \prime + \beta_1 ^ \prime x_1 + \beta_{ 2 } ^ \prime x_2 + \epsilon ^ \prime $$

By definition, $x_2$ is the suppressor we are looking for.

## A Stylized Example

```r
n <- 100
x1 <- rnorm(n, 0, 0.01) # random varaible drawn from normal distribution
x2 <- runif(n, 0, 10) # random variable drawn from uniform distribution
epsilon <- rnorm(n, 0, 0.001)
y <- 3 + 1 * x1 + 1 * x2 + epsilon
```

As a result, $x1$ by itself will have limited explanatory power:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/suppressor/plot1.svg" />
</div>

But once we bring $x2$ into the equation, . This is due to the fact that after controlling for $x2$, the remainder of $y$ can be explained by $x2$ fairly well:

<div align="center">
  <img src="https://shawenyao.github.io/R/output/suppressor/plot2.svg" />
</div>


## Implications
The existence of suprressor calls for caution when we delete explanatory variable soley based on its insiginificance. 
