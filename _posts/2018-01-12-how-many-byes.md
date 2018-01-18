---
layout: post
title:  "How many players need to be given byes to the next round?"
date:   2018-01-12
categories: tournament byes
use_math: true
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
would be 32 and you have (32 - 21 = 11) byes. To round off, if number
of players is exactly same as exponential of 2 (such as 16 or 32),
there won't be any need for byes.

Now, we can see that the formula works pretty well but can we actually
prove that this is the case for any N? Let us give it a try.

Before we begin, here is a property that holds true for N (number of
players):

*2<sup>m-1</sup> < N < 2<sup>m</sup>*

This must be true as otherwise, N would be an exponential of 2 and
there would be no need for any byes. To give an example, if N is 21,
*m* would be 5.

Now, the formula we came up with above can be written as *2<sup>m</sup>- N*. 

Let us try to calculate the number of players who
would make it to the second round (say N<sub>2nd</sub>). 

\\[x \over y\\]

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$

N<sub>2nd</sub> = number of players who got byes + half of remaining
                           players who will play in the first round.

    = (2<sup>m</sup> - N) + (N - (2<sup>m</sup> - N))/2

The problem presents an interesting teching momemt to kids because
they can see that the formula works but they need to learn that just
because it worked for few numbers, there is no guarantee that  it
would work for all numbers. One needs to prove it is true formally.

Include reference to Ramanujan's prime numner theorem.
