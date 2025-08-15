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

By De Morgan's Law, this also implies it is closed under countable intersections.

*Proof*    De Morgan's law states that $\bar{\mathcal{A}} \cap \bar{\mathcal{B}} = \bar{\mathcal{A} \cap \mathcal{B}}$, where we define the complement $\bar{\mathcal{A}} \equiv \Omega / \mathcal{A}$.

By the closed under countable unions condition,
$$
\left{ \mathcal{A}_i \in \mathcal{F} \right} \implies \bigcup _i \mathcal{A}_i \in \mathcal{F}.
$$
By the closed under complement condition,
$$
\Omega \ \bigcup _i \mathcal{A}_i \in \mathcal{F}
$$
By De Morgan's Law,
$$
\bigcap _i \left( \Omega \ \mathcal{A}_i \right) \in \mathcal{F}
$$
Let $\mathcal{B}_i \equiv \Omega \ \mathcal{A}_i$, and apply the closed under complement condition,
$$
$\mathcal{A}_i \in \mathcal{F} \implies \mathcal{B}_i \in \mathcal{F}$
$$
$$
\therefore \mathcal{B}_i \in \mathcal{F} \implies \bigcap _i \mathcal{B}_i \in \mathcal{F}.
$$
$$\qed$$

## What is a measure?

A measure is a function that assigns a non-negative number to subsets of a set, generalizing the notion of length, are, volume, mass and probability.

Given a measurable (Borel) space $\left( \Omega, \mathcal{F} \right)$ (sample space, $\sigma$-algebra), a measure, $\mu$, is defined as

$$
\mu : \Omega \rightarrow \left[0, \infty \right].
$$

Take note that the infinity is bounded. This is a subtle but important point to be clarified later. The measure must satisfy the following two conditions,

1. $$ \mu\left( \empty \right) = 0 $$.
2. $$ \mu\left( \bigcup _i \mathcal{A}_i \right) = \sum _i \mu\left( \mathcal{A}_i \right) \forall \mathtext{disjoint} \mathcal{A}_i \in \mathcal{F} $$.

For probability measures, there are further more stringent conditions, namely the Kolmogorov axioms, that must be satisfied.

3. $$\mu\left( \Omega \right) = 1 $$.
4. $$\mu\left( \Omega \right) \in \left[ 0, 1 \right] $$.
5. $$\mathcal{A} \subset \mathcal{B} \implies \mu\left( \mathcal{A} \right) \leq \mu\left( \mathcal{B} \right) $$.