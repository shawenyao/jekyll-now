---
layout: post
title: How to Smooth a Path
tag:
  - visualization
  - maths
---

Context-aware interpolation.

$$\vec{ D } = \frac{ 1 }{ 2 } (\vec{ A } + \vec{ B })$$

$$\vec{ D' } = \vec{ D } + \lambda \lvert \vec{ AB } \rvert \left( 1 + \frac{ \vec{ BA } \cdot \vec{ BC } }{ \lvert \vec{ BA } \rvert \lvert \vec{ BC } \rvert } \right) \frac{ \vec{ CE } }{ \lvert \vec{ CE } \rvert }$$
