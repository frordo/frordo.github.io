---
title: Pairs of Dice
date: 2026-05-26 02:00:00 +0530
categories: [math]
tags: [math-for-fun]
author: 
description: Are there equivalent sets of pairs of dice?
math: true
---

If you roll two six-sided die and add up their values, you get a certain probability distribution. Here it is for reference (rescaled):

$$
\begin{array}{|c|c|c|c|c|c|c|c|c|c|c|c|}
\hline
X & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 \\ \hline
P(X) & 1 & 2 & 3 & 4 & 5 & 6 & 5 & 4 & 3 & 2 & 1 \\ \hline
\end{array}
$$

Our goal is two find all other pairs of die so that it has the same probability distribution.

-----

Now I will impose the following conditions:
+ sides must be a positive whole number
+ the die must be six sided

This problem is almost _asking_ for the generating function approach. So here it is!

Each dice is represented by the polynomial $$(x + x^2 + x^3 + x^4 + x^5 + x^6)$$. Recall that the exponent gives the value and its coefficient the probability. Now for two die it is:

$$
(x + x^2 + x^3 + x^4 + x^5 + x^6)^2 = x^2 + 2x^3 + 3x^4 + 4x^5 + 5x^6 + 6x^7 + 5x^8 + 4x^9 + 3x^{10} + 2x^{11} + x^{12}
$$

(the reason this works is because polynomial multiplication is the same as convolution of their coefficients.)

So in essence we want another factorization of $$f(x)^2$$, where $$f(x) = (x + x^2 + x^3 + x^4 + x^5 + x^6)$$. In particular, we want a factorization of $$f$$ into two polynomials, ie, $$f = P_1 P_2$$ where both $$P_1$$ and $$P_2$$ satisfy
+ $$P(0) = 0$$ (no $$x^0$$ terms)
+ $$P(1) = 6$$ (if $$P = \sum a_i x^i$$, $$\sum a_i = 6$$ since it's six sided)
+ all coefficients are non-negative integers.

Note that $$f(x) = x(1 + x + x^2 + \cdots + x^5) = x \frac{x^6 - 1}{x-1} $$. Now using the some roots of unity stuff,

$$
f(x) = x(x+1)(x^2 - x + 1)(x^2 + x + 1)
$$

(A faster way to get these are the [cyclotomic polynomials](https://en.wikipedia.org/wiki/Cyclotomic_polynomial))

-----

Therefore

$$
f(x)^2 = x^2(x+1)^2(x^2+x+1)^2(x^2-x+1)^2
$$

Writing $$P = x Q$$ (each of the $$P$$'s need an $$x$$, otherwise they would have a constant term!), we need $$Q_1 Q_2 = (x+1)^2(x^2+x+1)^2(x^2-x+1)^2$$ with $$Q(1) = 6$$.

Now evaluating each factor at $$x = 1$$:

$$
(1+1) = 2, \quad (1+1+1) = 3, \quad (1-1+1) = 1
$$

Now $$Q(1) = 6$$ implies each die must receive a factor of $$(x+1)$$ and a factor of $$(x^2+x+1)$$. The only freedom lies in which way we divvy up $$(x^2-x+1)^2$$.

Case 1: Equal split

$$Q_1 = Q_2 = (x+1)(x^2+x+1)(x^2-x+1) = 1+x+x^2+x^3+x^4+x^5$$

This is our original solution.

Case 2: 

$$Q_1 = (x+1)(x^2+x+1) = x^3+2x^2+2x+1 \implies P_1 = x^4+2x^3+2x^2+x$$
$$Q_2 = (x^2+x+1)(x^3+1)(x^2-x+1) = x^7+x^5+x^4+x^3+x^2+1 \implies P_2 = x^8+x^6+x^5+x^4+x^3+x$$

This corresponds to dice with faces $$\{1, 2, 2, 3, 3, 4\}$$ and $$\{1, 3, 4, 5, 6, 8\}$$.

Note that swapping the factor gives the same answer.

-----

Since we covered all possible cases, we have proved that there is exactly one non-trivial solution!

These are known as Sicherman dice, first discovered by George Sicherman in 1978. Solving discrete problems with generating functions always does feel a bit magical!

-----

I wanted to write this since I eventually want to write something motivating the convolution theorem. And generating functions really help with this, I feel. So I would like to rewrite this to introduce and motivate generating functions a bit more in the future.