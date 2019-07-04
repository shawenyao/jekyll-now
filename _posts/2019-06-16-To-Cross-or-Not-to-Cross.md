---
layout: post
title: To Cross or Not to Cross
tag:
  - maths
comments: true
draft: true
---

A numerical experiment on how to optimally wait for traffic signals.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/to_cross_or_not_to_cross/plot1.svg" />
</div>

You are commuting on foot in Manhattan. You wish to go from point A to point B. The only thing standing in your way is the numerous traffic lights. How should you strategize? To start with, do you go north or east first?

Since there's no obvious advantage or disadvantage going either way, you decide to let the green light guide your way. All goes well until you've reached point C or point D, where finally, there is a clear winner.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/to_cross_or_not_to_cross/plot2.svg" />
</div>

I am not sure about you, but I would very much prefer to be at point D.

Why? Because red and green signals aren't evenly distributed. Usually, main streets have a larger share of green light, while the minor ones get more red. Each road has a certain level of "importance" associated with it, as demonstratively indicated by the width of the lane in the plot above.

So you say to yourself: it seems a really good idea to end up in point D. In order to pull it off, does it make sense to wait for a few seconds in one or more of the preceding crossroads? More generally, does the optimal decision exist?

To find out, let's take a walk. Note that since you have to walk the full [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry) in any case, the time spent on actual walking is irrelevant for comparison purposes.

## Strategy 1: Let the Light Guide Your Way

## Strategy 2: Ride Along Main Street

## Strategy 3: Conditional Wait
