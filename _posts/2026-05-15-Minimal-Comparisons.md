---
title: Minimal-Comparisons
date: 2026-05-15 12:30:00 +0530
categories: [math, coding]
tags: [math-for-fun]
author: 
description: What's the minimum number of comparisons required to find the minimum and maximum of an array?
math: true
---
Given an array $$A$$ of length $$n$$, how many comparisons are required to find both the minimum and maximum?

First, we will tackle finding the maximum alone. Denote by $$n$$ the length of the array. An easy upper bound is to use $$n-1$$ comparisons. But what about a lower bound? Is it possible to do better than $$n-1$$? 

Think of any algorithm that determines the maximum element as being a knockout tournmanet. Each comparison that we do has a winner and a loser (if both elements are the same pick one to be the loser). The loser is knocked out, since it cannot be the maximum of our array. All elements in the array must play until a single winner remains (if there were more than one winner, they both could be maximal). This is a classic counting puzzle: each match produces exactly one loser, and there are $$n-1$$ losers, so $$n-1$$ comparisons are required.

The minimum of $$A$$ is just $$-\max{(-A)}$$ so the same argument goes through.

-----

You might wonder why bother doing all this? Isn't this [trivial](https://en.wikipedia.org/wiki/Proof_by_intimidation)? That was just a warmup! Here is our [puzzle](https://brainstellar.com/puzzles/strategy/1011) for today: 

>Given an array of $$n$$ numbers. Finding its minimum takes $$n-1$$ comparisons. Finding maximum takes $$n-1$$ comparisons. If you had to simultaneously find both the minimum and the maximum, can you do better than $$2n-2$$ comparisons?

And the answer is, you _can_ do better than $$2n-2$$. We might suspect this because of $$n=2$$. For two elements, we required only one comparison, not $$2(2) - 2= 2$$. In fact you can do it in $$\frac{3n}{2}$$ish comparisons. Here is how: break the array of $$n$$ elements into $$\frac{n}2$$ pairs. Then for each pair find the min and max (which takes only one comparison!), and then find the max of these $$\frac{n}{2}$$ maximums. So the total number of comparisons is $$\frac{n}{2} + \frac{n}{2} + \frac{n}{2} = \frac{3n}{2}$$.

------

But how do we know there is no clever trick that can do better? Here is an exercise from CLRS:

>Prove the lower bound of $$\left \lceil \frac{3n}{2} \right \rceil - 2$$ comparisons in the worst case to find both the maximum and minimum of n numbers. (Hint: Consider how many numbers are potentially either the maximum or minimum, and investigate how a comparison affects these counts.)

Following the hint, all the $$n$$ numbers are potentially the minimum or maximum. Let $$X = \text{#possible maximums} + \text{#possible minimums}$$. Suppose we compare two elements we have not compared yet. Then we can reduce the size of $$X$$ by two. Any other comparison reduces $$X$$ by one. So it's best to keep comparing fresh elements. There are only $$\frac{n}{2}$$ fresh elements. After comparing them we will have two arrays of size $$\frac{n}{2}$$ and $$\frac{n}{2}$$. So in total we have $$\frac{n}{2}- 1 + \frac{n}{2} -1 + \frac{n}{2} = \frac{3n}{2} - 2$$ comparisons as a lower bound, as desired. (To get the ceils requires some fiddling -- [left as an exercise](https://github.com/s-macke/Abstruse-Goose-Archive/blob/master/comics/math_text.png)! 😜)

Our algorithm above achieves this lower bound.

>Exercise, for the reader: Show that the second smallest of $$n$$ elements can be found with $$n + \left \lceil \log n \right \rceil - 2$$ comparisons in the worst case.