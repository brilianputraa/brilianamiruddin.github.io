---
layout: post
title: "[Optimal Control/최적제어] Convexity"
toc: true
author:
  - Brilian Putra Amiruddin
tags: [optimal_control,model_predictive_control]
---

## Convex Set
`Definition` a line connecting to line in the sets is constrained in the set. The simple terms is we can connect any two points inside the set with a line. **In condition that the line which connects the two points is inside the sets**.

### Examples of Convex Sets:
- `Linear Subspace` $$\begin{align} Ax =b \end{align}$$
- `Half-space, Hyperplane, Polytope` $$\begin{align} Ax \leq{b} \end{align}$$
- `Elipsoids` $$\begin{align} x^TPx \leq 1, P \gt 0 \end{align}$$
- `Cones` $$\begin{align} \| x_{2:n}\|_2 \leq  x_1  \end{align}$$

## Convex Function
$$ \begin{aligned} \text{A function} \, f(x) :  \mathbb{R^n} \rightarrow \mathbb{R} \, \text{whose epigraph is a convex set.}  \end{aligned}$$

But what is epigraph? `Everything above the function lines is called epigraph.`

### Examples of Convex Function:
- `Linear` $$\begin{align} f(x) = c^Tx \end{align}$$
- `Quadratic` $$\begin{align} f(x) = \frac{1}{2}x^TQx + q^Tx, Q \gt{0} \end{align}$$
- `Norms (Any Norms)` $$\begin{align}  \lvert x \rvert \end{align}$$

## Convex Optimization Problem
Generally, solving a convex optimization problem is **minimizing a convex function over a convex sets**. 
### Examples of Convex Optimization Problem:
- `Linear Program (LP)` $$\begin{aligned}  \text{linear cost function} \, f(x) \, \text{and} \, \text{linear constraints} \, c(x) \end{aligned}$$
- `Quadratic Program (QP)` $$\begin{aligned}  \text{quadratic cost function} \, f(x) \, \text{and} \, \text{linear constraints} \, c(x) \end{aligned}$$
- `Quadratically Constrained QP (QCQP)` $$\begin{aligned}  \text{quadratic cost function} \, f(x) \, \text{and} \, \text{elipsoid constraints} \, c(x) \end{aligned}$$
- `Second Order Cone Program (SOCP)` $$\begin{aligned}  \text{linear cost function} \, f(x) \, \text{and} \, \text{conic constraints} \, c(x) \end{aligned}$$

`In the Convex Optimization, there is no spurious local optima solution`. Technically, **if we manage to find the local optima Karush–Kuhn–Tucker (KKT) condition it will be our global solution**.

Newton's Method can work really well and converge really fast with 5~10 iterations (able to bound solution for the real-time control).
> [Written based on CMU Optimal Control Course 16-745](https://www.youtube.com/playlist?list=PLZnJoM76RM6KugDT9sw5zhAmqKnGeoLRa).
