---
layout: post
title: To Wait or Not to Wait
tag:
  - maths
comments: true
draft: true
---

A numerical experiment on how to optimally wait for traffic signals.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/to_cross_or_not_to_cross/plot1.svg" />
</div>

You are commuting on foot in Manhattan. You wish to go from point A to point B. The only thing standing in your way is the numerous traffic lights. How should you strategize? To start with, do you go south or east first?

Since there's no obvious advantage or disadvantage going either way, you decide to let the green light guide your way. All goes well until you've reached point C or point D, where finally, there is a clear winner.

<div align="center">
  <img src="https://shawenyao.github.io/R/output/to_cross_or_not_to_cross/plot2.svg" />
</div>

I am not sure about you, but between point C and point D, I would very much prefer the latter.

Why? Because traffic signals aren't evenly distributed. Usually, main streets have a larger share of green light, while the minor ones get more red. Each road has a certain level of "importance" associated with it, as demonstratively indicated by the width of the lane in the plot above.

So you say to yourself: it seems a really good idea to end up in point D. To pull it off, does it make sense to wait for a few seconds in one or more of the preceding crossroads? More generally, is there an optimal decision?

To find out, let's take a walk. Note that since you have to walk the full [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry) in any case, the time spent on actual walking is irrelevant for comparison purposes.

## Strategy 1: Let the Light Guide Your Way

You are a brave soul. You don't want to be bound by any rules. So you keep it simple. You follow wherever the green light tells you to go, unless you've already reached the boundary, in which case you wait for the signals to turn green (if you have to).

## Strategy 2: Conditional Wait

We've already shown that not every traffic signal comes equal. Suppose you are walking _eastbound_ along one of the major streets. More likely than not, you run into a green light. But you also notice that the green light that allows you to walk straight ahead is dying out, and soon enough, you will be able to make a turn and go _southbound_. You decide to seize the opportunity, beacuse waiting a few seconds for something this rare sounds like a good deal.

The conditional wait strategy requires the introduction of two new parameters:
* the "rarity" of a green light, defined as the ratio of the current wait time to maximum wait time
* the relative "importnace" of a road, defined as the ratio of the absolute "importance" of the two crossing roads

## Strategy 3: Ride Along Main Street

Main Street, defined as the street of the highest "importance" (either horizontaly or vertically), has a nice property to it. If you walk along Main Street, chances are that you will face green traffic signals more often than it would have been otherwise on any other street.

## Putting it All Together

<div align="center">
  <img src="https://shawenyao.github.io/R/output/to_cross_or_not_to_cross/plot3.svg" />
</div>

Numerical simulation suggests that you simply cannot beat strategy 1. Strategy 2 gradually gets worse as we increase the two artificial thresholds that enable it to behave differently from strategy 1. Strategy 3, while doesn't sound like a terrible idea, performs the worst.

