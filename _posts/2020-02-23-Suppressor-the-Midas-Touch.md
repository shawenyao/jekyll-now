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

Not so fast. In this post, I show that there exisits a certain category of explanatory variable (formerly known as [*suppressor*](https://en.wikipedia.org/wiki/Mediation_(statistics)#Other_third_variables)), the inclusion of which will increase the explanatory power of exisiting variables, so much so that insignificant ones might end up being significant.

## Problem Formulation
Find $x_1$, $x_2$ and $y$ such that $x_1$ is insiginificant according specification:

$$ y = \alpha + \beta_1 x_1 + \epsilon $$

but siginificant in specification:

$$ y = \alpha ^ \prime + \beta_1 ^ \prime x_1 + \beta_{ 2 } ^ \prime x_2 + \epsilon ^ \prime $$

As a result, $x_2$ will be the supressor we are looking for.

## A Stylized Example

<div align="center">
  <img src="https://shawenyao.github.io/R/output/supressor/plot1.svg" />
</div>

<div align="center">
  <img src="https://shawenyao.github.io/R/output/supressor/plot2.svg" />
</div>


## Implications
The existence of $suprressor$ calls for caution when we delete explanatory variable soley based on its insiginificance. 
