---
layout: post
title:  "How many players need to be given byes to the next round?"
date:   2018-01-20
categories: tournament byes
---

This question came up recently in our household as we were looking at
the draw of a tennis tournament. There were 20 players in the
tournament so the answer was 12.

We then tried to guess the answer in different cases. With 6 players, 2
will get byes and with 21, the answer would be 11. So here is the
pattern (number of players followed by number of players getting
byes):

```
     6 - 2
    20 - 12
    21 - 11
```

The pattern becomes clear with little bit of an effort. Did you spot
it? All you need to do is to find an exponential of 2 that is larger
than the number of players and then subtract number of players from
it. For example, if there are 21 players, the closest exponential of 2
greater than 21 would be 32 and you have (32 - 21 = 11) byes. To round
off, if number of players is exactly same as exponential of 2 (such as
16 or 32), there won't be any need for byes.

### Proving the formula

We can see that the formula works pretty well but can we actually
prove that this is the case for any N? Let us give it a try.

Before we begin, here is a property that holds true for N (number of
players):

$$2^{m-1} < N < 2^m\tag{1}\label{1}$$

As an example, if N is 21, *m* would be 5. The above property must be
true for any N as otherwise, N would be an exponential of 2 and there
would be no need for any byes.

Now, the formula we came up with above can be written as
*2<sup>m</sup>- N*.  Let us try to calculate the number of players who
would make it to the second round (say *N<sub>2nd</sub>*).

*N<sub>2nd</sub> = number of players who got byes + half of remaining
                           players who will play in the first round*

$$
\begin{align}
N_{2nd} & = (2^m - N) + \frac{N - (2^m - N)}{2} \\

& = 2^m - N + \frac{2N - 2^m}{2} \\

& = 2^m - N + N - 2^{m-1} \\

& = 2^m - 2^{m-1} \\

& = 2^{m-1}
\end{align}
$$

So using the formula $$2^m - N$$ for number of byes, we calculated the
number of players who would go on to the second round as
$$2^{m-1}$$. But from property $$\eqref{1}$$, we can see that this is
indeed true so we proved the formula $$2^m - N$$ for any *N*.

### Deriving the formula

We have proved above that the formula we came up with by looking at
the pattern is indeed true. But you may not be able to come up with a
formula every time just by looking at few examples. In these cases,
you will have to derive the formula from the problem statement
itself. Let us see if we can do that for this problem.

Let us assume that number of byes is *x*. So number of players who
would go on to second round would be 

$$
N_{2nd} = x + \frac{N - x}{2}
$$

From property $$\eqref{1}$$, we know that number of players in
second round would be $$2^{m-1}$$. So

$$
\begin{align}
x + \frac{N - x}{2} & = 2^{m-1} \\

x + \frac{N}{2} - \frac{x}{2} & = 2^{m-1} \\

\frac{x}{2} + \frac{N}{2} & = 2^{m-1} \\

\frac{x + N}{2} & = 2^{m-1} \\

x + N & = 2 * 2^{m-1} \\

x + N & = 2^m \\

x & = 2^m - N \\
\end{align}
$$

There you go! Starting from the problem statement, we have derived
the formula for number of byes to be $$2^m - N$$.

### Conclusion

So we not only discovered the pattern and proved that it is true but we
also found the solution starting from problem statement itself.

Sure, the math is pretty elementary but all the same, the formal
treatment of the problem presented a pleasant deviation from the usual
coding work :-).

Even more importantly, the problem provided an interesting
opportunity to teach kids that what works for few inputs may not work
for all inputs and that it is very important to prove the solution for
a general case.
