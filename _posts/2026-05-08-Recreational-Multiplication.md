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

From this definition as a power series, it isn't so clear that our function really does behave like an exponential. Any exponent satisfies $$a^{m+n} = a^m a^n$$. So our goal here is to show that $$\exp(x+y) = \exp(x) \exp(y)$$. 

As a warmup, first we will show the easier $$\exp(2x) = \exp(x)\exp(x)$$.

$$
\exp(x) \exp(x) = \sum_{p=0}^{\infty} \frac{x^p}{p!} \sum_{q=0}^{\infty} \frac{x^q}{q!}
= \sum_{p, \ q \geq 0} \frac{x^p x^q}{p! \ q!}
$$

Denote by $$[x^k]$$ the coefficient of $$x^k$$. To find it, set $p + q = k$. Then

$$
\begin{align*}
    [x^k] &= \sum_{p + q = k} \frac{1}{p! \ q!} \\
          &= \frac{1}{0! \, k!} + \frac{1}{1! \, (k-1)!} + \dots + \frac{1}{k! \, 0!} \\
          &= \frac{1}{k!} \sum_{p=0}^{k} \binom{k}{p} \\
          &= \frac{2^k}{k!}
\end{align*}
$$

Aha! The coefficient of $$x^k$$ is $$\frac{2^k}{k!}$$, so the $k$-th term is given by $$\frac{(2x)^k}{k!}$$, as desired.

Now that we have a hold on a specific case, let us move on to the general one.


$$
\exp(x) \exp(y) = \sum_{p=0}^{\infty} \frac{x^p}{p!} \sum_{q=0}^{\infty} \frac{y^q}{q!}
= \sum_{p, \ q \geq 0} \frac{x^p y^q}{p! \ q!}
$$

Now letting $p + q = k$ and summing over all $k$ is the same as the sum above[^1]

$$
\begin{align*}
    \exp(x) \exp(y) &= \sum_{k=0}^{\infty} \sum_{p + q = k} \frac{x^p y^q}{p! \ q!} \\
                    &= \sum_{k=0}^{\infty} \sum_{p=0}^k \frac{x^p y^{k-p}}{p! \ (k-p)!} \\
                    &= \sum_{k=0}^{\infty} \frac{1}{k!} \sum_{p=0}^k \binom{k}{p} x^p y^{k-p} \\
                    &= \sum_{k=0}^{\infty} \frac{1}{k!} (x+y)^k \quad \href{https://en.wikipedia.org/wiki/Binomial_theorem}{\text{(binomial theorem)}} \\
                    &= \sum_{k=0}^{\infty} \frac{(x+y)^k}{k!} \\
                    &= \exp(x+y) \quad \blacksquare
\end{align*}
$$

And so we are done! What we are doing here is called the [Cauchy product](https://en.wikipedia.org/wiki/Cauchy_product).

Exercise left to the reader: now prove the formula for $$\sin(x+y)$$... 😜

[^1]: This rearrangement holds by [Fubini's theorem](https://en.wikipedia.org/wiki/Fubini%27s_theorem), as the exponential series converges absolutely.


-----

Let us now work with another definition of $$\exp$$. Define $$\exp(x)$$ to be the solution to the equation $$f'(x) = f(x)$$ with $$f(0) = 1$$. Now our goal is to show that $$\exp(x+y) = \exp(x) \exp(y) $$. Let $$g(x) = \exp(x+y)$$ and $$h(x) = \exp x \exp y$$. Then it is trivial to check that these satisfy the differential equation:

$$
g'(x) = \frac{d}{dx} \exp(x+y) = \exp(x+y) = g(x)
$$

by the chain rule and

$$
h'(x) = \frac{d}{dx} \exp x \exp y = \exp x \exp y = h(x).
$$

And also that $$g(0) = h(0) = \exp y$$, using $$\exp 0 =1$$. 

Now by [Picard–Lindelöf](https://en.wikipedia.org/wiki/Picard%E2%80%93Lindel%C3%B6f_theorem), we have two functions satisfying the same ODE with the same initial values, and so they are the same function by uniqueness. $$\blacksquare$$

-----

The reader is encouraged to also show this for the limit definition,

$$
\exp x := \lim_{n \to \infty} \left(1 + \frac{x}{n} \right)^n
$$

Heuristic: 

$$
\left(1+\frac{x}{n}\right)^n\left(1+\frac{y}{n}\right)^n = \left(1+\frac{x+y}{n}+\frac{xy}{n^2}\right)^n = \cdots
$$

-----

Upd. (added 21/05/26): 

Here is a neat little extensions of the method above. Consider $$g(x) = \exp(ix)$$ where $$i^2 = 1$$. Then $$g' = i g$$ and $$y(0) = 1$$. Can you see where I'm going with this? Now also consider $$h(x) = \cos x + i \sin x$$. Then $$h' = ih$$ and $$h(0) = 1$$. And hence Euler's formula is proved!

Another exercise for the conscientious reader: 
>Show that $$\exp(x)^r = \exp(r)$$ for all real numbers $$r$$. Use your favorite definition! 

Cheers!
