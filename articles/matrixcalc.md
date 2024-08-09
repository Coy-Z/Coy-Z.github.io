---
layout: default
title: Matrix Calculus
permalink: /articles/matrixcalc/
---

# Matrix Calculus

In this article, I do not use any specifying notation for vectors for sake of generality.

## Introduction to Differentials and Linearisation

We all know the formula of derivatives,

$$f'(x) = \frac{\mathrm{d}f}{\mathrm{d}x},$$

and we are taught that $f'(x)$ represents the localised gradient of a point on a curve.
However, this idea is more difficult to generalise into higher order $x$ such as vectors, matrices and tensors.
Instead, we should consider that the derivative is really a linearisation of a function, and we can show this using the Taylor series expansion,

$$f(x + \delta x) = f(x) + f'(x)\delta x + \frac{f''(x)}{2}\delta x^2 + ...$$

Linearising the curve means we discard terms $\mathcal{O}(\mid \delta x \mid^2)$ and for $\lim_{\delta x \rightarrow 0}$ (small perturbations), this is a logical move.
Therefore, we are left with the resulting approximation,

$$f(x + \delta x) \approx f(x) + f'(x)\delta x.$$

In essence, the reason we refer to this as linearisation since we have effectively computed the function which is tangent to $f$ at $x$. This idea is key, since we can generalise this to more complicated objects, e.g. a surface $f$ is linearised to a plane.
The approximation above becomes an equality as $\lim_{\delta x \rightarrow 0}$, in which case the $\delta x$ becomes a differential $\mathrm{d}x$,

$$f(x + \mathrm{d}x) = f(x) + f'(x)\mathrm{d}x.$$

We can rearrange the equation to give,

$$f(x + \mathrm{d}x) - f(x) = f'(x)\mathrm{d}x,$$

and we can represent $f(x + \mathrm{d}x)$ as $f + \mathrm{d}f$, which gives,

$$\mathrm{d}f = f'(x)\mathrm{d}x.$$

We can recognise that this is effectively "multiplying up" the $\mathrm{d}x$ on both sides of our standard form for the single-variable derivative formula.
Now, it is immediately apparent that this form of the derivative is far more generalised, because $\mathrm{d}x$ is not limited to $\mathbb{R}$. The above formula holds some genuine meaning in that $\mathrm{d}f$ represents a small output perturbation and $\mathrm{d}x$ a small input perturbation.

## The Jacobian

We call $f'(x)$ the **Jacobian**. The Jacobian gives the linear relationship between input and output perturbations, which is more accurate the smaller the perturbations, since the $\mathcal{O}(\mid \delta x \mid ^2)$ terms become more and more negligible with respect to the first order.

Take, for example, some function $f$ such that,

$$f : \mathbb{R}^n \rightarrow \mathbb{R}^m,$$

i.e. $f$ is an m-vector and $x$ an n-vector. In this case, for the derivative formula to be satisfied, we require

$$f'(x) \in \mathbb{R}^{m \times n},$$

and so in this example, $f'(x)$ is a matrix. But how can we construct a Jacobian matrix? We shall consult the total differential form relationship listed below, we use the same $f$ as above,

$$\mathrm{d}f_i = \frac{\partial f_i}{\partial x^j} \mathrm{d}x_j.$$

Here, we have used Einstein summation notation. Converting this expression into a matrix-vector multiplication, we get

$$\begin{pmatrix} \mathrm{d}f_1 \\ \vdots \\ \mathrm{d}f_m \end{pmatrix} = \begin{pmatrix} \frac{\partial f_1}{\partial x^1} & \dots & \frac{\partial f_1}{\partial x^n} \\ \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x^1} & \dots & \frac{\partial f_m}{\partial x^n} \end{pmatrix} \begin{pmatrix} \mathrm{d}x_1 \\ \vdots \\ \mathrm{d}x_n \end{pmatrix}.$$

And so we can define the Jacobian matrix,

$$f'(x) = \begin{pmatrix} \frac{\partial f_1}{\partial x^1} & \dots & \frac{\partial f_1}{\partial x^n} \\ \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x^1} & \dots & \frac{\partial f_m}{\partial x^n} \end{pmatrix}.$$

To reinforce this idea, we will observe a very trivial example. This should also briefly introduce our approach to taking derivatives in matrix calculus. We define $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$ such that,

$$f(x) = Ax,$$

where $A$ is a constant matrix. Starting from first principles,

$$f'(x) \mathrm{d}x = \mathrm{d}f = f(x + \mathrm{d}x) - f(x).$$

Next we substitute the function $f$ into the equation,

$$f'(x) \mathrm{d}x = A(x + \mathrm{d}x) - Ax.$$

Since matrix multiplication is distributive,

$$f'(x) \mathrm{d}x = A \mathrm{d}x,$$

$$f'(x) = A.$$

We have found the Jacobian matrix, but let us check it with our partial derivative construction,

$$\mathrm{d}f_i = \frac{\partial f_i}{\partial x^j} \mathrm{d}x_j.$$

From the definition of the function $f$, we know that,

$$f_i = A_{ij}x_j,$$

and so,

$$\frac{\partial f_i}{\partial x^j} = A_{ij},$$

$$\therefore f'(x)_{ij} = A_{ij} \implies f'(x) = A,$$

which agrees with the above.

## Loss Functions and Grad

Let us consider another example where $f : \mathbb{R}^n \rightarrow \mathbb{R}$. We call this kind of scalar function a **Loss**/**Cost** function in machine learning, since it takes in many parameters and returns a scalar that quantifies some sort of loss or cost.
$$\mathrm{d}f = f'(x)\mathrm{d}x$$ tells us that $f'(x)$ must be a row-vector/covector. Using vector notation we can say,

$$\mathrm{d}f = f'(x)^T \cdot \mathrm{d}x.$$

From the equation for the total derivative, we can recall that for some scalar field $f : \mathbb{R}^n \rightarrow \mathbb{R}$ (using Einstein summation convention),

$$\mathrm{d}f = \frac{\partial f}{\partial x^i} \mathrm{d}x_i = \nabla f \cdot \mathrm{d}x.$$

Comparing the two equations above,

$$ \nabla f = f'(x)^T .$$

Establishing the grad operator here allows us to extend grad to virtually all Hilbert spaces (vector spaces with a defined inner product).

## Brief Interlude on Linear Operators

A linear operator is any operator $L: \mathcal{U} \rightarrow \mathcal{V}$ that satisfies the following equation,

$$L(\alpha x + \beta y) = \alpha L(x) + \beta L(y),$$

where $x, y \in \mathcal{U}$ and $\alpha , \beta \in \mathbb{R}$. As a generic example, we can take $L: \mathbb{R}^n \rightarrow \mathbb{R}^m$ such that,

$$L(x) = Ax$$

for a constant $A \in \mathbb{R}^{m \times n}$. From matrix multiplication rules, we can quickly see that,

$$A(\alpha x + \beta y) = \alpha Ax + \beta Ay,$$

because matrix multiplication is distributive and multiplication by scalars is both associative and commutative.
In a sense, this demonstration is mildly cyclic since matrix multiplication is defined in such a way to satisfy the criteria of linearity, given it represents a linear transformation.

## The Derivative as a Linear Operator

Let us play with an example,

$$f(X) = X^2.$$

Through this example, I hope to further establish the first principles for taking the derivative of a matrix function, as well as illustrating the derivative as a linear operator.

From first principles,

$$f'(X)\mathrm{d}X = \mathrm{d}f = f(X + \mathrm{d}X) - f(X).$$

Substitute our $f$ into the equation,

$$f'(X)\mathrm{d}X = (X + \mathrm{d}X)^2 - X^2,$$

$$f'(X)\mathrm{d}X = X^2 + X \mathrm{d}X + \mathrm{d}X X + \mathrm{d}X^2 - X^2.$$

In expanding, care must be taken to preserve the order of matrix multiplication since it is a non-commutative operation. We can now discard the non-linear terms, i.e. $\mathcal{O}(\mathrm{d}X^2)$,

$$f'(X)\mathrm{d}X = X \mathrm{d}X + \mathrm{d}X X.$$

On the surface, it may appear as if we are in trouble! How are we going to represent $f'(x)$ as a matrix? In short, we cannot and instead we will define $f'(x)$ as a linear operator, such that

$$f'(X)[\mathrm{d}X] = X \mathrm{d}X + \mathrm{d}X X.$$

This subtle change in notation allows us to differentiate a far greater set of matrix functions. The formal name for this is the Fréchet derivative.

## Vectorising Matrices

One may recognise that an $m \times n$ matrix is isomorphic to an $mn$-vector, and indeed, there is a linear operation for the aforementioned matrix to vector map. We call this the vectorising function, and with its aid, we can form Jacobian matrices in cases where previously we had to settle for linear operators. Let us define,

$$\mathrm{vec} : \mathbb{R}^{m \times n} \rightarrow \mathbb{R}^{mn},$$

such that the column vectors within the matrix are stacked on top of eachother, i.e.

<!--$$\mathrm{vec}\begin{pmatrix} a_{11} & \dots & a_{1n} \\ \vdots & \ddots & \vdots \\ a_{m1} & \dots & a_{mn} \end{pmatrix} = \begin{pmatrix} a_{11} \\ \vdots \\ a_{m1} \\ a_{12} \\ \vdots \\ a_{m2} \\ \vdots \\ a_{1n} \\ \vdots \\ a_{mn} \end{pmatrix}.$$-->

$$\mathrm{vec}\begin{pmatrix} \uparrow & \dots & \uparrow \\ u_1 & \dots & u_n \\ \downarrow & \dots & \downarrow \end{pmatrix} = \begin{pmatrix} \uparrow \\ u_1 \\ \downarrow \\ \vdots \\ \uparrow \\ u_n \\ \downarrow \end{pmatrix}.$$

where $u_i$ represents the $i$-th column vector in the matrix. Using this new vec operator, we can actually construct a Jacobian matrix from the function $f(X) = X^2$.
Let us take a $2 \times 2$ matrix $A$, such that

$$A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix},$$

and we match to it some small perturbation,

$$\mathrm{d}A = \begin{pmatrix} \mathrm{d}a_{11} & \mathrm{d}a_{12} \\ \mathrm{d}a_{21} & \mathrm{d}a_{22} \end{pmatrix}.$$

We shall observe the example of using $f(X) = X^2$,

$$A^2 = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}^2 = \begin{pmatrix} a_{11}^2 + a_{12}a_{21} & a_{12}(a_{11}+a_{22}) \\ a_{21}(a_{11} + a_{22}) & a_{22}^2 + a_{12}a_{21} \end{pmatrix},$$

$$(A+\mathrm{d}A)^2 = \begin{pmatrix} a_{11} + \mathrm{d}a_{11} & a_{12} + \mathrm{d}a_{12} \\ a_{21} + \mathrm{d}a_{21} & a_{22} + \mathrm{d}a_{22} \end{pmatrix}^2.$$

Here, we skip some steps and give the final result (omitted steps left as an exercise for the reader... the exercise can be approached by matrix algebra or by differentiating the elements of the matrix).

$$\mathrm{d}A^2 = (A+\mathrm{d}A)^2 - A^2$$

$$ = \begin{pmatrix} 2a_{11}\mathrm{d}a_{11} + a_{12}\mathrm{d}a_{21} + a_{21}\mathrm{d}a_{12} & (a_{11} + a_{22})\mathrm{d}a_{12} + a_{12}(\mathrm{d}a_{11} + \mathrm{d}a_{22}) \\ (a_{11} + a_{22})\mathrm{d}a_{21} + a_{21}(\mathrm{d}a_{11} + \mathrm{d}a_{22})& 2a_{22}\mathrm{d}a_{22} + a_{12}\mathrm{d}a_{21} + a_{21}\mathrm{d}a_12 \end{pmatrix}.$$

We vectorise this matrix into,

$$\mathrm{vec}(\mathrm{d}A^2) = \begin{pmatrix} 2a_{11}\mathrm{d}a_{11} + a_{12}\mathrm{d}a_{21} + a_{21}\mathrm{d}a_{12} \\ (a_{11} + a_{22})\mathrm{d}a_{21} + a_{21}(\mathrm{d}a_{11} + \mathrm{d}a_{22}) \\ (a_{11} + a_{22})\mathrm{d}a_{12} + a_{12}(\mathrm{d}a_{11} + \mathrm{d}a_{22}) \\ 2a_{22}\mathrm{d}a_{22} + a_{12}\mathrm{d}a_{21} + a_{21}\mathrm{d}a_12 \end{pmatrix}.$$

Now, it is handy to realise that this can be expressed as,

$$\mathrm{vec}(\mathrm{d}A^2) = \begin{pmatrix} 2a_{11} & a_{12} & a_{21} & 0 \\ a_{21} & a_{11} + a_{22} & 0 & a_{21} \\ a_{12} & 0 & a_{11} + a_{22} & a_{12} \\ 0 & a_{12} & a_{21} & 2a_{22} \end{pmatrix} \mathrm{vec}(\mathrm{d}A),$$

and hence, we have acquired an expression for the Jacobian! 

N.B. The vectorization approach should be used with care, as it encourages an element-centric mindset towards matrices, which often is not the best way to consider matrices.

## Deriving General Differentiation Rules

In regular scalar calculus, we are able to achieve such lengths in differentiation due to various rules that can be proved for general holomorphic functions. These rules are then rendered a toolkit for evaluating derivatives of greater complexity. In this section, we look at extending these rules into matrix calculus, alongside some matrix-specific rules. You should expect to notice that all of these rules are valid when we take $1 \times 1$ matrices, i.e. scalars.
### Sum Rule

Let is begin with $f(x) = g(x) + h(x)$ where $f,g$ and $h$ take matrix input and outputs. Starting from first principles,

$$\mathrm{d}f = f(x + \mathrm{d}x) - f(x) = g(x + \mathrm{d}x) + h(x + \mathrm{d}x) - g(x) - h(x).$$

Matrix addition is commutative, so the sum on the right hand side can be trivially rearranged,

$$\mathrm{d}f = g(x + \mathrm{d}x) - g(x) + h(x + \mathrm{d}x) - h(x),$$

$$\therefore \mathrm{d}(g+h) = \mathrm{d}g + \mathrm{d}h.$$

### Product Rule

For the product rule, let $f(x) = g(x)h(x)$, where $f,g$ and $h$ are defined similarly. Adopting the same approach,

$$\mathrm{d}f = (f + \mathrm{d}f) - f = (g+\mathrm{d}g)(h+\mathrm{d}h) - gh.$$

The key is to preserve the order of matrix multiplication. Expanding the above equation and discarding second-order terms, we acquire

$$\mathrm{d}f = g\mathrm{d}h + \mathrm{d}gh.$$

$$\therefore \mathrm{d}(gh) = g\mathrm{d}h + \mathrm{d}gh.$$

### Chain Rule

To tackle the chain rule, we define $f(x) = h(g(x))$, such that $g$ acts on $x$ first, then followed by $h$. To cement this, we could apply an example (however the proof below is general beyond the example). Let $x \in \mathbb{R}^n$, $g: \mathbb{R}^n \rightarrow \mathbb{R}^m$, $h: \mathbb{R}^m \rightarrow \mathbb{R}^k$ and $f: \mathbb{R}^n \rightarrow \mathbb{R}^k$.

$$\mathrm{d}f = h(g(x+\mathrm{d}x)) - h(g(x)),$$

$$\mathrm{d}f = h(g+\mathrm{d}g) - h(g(x)).$$

The observation we must make here is that $\mathrm{d}g = g'(x)\mathrm{d}x$ is still an infinitesimal. The way to consider the following step is to think of $h'(g(x))$ as the derivative of $h$ evaluated at a point $g(x)$ in $g$-space.

$$\mathrm{d}f = h(g(x)) + h'(g(x))\mathrm{d}g - h(g(x)) = h'(g(x))g'(x)\mathrm{d}x.$$

$$\therefore f'(x) = h'(g(x))g'(x).$$

The example at the start of this section was not chosen blindly. It illustrates the composition of several vector-to-vector functions. You will notice, $h'(g(x))$ is just the Jacobian of $h$ evaluated at $g(x)$, and $g'(x)$ is just the Jacobian of $g$ evaluated at $x$. In short, the chain rule for vector-to-vector functions is simply the product of Jacobians. Computationally, when chains and vectors get long, it makes a massive difference which way we perform the matrix multiplication (left-to-right or right-to-left). We will discuss this in much further depth later on in this article.

### Inverse Rule

This rule is obviously a matrix specific rule, or is it? We will see. Let $f(X) = X^{-1}$, where $X$ is a matrix. We will employ a trick to evaluate this derivative.

$$X X^{-1} = I,$$

where $I$ is the identity matrix. This is a constant matrix, and so will have a derivative of $0$.

$$\implies \mathrm{d}(XX^{-1}) = 0.$$

Applying the product rule,

$$X\mathrm{d}X^{-1} + \mathrm{d}XX^{-1} = 0,$$

$$X\mathrm{d}X^{-1} = -\mathrm{d}XX^{-1},$$

$$\therefore \mathrm{d}X^{-1} = -X^{-1}\mathrm{d}XX^{-1}.$$

So let's see if it really is matrix specific. Suppose $X$ were a scalar, the scalar identity is just 1 and so $X^{-1}$ is just the reciprocal of $X$, so

$$\mathrm{d}X^{-1} = -X^{-1}\mathrm{d}XX^{-1} = -\frac{\mathrm{d}X}{X^2},$$

and

$$\frac{\mathrm{d}X^{-1}}{\mathrm{d}X} = -\frac{1}{X^2},$$

which is the expected result.

# Defining an Inner Product and Norm

To define an inner product, we will make use of the matrix-vector isomorphism. Specifically, the spaces of $R^{m\times n}$ and $R^{mn}$ via the vectorising function. For the vectors formed by vectorising matrices $A$ and $B$,

$$\mathrm{vec}A \cdot \mathrm{vec}B = (\mathrm{vec}A)^T\mathrm{vec}B.$$

But, without using the vectorising function,

$$(\mathrm{vec}A)^T\mathrm{vec}B = A_{ij}B_{ij} = \mathrm{tr}(A^TB).$$

The most obvious generalisation is to say $\langle A, B \rangle = \mathrm{vec}A \cdot \mathrm{vec}B$. This is called the Frobenius Inner Product, and is defined,

$$\langle A, B \rangle = \mathrm{tr}(A^TB) = A_{ij}B_{ij}.$$

In essence, this is just multiplying corresponding elements from $A$ and $B$, then summing the products, which is again very intuitive. A vector space with a defined inner product is formally known as a **Hilbert** space.

Following on from the inner product, in vectors, we can define the norm of a vector as its length, which is given by

$$|\vec{a}| = \sqrt{a_i^2} = \sqrt{\vec{a} \cdot \vec{a}}.$$

Again, we make the obvious generalisation and define the Frobenius Norm (also known as the 2-norm) as,

$$|A| = \sqrt{\langle A, A \rangle} = \sqrt{\mathrm{tr}(A^TA)} = \sqrt{A_{ij}^2}.$$

A vector space with a defined norm is formally known as a **Banal** space. Note, in our chosen definition, the two spaces come together, but this is not generally true. Therefore, it is important to make the distinction here.