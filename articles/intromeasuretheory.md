---
layout: default
title: Introduction to Measure Theory
permalink: /articles/intromeasuretheory/
---

# An Introduction to Measure Theory -- With a focus on Probability

Measure theory is a branch of mathematics that generalizes the intuitive notions of length, area, and volume to more abstract settings. It provides a rigorous framework for defining and working with measures, which are functions that assign a "size" or "weight" to subsets of a given space. These measures can represent various quantities like length, area, volume, probability, or even "mass" in a generalized sense. We shall approach it with a probabilistic lens in this article.

We formally define probability distributions with a probability *ensemble* or *triple*,

$$\left( \Omega, \mathcal{F}, \mu \right).$$

In the above, $\Omega$ is the sample space: the set of all possible outcomes. $\mathcal{F}$ is the sigma-algebra ($\sigma$-algebra): a collection of subsets of $\Omega$ (events) that are "measurable". $\mu$ is the probability measure (generalisation of a distribution). What does all of this really mean though?

## What is a $\sigma$-algebra?

The $\sigma$-algebra $\mathcal{F}$ over a set $\Omega$ is a collection of subsets of $\Omega$ satisfying:

1. Contains the whole set: $\Omega \in \mathcal{F}$.
2. Closed under complement: $\mathcal{A} \in \mathcal{F} \implies \Omega \ \mathcal{A} \in \mathcal{F}$.
3. Closed under countable unions: $\mathcal{A}_i \in \mathcal{F} \implies \bigcup _i \mathcal{A}_i \in \mathcal{F}$.

By De Morgan's laws, this also implies it is closed under countable intersections.

*Proof* D.M. states $\bar{\mathcal{A}} \cap \bar{\mathcal{B}} = \bar{\mathcal{A} \cap \mathcal{B}}$, where we define the complement $\bar{\mathcal{A}} \identity \Omega / \mathcal{A}$.
