---
title: Math Notes
tags: [Math, Notes]
date: 2019-07-07 19:43:00
categories: 科研 / Research
mathjax: true
---

Here I'd like to take some time for my math notebook so that I wouldn't learn and forget definitions or theorems again and again :laughing:.

<!-- more -->

## Lipschitz continuous

Given two metric space $(X, d_X)$ and $(Y, dY)$. Given function $f:X\rightarrow Y$, if there exist a real constant $K\geq 0$ such that for all $x_1, x_2$ in $X$,
$$
d_Y(f(x_1)f(x_2))\leq Kd_X(x_1,x_2)
$$
Then $f$ is called Lipschitz continuous.

In particular, for real valued function $f: \mathbb{R}\rightarrow\mathbb{R}$ is called Lipschitz continuous if
$$
|f(x_1)-f(x_2)|\leq K|x_1-x_2|
$$
Apparently, Lipschitz continuous is stricter than uniform continuity.

## Parseval's identity

The identity asserts that, the sum of the squares of the Fourier coefficients of a function is equal to the integral of the square of the function
$$
\sum _{n=-\infty}^{\infty}|c_{n}|^2={\frac{1}{2\pi}}\int_{-\pi}^{\pi}|f(x)|^{2}\,dx
$$
where the Fourier coefficients $c_n$ of $f$ are given by
$$
c_{n}={\frac {1}{2\pi }}\int _{-\pi }^{\pi }f(x)\mathrm {e} ^{-inx}\,dx
$$

## 