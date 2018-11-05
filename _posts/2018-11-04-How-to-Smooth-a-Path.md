---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation.

$$\vec{ D } = \frac{ 1 }{ 2 } (\vec{ A } + \vec{ B })$$

$$\vec{ D' } = \vec{ D } + \lambda \left\lVert \vec{ AB } \right\rVert \left( 1 + \frac{ \vec{ BA } \cdot \vec{ BC } }{ \left\lVert \vec{ BA } \right\rVert \left\lVert \vec{ BC } \right\rVert } \right) \frac{ \vec{ CE } }{ \left\lVert \vec{ CE } \right\rVert }$$
