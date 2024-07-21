---
layout: default
title: Matrix Calculus
permalink: /articles/matrixcalc/
---

# Matrix Calculus

## Introduction to Differentials and Linearisation

We all know the formula of derivatives,

$$f'(x) = \frac{\mathrm{d}f}{\mathrm{d}x},$$

and we are taught that $f'(x)$ represents the localised gradient of a point on a curve.
However, this idea is more difficult to generalise into higher order $x$ such as vectors, matrices and tensors.
Instead, we should consider that the derivative is really a linearisation of a function, and we can show this using the Taylor series expansion,

$$f(x + \delta x) = f(x) + f'(x)\delta x + \frac{f''(x)}{2}\delta x^2 + ...$$

Linearising the curve means we discard terms $\mathcal{O}(\delta x^2)$ and for $\lim_{\delta x \rightarrow 0}$, this is a logical move.
And so, we are left with the resulting approximation,

$$f(x + \delta x) \approx f(x) + f'(x)\delta x.$$

In essence, the reason we refer to this as linearisation since we have effectively computed the function which is tangent to $f$ at $x$. This idea is key, since we can generalise this to more complicated objects, e.g. a surface $f$ is linearised to a plane.
The approximation above becomes an equality as $\lim_{\delta x \rightarrow 0}$, in which case the $\delta x$ becomes a differential $\mathrm{d}x$,

$$f(x + \mathrm{d}x) = f(x) + f'(x)\mathrm{d}x.$$

We can rearrange the equation to give,

$$f(x + \mathrm{d}x) - f(x) = f'(x)\mathrm{d}x,$$

and we can represent $f(x + \mathrm{d}x)$ as $f + \mathrm{d}f$, which gives,

$$\mathrm{d}f = f'(x)\mathrm{d}x.$$

We can recognise that this is effectively ``multiplying up" the $\mathrm{d}x$ on both sides of our standard form for the single-variable derivative formula.
Now, it is immediately apparent that this form of the derivative is far more generalised, because $\mathrm{d}x$ is not limited to $\mathbb{R}$.

We call $f'(x)$ the **Jacobian**.

Take, for example, some function $f$ such that,

$$f : \mathbb{R}^n \rightarrow \mathbb{R}^m,$$

i.e. $f$ is an m-vector and $x$ an n-vector. In this case, for the derivative formula to be satisfied, we require

$$f'(x) \in \mathbb{R}^{m \times n},$$

and so in this example, $f'(x)$ is a matrix.