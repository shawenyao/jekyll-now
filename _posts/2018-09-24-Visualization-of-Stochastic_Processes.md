---
layout: post
title: Visualization of Stochastic Processes
tag:
  - visualization
  - maths
  - r
comments: true
---

Stochastic process makes for an excellent source of graphical beauty.

In this demo, I present the dynamics of stochastic processes along the three physical diemensions of:
* $t$: time
* $x$: the value of the stochastic process at time $t$
* $f(x)$: the probability density (or the probablity mass in the discrete case) of $x$ at time $t$

Note that the expected value (or the closest permissible value in the discrete case) at each time $t$ is also highlighted.

All plots are meant to be interactive. Drag to rotate and scroll to zoom in/out on WebGL-compatable devices. Certain feature like drift, dispersion, mean-reversion or non-negativeness might be more clearly visible from a different angle.


## Trend Stationary Model (without Drift)
$X_t = X_0 + \epsilon_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/01_tn1.html" style="border:none;height:500px;width:500px;"></iframe>

## Trend Stationary Model
$X_t = X_0 + \beta t + \epsilon_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/02_tn2.html" style="border:none;height:500px;width:500px;"></iframe>

## Brownian Motion (without Drift)
$dX_t = \sigma dW_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/03_bm1.html" style="border:none;height:500px;width:500px;"></iframe>

## Brownian Motion
$dX_t = \mu t + \sigma dW_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/04_bm2.html" style="border:none;height:500px;width:500px;"></iframe>

## Brownian Bridge
$X_t = \frac{t}{T} X_T + \frac{T-t}{T} (X_0 + \sigma W_t)$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/05_bb.html" style="border:none;height:500px;width:500px;"></iframe>

## Geometric Brownian Motion
$dX_t = \mu X_t t + \sigma X_t dW_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/06_gb.html" style="border:none;height:500px;width:500px;"></iframe>

## Vasicek Model
$dX_t = a(b-X_t)dt + \sigma dW_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/07_vasicek.html" style="border:none;height:500px;width:500px;"></iframe>

## Cox–Ingersoll–Ross Model
$dX_t = a(b-X_t)dt + \sigma \sqrt{X_t}dW_t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/08_CIR.html" style="border:none;height:500px;width:500px;"></iframe>

## Poisson Process
$P(X_t = k) = e^{-\lambda t} \frac{(\lambda t) ^ k}{k,!}$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/09_poisson.html" style="border:none;height:500px;width:500px;"></iframe>

## Compensated Poisson Process
$X_t = N_t - \lambda t$
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/10_comp_poisson.html" style="border:none;height:500px;width:500px;"></iframe>
