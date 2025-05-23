---
layout: post
title:  "How To Solve It"
date:   2025-05-22 17:05:01 +0530
categories: coding, cses, how-to-solve-it
---

Today I started reading the book *How to solve it* by G. Polya. First we are introduced to some general problem solving techniques. Some of the advice may seem obvious, but there is some nuance to it. It is very well written. One of the tips was to look back at finished problems, something I rarely do. So I will try to fix that:

I am trying out the [CSES problem set](https://cses.fi/problemset/list/). I'm using python right now, because I'm not very comfortable with C++ yet. Here is some commentary on the first few introductory problems: 

1. [Weird Algorithm](https://cses.fi/problemset/task/1068): This one is pretty easy to code. Not much to say.

2. [Increasing Array](https://cses.fi/problemset/task/1094): This one looks intimidating. But once you look at an example the idea is very clear. My solution was to go through the array, and add the difference of two consecutive elements to a counter variable, and then replace an element. Pretty much the same as the official solution. Both the algorithm and its implementation are straightforward.

------


[Two Sets](https://cses.fi/problemset/task/1092/): This was a very interesting one. I decided to bash it out and see.

Firstly whenever I see "sum" and "first \\(n\\) natural numbers" I am inclined to think of Gauss's trick. Which is still useful here!

For instance when \\(n=8\\), we can pair up terms like so:

\\(1, 2, 3, 4, 5, 6, 7, 8\\)

\\(1 + 8 = 9\\)

\\(2 + 7 = 9\\)

\\(3 + 6 = 9\\)

\\(4 + 5 = 9 \\)

and the solution is clear from here. This easily generalizes to \\(n\\) of the form \\(4k\\).

Now I claim that it is impossible when \\(n=4k+1\\) and \\(4k+2\\). As an example, for \\(n=5\\)

\\(1, 2, 3, 4, 5 \\)

Notice that this has an odd number of odd numbers. So when we try to split into two groups:

| | Odds in Group 1 | Odds in Group 2 |
||--------|---------|
| 1 | 3 | 0 |
| 2 | 2 | 1 |

Group 1 and group 2 will have different parities (ie one will be odd and the other even). The same holds for \\(n=6\\). This easily generalizes. So we are done.

Now what about the case when \\(n=4k+3?\\)

This was significantly harder, and involves a lot of ugly bashing. Here is my code if you are curious:

{% highlight python %}
if n%4 == 3:
    e = []
    o = []
    for i in range(1, n//2 + 1):
        if i%2 == 0:
            e.append(i)
            e.append(n-i + 1)
        else:
            o.append(i)
            o.append(n-i + 1)

    if ( (n+1) //2 ) % 4 == 0:
        e.append(o[-1])
        e.append(o[-2])
        o.pop()
        o.pop()
        o.append((n+1)//2)
        e.remove(((n+1)//2) // 2)
        o.append(((n+1)//2) // 2)
        
    else:
        o.remove( ((n+1)//2) //2 )
        e.append(((n+1)//2))
        e.append( ((n+1)//2) //2 )
{% endhighlight %}

The logic is not too hard to identify. I worked through the cases \\(n =7, 11, 15\\) and generalized. It seems to work, but is hardly very elegant. Also this case-bash approach seems very ugly. Is there a better way? Indeed there is!

----------


Discussion of the [official solution](https://cses.fi/problemset/model/1092/):

This is very clever. If the sum of the two sets are to be equal, then the sum of one of them must be \\(s/2\\). With this observation we will greed our way into this, similar to the famous coin problem, by subtracting as many big numbers as we can. And of course for this to work \\(s\\) must be even. They proved it works by induction. It can also be proved by going through the cases \\(n \pmod 4\\).

I think I was thinking too mathematically, trying to prove a construction instead of looking at the problem. I should perhaps have realized that after proving my construction works I could have greed-ed immediately.



