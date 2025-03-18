---
layout: post
title: Russel's Theory of Descriptions
---

Famous for his work in philosophy, logic and math, founder of
[analytic philosophy](https://en.wikipedia.org/wiki/Analytic_philosophy),
co-writer of [Principia Mathematica](https://en.wikipedia.org/wiki/Principia_Mathematica)
(not the [Newton one](https://en.wikipedia.org/wiki/Philosophiæ_Naturalis_Principia_Mathematica)),
inventor of the famous [Russel's paradox](https://en.wikipedia.org/wiki/Russell%27s_paradox), and a recipient
of the Nobel Prize in literature, Russel was quite a guy.

On top of that, he was an atheist and a pacifist.
In 1918, he was sentenced to six months in Brixton Prison for his pacifist views, violating
Britain's Defence of the Realm Act.
[Here are all 105 of his prison letters.](https://russell-letters.mcmaster.ca/letters)

In is his [Theory of descriptions](https://en.wikipedia.org/wiki/Theory_of_descriptions), he explains the
problem of nouns getting their meaning (or at least part of it) from the actual object they are referring to.

For example, there is a problem with statements like "King of New York is bald", because there is actually no such thing
as the "King of New York". This violates the
[law of the excluded middle](https://en.wikipedia.org/wiki/Law_of_excluded_middle), which says that
for every proposition, either the proposition or its negation must be true. Is the King of New York really bald?

There were attempts by philosophers to explain how a thing can *exist* (e.g. the King of Spain, a dog) or *subsist*
(e.g. the King of New York, a unicorn), latter being  things that don't exist in reality, but they exist as
a concept that we can reference.

Russel solves this whole mess by using *descriptions*, turning the above example into something like this

(*F* = "is king of New York", *G* = "is bald"):

$$
\exists x((Fx \wedge \forall y (Fy \rightarrow x = y)) \wedge Gx)
$$

This informally translates to
- It holds for some *x* that
    - It has the property *F*
    - It is unique (for every *y*, if *Fy*, then *y* must be *x*)
    - It has the property *G*

King of New York no longer needs to exist. It all becomes predicate logic.
If there are no entities *x* with property *F*,
the proposition "*x* has property *G*" is simply false for all values of *x*.
In other words, there is no direct reference to any object, so we no longer have the question whether some non-existent
object exists or not. The sentence is simply false.

The problem explained above deals with so-called *non-referring expressions*. There is also a problem of
objects with multiple identities - *co-referring expressions*.
This is often illustrated via "morning star" vs "evening star", both referring
to the same object in the sky (Venus), but seen at different times of the day. It's problematic because one
cannot easily be substituted for another in a sentence, which should be possible with identical expressions.

Russel's descriptions solve this problem as well. "Morning star" and "evening star" are no long synonyms, but
unique things separated from their referenced object in the real world.

Non-referring and co-referring expressions both fall under the umbrella of *definite descriptions*. Russel
tackles the problem of *indefinite descriptions* as well. They also refer to non-existent entities,
for example "an interesting person" (who is that exact person?).
By describing this as $\exists x(Px \wedge Ix)$,
we no longer need some mysterious unknown person to exist (and be interesting); we simply
say "there exists an object *x* such that *x* is a person and *x* is interesting".

[Original essay](https://zenodo.org/records/1431813), [online version](http://bactra.org/Russell/denoting/).

