---
sidebar_label: Tutorial 1
sidebar_position: 1
---

# Tutorial 1

:::info
Pending changes
:::

## Problem 1 - Moore-Penrose Pseudoinverse

Recall that the pseudoinverse $X^+=(X^\intercal X)^{-1}X^\intercal$ appears as part of the analytic solution of linear regression. In this problem, we will explore some of the properties of this pseudoinverse.

### Problem 1.1

Let $X\in\mathbb{R}^{N\times D}$ and assume $X^\intercal X$ is nonsingular.

1. Show that $X^+X=I$.

    We use the definition of the Moore-Penrose Psuedoinverse: $X^+=(X^\intercal X)^{-1}X^\intercal$. Thus,

    $$
    \begin{align*}
    X^+X 
    &= (X^\intercal X)^{-1}X^\intercal X \\
    &= (X^\intercal X)^{-1}(X^\intercal X) \\
    &= I
    \end{align*}
    $$

    The final step follows the definition of a matrix inverse, $XX^\intercal = X^\intercal X = I$, and thus $(X^\intercal X)^{-1}(X^\intercal X) = I$.


2. What is the dimension of $I$?

    Suppose that $X$ has dimension $m\times n$. We know that $X^\intercal$ has dimension $n\times m$ and thus, $X^\intercal X$ has dimension $n \times n$.

    Therefore, $I=(X^\intercal X)^{-1}(X^\intercal X)$ has the dimension of $X^\intercal X$, which is $n \times n$, or equivalent to a square matrix with the number of columns in $X$.

### Problem 1.2

The pseudoinverse $X^+=(X^\top X)^{-1}X^\top$ is also known as a left-inverse.

1. Why do we call $X^+$ a left-inverse?

    Recall that in your linear algebra class, matrices $X$ and $Y$ has two different multiplication operations. If we **left-multiply** $X$ to $Y$, then we would obtain $XY$. Similarly, if we **right-multiply** $Y$ to $X$, then we would obtain $YX$. Note that $XY$ may not be equal to $YX$.

    Thus, we establish a similar convention here. $X^+$ is a left-inverse, since if we left-multiply $X^+$ to $X$, $X^+X=I$. However, $XX^+$ may not be equal to $I$.

2. What is a natural way to define a right-inverse (what do you need to assume with that definition)?

    A natural way of defining this, would be to establish the right-inverse $A^+$ such that when we **right-multiply** $A^+$ onto $A$, we would obtain $AA^+=I$.
    
    Thus, we just have to switch the orders, to obtain $A^+ = A^\intercal(AA^\intercal)^{-1}$.

    (Follow up: can you show why this is a correct right-inverse?)

### Problem 1.3



