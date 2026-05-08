---
title: Recreational Multiplication
date: 2026-05-08 12:30:00 +0530
categories: [math]
tags: [math-for-fun]
author: 
description: Proving that exp(x) exp(y) = exp(x+y)
math: true
---
Define the exponential function 

$$
\exp(x) := 1 + x + \frac{x^2}{2!} + \cdots = \sum_{k=0}^{\infty} \frac{x^k}{k!}
$$

Now our goal is to show that $$\exp(x+y) = \exp(x) \exp(y)$$. First we will show the easier $$\exp(2x) = \exp(x)\exp(x)$$.

$$
\exp(x) \exp(x) = \sum_{p=0}^{\infty} \frac{x^p}{p!} \sum_{q=0}^{\infty} \frac{x^q}{q!}
= \sum_{p, \ q \geq 0} \frac{x^p x^q}{p! q!}
$$

Now to find the coefficient of $x^k$, set $p + q = k$. Then

$$
\begin{align*}
    [x^k] &= \sum_{p + q = k} \frac{1}{p! q!} \\
          &= \frac{1}{0! \, k!} + \frac{1}{1! \, (k-1)!} + \dots + \frac{1}{k! \, 0!} \\
          &= \frac{1}{k!} \sum_{p=0}^{k} \binom{k}{p} \\
          &= \frac{2^k}{k!}
\end{align*}
$$

Aha! The coefficient of $$x^k$$ is $$\frac{2^k}{k!}$$, so the $k$-th term is given by $$\frac{(2x)^k}{k!}$$, as desired.

Now that we have a taste for this specific case, let us move on to the general one.


$$
\exp(x) \exp(y) = \sum_{p=0}^{\infty} \frac{x^p}{p!} \sum_{q=0}^{\infty} \frac{y^q}{q!}
= \sum_{p, \ q \geq 0} \frac{x^p y^q}{p! q!}
$$

Now set $$p + q = k$$ and summing over all $$k$$ is the same as the above sum

$$
\begin{align*}
    \exp(x) \exp(y) &= \sum_{k=0}^{\infty} \sum_{p + q = k} \frac{x^p y^q}{p! q!} \\
                    &= \sum_{k=0}^{\infty} \sum_{p=0}^k \frac{x^p y^{k-p}}{p! (k-p)!} \\
                    &= \sum_{k=0}^{\infty} \frac{1}{k!} \sum_{p=0}^k \binom{k}{p} x^p y^{k-p} \\
                    &= \sum_{k=0}^{\infty} \frac{1}{k!} (x+y)^k \text{(binomial theorem)} \\
                    &= \sum_{k=0}^{\infty} \frac{(x+y)^k}{k!} \\
                    &= \exp(x+y) \quad \blacksquare
\end{align*}
$$

And so we are done!

Exercise left to the reader: now prove the formula for $$\sin(x+y)$$... ;)