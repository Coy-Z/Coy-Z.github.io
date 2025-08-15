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
2. Closed under complement: $\mathcal{A} \in \mathcal{F} \implies \Omega \backslash \mathcal{A} \in \mathcal{F}$.
3. Closed under countable unions: $\mathcal{A}_i \in \mathcal{F} \implies \bigcup _i \mathcal{A}_i \in \mathcal{F}$.

By De Morgan's Law, this also implies it is closed under countable intersections.

*Proof*    De Morgan's law states that $\bar{\mathcal{A}} \cap \bar{\mathcal{B}} = \bar{\mathcal{A} \cap \mathcal{B}}$, where we define the complement $\bar{\mathcal{A}} \equiv \Omega \backslash \mathcal{A}$.

By the closed under countable unions condition,

$$
\{ \mathcal{A}_i \in \mathcal{F} \} \implies \bigcup _i \mathcal{A}_i \in \mathcal{F}.
$$

By the closed under complement condition,

$$
\Omega \ \bigcup _i \mathcal{A}_i \in \mathcal{F}
$$

By De Morgan's Law,

$$
\bigcap _i \left( \Omega \backslash \mathcal{A}_i \right) \in \mathcal{F}
$$

Let $\mathcal{B}_i \equiv \Omega \backslasn \mathcal{A}_i$, and apply the closed under complement condition,

$$
\mathcal{A}_i \in \mathcal{F} \implies \mathcal{B}_i \in \mathcal{F},\\
\therefore \mathcal{B}_i \in \mathcal{F} \implies \bigcap _i \mathcal{B}_i \in \mathcal{F}.\
\square$$

A way of gaining intuition for the $\sigma$-algebra is via a game of coin toss. Let us toss the coin twice, with $H, T$ representing heads and tails respectively. Say we only care about the number of heads (i.e. combinations rather than permutations), then our probability distribution $\left( \Omega, \mathcal{F}, \mu \right)$ is characterised as follows,

$$
\Omega = \{TT, TH, HT, HH \}, \mathcal{F} = \{ TT, TH, HH \}
$$

and

$$
\mu(X) = \begin{cases} 
      0.25 & X = TT \\
      0.5 & X = TH \\
      0.25 & X = HH 
   \end{cases}.
$$

In the case where we do indeed care about permutations, we get $\mathcal{F} = \{ TT, TH, HT, HH \}$, which is called the Borel $\sigma$-algebra, defined to be the smallest σ-algebra containing all open sets of $\Omega$.

## What is a measure?

A measure is a function that assigns a non-negative number to subsets of a set, generalizing the notion of length, are, volume, mass and probability.

Given a measurable (Borel) space $\left( \Omega, \mathcal{F} \right)$ (sample space, $\sigma$-algebra), a measure, $\mu$, is defined as

$$
\mu : \Omega \rightarrow \left[0, \infty \right].
$$

Take note that the infinity is bounded. This is a subtle but important point to be clarified later. The measure must satisfy the following two conditions,
1. $$ \mu\left( \emptyset \right) = 0 $$.
2. $$ \mu\left( \bigcup _i \mathcal{A}_i \right) = \sum _i \mu\left( \mathcal{A}_i \right) \forall \, \mathrm{disjoint} \, \mathcal{A}_i \in \mathcal{F} $$.

For probability measures, there are further more stringent conditions, namely the Kolmogorov axioms, that must be satisfied.

3. $$\mu\left( \Omega \right) = 1 $$.
4. $$\mu\left( \Omega \right) \in \left[ 0, 1 \right] $$.
5. $$\mathcal{A} \subseteq \mathcal{B} \implies \mu\left( \mathcal{A} \right) \leq \mu\left( \mathcal{B} \right) $$.

## Integration Theory

![Integration](/files/riemann_lebesgue.jpg)
*Figure 1: A comparison of Riemann vs Lebesgue integration.*

Two methods of integration are illustrated above, with Riemann integration on the left and Lesbegue integration on the right. Lebesgue compares the two succintly,

*"I have to pay a certain sum, which I have collected in my pocket. I take the bills and coins out of my pocket and give them to the creditor in the order I find them until I have reached the total sum. This is the Riemann integral. But I can proceed differently. After I have taken all the money out of my pocket I order the bills and coins according to identical values and then I pay the several heaps one after the other to the creditor. This is my integral."*

We are used to taking the Riemann integral, since this works well with the notion of the integral being the anti-derivative. However, the Riemann integral breaks down for functions that are discontinuous almost everywhere, and does not generally permit taking limits under the integral sign. Lebesgue addresses this using the notion of simple functions and measures.

A simple function, $\varphi$, is a measurable function that takes only finitely many values, i.e.

$$
\varphi = \sum _{i = 1}^n a_i \mathbb{1}_{\mathcal{A}_i}\left( x \right),
$$

where $a_i \geq 0$ and $mathcal{A}_i \in \mathcal{F}$ are disjoint sets that span the sample space and $\mathbb{1}_{\mathcal{A}_i}(\dot)$ is the indicator function for the set $\mathcal{A}_i$.
Following this concept, we define its integral as,

$$
\int _\mathcal{A} \varphi \mathrm{d} \mu = \sum _{i = 1}^n a_i \mu\left( \mathcal{A}_i \right) 
$$

such that $\{ \mathcal{A}_i \}$ are disjoint and $\bigcup _i \mathcal{A}_i = \mathcal{A}$.

N.B. *Every* measurable, non-negative function can be approximated by simple functions. There is a subtle point in the non-negativity that relates back to the previous bounded infinity, which we dive into next.

### The Lebesgue Integral