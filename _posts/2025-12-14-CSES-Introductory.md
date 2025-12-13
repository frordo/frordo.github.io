---
title: Hello, World!
date: 2025-12-14 02:30:00 +0530
categories: [coding]
tags: [cses, competitive_programming]
author: <rahul>
description: CSES Introductory
math: true
---
Remark: This was originally posted on another blog on 19/6/25.

The following are my thoughts and commentary on the first few [CSES](https://cses.fi/problemset/list/) Introductory Problems. Of course, these are more an exercise in writing than actual solutions, since official (and unofficial) solutions are available readily.

As a side note: I'm using python right now, because I'm not very comfortable with C++ yet. For input I mostly use `map(int, input().split())`

------

1. [Weird Algorithm](https://cses.fi/problemset/task/1068): This one is pretty easy to code. Simply follow the instructions given.

2. [Missing Number](https://cses.fi/problemset/task/1083): Since we are given $$n$$, and there is only one missing number, we can just subtract the sum of the given list from $$1 + 2 + 3 \cdots + n = n(n+1)/2$$. Done!

3. [Repetitions](https://cses.fi/problemset/task/1069): This is asking us to find the length of the *maximal contiguous subsequence*. Since only the length is asked, we can simply loop through the list, count the length of each block of letters, and update if necessary. 

    The implementation is as follows. Get two variables, `max_length` and `temp`. Loop through the string, each time checking if `string[i] == string[i+1]`. In `temp` we will store the length of the current block. At the end of each block we will do `max_length = max(max_length, temp)`. Done!

4. [Increasing Array](https://cses.fi/problemset/task/1094): This one looks intimidating. But once you look at an example the idea is very clear. My solution was to go through the array, and add the difference of two consecutive elements to a counter variable, and then replace an element. Pretty much the same as the official solution. Both the algorithm and its implementation are straightforward.

5. [Permutations](https://cses.fi/problemset/task/1070/): So the logic for this is pretty straightforward. Just group the evens and the odds and it will obviously work, except for some small edge cases. So we just deal with $$n=2$$ and $$n=3$$ separately. My first submission had a <code style="color: red;">TIME LIMIT EXCEEDED</code>. But I realized it was because I was calling the `print` function $$n$$ times. 

    So instead I switched to <code>sys.stdout.write(" ".join(map(str, a)))</code> which is something new I learnt. Python is weird.

6. [Two Sets](https://cses.fi/problemset/task/1092/): This was a very interesting one. I decided to bash it out and see.

    Firstly whenever I see "sum" and "first $$n$$ natural numbers" I am inclined to think of Gauss's trick. Which is still useful here!

    For instance when $$n=8$$, we can pair up terms like so:

    $$1, 2, 3, 4, 5, 6, 7, 8$$

    $$1 + 8 = 9$$

    $$2 + 7 = 9$$

    $$3 + 6 = 9$$

    $$4 + 5 = 9 $$

    and the solution is clear from here. This easily generalizes to $$n$$ of the form $$4k$$.

    Now I claim that it is impossible when $$n=4k+1$$ and $$4k+2$$. As an example, for $$n=5$$

    $$1, 2, 3, 4, 5 $$

    Notice that this has an odd number of odd numbers. So when we try to split into two groups:

    | | Odds in Group 1 | Odds in Group 2 |
    ||--------|---------|
    | 1 | 3 | 0 |
    | 2 | 2 | 1 |

    Group 1 and group 2 will have different parities (ie one will be odd and the other even). The same holds for $$n=6$$. This easily generalizes. So we are done.

    Now what about the case when $$n=4k+3$$?

    This was significantly harder, and involves a lot of ugly bashing. I worked through the cases $$n =7, 11, 15$$ and generalized. It seems to work, but is hardly very elegant. Also this case-bash approach seems very ugly. Is there a better way?

    Discussion of the [official solution](https://cses.fi/problemset/model/1092/):

    This is very clever. If the sum of the two sets are to be equal, then the sum of one of them must be $$s/2$$. With this observation we will greed our way into this, similar to the famous coin problem, by subtracting as many big numbers as we can. And of course for this to work \\(s\\) must be even.

7. [Bit Strings](https://cses.fi/problemset/task/1617): I think pretty much everybody knows this. The $$\pmod{10^9 + 7}$$ part is to prevent overflows. One should use the fact that $$\pmod{}$$ distributes over multiplication. As an aside, $$2^n$$ can be calculated in $$\mathcal{O}(\log_2n)$$ steps, by representing $$n$$ in binary.

8. [Trailing Zeros](https://cses.fi/problemset/task/1618): It would've made for a nice problem. Unfortunately I already knew the solution from JEE prep. This is just the p-adic valuation $$(\nu_5(n!))$$. Obviously there are more factors of five than two. See [Legendre's formula](https://en.wikipedia.org/wiki/Legendre%27s_formula).




