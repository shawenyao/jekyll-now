---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation.

![plot1](https://shawenyao.github.io/R/output/plot1.svg)

In some cases, a `spline` function would be able to solve the problem in an efficient and elegant manner. However, it is not inconceivable to have a path so twisted that a function (in the mathematical sense) simply fails to characterize the trajectory, and this is where computational algorithm.

## Problem Formulation

## A Heuristic Solution
$$\overrightarrow{ D } = \frac{ 1 }{ 2 } (\overrightarrow{ A } + \overrightarrow{ B })$$

$$\overrightarrow{ D' } = \overrightarrow{ D } + \lambda \| \overrightarrow{ AB } \| \left( 1 + \frac{ \overrightarrow{ BA } \cdot \overrightarrow{ BC } }{ \| \overrightarrow{ BA } \| \| \overrightarrow{ BC } \| } \right) \frac{ \overrightarrow{ CE } }{ \| \overrightarrow{ CE } \| }$$

## Discussion

## Extension

## Examples

