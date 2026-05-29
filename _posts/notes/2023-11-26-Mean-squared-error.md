---
layout: post
title: Mean Squared Error
---

Given a set of measurements / observations / numerical outcomes, 
why should we ever use MSE (Mean Squared Error) for approximating the true value? 
Some people think
it's because it gets rid of negative error values, but MAE (Mean Absolute Error) does the same.

So why then?

One reason is that MSE is differentiable and MAE (Mean Absolute Error) isn't, 
but there's another important reason - MSE approximates the
mean, while MAE approximates the median. You will also hear how "MSE punishes outliers
more than MAE", but the mean vs median argument covers that too, as I aim to show below.

Let's consider the following set 
of observed measurements: [1, 2, 5]. 
- Its mean is (1 + 2 + 5) / 3 = 2.6666 = (rounded to) 3.
- Its median is the middle value, 2.

Let's now evaluate each potential true value candidate *x* with
MSE and MAE. Actually, to save time, let's just consider 2 and 3, because others
are obviously "more wrong".

Mean squared error:

$$
MSE(x) = \frac{(1 - x)^2 + (2 - x)^2 + (5 - x)^2}{3}
$$

$$
MSE(2) = 3.33
$$

$$
MSE(3) = 3.00
$$

Minimal value is obtained for *x = 3* (since 3 < 3.33).
This is also the mean.

Mean absolute error:

$$
MAE(x) = \frac{|1 - x| + |2 - x| + |5 - x|}{3}
$$

$$
MAE(2) = 1.33
$$

$$
MAE(3) = 1.66
$$

Minimal value is obtained for *x = 2* (since 1.33 < 1.66).
This is also the median.

We can see how MAE doesn't really care about the actual values.
What happens when we go from *x = 2* to *x = 3* is simply that there are
two values we're getting further away from (1 and 2), and one value we're getting
closer to (5), so the net difference is that such move is penalized by one. MAE
strives to equalize the number of values on its left and its right, and
penalizes moving away from that position.
Note that having the same number
of lower and higher values is also the exact definition of a median. The values
themselves can be modified without consequences for the median, as long as the balance
between those on the left and those on the right remains untouched.

But mean is affected by the actual values. And so is MSE, particularly the outliers
(because of exponential growth).

I know it's a bit handwavy, but I just wanted to build some intuition for myself,
and perhaps it helped someone else too.