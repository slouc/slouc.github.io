---
layout: post
title: Intuition behind the Monty Hall problem
---

[Monty Hall problem](https://en.wikipedia.org/wiki/Monty_Hall_problem) is a popular puzzle based on
probability and our biases around it. In case you're not familiar with it, here's the problem:

You are a guest in a talk show, where the host presents you with three closed doors.
One of the doors contains a prize - a brand new car. Other two doors each contain a goat.
You are asked to pick one of the three doors. After you pick, the host will reveal one of the
two remaining doors, showing you a goat. The host knows the placement of the car and two goats upfront,
so you'll always be shown a goat.

Now you have the opportunity to change your mind and
pick the other remaining door, or stick to your original decision.

Our natural instant reaction is "there are two doors left so the chances
are 50:50", whereas in reality, you have a 66% of winning a car if you switch and 33% if you stay.

I first heard about this problem back in the days of old dial-up internet in the late 90s, when
the term "surfing the web" was popular. And I can't remember if it was the actual math forum
where I first found it, or I stumbled upon that forum while searching for the solution.
Either way, I found this bulletin board
where a math professor was trying to convince a bunch of shocked people that the math really
does work out - you should switch the door. Everyone was absolutely convinced that the chances
are 50-50.
[Here are some of the comments](http://facweb1.redlands.edu/fac/jim_bentley/Data/Math%20311/MontyHall/MontyHall.html#comments-1) 
(sadly, the original forum is down).

<img src="../images/monty.png" width="400" height="400">

_[DALL-E: “a math professor woman is correct about the two goats and a car”](https://labs.openai.com/s/pSLczN8WU9XEWA3jfB3ROW3y)_

To be honest, I didn't see it either. I was young, but I definitely had enough
of basic probability knowledge to work it out; however, the counter-intuition was so strong that
I was compelled to write a short C program to check it. 
Randomly assign the positions, eliminate one goat door, make the decision.
Run a few million times for each of the two possible decisions.
Sure enough, switching the door was the winning strategy in 66% of the cases,
while not switching only won in 50% of the cases.

When I explain this problem to someone for the first time, and they are as puzzled as I was,
it's hard to present a simple solution and have them buy it right away. The moment you start
writing equations or drawing boxes or enumerating different scenarios, it turns into a
complex discussion.

So instead, I usually use the following intuition, which immediately achieves the desired "aha" moment:

>Imagine there were a hundred doors.
You pick one door, say, door 27. The host now opens all other doors (showing goats behind them), 
except for the door 53.
Since the host will never reveal a car door, there's a 1% chance
that you were right with your initial 1/100 probability pick, and 99% chance that you should
actually listen to the host. It's just that the original problem uses only three doors instead.

