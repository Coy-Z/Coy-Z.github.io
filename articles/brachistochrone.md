---
layout: default
title: Brachistochrone Problem
permalink: /articles/brachistochrone/
---

# Brachistochrone Problem

The problem objective is to find the shape of a slope connecting two points, such that a ball rolling down the slope (from the higher to lower point) would do so in the shortest time. The gif (taken from <a href="https://nilabhasaha.wordpress.com/2019/02/24/a-tour-through-some-curves-part-1-the-brachistochrone-problem/">nilabhasaha.wordpress.com</a>) attached below illustrates this concept, using three curves: the path of shortest distance, the path of highest maximum acceleration and the brachistochrone.

<img src="/files/brachistochrone.gif" alt="" width="400" height="200"/>

The mathematics I will use to solve this problem requires some understanding of matrix calculus, which I discuss in another <a href="/articles/matrixcalc/">article</a>.

## Defining Problem Parameters

I define the fixed end points to be $(0,0)$ to $(L,-H)$ and the slope to be $y(x)$. There is an implicit assumption that $y$ is somewhat well-behaved.

Here, $y \in \mathcal{V}$ where $\mathcal{V}$ denotes the vector space of functions defined on the range $\[0,L\]$

## Quantifying the Time of Descent

We wish to determine the minimum value of a functional $T: \mathcal{V} \rightarrow \mathbb{R}$.
To quantify the time of descent, $T$, we need to perform the integral

$$T(y) = \int \mathrm{d}t,$$

where $\mathrm{d}t$ is a minute timestep. We can calculate $\mathrm{d}t$ as

$$\mathrm{d}t = \frac{\mathrm{d}s}{v}.$$

It appears as though we have added more problems for ourselves! However, we can apply the conservation of energy to find v, as shown below,

$$mg \Delta h = \frac{1}{2}mv^2,$$

$$v = \sqrt{2g \Delta h}.$$

From our definitions of the problem parameters, i.e. the start and end points of the slope,

$$\implies \Delta h = -y,$$

$$\therefore v = \sqrt{-2gy}.$$

The next piece of the puzzle is to determine $\mathrm{d}s$, but this is just an infinitesimal increment of the arc length, and so can be given by the standard formula,

$$\mathrm{d}s = \sqrt{1 + y'^2}\mathrm{d}x.$$

This gives us the final formula for $T$,

$$T(y) = \int \frac{\sqrt{1 + y'^2}}{\sqrt{-2gy}}\; \mathrm{d}x.$$

## Functional Differentiation

What we really wish to aquire is $\nabla _y T$ and set it equal to 0 for the minimum $T$. To do this, we utilise a concept from matrix calculus,

$$\mathrm{d}f = \nabla f(x) \cdot \mathrm{d}x.$$

and we generalise the inner/dot product to the Hilbert space of functions. We define the inner product of $u,v \in \mathcal{V}$ to be,

$$\langle u,v \rangle = \int uv\; \mathrm{d}x.$$

Now, let us use this in calculating $\nabla _y T$,

$$\mathrm{d}f = \int \left{ \frac{\sqrt{1 + \left[(y + \mathrm{d}y)' \right]^2}}{\sqrt{-2g(y+\mathrm{d}y)}} - \frac{\sqrt{1 + y'^2}}{\sqrt{-2gy}} \right}\; \mathrm{d}x$$