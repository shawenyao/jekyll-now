---
layout: post
title: Visualization of Stochastic Processes
tag: R "Stochastic Processes"
---

Stochastic process makes for an excellent source of visualization.

In this demo, I show the dynamics of stochastic processes along the three physical diemensions:
* `t`: time
* `x`: the value of the stochastic process at time `t`
* `f(x)`: the probability density (or the probablity mass in the discrete case) of `x` at time `t`

Note that the expected value (or the closest permissible value in the discrete case) at each time `t` is also highlighted.

All plots are meant to be interactive. Drag to rotate and scroll to zoom in/out on WebGL-compatable devices. Certain feature like drift, dispersion, mean-reversion or non-negativeness might be more clearly visible from a different angle.


### Trend Stationary Model (without Drift)
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/01_tn1.html" style="border:none;height:500px;width:500px;"></iframe>

### Trend Stationary Model
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/02_tn2.html" style="border:none;height:500px;width:500px;"></iframe>

### Brownian Motion (without Drift)
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/03_bm1.html" style="border:none;height:500px;width:500px;"></iframe>

### Brownian Motion
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/04_bm2.html" style="border:none;height:500px;width:500px;"></iframe>

### Brownian Bridge
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/05_bb.html" style="border:none;height:500px;width:500px;"></iframe>

### Geometric Brownian Motion
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/06_gb.html" style="border:none;height:500px;width:500px;"></iframe>

### Vasicek Model
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/07_vasicek.html" style="border:none;height:500px;width:500px;"></iframe>

### Cox–Ingersoll–Ross Model
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/08_CIR.html" style="border:none;height:500px;width:500px;"></iframe>

### Poisson Process
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/09_poisson.html" style="border:none;height:500px;width:500px;"></iframe>

### Compensated Poisson Process
<iframe src="https://shawenyao.github.io/Visualization-of-Stochastic-Processes/html_output/10_comp_poisson.html" style="border:none;height:500px;width:500px;"></iframe>
