---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation even when spline fails.

<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot1.svg" />
</p>

In some cases, the `spline` function alone would have already solved the problem. However, it is not inconceivable to have a path so twisted that a function (in the mathematical sense) simply fails to characterize all the trajectories, and this is where an alternative approach is needed.

## Problem Formulation
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_problem_formulation.svg" />
</p>

## A Heuristic Solution
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_heuristic_solution.svg" />
</p>

$$\overrightarrow{ D } = \frac{ 1 }{ 2 } (\overrightarrow{ A } + \overrightarrow{ B })$$

$$\overrightarrow{ P } = \overrightarrow{ D } + \lambda \| \overrightarrow{ AB } \| \left( 1 + \frac{ \overrightarrow{ BA } \cdot \overrightarrow{ BC } }{ \| \overrightarrow{ BA } \| \| \overrightarrow{ BC } \| } \right) \frac{ \overrightarrow{ CE } }{ \| \overrightarrow{ CE } \| }$$

## Discussion

## Extension

## Examples
<p align="center">
  <img src="https://shawenyao.github.io/R/output/plot_example.svg" />
</p>
